# Building Contoso Travel (Prompt Agent) Using Foundry SDK

By now you should have completed the _infastructure setup_ and _dev environment_ setup steps and have a running GitHub Codespaces that is connected to an existing Foundry project in your Azure subscription.

In this path, you'll execute notebooks in order - walking you through the journey of building a Contoso Travel agent, grounding it in custom data and tools, then evaluating and tracing it - and running an AI Red Teaming scan to assess vulnerability to attack.

### 2.1 How To: Run a Notebook

The GitHub Codespaces environment has pre-instealled extensions and tools to support Jupyter notebooks. Just take these actions to "Run" any notebook:

1. Open the notebook (`.ipynb` file) in Visual Studio Code
1. Click **Select Kernel**, and pick the **Python 3.12** option. 
1. Clear all outputs first, then **run each cell one at a time** (rather than "Run All") 
1. Observe the results and understand each step before moving on. 

**IMPORTANT**: Do NOT run the final cell of the notebook until you are done with the lab and have understood the code. Running the final cell will clear out not just the outputs in the notebook but any related assets (e.g., agents) created in Foundry. 

<br/>

### 2.2 Lab Notebooks

| Notebook | Description |
|---|---|
| [lab-01-setup.ipynb](lab-01-setup.ipynb) | Validate your environment, authenticate to Microsoft Foundry, and confirm your model deployment is ready. |
| [lab-02-agent.ipynb](lab-02-agent.ipynb) | Create a basic Contoso Travel concierge agent with system instructions and test it with travel queries. |
| [lab-03a-tools.ipynb](lab-03a-tools.ipynb) | Give the agent tools (functions) to look up flights, hotels, and car rentals from CSV data. |
| [lab-03b-workflow.ipynb](lab-03b-workflow.ipynb) | Orchestrate multiple specialized agents into a multi-agent workflow that collaborates on trip planning. |
| [lab-04-tracing.ipynb](lab-04-tracing.ipynb) | Instrument the agent with OpenTelemetry tracing and export telemetry to Application Insights. |
| [lab-05-evaluation.ipynb](lab-05-evaluation.ipynb) | Evaluate agent quality, safety, and agentic performance using built-in Foundry evaluators. |
| [lab-06-redteam.ipynb](lab-06-redteam.ipynb) | Run cloud-based adversarial red-team scans to find vulnerabilities before production deployment. |
| |

**Note**:
_The AI Red Teaming agent is currently undergoing being updated. You _may_ encounter issues running the notebook or viewing scans in the portal in some contexts in that case. Just pause the notebook for now and keep an eye on this repo for updates on when you can retry that lab_.
