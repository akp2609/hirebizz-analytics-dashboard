📊 HireBizz Analytics Dashboard
This repository contains the Power BI Dashboard for the HireBizz platform, providing real-time and historical analytics for user engagement, system usage, and cloud costs.

The dashboard integrates multiple data sources (MongoDB, Redis, BigQuery, GCS, OpenAI APIs, and GCP Billing Export) into a single visual interface for monitoring platform health, costs, and user behavior.

🚀 Features
User Analytics

Downloads and installations

Active users (hourly, daily, monthly, yearly)

Login failures with reason and IP breakdown

Platform Usage

Number of job postings vs. resumes

Resume-job similarity scores (average and distribution)

Redis-based hourly usage tracking

Cost Analytics

Daily GCP billing breakdown

OpenAI API usage & cost monitoring

Aggregated cost views across daily/weekly/monthly

Security & Monitoring

Failed login attempts by reason (e.g., expired token, invalid password)

IP address distribution of failed logins

Protected API routes with Azure AD-based access

flowchart LR
    MongoDB[(MongoDB)] -->|Weekly Batch| Dataflow[GCP Dataflow] --> BigQuery[(BigQuery)]
    GCS[(GCS Billing Export)] --> BigQuery
    Redis[(Redis Cache)] -->|Hourly API Calls| GitHubActions[GitHub Actions] --> MongoDB
    BigQuery --> PowerBI[Power BI Dashboard]


⚙️ Technology Choices
🔑 Azure AD over JWT
Why not plain JWT?

JWTs are easier but less secure for enterprise use.

Azure AD adds centralized identity management, token lifetimes, revocation, and role-based access (RBAC).

✅ Chosen for enterprise-grade security and integration with future HireBizz admin modules.

⚡ Redis for Hourly Data
Why not MongoDB directly?

MongoDB is great for batch and weekly loads but inefficient for high-frequency hourly writes/reads.

Redis provides in-memory caching, fast writes, and low latency API responses.

✅ Chosen for real-time hourly tracking without stressing MongoDB.

🗄️ BigQuery as the Warehouse
Handles large-scale aggregation across MongoDB and billing exports.

Allows Power BI direct queries for near real-time analytics.

📈 Visuals
The dashboard is divided into 8 core visuals:

📊 Downloads & Installs – total and trends over time

👥 Active Users – hourly, daily, monthly, yearly breakdown

💸 GCP Billing Daily View – fragmented daily cost analytics

🧾 OpenAI API Usage – request counts & associated costs

📑 Jobs vs. Resumes – count comparison and trends

🎯 Resume-Job Similarity – average similarity score across processed resumes

🚨 Failed Login Attempts – reason breakdown (e.g., expired token, invalid credentials)

🌍 Failed Login by IP – geographical/IP breakdown of suspicious logins

🔗 Related Repositories
- [HireBizz Web App](https://github.com/akp2609/hirebizz)
- [HireBizz Android](https://github.com/akp2609/hirebizz-mobile)
- [HireBizz Resume Analyser](https://github.com/akp2609/resume-analyzer-microservice)

📌 Notes
Data is updated weekly from MongoDB via GCP Dataflow → BigQuery.

Hourly data is fetched via Redis + GitHub Actions.

Dashboard supports enterprise security via Azure AD.