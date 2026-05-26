# PowerBI-Workspace-Usage-Tracker
## 📌 Overview
This project is an **end-to-end Power BI Workspace Usage Tracking solution** designed to monitor report consumption, identify inactive workspaces, and enable data-driven governance decisions.
The solution integrates **Microsoft 365 audit logs**, **Azure services**, and **Power BI** to deliver **real-time insights** into workspace usage, helping reduce redundant resources and optimize operational costs.

## 🧩 Problem Statement
Organizations often accumulate a large number of Power BI workspaces and reports without visibility into actual usage, leading to:

- Increased infrastructure and licensing costs
- Redundant or inactive workspaces
- Lack of insights into report adoption
- Inefficient governance and resource management

There is a need for a centralized, automated solution to track usage and identify optimization opportunities.

## 💡 Solution Overview
The solution captures Power BI usage activity logs from Microsoft 365, processes them using Azure serverless architecture, and pushes data into a streaming dataset for near real-time analytics.
It enables:

- Monitoring report usage patterns
- Tracking user engagement
- Identifying unused workspaces
- Supporting cost optimization initiatives


## 🏗️ Architecture (High-Level)


### Data Source

Microsoft 365 Activity Logs (Power BI audit logs)



### Data Ingestion

Azure Function (timer-triggered)
API-based data extraction using Management Activity APIs



### Storage & Processing

Blob storage for incremental tracking and historical archiving
CSV generation for daily usage logs



### Analytics Layer

Power BI semantic model with calculated measures and tables



### Visualization

Power BI dashboards for usage and workspace insights




## ⚙️ Implementation Steps (Detailed)
### 1) Azure AD Application Setup

 - Registered an application in Azure AD
- Configured application permissions to access activity logs
- Granted admin consent for tenant-wide data access
- Generated client credentials for secure API authentication

_👉 Purpose: Enables secure, automated access to Microsoft 365 activity logs._

### 2) Power BI Streaming Dataset Creation

- Created a streaming dataset using API input
- Defined schema aligned with audit log fields (e.g., CreationTime, UserId, Activity)
- Enabled historical data analysis for trend reporting

_👉 Purpose: Allows near real-time ingestion and analysis of usage data._

### 3) Azure Function Development
A timer-triggered Azure Function was developed to automate log ingestion and processing.
#### 🔄 Execution Flow
**Secure Authentication**

- Fetches credentials securely from Key Vault
- Uses OAuth client credentials to obtain API access token


**Subscription Handling**

- Refreshes activity feed subscription to ensure continuous data availability


**Incremental Data Processing**

- Reads last processed timestamp from storage
- Fetches logs only for the new time window
- Updates timestamp after successful execution

_👉 Ensures efficient, duplicate-free data processing_

**Log Retrieval**

- Fetches content URIs from activity feed API
- Downloads audit logs from each URI
- Aggregates all log entries


**Filtering (Power BI-specific logs)**

- Filters logs where workload corresponds to Power BI

_👉 Keeps dataset clean and relevant_

**Push to Streaming Dataset**

- Sends logs in batches to Power BI streaming endpoint
- Ensures efficient data transfer and ingestion


**Historical Archival**

- Generates daily CSV files for usage logs
- Stores data in cloud storage for long-term tracking

_👉 Supports governance, auditing, and trend analysis_

## 📊 Data & Logs Used
### 🔹 Microsoft 365 Activity Logs
These logs capture user interactions such as:

- Report views
- Dashboard interactions
- Workspace access
- Dataset usage

_👉 Value: Enables tracking of real user engagement with Power BI assets_

### 🔹 Power BI Streaming Dataset
Used for:

- Real-time ingestion of usage events
- Continuous monitoring of activity
- Supporting live dashboard updates

_👉 Value: Enables near real-time visibility into report usage_

## 📈 Key Analytics & Metrics
### ✅ Unique Views per Report per Day

- Counts distinct users viewing each report daily
- Removes duplicate views from the same user

_👉 Business Impact: Identifies high-value reports and low adoption areas_

### ✅ Workspace Utilization Classification
Workspaces are categorized based on usage:

- Used Workspaces: Present in usage logs
- Unused Workspaces: Present in inventory but not used
- Other classifications: Based on dataset comparisons

Implemented using:

- Set-based logic (INTERSECT, EXCEPT, UNION)
- Calculated tables for classification

_👉 Business Impact: Enables identification and removal of inactive workspaces_

## 📊 Visualization
The solution provides intuitive dashboards with:

- Report usage trends over time
- User engagement patterns
- Workspace utilization breakdown
- KPI cards for quick insights
- Drill-through for detailed analysis


## 📈 Business Impact


### ✅ Cost Optimization

- Identification and removal of unused workspaces
- Reduced storage and licensing overhead



### ✅ Improved Governance

- Enhanced visibility into workspace usage
- Better control over reporting assets



### ✅ Data-Driven Decisions

- Enables proactive management of BI environment
- Supports adoption tracking and optimization



### ✅ Operational Efficiency

- Eliminates manual tracking of usage
- Automated pipeline reduces effort significantly




_🔒 **Data Privacy & Confidentiality**
This project is a sanitized representation of a production solution:
No tenant-specific identifiers or credentials included
No endpoint URLs or sensitive configuration exposed
All logic preserved without revealing confidential information_

## 🛠️ Tech Stack

- Power BI – Reporting & visualization
- Azure Functions – Serverless automation
- Azure AD – Authentication & authorization
- Azure Key Vault – Secure secret management
- Azure Blob Storage – Data persistence & state management
- REST APIs – Activity log extraction


## 🚀 Key Highlights

- Real-time + batch processing combined in one architecture
- Secure and scalable cloud-based implementation
- Advanced DAX-based analytics and classification
- Strong business focus on cost savings + governance


## ⭐ Why This Project Matters
This solution transforms raw audit logs into actionable insights, enabling organizations to:

- Optimize BI infrastructure usage
- Reduce unnecessary costs
- Improve reporting efficiency
- Drive data-driven governance
