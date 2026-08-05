# Weave - End-User System Usage Documentation

Welcome to Weave, the central multi-tenant **Agentic OS** designed to configure, monitor, and scale your autonomous AI agent fleet. This guide details the step-by-step workflow for business users to operate the dashboard.

> **System Version:** V4 (Enhanced Ecosystem)  
> **Last Updated:** July 28, 2026

---

## 1. Getting Started: Signup & Workspace Initialization

1. **Accessing the Portal**: Navigate to `https://agents.pluggedspace.org/login`.
2. **Registration**: 
   - Toggle to **Register** and enter your Full Name, Email, Password, and your **Company/Organization Name** (this creates your isolated tenant space).
   - Click **Create Account**. You will receive an email verification link.
3. **Workspace Provisioning**: Upon successful registration, the backend automatically initializes a default tenant database schema, provisions unique widget API keys, and sets up your default agent profiles (Monica, Marketer, Business Finder).
4. **V4 Features**: Your workspace now includes access to the **Marketplace** for agent packages, **Skills System** for reusable capabilities, **28+ Tools** across domains, and enhanced **Observability Dashboard**.

---

## 2. Main Navigation & Modules

The platform is organized into distinct panels on the left-hand navigation bar:

```
[Overview]        - High-level health, telemetry, and pending task summary
[Inbox]           - The Human-in-the-Loop approval queue for agent actions
[Agent Fleet]     - Configuration panels for Monica, Marketer, Finder, etc.
[Tenant Agents]   - Custom agent builder with skills and tool scope (V4)
[Marketplace]     - Browse and install agent packages from community (V4)
[Memory Bank]     - Document upload center for RAG semantic knowledge ingestion
[Artifacts]       - Persistent file artifacts with versioning (V4)
[Command Center]  - Real-time telemetry, intent stream monitor, and overrides
[Integrations]    - Connect API keys and accounts (Stripe, Apollo, Coinbase)
[Governance]      - Procurement audit logs, vendor verification, and invoice audits
[Finance]         - Financial runways, budget forecasts, and cashflow charts
[Skills]          - Reusable skill library and management (V4)
[Policy]          - Configure agent behavior rules and constraints (V4)
[Console]         - Interactive debugging and agent testing interface (V4)
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
3. **V4 Observability Dashboard**: Enhanced metrics including tool health reports, per-agent telemetry, alert engine for system health, and real-time event streaming via WebSocket.

---

### Workflow F: Creating Custom Tenant Agents (V4)
Build your own agents with the Tenant Agent builder.
1. Go to **Tenant Agents** in the sidebar.
2. Click **Create New Agent**.
3. **Basic Configuration**:
   - **Name**: Give your agent a descriptive name.
   - **Description**: Explain what this agent does.
   - **Agent Type**: Choose `reactive` (responds to triggers), `proactive` (scheduled tasks), or `hybrid`.
4. **Capabilities**:
   - **Skills**: Select from the skill library (e.g., WebsiteAuditor, SEOAnalyzer, InvoiceExtractor).
   - **Tool Scope**: Choose which tools the agent can access (email, crm, browser, database, etc.).
   - **Trigger Words**: Define keywords that activate this agent.
   - **Memory Types**: Select memory types the agent can read/write.
5. **Behavior**:
   - **System Prompt**: Customize the agent's personality and instructions.
   - **Persona Name**: Give your agent a persona name.
6. **Publish**: Toggle **Publish to Marketplace** to share your agent with other tenants (optional).
7. Click **Save** to create your custom agent.

---

### Workflow G: Using the Marketplace (V4)
Discover and install agent packages from the community.
1. Go to **Marketplace** in the sidebar.
2. **Browse Packages**: View published agent packages from other tenants with ratings and reviews.
3. **Package Details**: Click on a package to see:
   - Description and capabilities
   - Average rating and review count
   - Installation status
4. **Install Package**: Click **Install** to add the package to your workspace.
5. **Rate Package**: After using a package, leave a rating (1-5 stars) and review to help others.
6. **Manage Installed**: View all your installed packages in the **Installed** tab and uninstall if needed.

---

### Workflow H: Managing Skills (V4)
Skills are reusable capabilities that can be shared across agents.
1. Go to **Skills** in the sidebar.
2. **Browse Skills**: View available skills including:
   - **WebsiteAuditor**: Analyzes website HTML for technographics
   - **SEOAnalyzer**: Analyzes SEO metadata and page structure
   - **InvoiceExtractor**: Extracts structured data from invoices
   - **LeadGenerator**: Generates leads from search results
   - **VendorVerifier**: Verifies vendor credentials and compliance
3. **Skill Details**: Click on a skill to see its description, required tools, and output schema.
4. **Use in Agents**: When creating or editing a Tenant Agent, select skills from the library to add capabilities.

---

### Workflow I: Configuring Policies (V4)
Set up rules to control agent behavior and enforce constraints.
1. Go to **Policy** in the sidebar.
2. **Create Policy Rule**:
   - **Agent Pattern**: Use glob patterns to match agents (e.g., `*` for all, `finance` for finance agent only).
   - **Action Pattern**: Match specific actions (e.g., `transfer`, `delete`).
   - **Constraint Type**: Choose from:
     - `max_amount`: Limit monetary amounts
     - `rate_limit`: Restrict execution frequency
     - `time_window`: Restrict execution to specific time periods
     - `require_approval`: Force human approval
     - `deny`: Block the action entirely
     - `allow`: Permit the action
     - `confidence_threshold`: Require minimum AI confidence
   - **Constraint Value**: Set specific values for the constraint.
   - **Approval Role**: Specify who must approve (if `require_approval`).
   - **Priority**: Set rule priority (higher priority rules override lower ones).
3. **Activate Policy**: Toggle **Active** to enable the rule.
4. **Test Policy**: Use the **Evaluate** endpoint to test how a policy would affect specific actions.

---

### Workflow J: Using the Console (V4)
Debug and test agents interactively via the console interface.
1. Go to **Console** in the sidebar.
2. **Available Commands**:
   - `list`: List all available agents
   - `inspect <agent_id>`: Inspect agent configuration and state
   - `test <agent_id> <input>`: Test an agent with specific input
   - `status`: Show system status and health
   - `help`: Show available commands
3. **Interactive Testing**: Use the console to quickly test agent responses without going through the full workflow.
4. **Debugging**: Inspect agent state, variables, and execution history for troubleshooting.

---

### Workflow K: Managing Artifacts (V4)
Access and manage persistent file artifacts created by agents.
1. Go to **Artifacts** in the sidebar.
2. **View Artifacts**: Browse all artifacts created by your agents, filterable by:
   - Type (PDF, Excel, CSV, JSON, Image, etc.)
   - Agent that created it
   - Workspace
3. **Artifact Details**: Click on an artifact to see:
   - Metadata and creation info
   - Version history
   - Checksum for integrity verification
4. **Download**: Click **Download** to retrieve the artifact file.
5. **Version Control**: Create new versions of artifacts when agents update them, maintaining full history.
6. **Delete**: Remove artifacts that are no longer needed.

---

## 4. V4 Enhanced Tool Ecosystem

Weave V4 includes **28 comprehensive tools** across multiple domains, expanding from the original 14 tools. These tools are available to agents based on their configured tool scope.

### Tool Categories

**Communication Tools:**
- `email` - Send, read, and list emails
- `slack`Send and read Slack messages
- `whatsapp` - Send and read WhatsApp messages
- `notification` - Send notifications and alerts

**Data & Content Tools:**
- `database` - Query databases and inspect schemas
- `excel` - Read and write Excel spreadsheets
- `pdf` - Read and extract content from PDFs
- `ocr` - Extract text from images using OCR
- `search` - Web search and news search
- `scraper` - Web scraping and data extraction

**Business & CRM Tools:**
- `crm` - Read, write, and search CRM data
- `payments` - Process charges and refunds
- `calculator` - Perform calculations and evaluate expressions
- `report` - Generate and export reports

**Development & Integration Tools:**
- `github` - Manage repositories, pull requests, and issues
- `browser` - Browser automation and screenshots
- `maps` - Geocoding and distance calculations
- `calendar` - Read and write calendar events

**Analytics & Intelligence Tools:**
- `sentiment_analyzer` - Analyze sentiment in text
- `seo_tool` - SEO analysis and auditing
- `social_media_tool` - Social media posting and analysis
- `telemetry_tool` - Collect and report telemetry data
- `ticket_tool` - Create and manage support tickets

**Specialized Tools:**
- `compliance_checker` - Check compliance and validate regulations
- `enrichment_api` - Enrich data with external APIs
- `newsletter_tools` - Create, send, and schedule newsletters

### Tool Access

Tools are automatically available to agents based on:
1. **Agent Configuration**: Each agent's tool scope determines which tools it can access
2. **Tenant Policies**: Policy rules can restrict tool usage based on constraints
3. **Skill Requirements**: Skills specify which tools they need to function
4. **Integration Status**: Some tools require connected integrations (e.g., Slack requires Slack API credentials)

---

## 5. V4 System Enhancements Summary

### New Capabilities in V4

**Tenant Agent Builder:**
- Create custom agents with configurable skills, tool scope, and behavior
- Publish agents to the marketplace for sharing
- Test agents interactively before deployment

**Enhanced Marketplace:**
- Browse community-created agent packages
- Rate and review packages
- Install packages with one click

**Skills System:**
- Reusable skill library with extensive pre-built skills
- Skills can be composed across multiple agents
- Skill definitions include required tools and output schemas

**Policy Engine:**
- Fine-grained control over agent behavior
- Multiple constraint types (amount limits, rate limits, time windows, etc.)
- Priority-based rule evaluation

**Observability Dashboard:**
- Real-time tool health monitoring
- Per-agent telemetry and metrics
- Alert engine for system health issues
- WebSocket-based event streaming

**Console Interface:**
- Interactive debugging and testing
- Agent inspection and state viewing
- Quick command-line access to system functions

**Background Scheduler:**
- Advanced task scheduling with cron-like capabilities
- Task lifecycle management
- Background task monitoring and cancellation

**Package System:**
- Agent package management
- Dynamic loading and unloading
- Manifest-based package definitions

**Enhanced Memory:**
- Expanded memory types (9 types vs original 3)
- Improved semantic search capabilities
- Better legacy BrainBox integration

**Artifact Management:**
- Version control for all agent-generated files
- Checksum verification for integrity
- Workspace association and filtering

---

## 6. Best Practices

### Security
- Always use **Hybrid** or **Manual** mode for high-risk agents (Finance, Governance)
- Regularly review and update your **Policy Rules** to match business requirements
- Keep your **Integrations** credentials secure and rotate them periodically
- Use **Domain Locking** for the Monica widget to prevent unauthorized usage

### Performance
- Monitor the **Observability Dashboard** regularly for system health
- Use **Artifact versioning** to manage file storage efficiently
- Configure **Policy rate limits** to prevent API overuse
- Review **Tool health reports** to identify degraded tools

### Agent Management
- Start with **Hybrid mode** for new agents to balance autonomy and safety
- Use **Skills** to avoid duplicating capabilities across agents
- Test agents in the **Console** before full deployment
- Review **Agent telemetry** to optimize performance

### Memory Management
- Regularly upload relevant documents to the **Memory Bank**
- Use appropriate **Memory types** for different kinds of data
- Monitor **Memory usage** to ensure efficient storage
- Leverage **Semantic search** for context-aware agent responses

---

## 7. Troubleshooting

### Common Issues

**Agent not responding:**
1. Check **Command Center** for active tasks and errors
2. Verify **Integrations** are properly connected
3. Review **Policy rules** that might be blocking actions
4. Use **Console** to test the agent directly

**High approval queue backlog:**
1. Consider switching to **Hybrid mode** for low-risk actions
2. Adjust **Policy rules** to reduce required approvals
3. Review **Agent telemetry** to identify bottlenecks
4. Scale **Celery workers** if processing is slow

**Memory search not returning results:**
1. Ensure documents are properly uploaded to **Memory Bank**
2. Check that **Vector indexing** completed successfully (green status)
3. Verify **Memory types** are correctly configured
4. Review **Search queries** for appropriate terms

**Tool execution failures:**
1. Check **Tool health reports** in Observability
2. Verify **Integration credentials** are valid
3. Review **Policy constraints** that might block the tool
4. Check **Background task logs** for detailed error messages

### Getting Help

- **Documentation**: Refer to `COMPREHENSIVE_SYSTEM_ARCHITECTURE.md` for detailed technical documentation
- **API Reference**: Check `api_endpoints.md` for complete API documentation
- **Reproducibility**: Refer to `reproducibility.md` for detailed reproducibility information
- **Status**: Review `WHATSUP.md` for known issues and system status
- **Support**: Contact support through the **Settings** panel or email support@pluggedspace.org
