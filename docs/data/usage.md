# Akili’s Weave (Space): Usage Guide

This guide outlines user responsibilities and workflows based on their role in the system.

## 🛡️ Role: Admin
Admins manage the operational aspects of the platform for a tenant.
- **Metadata Management**: Create and manage Worlds/Domains for data organization.
- **Pipelines**: Monitor and trigger data processing pipelines. View run history and logs.
- **System Health**: Monitor ingestion jobs and notification feeds.
- **Compliance**: Review audit logs and compliance check results.

## 🏢 Role: Tenant User
Tenant Users are categorized based on their technical needs.

### 🔭 Viewer
- **Data Discovery**: Browse public and tenant-specific datasets.
- **Metadata Review**: View dataset schemas, tags, and descriptions.
- **Notifications**: Receive alerts about dataset updates.

### 📊 Analyst
*Includes all Viewer capabilities, plus:*
- **Querying**: Run SQL queries on datasets via the DuckDB engine.
- **NLP Search**: Use natural language to find and filter data.
- **Exporting**: Download filtered datasets or query results as CSV/JSON.

### 🧪 Intelligence Analyst (formerly Data Scientist)
*Includes all Analyst capabilities, plus:*
- **Inference Optimization**: Utilize pre-trained enterprise models for predictive tasks.
- **Performance Monitoring**: Review accuracy and reliability metrics of available models.
- **Custom Inference**: Configure inference parameters for specific business use cases.
- **Intelligence Pipelines**: Integrate platform-delivered insights into external workflows.

## 🌎 Role Hierarchy & Permissions

| Role | Responsibility | Key Capability |
| :--- | :--- | :--- |
| **Tenant Owner** | Account & Legal Authority | Subscription Management, Admin Management |
| **Admin** | Operational Data Management | **Pipeline Management**, Domain Setup, Ingestion Monitoring |
| **Analyst** | Intelligence Consumption | SQL/NLP Queries, Exports, Basic Inference |
| **Viewer** | Data Oversight | Read-only access to Metadata & Public Datasets |

> [!IMPORTANT]
> In the Enterprise Intelligence model, heavy-duty model training and refinement are managed centrally by the Platform Owner and System Admins. Tenants focus on **Intelligence Orchestration** via pipelines.
