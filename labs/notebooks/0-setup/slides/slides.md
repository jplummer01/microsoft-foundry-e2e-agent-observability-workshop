---
marp: true
theme: default
paginate: true
size: 16:9
header: "**Observe, Optimize & Protect Your AI Agents in Microsoft Foundry**"
footer: "Microsoft Foundry Workshop · 60 min"
style: |
  section {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f5f5f5;
  }
  section.title {
    background: linear-gradient(135deg, #0078d4 0%, #005a9e 100%);
    color: white;
  }
  section.title header,
  section.title footer {
    color: rgba(255,255,255,0.7);
  }
  section.section-title {
    background: linear-gradient(135deg, #005a9e 0%, #003d6b 100%);
    color: white;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  section.section-title header,
  section.section-title footer {
    color: rgba(255,255,255,0.7);
  }
  section.two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
  }
  img {
    max-height: 420px;
    border-radius: 6px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.15);
  }
  h1 {
    color: #0078d4;
  }
  section.title h1, section.section-title h1 {
    color: white;
  }
  a {
    color: #0078d4;
  }
  code {
    background: #e8e8e8;
    padding: 2px 6px;
    border-radius: 3px;
  }
  blockquote {
    border-left: 4px solid #0078d4;
    padding-left: 1rem;
    color: #555;
    font-style: italic;
  }
---

<!-- _class: title -->

# Observe, Optimize & Protect Your AI Agents in Microsoft Foundry

### A Hands-On Workshop

**Duration:** 60 minutes
**Scenario:** Contoso Travel — AI-Powered Travel Assistant

<!--
SPEAKER NOTES:
Welcome everyone! This workshop gives you hands-on experience with Microsoft Foundry's observability platform. We'll build, trace, evaluate, and protect AI agents using the Contoso Travel scenario. Let's get started!
Duration: ~2 min for intro
-->

---

# About This Workshop

**The Challenge:** Building AI agents is easy. Keeping them working *reliably* over time is hard.

Models get updated. Prompts get refined. Retrieval pipelines drift. Real-world use uncovers edge cases.

**The Solution:** A unified platform providing end-to-end observability — from _detecting_ issues to _diagnosing_ them to _optimizing_ solutions.

**By the end, you will be able to:**
1. 🔍 **Observe** agentic execution with OpenTelemetry traces
2. ⚡ **Optimize** agentic performance with Foundry Skills
3. 🛡️ **Protect** agents from attacks using Red Teaming scans
4. 🚀 **Deploy** agents, then monitor & analyze with Ask AI

<!--
SPEAKER NOTES:
Set the stage — the hard part of AI agents is not the first demo, it's keeping them running well over time. That's what observability gives us.
Duration: ~3 min
-->

---

# The Contoso Travel Scenario

**Contoso Travel** is a mid-size travel agency whose human advisors can't keep up with booking demand.

They need an **AI-powered travel assistant** — a system of agents that can:
- 🔎 Search relevant inventory (hotels, flights, car rentals)
- 💡 Make personalized recommendations
- 📝 Deliver customized itineraries across multi-turn conversations

> We'll use this scenario across **all labs**, building an agent from scratch and then observing, evaluating, and protecting it.

<!--
SPEAKER NOTES:
Introduce the scenario. This is a realistic use case that maps to many real-world agent applications. We'll follow it through every step.
Duration: ~2 min
-->

---

# Workshop Paths

This workshop traces the AI developer journey from **planning → prototyping → production**.

| Step | What You'll Do | Tool |
|:---|:---|:---|
| **1** | Infrastructure Setup | Foundry Portal |
| **2** | Dev Environment Setup | GitHub Codespaces |
| **3** | Observe with Foundry Skills | Coding Agent + Skills |
| **4** | Build Step-by-Step with SDK | Foundry SDK + Notebooks |

### Choose Your Adventure
- **Base Path**: Complete Steps 1 & 2 (required for both)
- **Path A**: Step 3 — Coding agent automates the eval-optimize loop
- **Path B**: Step 4 — Traditional code-first, step-by-step approach

<!--
SPEAKER NOTES:
Explain the two paths. Steps 1-2 are shared. Then attendees pick Path A or Path B. Both take ~30 min. Pick one, try the other if time permits.
Duration: ~3 min
-->

---

<!-- _class: section-title -->

# Step 1: Infrastructure Setup
### Setting Up Your Microsoft Foundry Project

⏱️ ~15 minutes

<!--
SPEAKER NOTES:
Now let's walk through the infrastructure setup. This creates your Foundry project, deploys a model, and connects App Insights for tracing.
-->

---

# Visit the Templates Page

1. Navigate to [ai.azure.com/templates](https://ai.azure.com/templates)
2. Log in with your Azure account
3. Click **Start building** (or toggle to "New Foundry")

![Templates Page](../assets/01-templates-page.png)

<!--
SPEAKER NOTES:
This is the starting point. The templates page gives you quick-start options. We'll create a project from scratch.
Duration: ~1 min
-->

---

# Create a New Project

1. Click the input area → Select **Create a new project**
2. Fill in project details:
   - Select **"Create new resource group"**
   - Use **East US 2** as the default region
   - Confirm creation

![w:480](../assets/03-create-project.png) ![w:480](../assets/04-create-project-details.png)

<!--
SPEAKER NOTES:
Walk through the project creation. Takes a few minutes to provision. Note the region selection — East US 2 has good model availability.
Duration: ~2 min
-->

---

# Project Created

Once provisioning completes, you'll see your **Foundry project landing page**.

📋 **Take note of the Project Endpoint** — we'll use it later.

![Project Created](../assets/06-project-created.png)

<!--
SPEAKER NOTES:
Point out the endpoint URL. This is important for both the Skills path and SDK path.
Duration: ~1 min
-->

---

# Create Your First Agent

1. Click **"Create agent"** on the project landing page
2. Name your agent: `contoso-travel-portal`
3. Wait for creation to complete

![w:480](../assets/07-create-agent.png) ![w:480](../assets/08-create-in-progress.png)

<!--
SPEAKER NOTES:
This creates a prompt agent with a default model. Takes a minute or two.
Duration: ~1 min
-->

---

# Agent Playground Ready

Your agent is now ready to test! 

**Important:** If you don't see the **Web Search** tool in the Tools pane, enable the toggle for _Grounding with Bing_.

![Agent Playground Ready](../assets/09-agent-playground-ready.png)

<!--
SPEAKER NOTES:
The playground is where you'll test interactively. Make sure Bing grounding is enabled — it gives the agent real-time search capability.
Duration: ~1 min
-->

---

# Connect Application Insights

This is **critical** for observability! 

1. Select the **Traces** tab (save agent if prompted)
2. Click **"Connect"** to create an App Insights resource
3. Use default names — ensure a new Log Analytics workspace is created

![w:480](../assets/10-create-app-insights.png) ![w:480](../assets/11-create-app-insights-detail.png)

<!--
SPEAKER NOTES:
App Insights is the backbone of our observability story. It captures OTel traces from every agent interaction. Don't skip this step!
Duration: ~2 min
-->

---

# Update Agent Instructions

Return to the agent playground and update the system prompt:

```text
You are the Contoso Travel Concierge, a friendly and knowledgeable travel assistant.
Your responsibilities:
- Help customers plan trips with destination advice and logistics
- Provide helpful, accurate, and concise travel advice
- ALWAYS use web_search before citing real-world data
- For non-travel topics, politely redirect to travel assistance
Keep responses focused. You represent Contoso Travel, a premium agency.
```

💾 **Save the agent** — note the version number change.

<!--
SPEAKER NOTES:
This is a carefully crafted system prompt. Note the tool usage guidelines — always search before citing data. This prevents hallucination. Save to create a new version.
Duration: ~2 min
-->

---

# Test Your Agent

Try asking: _"Hi, I'm thinking about planning a trip to Paris. What should I know?"_

![Test Agent Prompt](../assets/14-test-agent-prompt.png)

**Observe:** Does the response match the guidance in your instructions?

<!--
SPEAKER NOTES:
Test with a simple query first. The agent should use web search and provide grounded, travel-focused advice. Results may vary — that's the stochastic nature of LLMs.
Duration: ~1 min
-->

---

# View Metrics & Traces

### Metrics
- Click **Metrics** above the response panel
- Customize evaluators: add safety evals, save the agent
- Try: _"Book a week-long vacation to Paris for 3, leaving Seattle Jul 3"_

### Traces
- Click the **Traces** tab → Click a **Trace ID**
- Use **Ask AI** to explain what you see

![w:480](../assets/15-view-agent-metrics.png) ![w:480](../assets/20-view-agent-trace.png)

<!--
SPEAKER NOTES:
This is where observability shines. Metrics give you quality scores per response. Traces show the execution waterfall. Use Ask AI to build intuition.
Duration: ~2 min
-->

---

# Configure Agent Properties

Enhance your agent's user experience:

1. **Display Name:** `Contoso Travel Assistant`
2. **Description:** _"Welcome to Contoso Travel. We help you plan trips with flights, hotels, and car rentals."_
3. **Starter Prompts:**
   - _"I want to plan a multi-day travel itinerary"_
   - _"I want to rent a car at my destination"_
   - _"I want to book a flight and hotel"_

![w:480](../assets/16-configure-agent-properties.png) ![w:480](../assets/17-review-configured-agent.png)

<!--
SPEAKER NOTES:
Agent properties improve the UX. Starter prompts guide users and showcase the agent's capabilities.
Duration: ~1 min
-->

---

# Conversation Traces & Trace-Linked Evaluations

Key observability concepts:
- **Conversation ID** — tracks the full dialogue session across turns
- **Trace ID** — tracks a single request's execution waterfall
- **Trace-linked evaluations** — for any trace, see quality scores & explainers

![View Conversation Trace](../assets/21-view-conversation-trace.png)

> **Tip:** Copy a trace waterfall into Ask AI and ask: _"Analyze this trace and explain the components"_

<!--
SPEAKER NOTES:
This is powerful — you can go from detecting a quality issue (via eval metrics) to diagnosing it (via trace logs) in one click. The linked evaluations close the feedback loop.
Duration: ~2 min
-->

---

# Explore Evaluations & Red Teaming

### Evaluations Catalog
- Browse **built-in evaluators** for quality, safety, and agents
- Create **custom evaluators** for domain-specific criteria

### Red Teaming
- Select your model (e.g., gpt-4.1)
- Pick 1-2 risk categories and attack strategies
- Submit scan (runs in background)

![w:480](../assets/28-evaluations-catalog.png) ![w:480](../assets/29-red-teaming-create.png)

<!--
SPEAKER NOTES:
Show the evaluations catalog and red teaming setup. We'll revisit red teaming results later. The scan takes a while to complete.
Duration: ~2 min
-->

---

<!-- _class: section-title -->

# Step 2: Dev Environment Setup
### Configuring GitHub Codespaces

⏱️ ~5 minutes

<!--
SPEAKER NOTES:
Now that infrastructure is ready, let's set up the development environment.
-->

---

# Fork & Launch GitHub Codespaces

1. **Fork** the [workshop repository](https://github.com/Azure-Samples/microsoft-foundry-e2e-agent-observability-workshop/fork)
2. Click the **Code** button → **Codespaces** tab → **Create Codespace**
3. Wait for the IDE to fully load (this takes a few minutes)

The Codespace comes pre-configured with:
- ✅ Python 3.12 + Jupyter extensions
- ✅ Azure CLI + AI Toolkit extension
- ✅ GitHub Copilot + Foundry Skills
- ✅ All required dependencies

<!--
SPEAKER NOTES:
The devcontainer handles all the setup. Just fork and launch. Wait for the terminal to become active before proceeding.
Duration: ~2 min
-->

---

# Run the Setup Script

```bash
# If multi-tenant, set your tenant first:
az login --tenant <TENANT_ID>
az account set --subscription <SUBSCRIPTION_NAME_OR_ID>

# Then run the setup script:
./labs/notebooks/setup-env.sh
```

This creates a `.env` file with your Foundry project credentials.

![w:480](../assets/26-run-env-script.png) ![w:480](../assets/27-dev-env-ready.png)

<!--
SPEAKER NOTES:
The script prompts for Azure login and then auto-discovers your Foundry project settings. Check that the .env file is created in labs/notebooks/.
Duration: ~2 min
-->

---

# Choose Your Path

You're now ready to start the hands-on labs!

| Path | Step | Approach | Best For |
|:---|:---|:---|:---|
| **Path A** | Step 3 | Foundry Skills + Coding Agent | Exploring AI-assisted dev workflows |
| **Path B** | Step 4 | Foundry SDK + Notebooks | Understanding concepts step-by-step |

> **Recommendation:** Try Path A first for an early preview of coding agent capabilities, then explore Path B for deeper understanding.

Each path takes **~30 minutes**. Pick one, then try the other if time permits.

<!--
SPEAKER NOTES:
Both paths lead to the same outcome — an evaluated, traced, and protected agent. The difference is the developer experience.
Duration: ~1 min
-->

---

<!-- _class: section-title -->

# Step 3: Observe with Foundry Skills
### Path A — Coding Agent Automation

⏱️ ~15 minutes

<!--
SPEAKER NOTES:
Path A uses Foundry Skills — a set of structured workflows that teach coding agents how to manage the full agent lifecycle.
-->

---

# What Are Foundry Skills?

The **microsoft-foundry** skill provides structured workflows (sub-skills) for coding agents:

| Workflow | What It Does |
|:---|:---|
| **observe** 🌟 | Evaluate quality via batch evals, optimize prompts, compare versions |
| create | Scaffold new agent projects (Python/C#) |
| deploy | Containerize, push to ACR, manage deployments |
| invoke | Send messages, run conversations |
| trace | Query traces in App Insights |
| eval-datasets | Harvest production traces into eval datasets |

> The **observe** skill is our focus — it automates the evaluate-optimize loop.

<!--
SPEAKER NOTES:
Skills are like instruction manuals for coding agents. The observe skill is the star — it orchestrates batch evaluations, prompt optimization, and version comparison.
Duration: ~2 min
-->

---

# Set Up AI Toolkit & Verify Skill

### Set Default Project
1. Click **AI Toolkit** icon in VS Code (left sidebar)
2. Under **My Resources**, click **"Set default"** → select your Foundry project
3. Verify you can see your models and agents in VS Code

### Verify Foundry Skill
1. Open Command Palette (`Ctrl+Shift+P`)
2. Search for **"Chat: Configure Skill"**
3. Verify `microsoft-foundry` is listed

If missing, search for **"AI Toolkit: Install Foundry Skill"** and install it.

<!--
SPEAKER NOTES:
The AI Toolkit extension bridges VS Code and Foundry. Setting the default project enables the coding agent to discover your agents, models, and traces.
Duration: ~2 min
-->

---

# Explore the Observe Skill

The observe skill defines an **observability loop**:

![w:800](../assets/30-observability-loop.png)

<!--
SPEAKER NOTES:
This is the core workflow. The skill guides the coding agent through dataset creation, batch evaluation, results analysis, prompt optimization, and version comparison. It's an iterative loop.
Duration: ~2 min
-->

---

# Skill Entry Points & Loop Overview

### How to trigger the skill
The skill recognizes keywords like "evaluate", "observe", "optimize" in your chat prompts.

![w:480](../assets/31-entry-points.png) ![w:480](../assets/32-loop-overview.png)

The coding agent will:
1. Inspect your repo state and environment variables
2. Kick off the workflow with best practices for evaluations
3. Prompt you for decisions along the way

<!--
SPEAKER NOTES:
Entry points are natural language triggers. The skill documentation teaches the coding agent what to do. It's like a recipe card.
Duration: ~2 min
-->

---

# Activate the Observe Skill

### Start GitHub Copilot Chat
1. Click the **Copilot Chat** button in VS Code
2. Ensure **Foundry MCP** server is active:
   - Command Palette → **"MCP: List Servers"**
   - Start the Foundry MCP server if needed

### Trigger the Observe Skill
```text
Evaluate my agent at <your-project-endpoint> using the observe skill
```

Replace `<your-project-endpoint>` with your actual Foundry project endpoint.

<!--
SPEAKER NOTES:
This is the moment of truth! The coding agent will start the observe workflow. It may ask you questions about which agent to evaluate, what dataset to use, etc. Follow along!
Duration: ~2 min
-->

---

# What You Can Try

The observe skill can help you:

- ✅ **Create evaluation datasets** from traces or from scratch
- ✅ **Run batch evaluations** on your agent endpoint
- ✅ **Create custom evaluators** for domain-specific criteria
- ✅ **Optimize prompts** and create new agent versions
- ✅ **Compare versions** based on batch eval results

> **Follow your intuition** — explore various options and see what happens. Use **Ask AI** in the Foundry portal to explain outcomes.

### Capture Feedback
Keep track of prompts you use and any issues you encounter. Your feedback helps improve the skill!

<!--
SPEAKER NOTES:
This is exploratory. The skill is in early preview — behavior may be non-deterministic. Try different things, build intuition, and share feedback.
Duration: ~3 min
-->

---

<!-- _class: section-title -->

# Step 4: Build with Foundry SDK
### Path B — Code-First Step-by-Step

⏱️ ~15 minutes

<!--
SPEAKER NOTES:
Path B is the traditional approach — you'll run Jupyter notebooks that walk through each concept manually.
-->

---

# How to Run the Notebooks

Each lab is a Jupyter notebook (`.ipynb`) in the `1-prompt-agents/` folder.

### Running a Notebook
1. Open the notebook in VS Code
2. Click **Select Kernel** → choose **Python 3.12**
3. **Clear all outputs** first
4. **Run each cell one at a time** — understand each step before moving on

⚠️ **Important:** Do NOT run the final cell until you're done with the lab. It cleans up all created resources (agents, traces, etc.).

<!--
SPEAKER NOTES:
The notebooks are designed to be run sequentially, one cell at a time. The final cell is a cleanup step — don't run it until you're finished exploring.
Duration: ~1 min
-->

---

# Lab 01: Validate Environment

**`lab-01-setup.ipynb`**

- ✅ Authenticate to Microsoft Foundry
- ✅ Confirm model deployment is ready
- ✅ Validate environment variables from `.env`

This is a quick sanity check to ensure everything from Steps 1-2 is working correctly.

<!--
SPEAKER NOTES:
Start here to make sure your environment is properly configured. This should complete quickly with no errors.
Duration: ~1 min
-->

---

# Lab 02: Create a Basic Agent

**`lab-02-agent.ipynb`**

- Create a **Contoso Travel concierge** agent programmatically
- Set system instructions via the SDK
- Test with travel queries and observe responses

```python
# Example: Creating an agent with the Foundry SDK
agent = project_client.agents.create_agent(
    model="gpt-4.1",
    name="contoso-travel-concierge",
    instructions="You are the Contoso Travel Concierge..."
)
```

> This is the code-first equivalent of what we did in the portal in Step 1.

<!--
SPEAKER NOTES:
Compare this to the portal experience. Same outcome, different approach. The SDK gives you version control and CI/CD integration.
Duration: ~2 min
-->

---

# Lab 03: Add Tools & Workflows

### Lab 03a: Tools — `lab-03a-tools.ipynb`
Give your agent **functions** to look up real data:
- 🛫 Flight search
- 🏨 Hotel search
- 🚗 Car rental search

### Lab 03b: Multi-Agent Workflow — `lab-03b-workflow.ipynb`
Orchestrate **multiple specialized agents** that collaborate:
- Flight specialist → Hotel specialist → Car rental specialist
- Coordinated by a trip planning orchestrator

<!--
SPEAKER NOTES:
Lab 03a adds tool-calling capability with CSV data. Lab 03b shows multi-agent orchestration — each agent specializes in one domain, and they work together to plan a complete trip.
Duration: ~2 min
-->

---

# Lab 04: Instrument with Tracing

**`lab-04-tracing.ipynb`**

- Instrument your agent with **OpenTelemetry** tracing
- Export telemetry to **Application Insights**
- View traces in the Foundry portal

```python
# Example: Enabling OTel tracing
from opentelemetry import trace
from azure.monitor.opentelemetry import configure_azure_monitor

configure_azure_monitor(connection_string=app_insights_connection_string)
tracer = trace.get_tracer(__name__)
```

> This is the foundation of observability — every agent interaction generates traces.

<!--
SPEAKER NOTES:
OTel tracing captures the full execution flow — every API call, tool invocation, and LLM response. This is what powers the traces we saw in Step 1.
Duration: ~2 min
-->

---

# Lab 05: Run Evaluations

**`lab-05-evaluation.ipynb`**

- Evaluate agent quality, safety, and agentic performance
- Use **built-in Foundry evaluators**:
  - 📊 AI Quality (relevance, coherence, groundedness)
  - 🛡️ Safety (harmful content, protected material)
  - 🤖 Agentic (tool selection accuracy, task completion)

> Evaluations turn subjective "does it feel right?" into measurable metrics.

<!--
SPEAKER NOTES:
This is where you go from qualitative gut feeling to quantitative measurement. Evaluators score each response on multiple dimensions. You can run them in batch over test datasets.
Duration: ~2 min
-->

---

# Lab 06: Red Teaming

**`lab-06-redteam.ipynb`**

- Run cloud-based **adversarial red-team scans**
- Test against targeted risk categories:
  - Jailbreaks and prompt injection
  - Harmful content generation
  - Information disclosure
- Assess attack strategies and defense effectiveness

> Find vulnerabilities **before** production deployment, not after.

<!--
SPEAKER NOTES:
Red teaming is automated adversarial testing. The AI Red Teaming agent tries various attack strategies against your agent and reports what worked. This is your security safety net.
Duration: ~2 min
-->

---

<!-- _class: section-title -->

# Closing
### Wrapping Up & Next Steps

⏱️ ~5 minutes

<!--
SPEAKER NOTES:
Let's bring it all together with key takeaways and next steps.
-->

---

# The Foundry Control Plane

The Microsoft Foundry Control Plane provides tools for **security, compliance, fleet management, and observability** — accessed through the "Operate" tab.

![w:800](../../assets/foundry-control-plane.png)

> Today we focused on **Observability** — but the platform covers the full lifecycle.

<!--
SPEAKER NOTES:
The control plane is the enterprise management layer. Observability is one piece of a larger story that includes security, compliance, and fleet management.
Duration: ~1 min
-->

---

# Key Takeaway

The Microsoft Foundry Observability platform works with **any agent** — regardless of programming language or framework — provided it supports:

1. ✅ **OpenTelemetry-compliant traces** — standard observability protocol
2. ✅ **Responses API-compliant endpoints** — standard agent interface

### The Developer Loop

```
Build → Trace → Evaluate → Diagnose → Optimize → Repeat
```

> This is not a one-time setup. It's an **ongoing practice** that keeps your agents reliable as models, prompts, and usage patterns evolve.

<!--
SPEAKER NOTES:
This is the most important slide. OTel + Responses API means you're not locked in. And observability is a continuous practice, not a one-time setup.
Duration: ~2 min
-->

---

# Related Resources

| Resource | Link |
|:---|:---|
| Foundry Control Plane | [learn.microsoft.com/.../control-plane/overview](https://learn.microsoft.com/en-us/azure/foundry/control-plane/overview?view=foundry) |
| Observability | [learn.microsoft.com/.../observability](https://learn.microsoft.com/en-us/azure/foundry/concepts/observability?view=foundry) |
| Agent Tracing | [learn.microsoft.com/.../trace-agent-concept](https://learn.microsoft.com/en-us/azure/foundry/observability/concepts/trace-agent-concept?view=foundry) |
| Evaluations | [learn.microsoft.com/.../built-in-evaluators](https://learn.microsoft.com/en-us/azure/foundry/concepts/built-in-evaluators?view=foundry) |
| Red Teaming | [learn.microsoft.com/.../ai-red-teaming-agent](https://learn.microsoft.com/en-us/azure/foundry/concepts/ai-red-teaming-agent?view=foundry) |

<!--
SPEAKER NOTES:
Share these links with attendees. Each resource goes deeper into the concepts we covered today.
Duration: ~1 min
-->

---

<!-- _class: title -->

# Thank You!

### Next Steps
- 🔀 **Try the other path** (A or B) if time permits
- 📌 **Fork & watch** the repo for v2 updates (May/June 2026)
- 🆕 **v2 preview:** Hosted agents with custom code + containerized runtimes
- 💬 **Share feedback** — your input shapes the next iteration

**Workshop Repository:**
[github.com/Azure-Samples/microsoft-foundry-e2e-agent-observability-workshop](https://github.com/Azure-Samples/microsoft-foundry-e2e-agent-observability-workshop)

<!--
SPEAKER NOTES:
Thank everyone for attending. Encourage them to try the other path, fork the repo, and share feedback. V2 will expand to hosted agents with containerized environments.
Duration: ~1 min
-->
