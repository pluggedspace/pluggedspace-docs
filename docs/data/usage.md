# Pluggedspace Atlas: User Guide & Workflows

This guide provides step-by-step instructions on how to use **Pluggedspace Atlas** to import datasets, analyze data using natural language or SQL, run automated pipelines, and manage team access.

---

## 👥 Team Roles & Permissions

Atlas uses role-based access control to ensure team members have the appropriate permissions:

| Role | Ideal For | What They Can Do |
| :--- | :--- | :--- |
| **Workspace Owner** | Account Owners & Team Leads | Manage subscriptions, billing, workspace settings, and invite Admins. |
| **Admin** | Operations & Data Managers | Create domains, configure automated data pipelines, monitor ingestion health, and manage datasets. |
| **Analyst** | Business Analysts & Data Teams | Query datasets with SQL or Natural Language, generate reports, configure predictive models, and export results. |
| **Viewer** | Stakeholders & Executives | Search and explore published datasets, view metadata schemas, and receive automated alerts. |

---

## 🛠️ Core User Workflows

### Workflow 1: Importing and Managing Datasets

1. **Navigate to Datasets**: From your Atlas dashboard, click **Datasets** in the left navigation.
2. **Upload Data**: Click **+ New Dataset** and select your file (`.csv`, `.xlsx`, or `.parquet`).
3. **Configure Dataset Info**:
   - Give your dataset a descriptive **Name** and **Domain/Category** (e.g., *Sales*, *Marketing*, *Operations*).
   - Add searchable **Tags** and a description for your team.
4. **Automated Validation**: Atlas scans the file for formatting and quality issues, infers the schema automatically, and assigns it an active version tag (e.g., `v1.0`).
5. **View Schema & Metadata**: Inspect column data types, row counts, and summary statistics on the dataset overview page.

---

### Workflow 2: Querying Data with Natural Language & SQL

Atlas allows both technical and non-technical team members to extract insights immediately.

#### Option A: Natural Language Querying (NLP)
1. Open any dataset and click **Explore with AI**.
2. Type your question in plain English into the search bar:
   - *"What were our top 5 selling products last month?"*
   - *"Find all customer accounts created after March with over $500 in spend."*
3. Atlas translates your query and displays the filtered data table instantly.

#### Option B: SQL Editor
1. Click the **SQL Studio** tab.
2. Write and run standard SQL queries directly against your datasets:
   ```sql
   SELECT region, SUM(revenue) AS total_revenue
   FROM sales_data
   WHERE year = 2026
   GROUP BY region
   ORDER BY total_revenue DESC;
   ```
3. View results in the interactive table or click **Export** (CSV/JSON).

---

### Workflow 3: Running Predictive Intelligence & Models

1. Navigate to **Intelligence Models** from the sidebar.
2. Select a pre-trained model suitable for your business goal (e.g., *Customer Churn Predictor*, *Revenue Forecaster*, *Anomaly Detector*).
3. **Map Input Data**: Choose the target dataset and match the required columns.
4. Click **Run Prediction**: Atlas processes the dataset and appends predictive scoring and confidence metrics directly to your results.

---

### Workflow 4: Setting Up Automated Data Pipelines

Automate recurring data transformations so your reports are always up to date.

1. Go to **Pipelines** > **Create Pipeline**.
2. Select the **Source Dataset** (e.g., daily sales uploads).
3. Define the **Transformation & Intelligence Rules** (e.g., filter out test transactions, apply currency conversion, generate predictive scores).
4. Set the **Trigger Schedule** (e.g., Daily at 02:00 UTC or Upon New File Upload).
5. Click **Activate Pipeline**. You can monitor run history and status logs from the **Pipeline Monitor**.

---

### Workflow 5: Exporting & Integrating Insights

- **Manual Download**: Click **Export** on any query or dataset view to download as **CSV** or **JSON**.
- **Agent Integration**: Share Atlas datasets directly with **Pluggedspace Console Agents** (e.g., Monica for customer support context or Marketer for audience segmentation).
- **API Access**: Use your Atlas API Key to query datasets programmatically from your own applications or BI dashboards.

---

## 💡 Best Practices

- **Keep Data Clean**: Use standard header names in CSV/Excel files to optimize automatic schema detection.
- **Tag Datasets Thoroughly**: Adding relevant domains and tags makes it easy for your whole team to find assets.
- **Use NLP for Quick Checks**: Start with Natural Language prompts to quickly explore hypotheses before writing detailed SQL queries.
- **Automate with Pipelines**: Instead of manual re-uploads, schedule automated pipelines to keep business metrics fresh.
