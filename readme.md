# 📊 HireBizz Analytics Dashboard

![Dashboard Screenshot](.//images/hirebizz_dashboard.png)

This repository contains the **Power BI Dashboard** for the HireBizz platform, providing real-time and historical analytics for user engagement, system usage, and cloud costs.

The dashboard integrates multiple data sources (**MongoDB, Redis, BigQuery, GCS, OpenAI APIs, and GCP Billing Export**) into a single visual interface for monitoring platform health, costs, and user behavior.

---

## 🚀 Features

### 👥 User Analytics
- Downloads and installations  
- Active users (hourly, daily, monthly, yearly)  
- Login failures with reason and IP breakdown  

### 🧭 Platform Usage
- Number of job postings vs. resumes  
- Resume-job similarity scores (average and distribution)  
- Redis-based hourly usage tracking  

### 💸 Cost Analytics
- Daily GCP billing breakdown  
- OpenAI API usage & cost monitoring  
- Aggregated cost views (daily/weekly/monthly)  

### 🛡 Security & Monitoring
- Failed login attempts by reason (e.g., expired token, invalid password)  
- IP address distribution of failed logins  
- Protected API routes with Azure AD-based access  

---

## 📊 Data Flow

```mermaid
flowchart LR
    MongoDB[(MongoDB)] -->|Weekly Batch| Dataflow[GCP Dataflow] --> BigQuery[(BigQuery)]
    GCS[(GCS Billing Export)] --> BigQuery
    Redis[(Redis Cache)] -->|Hourly API Calls| GitHubActions[GitHub Actions] --> MongoDB
    BigQuery --> PowerBI[Power BI Dashboard]
