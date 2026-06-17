# PSAgents - End-User System Usage Documentation

Welcome to PSAgents, the central multi-tenant **Agentic OS** designed to configure, monitor, and scale your autonomous AI agent fleet. This guide details the step-by-step workflow for business users to operate the dashboard.

---

## 1. Getting Started: Signup & Workspace Initialization

1. **Accessing the Portal**: Navigate to `https://agents.pluggedspace.org/login`.
2. **Registration**: 
   - Toggle to **Register** and enter your Full Name, Email, Password, and your **Company/Organization Name** (this creates your isolated tenant space).
   - Click **Create Account**. You will receive an email verification link.
3. **Workspace Provisioning**: Upon successful registration, the backend automatically initializes a default tenant database schema, provisions unique widget API keys, and sets up your default agent profiles (Monica, Marketer, Business Finder).

---

## 2. Main Navigation & Modules

The platform is organized into distinct panels on the left-hand navigation bar:

```
[Overview]        - High-level health, telemetry, and pending task summary
[Inbox]           - The Human-in-the-Loop approval queue for agent actions
[Agent Fleet]     - Configuration panels for Monica, Marketer, Finder, etc.
[Memory Bank]     - Document upload center for RAG semantic knowledge ingestion
[Command Center]  - Real-time telemetry, intent stream monitor, and overrides
[Integrations]    - Connect API keys and accounts (Stripe, Apollo, Coinbase)
[Governance]      - Procurement audit logs, vendor verification, and invoice audits
[Finance]         - Financial runways, budget forecasts, and cashflow charts
[Settings]        - Workspace settings, domain locking, and profile details
```

---

## 3. Core Workflows for End-Users

### Workflow A: Uploading Knowledge to the Memory Bank
Agents cannot perform context-aware tasks without data. The **Memory Bank** is your central RAG (Retrieval-Augmented Generation) ingestion engine.
1. Click on **Memory Bank** in the sidebar.
2. Drag and drop or upload reference files: `.txt`, `.pdf`, `.docx`, or `.csv` (e.g., your business FAQ, service terms, pricing sheets, or company templates).
3. The platform automatically:
   - Extracts and structures the text.
   - Chunks the text with overlapping context.
   - Generates vector embeddings using the **Hugging Face connector**.
   - Indexes chunks in the `pgvector` database and syncs them to the unified **BrainBox Memory Substrate**.
4. Once indexed, the status will show **Vector Indexed** (Green). Your agents will now automatically reference this content in their prompt context window.

---

### Workflow B: Managing and Integrating Monica (CS Agent)
Monica is your customer service agent who runs via a chat widget on your public website.
1. Go to **Agent Fleet** > **Monica**.
2. **Operational Mode Configuration**:
   - **Manual**: Monica drafts answers, but every single response requires human approval.
   - **Hybrid (Recommended)**: Monica answers common queries autonomously. If confidence is low or a query is high-risk (e.g., refunds), the action is sent to the **Inbox** for approval.
   - **Autonomous**: Monica runs fully on autopilot, resolving all queries and escalations without manual check-ins.
3. **Behavior Customization**: Edit the **Personality Prompt** text area (e.g., *"You are a helpful customer support representative for Heyfae. Keep responses brief and polite."*).
4. **Website Widget Ingestion**:
   - Copy the integration script tag from the panel:
     ```html
     <script src="https://api.agents.pluggedspace.org/static/accounts/js/monica-widget.js?api_key=YOUR_API_KEY" async></script>
     ```
   - Paste it before the closing `</body>` tag on your website. Monica is now active and domain-locked to your website.

---

### Workflow C: Handling Action Approvals (The Inbox)
When an agent (like Monica or the Governance agent) triggers a critical action in **Manual** or **Hybrid** mode:
1. Navigate to **Inbox**.
2. Select any item from the left-hand feed. Each item details:
   - **Agent**: The agent that proposed the action (e.g., Monica).
   - **Proposed Action**: E.g., `refund_invoice`, `send_email`, or `process_data`.
   - **Confidence Score**: AI's self-assessed confidence (0.0 to 1.0).
   - **Risk Level**: Low, Medium, or High.
   - **AI Reasoning**: A concise explanation explaining why the agent chose this path.
3. Review the proposal, then click **Approve** (executes the payload and closes the task) or **Reject** (aborts the action).

---

### Workflow D: Managing Integrations
Enable your agents to interact with the real world by connecting your software stack.
1. Click **Integrations**.
2. Locate the service provider you wish to connect (e.g., **Stripe** for billing, **Apollo** for lead scraping, or **Coinbase** for cryptocurrency checkout).
3. Enter your API credentials or click **Connect Account** to complete the standard OAuth handshake.
4. Once marked **Connected**, agents can safely query these integrations to check invoice statuses, fetch new sales leads, or process payments.

---

### Workflow E: Monitoring Command Center & Logs
Track what your autonomous fleet is doing in real-time.
1. **Command Center**: View active tasks running in Celery worker pools, observe execution latency, and use the **Emergency Stop** override to temporarily pause all automated agent processes.
2. **Execution Logs**: Access the live stdout/stderr telemetry streams of background agent tasks (e.g., Marketer publishing posts or Business Finder scraping competitors) for debugging and audit logs.
