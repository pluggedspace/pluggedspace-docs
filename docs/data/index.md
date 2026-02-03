# Akili’s Weave (Space): Enterprise Intelligence Platform

Akili’s Weave is an **Enterprise Intelligence Platform** engineered to transform raw data into production-ready insights. It serves as a centralized hub for high-quality data assets and pre-trained AI models, optimized for African data contexts.

## 🏗️ High-Level Architecture
The system is built on **Django** for management and **DuckDB** for high-performance analytical queries. It supports multi-provider cloud storage and features a robust multi-tenancy model.

### Core Components
- **Dataset Management (`core`)**: Handles dataset metadata, versioning, and lifecycle.
- **SQL Engine (`duck`)**: Integrates DuckDB for fast, local-first SQL execution.
- **Ingestion Engine (`ingestion`)**: Automates schema inference and data loading.
- **Intelligence Infrastructure (`predictor`)**: Manages centrally provisioned models, performance logging, and inference.
- **Tenancy & Billing (`passapp`)**: Manages tenants, roles, and usage quotas.
- **Compliance (`drac`)**: Automated data quality and compliance checks.
- **Distributed Tasks**: Powered by **Celery** and **Redis** for asynchronous processing.

## 🛠️ Sub-level Functionality

### 1. Dataset Lifecycle
- **Ingestion**: Supports CSV, Parquet, and Excel. Automatically infers schema.
- **Layering**: Datasets move through `raw`, `processed`, `refined`, `feature_store`, and `trained` layers.
- **Versioning**: Every update creates a new version with an audit trail of changes.
- **Lineage**: Tracks dependencies between datasets and transformations.

### 2. Intelligent Querying
- **DuckDB Integration**: Allows running complex SQL on files without loading them into a traditional database.
- **NLP Interface**: Translates Natural Language queries into SQL or performs semantic searches across datasets.
- **Export**: Data can be exported as CSV or JSON via API.

### 3. Intelligence & Model Delivery
- **Curated Model Registry**: Provides access to high-performance, centrally managed AI models.
- **Intelligence Pipelines**: Automated workflows that transform refined data into actionable predictions.
- **Edge Inference**: Optimized endpoints for low-latency intelligence consumption by tenants.

### 4. Tenancy & Resource Management
- **Multi-tenancy**: Isolated data and resources per tenant.
- **Usage Quotas**: Tracks compute minutes, tokens, and storage bytes.
- **Billing**: Generates records based on usage logs and subscription plans.

### 5. Data Compliance (DRAC)
- **Pre-ingestion Checks**: Files are scanned for compliance before ingestion.
- **Audit Logging**: Every action is recorded for security and compliance monitoring.
