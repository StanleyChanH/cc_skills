# Crewai - Tools

**Pages:** 73

---

## Initialize from LlamaHub Tools

**URL:** llms-txt#initialize-from-llamahub-tools

**Contents:**
  - LlamaIndex 쿼리 엔진에서

wolfram_spec = WolframAlphaToolSpec(app_id="your_app_id")
wolfram_tools = wolfram_spec.to_tool_list()
tools = [LlamaIndexTool.from_tool(t) for t in wolfram_tools]
python Code theme={null}
from crewai_tools import LlamaIndexTool
from llama_index.core import VectorStoreIndex
from llama_index.core.readers import SimpleDirectoryReader

**Examples:**

Example 1 (unknown):
```unknown
### LlamaIndex 쿼리 엔진에서
```

---

## Full service with all tools

**URL:** llms-txt#full-service-with-all-tools

"crewai-amp:financial-data"

---

## Create an agent with SharePoint capabilities

**URL:** llms-txt#create-an-agent-with-sharepoint-capabilities

sharepoint_agent = Agent(
    role="SharePoint Manager",
    goal="Manage SharePoint sites, lists, and documents efficiently",
    backstory="An AI assistant specialized in SharePoint content management and collaboration.",
    apps=['microsoft_sharepoint']  # All SharePoint actions will be available
)

---

## Agent will use tools from working servers and log warnings for failing ones

**URL:** llms-txt#agent-will-use-tools-from-working-servers-and-log-warnings-for-failing-ones

**Contents:**
- Advanced: MCPServerAdapter
- Connection Configuration

**Examples:**

Example 1 (unknown):
```unknown
## Advanced: MCPServerAdapter

For complex scenarios requiring manual connection management, use the `MCPServerAdapter` class from `crewai-tools`. Using a Python context manager (`with` statement) is the recommended approach as it automatically handles starting and stopping the connection to the MCP server.

## Connection Configuration

The `MCPServerAdapter` supports several configuration options to customize the connection behavior:

* **`connect_timeout`** (optional): Maximum time in seconds to wait for establishing a connection to the MCP server. Defaults to 30 seconds if not specified. This is particularly useful for remote servers that may have variable response times.
```

---

## Create an agent with Microsoft Outlook capabilities

**URL:** llms-txt#create-an-agent-with-microsoft-outlook-capabilities

outlook_agent = Agent(
    role="Email Assistant",
    goal="Manage emails, calendar events, and contacts efficiently",
    backstory="An AI assistant specialized in Microsoft Outlook operations and communication management.",
    apps=['microsoft_outlook']  # All Outlook actions will be available
)

---

## Create an agent with Slack capabilities

**URL:** llms-txt#create-an-agent-with-slack-capabilities

slack_agent = Agent(
    role="Team Communication Manager",
    goal="Facilitate team communication and coordinate collaboration efficiently",
    backstory="An AI assistant specialized in team communication and workspace coordination.",
    apps=['slack']
)

---

## Create database tools

**URL:** llms-txt#create-database-tools

mysql_db = MySQLTool()
vector_search = QdrantVectorSearchTool()
nl_to_sql = NL2SQLTool()

---

## MCP tools are now automatically available to your agent!

**URL:** llms-txt#mcp-tools-are-now-automatically-available-to-your-agent!

**Contents:**
  - 🔧 **Advanced: MCPServerAdapter** (For Complex Scenarios)
- Video Tutorial
- Installation

**Examples:**

Example 1 (unknown):
```unknown
### 🔧 **Advanced: MCPServerAdapter** (For Complex Scenarios)

For advanced use cases requiring manual connection management, the `crewai-tools` library provides the `MCPServerAdapter` class.

We currently support the following transport mechanisms:

* **Stdio**: for local servers (communication via standard input/output between processes on the same machine)
* **Server-Sent Events (SSE)**: for remote servers (unidirectional, real-time data streaming from server to client over HTTP)
* **Streamable HTTPS**: for remote servers (flexible, potentially bi-directional communication over HTTPS, often utilizing SSE for server-to-client streams)

## Video Tutorial

Watch this video tutorial for a comprehensive guide on MCP integration with CrewAI:

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/TpQ45lAZh48" title="CrewAI MCP Integration Guide" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

## Installation

CrewAI MCP integration requires the `mcp` library:
```

---

## Good - only get the tools you need

**URL:** llms-txt#good---only-get-the-tools-you-need

mcps=["https://weather.api.com/mcp#get_forecast"]

---

## Create an agent with Gmail capabilities

**URL:** llms-txt#create-an-agent-with-gmail-capabilities

gmail_agent = Agent(
    role="Email Manager",
    goal="Manage email communications and contacts efficiently",
    backstory="An AI assistant specialized in email management and communication.",
    apps=['gmail']
)

---

## `ComposioToolSet`

**URL:** llms-txt#`composiotoolset`

**Contents:**
- Descrição
- Instalação
- Exemplo

Composio é uma plataforma de integração que permite conectar seus agentes de IA a mais de 250 ferramentas. Os principais recursos incluem:

* **Autenticação de Nível Empresarial**: Suporte integrado para OAuth, Chaves de API, JWT com atualização automática de token
* **Observabilidade Completa**: Logs detalhados de uso das ferramentas, registros de execução, e muito mais

Para incorporar as ferramentas Composio em seu projeto, siga as instruções abaixo:

Após a conclusão da instalação, execute `composio login` ou exporte sua chave de API do composio como `COMPOSIO_API_KEY`. Obtenha sua chave de API Composio [aqui](https://app.composio.dev)

O exemplo a seguir demonstra como inicializar a ferramenta e executar uma ação do github:

1. Inicialize o conjunto de ferramentas Composio

2. Conecte sua conta do GitHub

3. Obtenha ferramentas

* Recuperando todas as ferramentas de um app (não recomendado em produção):

* Filtrando ferramentas com base em tags:

* Filtrando ferramentas com base no caso de uso:

<Tip>Defina `advanced` como True para obter ações para casos de uso complexos</Tip>

* Usando ferramentas específicas:

Neste exemplo, usaremos a ação `GITHUB_STAR_A_REPOSITORY_FOR_THE_AUTHENTICATED_USER` do app GitHub.

Saiba mais sobre como filtrar ações [aqui](https://docs.composio.dev/patterns/tools/use-tools/use-specific-actions)

* Uma lista mais detalhada de ferramentas pode ser encontrada [aqui](https://app.composio.dev)

**Examples:**

Example 1 (unknown):
```unknown
Após a conclusão da instalação, execute `composio login` ou exporte sua chave de API do composio como `COMPOSIO_API_KEY`. Obtenha sua chave de API Composio [aqui](https://app.composio.dev)

## Exemplo

O exemplo a seguir demonstra como inicializar a ferramenta e executar uma ação do github:

1. Inicialize o conjunto de ferramentas Composio
```

Example 2 (unknown):
```unknown
2. Conecte sua conta do GitHub

<CodeGroup>
```

Example 3 (unknown):
```unknown

```

Example 4 (unknown):
```unknown
</CodeGroup>

3. Obtenha ferramentas

* Recuperando todas as ferramentas de um app (não recomendado em produção):
```

---

## Create an agent with GitHub capabilities

**URL:** llms-txt#create-an-agent-with-github-capabilities

github_agent = Agent(
    role="Repository Manager",
    goal="Manage GitHub repositories, issues, and releases efficiently",
    backstory="An AI assistant specialized in repository management and issue tracking.",
    apps=['github']
)

---

## Create an agent with Google Slides capabilities

**URL:** llms-txt#create-an-agent-with-google-slides-capabilities

slides_agent = Agent(
    role="Presentation Manager",
    goal="Create and manage presentations efficiently",
    backstory="An AI assistant specialized in presentation creation and content management.",
    apps=['google_slides']  # All Google Slides actions will be available
)

---

## Create scraping tools

**URL:** llms-txt#create-scraping-tools

simple_scraper = ScrapeWebsiteTool()
advanced_scraper = FirecrawlScrapeWebsiteTool()
browser_automation = SeleniumScrapingTool()

---

## Add tools to your agent

**URL:** llms-txt#add-tools-to-your-agent

agent = Agent(
    role="Research Analyst",
    tools=[FileReadTool(), SerperDevTool()],
    # ... other configuration
)
```

탐험을 시작할 준비가 되셨나요? 위에서 카테고리를 선택하여 사용 사례에 맞는 도구를 찾아보세요!

---

## Outlook Trigger

**URL:** llms-txt#outlook-trigger

**Contents:**
- Overview
- Enabling the Outlook Trigger
- Example: Summarize a new email
- Testando Localmente

Source: https://docs.crewai.com/pt-BR/enterprise/guides/outlook-trigger

Launch automations from Outlook emails and calendar updates

Automate responses when Outlook delivers a new message or when an event is removed from the calendar. Teams commonly route escalations, file tickets, or alert attendees of cancellations.

<Tip>
  Connect Outlook in **Tools & Integrations** and ensure the trigger is enabled for your deployment.
</Tip>

## Enabling the Outlook Trigger

1. Open your deployment in CrewAI AMP
2. Go to the **Triggers** tab
3. Locate **Outlook** and switch the toggle to enable

<Frame caption="Microsoft Outlook trigger connection">
  <img src="https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=f8a739ad0963ccddafeed60f21366628" alt="Enable or disable triggers with toggle" data-og-width="2186" width="2186" data-og-height="508" height="508" data-path="images/enterprise/outlook-trigger.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=280&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=03b5121587c619936c87f05e15992f08 280w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=560&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=651d2efd933f7109b216d343e6d6a6ce 560w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=840&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=a7a27424bf507c739280376fd57ea80d 840w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=1100&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=481164952ea35f62566b09d392a0910b 1100w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=1650&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=f4d3db361e699578e9ce44bde1e683fd 1650w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/outlook-trigger.png?w=2500&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=aaabf7a26259291cf3b8545a4c3a996d 2500w" />
</Frame>

## Example: Summarize a new email

The crew extracts sender details, subject, body preview, and attachments before generating a structured response.

## Testando Localmente

Teste sua integração de trigger do Outlook localmente usando a CLI da CrewAI:

```bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
The crew extracts sender details, subject, body preview, and attachments before generating a structured response.

## Testando Localmente

Teste sua integração de trigger do Outlook localmente usando a CLI da CrewAI:
```

---

## Original MCP server has tools: "search", "analyze"

**URL:** llms-txt#original-mcp-server-has-tools:-"search",-"analyze"

---

## Create agent with Gmail search and analysis capabilities

**URL:** llms-txt#create-agent-with-gmail-search-and-analysis-capabilities

email_analyst = Agent(
    role="Email Analyst",
    goal="Analyze email patterns and provide insights",
    backstory="An AI assistant that analyzes email data to provide actionable insights.",
    apps=['gmail/fetch_emails', 'gmail/get_message']  # Specific actions for email analysis
)

---

## Create agent with MCP tools

**URL:** llms-txt#create-agent-with-mcp-tools

research_agent = Agent(
    role="Research Analyst",
    goal="Find and analyze information using advanced search tools",
    backstory="Expert researcher with access to multiple data sources",
    mcps=[
        "https://mcp.exa.ai/mcp?api_key=your_key&profile=your_profile",
        "crewai-amp:weather-service#current_conditions"
    ]
)

---

## Create an agent with Notion capabilities

**URL:** llms-txt#create-an-agent-with-notion-capabilities

notion_agent = Agent(
    role="Documentation Manager",
    goal="Manage documentation and knowledge base in Notion efficiently",
    backstory="An AI assistant specialized in content management and documentation.",
    apps=['notion']
)

---

## Loading Tools

**URL:** llms-txt#loading-tools

search_tool = SerperDevTool()

---

## Create an agent with Box capabilities

**URL:** llms-txt#create-an-agent-with-box-capabilities

box_agent = Agent(
    role="Document Manager",
    goal="Manage files and folders in Box efficiently",
    backstory="An AI assistant specialized in document management and file organization.",
    apps=['box']
)

---

## Create an agent with HubSpot capabilities

**URL:** llms-txt#create-an-agent-with-hubspot-capabilities

hubspot_agent = Agent(
    role="CRM Manager",
    goal="Manage company and contact records in HubSpot",
    backstory="An AI assistant specialized in CRM management.",
    apps=['hubspot']
)

---

## Create an agent with Microsoft Teams capabilities

**URL:** llms-txt#create-an-agent-with-microsoft-teams-capabilities

teams_agent = Agent(
    role="Teams Coordinator",
    goal="Manage Teams communication and meetings efficiently",
    backstory="An AI assistant specialized in Microsoft Teams operations and team collaboration.",
    apps=['microsoft_teams']  # All Teams actions will be available
)

---

## Create research tools

**URL:** llms-txt#create-research-tools

web_search = SerperDevTool()
code_search = GitHubSearchTool()
video_research = YoutubeVideoSearchTool()

---

## OneDrive Trigger

**URL:** llms-txt#onedrive-trigger

**Contents:**
- Overview
- Enabling the OneDrive Trigger
- Example: Audit file permissions
- Testando Localmente

Source: https://docs.crewai.com/pt-BR/enterprise/guides/onedrive-trigger

Automate responses to OneDrive file activity

Start automations when files change inside OneDrive. You can generate audit summaries, notify security teams about external sharing, or update downstream line-of-business systems with new document metadata.

<Tip>
  Connect OneDrive in **Tools & Integrations** and toggle the trigger on for your deployment.
</Tip>

## Enabling the OneDrive Trigger

1. Open your deployment in CrewAI AMP
2. Go to the **Triggers** tab
3. Locate **OneDrive** and switch the toggle to enable

<Frame caption="Microsoft OneDrive trigger connection">
  <img src="https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=55774f3aee2c024ee81e8d543d9391be" alt="Enable or disable triggers with toggle" data-og-width="2166" width="2166" data-og-height="478" height="478" data-path="images/enterprise/onedrive-trigger.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=280&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=82cf038f92dfd9771c87ff44d364c42b 280w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=560&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=d79a78258619bcc517c9bcbf0e1b42f4 560w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=840&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=6e5fc33aaebcffe573195b7b7a85986e 840w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=1100&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=bbd2f96f33f12988c8c52f36e178e553 1100w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=1650&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=ef16d274ea3fe359655c8ac163b3c97a 1650w, https://mintcdn.com/crewai/oMMe1eXJrzmWf3MN/images/enterprise/onedrive-trigger.png?w=2500&fit=max&auto=format&n=oMMe1eXJrzmWf3MN&q=85&s=0efecea63f338e2cdf7372a627993bac 2500w" />
</Frame>

## Example: Audit file permissions

The crew inspects file metadata, user activity, and permission changes to produce a compliance-friendly summary.

## Testando Localmente

Teste sua integração de trigger do OneDrive localmente usando a CLI da CrewAI:

```bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
The crew inspects file metadata, user activity, and permission changes to produce a compliance-friendly summary.

## Testando Localmente

Teste sua integração de trigger do OneDrive localmente usando a CLI da CrewAI:
```

---

## Ferramenta LangChain

**URL:** llms-txt#ferramenta-langchain

**Contents:**
- `LangChainTool`

Source: https://docs.crewai.com/pt-BR/tools/ai-ml/langchaintool

O `LangChainTool` é um wrapper para ferramentas LangChain e mecanismos de consulta.

<Info>
  CrewAI integra-se perfeitamente com a abrangente [lista de ferramentas](https://python.langchain.com/docs/integrations/tools/) do LangChain, todas as quais podem ser usadas com CrewAI.
</Info>

```python Code theme={null}
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew
from crewai.tools import BaseTool
from pydantic import Field
from langchain_community.utilities import GoogleSerperAPIWrapper

---

## Create agent with HubSpot contact management capabilities

**URL:** llms-txt#create-agent-with-hubspot-contact-management-capabilities

crm_manager = Agent(
    role="CRM Manager",
    goal="Manage and organize HubSpot contacts efficiently.",
    backstory="An experienced CRM manager who maintains an organized contact database.",
    apps=['hubspot']  # All HubSpot actions including contact management
)

---

## Create automation tools

**URL:** llms-txt#create-automation-tools

apify_automation = ApifyActorTool()
platform_integration = ComposioTool()
browser_automation = MultiOnTool()

---

## Create Custom Tools

**URL:** llms-txt#create-custom-tools

**Contents:**
- Creating and Utilizing Tools in CrewAI
  - Subclassing `BaseTool`
  - Using the `tool` Decorator
  - Defining a Cache Function for the Tool

Source: https://docs.crewai.com/en/learn/create-custom-tools

Comprehensive guide on crafting, using, and managing custom tools within the CrewAI framework, including new functionalities and error handling.

## Creating and Utilizing Tools in CrewAI

This guide provides detailed instructions on creating custom tools for the CrewAI framework and how to efficiently manage and utilize these tools,
incorporating the latest functionalities such as tool delegation, error handling, and dynamic tool calling. It also highlights the importance of collaboration tools,
enabling agents to perform a wide range of actions.

### Subclassing `BaseTool`

To create a personalized tool, inherit from `BaseTool` and define the necessary attributes, including the `args_schema` for input validation, and the `_run` method.

### Using the `tool` Decorator

Alternatively, you can use the tool decorator `@tool`. This approach allows you to define the tool's attributes and functionality directly within a function,
offering a concise and efficient way to create specialized tools tailored to your needs.

### Defining a Cache Function for the Tool

To optimize tool performance with caching, define custom caching strategies using the `cache_function` attribute.

By adhering to these guidelines and incorporating new functionalities and collaboration tools into your tool creation and management processes,
you can leverage the full capabilities of the CrewAI framework, enhancing both the development experience and the efficiency of your AI agents.

**Examples:**

Example 1 (unknown):
```unknown
### Using the `tool` Decorator

Alternatively, you can use the tool decorator `@tool`. This approach allows you to define the tool's attributes and functionality directly within a function,
offering a concise and efficient way to create specialized tools tailored to your needs.
```

Example 2 (unknown):
```unknown
### Defining a Cache Function for the Tool

To optimize tool performance with caching, define custom caching strategies using the `cache_function` attribute.
```

---

## Instantiate tools

**URL:** llms-txt#instantiate-tools

docs_tool = DirectoryReadTool(directory='./blog-posts')
file_tool = FileReadTool()
search_tool = SerperDevTool()
web_rag_tool = WebsiteSearchTool()

---

## Create tools

**URL:** llms-txt#create-tools

file_reader = FileReadTool()
pdf_searcher = PDFSearchTool()
json_processor = JSONSearchTool()

---

## Create cloud tools

**URL:** llms-txt#create-cloud-tools

s3_reader = S3ReaderTool()
s3_writer = S3WriterTool()
bedrock_agent = BedrockInvokeAgentTool()

---

## Create an agent with ClickUp capabilities

**URL:** llms-txt#create-an-agent-with-clickup-capabilities

clickup_agent = Agent(
    role="Task Manager",
    goal="Manage tasks and projects in ClickUp efficiently",
    backstory="An AI assistant specialized in task management and productivity coordination.",
    apps=['clickup']
)

---

## Create an agent with Linear capabilities

**URL:** llms-txt#create-an-agent-with-linear-capabilities

linear_agent = Agent(
    role="Development Manager",
    goal="Manage Linear issues and track development progress efficiently",
    backstory="An AI assistant specialized in software development project management.",
    apps=['linear']
)

---

## Create an agent with Github capabilities

**URL:** llms-txt#create-an-agent-with-github-capabilities

github_agent = Agent(
    role="Repository Manager",
    goal="Manage GitHub repositories, issues, and releases efficiently",
    backstory="An AI assistant specialized in repository management and issue tracking.",
    apps=['github']  # All Github actions will be available
)

---

## Create agent with Slack search and user management capabilities

**URL:** llms-txt#create-agent-with-slack-search-and-user-management-capabilities

analytics_agent = Agent(
    role="Communication Analyst",
    goal="Analyze team communication patterns and extract insights from conversations",
    backstory="An analytical AI that excels at understanding team dynamics through communication data.",
    apps=[
        'slack/search_messages',
        'slack/get_user_by_email',
        'slack/list_members'
    ]  # Using canonical action names from canonical_integrations.yml
)

---

## Create an agent with Google Calendar capabilities

**URL:** llms-txt#create-an-agent-with-google-calendar-capabilities

calendar_agent = Agent(
    role="Schedule Manager",
    goal="Manage calendar events and scheduling efficiently",
    backstory="An AI assistant specialized in calendar management and scheduling coordination.",
    apps=['google_calendar']
)

---

## Add tools to agent

**URL:** llms-txt#add-tools-to-agent

**Contents:**
- Agent Memory and Context
- Context Window Management
  - How Context Window Management Works
  - Automatic Context Handling (`respect_context_window=True`)

researcher = Agent(
    role="AI Technology Researcher",
    goal="Research the latest AI developments",
    tools=[search_tool, wiki_tool],
    verbose=True
)
python Code theme={null}
from crewai import Agent

analyst = Agent(
    role="Data Analyst",
    goal="Analyze and remember complex data patterns",
    memory=True,  # Enable memory
    verbose=True
)
python Code theme={null}

**Examples:**

Example 1 (unknown):
```unknown
## Agent Memory and Context

Agents can maintain memory of their interactions and use context from previous tasks. This is particularly useful for complex workflows where information needs to be retained across multiple tasks.
```

Example 2 (unknown):
```unknown
<Note>
  When `memory` is enabled, the agent will maintain context across multiple interactions, improving its ability to handle complex, multi-step tasks.
</Note>

## Context Window Management

CrewAI includes sophisticated automatic context window management to handle situations where conversations exceed the language model's token limits. This powerful feature is controlled by the `respect_context_window` parameter.

### How Context Window Management Works

When an agent's conversation history grows too large for the LLM's context window, CrewAI automatically detects this situation and can either:

1. **Automatically summarize content** (when `respect_context_window=True`)
2. **Stop execution with an error** (when `respect_context_window=False`)

### Automatic Context Handling (`respect_context_window=True`)

This is the **default and recommended setting** for most use cases. When enabled, CrewAI will:
```

---

## Initialize tools with session management

**URL:** llms-txt#initialize-tools-with-session-management

initial_tool = BedrockInvokeAgentTool(
    agent_id="your-agent-id",
    agent_alias_id="your-agent-alias-id",
    session_id="custom-session-id"
)

followup_tool = BedrockInvokeAgentTool(
    agent_id="your-agent-id",
    agent_alias_id="your-agent-alias-id",
    session_id="custom-session-id"
)

final_tool = BedrockInvokeAgentTool(
    agent_id="your-agent-id",
    agent_alias_id="your-agent-alias-id",
    session_id="custom-session-id",
    end_session=True
)

---

## Create an agent with Google Docs capabilities

**URL:** llms-txt#create-an-agent-with-google-docs-capabilities

docs_agent = Agent(
    role="Document Creator",
    goal="Create and manage Google Docs documents efficiently",
    backstory="An AI assistant specialized in Google Docs document creation and editing.",
    apps=['google_docs']  # All Google Docs actions will be available
)

---

## Create an agent with Microsoft Word capabilities

**URL:** llms-txt#create-an-agent-with-microsoft-word-capabilities

word_agent = Agent(
    role="Document Manager",
    goal="Manage Word documents and text files efficiently",
    backstory="An AI assistant specialized in Microsoft Word document operations and content management.",
    apps=['microsoft_word']  # All Word actions will be available
)

---

## Create an agent with Stripe capabilities

**URL:** llms-txt#create-an-agent-with-stripe-capabilities

stripe_agent = Agent(
    role="Payment Manager",
    goal="Manage customer payments, subscriptions, and billing operations efficiently",
    backstory="An AI assistant specialized in payment processing and subscription management.",
    apps=['stripe']
)

---

## Ferramentas & Integrações

**URL:** llms-txt#ferramentas-&-integrações

**Contents:**
- Visão geral
- Explorar
- Relacionados

Source: https://docs.crewai.com/pt-BR/enterprise/features/tools-and-integrations

Conecte apps externos e gerencie ferramentas internas que seus agentes podem usar.

Ferramentas & Integrações é o hub central para conectar aplicações de terceiros e gerenciar ferramentas internas que seus agentes podem usar em tempo de execução.

<Frame>
    <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=c31a4b9031f0f517fdce3baa48471f58" alt="Ferramentas & Integrações" data-og-width="1024" width="1024" data-og-height="1024" height="1024" data-path="images/enterprise/crew_connectors.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=9e592d155e388bb67d003b26884dc081 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=0c8aa20b2dc82de9ea3d2da6920e4195 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=782fe13ea53120f6d2f8e643a7a7b838 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=780cd735280c569e6e93caa8262b12d1 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=08bfe86a58ca08ec36ae67dca4aa5cf9 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=e2bbe3b0fe0234001e030b501fa4d76c 2500w" />
</Frame>

<Tabs>
  <Tab title="Integrações" icon="plug">
    ## Aplicativos para Agentes (Integrações)

Conecte aplicações empresariais (por exemplo, Gmail, Google Drive, HubSpot, Slack) via OAuth para habilitar ações de agentes.

<Steps>
      <Step title="Conectar">
        Clique em <b>Conectar</b> no app desejado e conclua o OAuth.
      </Step>

<Step title="Configurar">
        Ajuste escopos, gatilhos e ações disponíveis conforme necessário.
      </Step>

<Step title="Usar em Agentes">
        Os serviços conectados ficam disponíveis como ferramentas para seus agentes.
      </Step>
    </Steps>

<Frame>
            <img src="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=43abfc4eae390e308bed0b8e15238a54" alt="Aplicativos" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/agent-apps.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=280&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=e5e30bd3d904891d5c2c4d9d6182002a 280w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=560&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=a146a0d69ff2309e7eac8d2f07da1cba 560w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=840&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=c85a4a7ebe043fc6819957ff51f3ef0d 840w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=1100&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=4ea77f15a4fe2671267f7e3668615970 1100w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=1650&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=7835e5d197251834d83a6dd7c7813d0a 1650w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=2500&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=06cea3ae58b49b925566a7962585b148 2500w" />
    </Frame>

### Conectar sua conta

1. Acesse <Link href="https://app.crewai.com/crewai_plus/connectors">Integrações</Link>
    2. Clique em <b>Conectar</b> no serviço desejado
    3. Conclua o fluxo OAuth e conceda os escopos
    4. Copie seu Token Enterprise em <Link href="https://app.crewai.com/crewai_plus/settings/integrations">Configurações de Integração</Link>

<Frame>
            <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=4e7388bcb76f3f8aa6c6802dd0a98956" alt="Token Enterprise" data-og-width="2264" width="2264" data-og-height="540" height="540" data-path="images/enterprise/enterprise_action_auth_token.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=f3d1bd9cd9783d3e83f42ab6ee42d26c 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=df1514f746270a9ae5fc252c07806761 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=a16c5c7986003435afad4106ccbaa7c5 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=81dabefb14a7f604a68c74eff26dff90 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=2833c9f202a291f2cf022026db261793 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=eeece6b187aebd0ec9e8af29d8bfc889 2500w" />
    </Frame>

### Instalar ferramentas de integração

Para usar as integrações localmente, instale a versão mais recente do pacote `crewai-tools`.

### Configuração de variável de ambiente

<Note>
      Para usar integrações com `Agent(apps=[])`, você deve definir a variável de ambiente `CREWAI_PLATFORM_INTEGRATION_TOKEN` com seu Enterprise Token.
    </Note>

Ou adicione ao seu arquivo `.env`:

<Tip>
      Use a nova abordagem simplificada para integrar aplicativos empresariais. Simplesmente especifique o aplicativo e suas ações diretamente na configuração do Agent.
    </Tip>

### Filtrando ferramentas

Em um crew implantado, você pode especificar quais ações ficam disponíveis em cada integração na página de configurações do serviço.

<Frame>
            <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=2e689397eabeacd23d0c226ff40566fd" alt="Filtrar Ações" data-og-width="3680" width="3680" data-og-height="2382" height="2382" data-path="images/enterprise/filtering_enterprise_action_tools.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=a6045a09da61d593e04098a4627777c9 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=257b1eea0bca2def5d43df960a4171ef 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6b9b8686a4fec0c0cdd8c7aa9acd4695 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e16c10384300b96d4962e2847f6633bf 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6de59b5409513b100c5cd36a69701e5f 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=32ed2ecc611c989e0fe9d8cb351740fa 2500w" />
    </Frame>

### Implantações com escopo (organizações multiusuário)

Você pode escopar cada integração para um usuário específico (por exemplo, usar a conta Gmail de um usuário).

<Tip>
      Útil quando diferentes equipes/usuários precisam manter o acesso a dados isolado.
    </Tip>

Use `user_bearer_token` para escopar a autenticação ao usuário solicitante. Se o usuário não estiver logado, o crew não usará integrações conectadas; caso contrário, usa o token padrão configurado na implantação.

<Frame>
            <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d62aed15392f304cfc16bfa38ab91a54" alt="Token de Usuário" data-og-width="532" width="532" data-og-height="732" height="732" data-path="images/enterprise/user_bearer_token.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=efe731a753ab7efb10a65f648fba75a7 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=232d8d25cd253f071856f53425cc40c2 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=df7b4956ab7668c23380394d8ce0f6c1 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=523850a6b69b5dd47ceaca3681f0ac35 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=561dcfa07461ecc8c39cd80865802d5e 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=06fbc44278b7d23fd2befd6b745622e7 2500w" />
    </Frame>

#### Comunicação & Colaboração

* Gmail — Gerenciamento de emails e rascunhos
    * Slack — Notificações e alertas do workspace
    * Microsoft — Integração com Office 365 e Teams

#### Gestão de Projetos

* Jira — Rastreamento de issues e projetos
    * ClickUp — Gestão de tarefas e produtividade
    * Asana — Coordenação de tarefas de equipe
    * Notion — Páginas e bancos de dados
    * Linear — Gestão de bugs e projetos de software
    * GitHub — Repositórios e issues

* Salesforce — Contas e oportunidades
    * HubSpot — Pipeline de vendas e contatos
    * Zendesk — Tickets de suporte

#### Negócios & Finanças

* Stripe — Pagamentos e clientes
    * Shopify — E‑commerce e produtos

#### Produtividade & Armazenamento

* Google Sheets — Sincronização de planilhas
    * Google Calendar — Eventos e agenda
    * Box — Armazenamento de arquivos

…e mais por vir!
  </Tab>

<Tab title="Ferramentas Internas" icon="toolbox">
    ## Ferramentas Internas

Crie ferramentas localmente, publique no Repositório de Ferramentas da CrewAI AMP e use nos seus agentes.

<Tip>
      Antes de executar os comandos abaixo, faça login na sua conta CrewAI AMP:

<Frame>
            <img src="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=b31a82341fb4dcd784c2ecfc1c3d576c" alt="Ferramenta Interna" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/tools-integrations-internal.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=280&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=4b7ea6075327365b2486b405db715126 280w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=560&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=857f73fdff530aa6c7d801267e3cbc8a 560w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=840&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=2e844aa05d5c5367f9f8c14deeb78ad7 840w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=1100&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=fd26df60df1b528fc1644e08289738da 1100w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=1650&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=11d2cd7d7e38cb9cfeed2e23c4e3fe87 1650w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=2500&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=cba0837b7f2039f9c59cdafb81cc53b9 2500w" />
    </Frame>

<Steps>
      <Step title="Criar">
        Criar uma nova ferramenta localmente.

<Step title="Publicar">
        Publicar a ferramenta no Repositório de Ferramentas.

<Step title="Instalar">
        Instalar a ferramenta do Repositório de Ferramentas.

* Nome e descrição
    * Visibilidade (Privado / Público)
    * Variáveis de ambiente necessárias
    * Histórico de versões e downloads
    * Acesso por equipe e função

<Frame>
            <img src="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=1896ebecec784bc15411a0309a0cf973" alt="Configurações de Ferramenta" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/tool-configs.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=280&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=fa0c14f9439ebad25474aa422f8b1bd7 280w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=560&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=d135d69d85a0ccb8d99403def21c8529 560w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=840&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=f65ac1de79956f4178a610be29c6e212 840w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=1100&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=3b13a8181819dbf6b07ed52f239f588a 1100w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=1650&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=0dc0e377941d126e06fa76cb176b70e2 1650w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=2500&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=53bf0fa4215eb47d5959d1c46a232db1 2500w" />
    </Frame>
  </Tab>
</Tabs>

<CardGroup cols={2}>
  <Card title="Repositório de Ferramentas" href="/pt-BR/enterprise/features/tool-repository" icon="toolbox">
    Publique e instale ferramentas para ampliar as capacidades dos seus crews.
  </Card>

<Card title="Automação com Webhook" href="/pt-BR/enterprise/guides/webhook-automation" icon="bolt">
    Automatize fluxos e integre com plataformas e serviços externos.
  </Card>
</CardGroup>

**Examples:**

Example 1 (unknown):
```unknown
### Configuração de variável de ambiente

    <Note>
      Para usar integrações com `Agent(apps=[])`, você deve definir a variável de ambiente `CREWAI_PLATFORM_INTEGRATION_TOKEN` com seu Enterprise Token.
    </Note>
```

Example 2 (unknown):
```unknown
Ou adicione ao seu arquivo `.env`:
```

Example 3 (unknown):
```unknown
### Exemplo de uso

    <Tip>
      Use a nova abordagem simplificada para integrar aplicativos empresariais. Simplesmente especifique o aplicativo e suas ações diretamente na configuração do Agent.
    </Tip>
```

Example 4 (unknown):
```unknown
### Filtrando ferramentas
```

---

## Create an agent with Shopify capabilities

**URL:** llms-txt#create-an-agent-with-shopify-capabilities

shopify_agent = Agent(
    role="E-commerce Manager",
    goal="Manage online store operations and customer relationships efficiently",
    backstory="An AI assistant specialized in e-commerce operations and online store management.",
    apps=['shopify']
)

---

## 도구 & 통합

**URL:** llms-txt#도구-&-통합

**Contents:**
- 개요
- 살펴보기
- 관련 문서

Source: https://docs.crewai.com/ko/enterprise/features/tools-and-integrations

외부 앱을 연결하고 에이전트가 사용할 내부 도구를 관리하세요.

도구 & 통합은 서드파티 애플리케이션을 연결하고 에이전트가 런타임에 사용할 내부 도구를 관리하는 중앙 허브입니다.

<Frame>
    <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=c31a4b9031f0f517fdce3baa48471f58" alt="도구 & 통합 개요" data-og-width="1024" width="1024" data-og-height="1024" height="1024" data-path="images/enterprise/crew_connectors.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=9e592d155e388bb67d003b26884dc081 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=0c8aa20b2dc82de9ea3d2da6920e4195 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=782fe13ea53120f6d2f8e643a7a7b838 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=780cd735280c569e6e93caa8262b12d1 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=08bfe86a58ca08ec36ae67dca4aa5cf9 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/crew_connectors.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=e2bbe3b0fe0234001e030b501fa4d76c 2500w" />
</Frame>

<Tabs>
  <Tab title="통합" icon="plug">
    ## 에이전트 앱 (통합)

Gmail, Google Drive, HubSpot, Slack 등 OAuth 기반 서비스에 연결하여 에이전트 액션을 활성화하세요.

<Steps>
      <Step title="연결">
        원하는 앱에서 <b>Connect</b>를 클릭하고 OAuth를 완료합니다.
      </Step>

<Step title="구성">
        필요에 따라 스코프, 트리거, 사용 가능한 액션을 조정합니다.
      </Step>

<Step title="에이전트에서 사용">
        연결된 서비스는 에이전트 도구로 사용 가능합니다.
      </Step>
    </Steps>

<Frame>
            <img src="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=43abfc4eae390e308bed0b8e15238a54" alt="앱 그리드" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/agent-apps.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=280&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=e5e30bd3d904891d5c2c4d9d6182002a 280w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=560&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=a146a0d69ff2309e7eac8d2f07da1cba 560w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=840&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=c85a4a7ebe043fc6819957ff51f3ef0d 840w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=1100&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=4ea77f15a4fe2671267f7e3668615970 1100w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=1650&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=7835e5d197251834d83a6dd7c7813d0a 1650w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/agent-apps.png?w=2500&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=06cea3ae58b49b925566a7962585b148 2500w" />
    </Frame>

1. <Link href="https://app.crewai.com/crewai_plus/connectors">Integrations</Link>로 이동
    2. 원하는 서비스에서 <b>Connect</b> 클릭
    3. OAuth 플로우 완료 및 스코프 승인
    4. <Link href="https://app.crewai.com/crewai_plus/settings/integrations">통합 설정</Link>에서 Enterprise Token 복사

<Frame>
            <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=4e7388bcb76f3f8aa6c6802dd0a98956" alt="Enterprise Token" data-og-width="2264" width="2264" data-og-height="540" height="540" data-path="images/enterprise/enterprise_action_auth_token.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=f3d1bd9cd9783d3e83f42ab6ee42d26c 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=df1514f746270a9ae5fc252c07806761 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=a16c5c7986003435afad4106ccbaa7c5 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=81dabefb14a7f604a68c74eff26dff90 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=2833c9f202a291f2cf022026db261793 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise_action_auth_token.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=eeece6b187aebd0ec9e8af29d8bfc889 2500w" />
    </Frame>

로컬에서 통합을 사용하려면 최신 `crewai-tools` 패키지를 설치하세요.

<Note>
      `Agent(apps=[])`와 함께 통합을 사용하려면 Enterprise Token으로 `CREWAI_PLATFORM_INTEGRATION_TOKEN` 환경 변수를 설정해야 합니다.
    </Note>

<Tip>
      새로운 간소화된 접근 방식을 사용하여 엔터프라이즈 앱을 통합하세요. Agent 구성에서 앱과 해당 액션을 직접 지정하기만 하면 됩니다.
    </Tip>

배포된 크루에서는 각 통합의 서비스 설정 페이지에서 사용 가능한 액션을 지정할 수 있습니다.

<Frame>
            <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=2e689397eabeacd23d0c226ff40566fd" alt="액션 필터링" data-og-width="3680" width="3680" data-og-height="2382" height="2382" data-path="images/enterprise/filtering_enterprise_action_tools.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=a6045a09da61d593e04098a4627777c9 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=257b1eea0bca2def5d43df960a4171ef 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6b9b8686a4fec0c0cdd8c7aa9acd4695 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=e16c10384300b96d4962e2847f6633bf 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=6de59b5409513b100c5cd36a69701e5f 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/filtering_enterprise_action_tools.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=32ed2ecc611c989e0fe9d8cb351740fa 2500w" />
    </Frame>

### 범위 지정 배포 (다중 사용자 조직)

각 통합을 특정 사용자로 범위 지정할 수 있습니다 (예: 특정 사용자의 Gmail 계정 사용).

<Tip>
      팀/사용자별 데이터 접근을 분리해야 할 때 유용합니다.
    </Tip>

`user_bearer_token`을 사용해 요청 사용자로 인증을 범위 지정합니다. 사용자가 로그인하지 않은 경우 연결된 통합을 사용하지 않으며, 그렇지 않으면 배포에 설정된 기본 토큰을 사용합니다.

<Frame>
            <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=d62aed15392f304cfc16bfa38ab91a54" alt="사용자 토큰" data-og-width="532" width="532" data-og-height="732" height="732" data-path="images/enterprise/user_bearer_token.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=efe731a753ab7efb10a65f648fba75a7 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=232d8d25cd253f071856f53425cc40c2 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=df7b4956ab7668c23380394d8ce0f6c1 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=523850a6b69b5dd47ceaca3681f0ac35 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=561dcfa07461ecc8c39cd80865802d5e 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/user_bearer_token.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=06fbc44278b7d23fd2befd6b745622e7 2500w" />
    </Frame>

* Gmail — 이메일 및 초안 관리
    * Slack — 워크스페이스 알림 및 경보
    * Microsoft — Office 365 및 Teams 통합

* Jira — 이슈 추적 및 프로젝트 관리
    * ClickUp — 작업 및 생산성 관리
    * Asana — 팀 작업 조율
    * Notion — 페이지 및 데이터베이스 관리
    * Linear — 버그/프로젝트 추적
    * GitHub — 리포지토리 및 이슈 관리

* Salesforce — 계정 및 기회 관리
    * HubSpot — 파이프라인/연락처 관리
    * Zendesk — 고객 지원 티켓 관리

* Stripe — 결제 처리 및 고객 관리
    * Shopify — 전자상거래 및 상품 관리

* Google Sheets — 스프레드시트 동기화
    * Google Calendar — 일정/이벤트 관리
    * Box — 파일 스토리지

…더 많은 통합이 추가될 예정입니다!
  </Tab>

<Tab title="내부 도구" icon="toolbox">
    ## 내부 도구

로컬에서 도구를 만들고, CrewAI AMP 도구 저장소에 게시한 후, 에이전트에서 사용하세요.

<Tip>
      아래 명령을 실행하기 전에 CrewAI AMP 계정에 로그인하세요:

<Frame>
            <img src="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=b31a82341fb4dcd784c2ecfc1c3d576c" alt="내부 도구" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/tools-integrations-internal.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=280&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=4b7ea6075327365b2486b405db715126 280w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=560&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=857f73fdff530aa6c7d801267e3cbc8a 560w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=840&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=2e844aa05d5c5367f9f8c14deeb78ad7 840w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=1100&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=fd26df60df1b528fc1644e08289738da 1100w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=1650&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=11d2cd7d7e38cb9cfeed2e23c4e3fe87 1650w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tools-integrations-internal.png?w=2500&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=cba0837b7f2039f9c59cdafb81cc53b9 2500w" />
    </Frame>

<Steps>
      <Step title="생성">
        로컬에서 새 도구 생성

<Step title="게시">
        도구 저장소에 게시

<Step title="설치">
        도구 저장소에서 설치

* 이름 및 설명
    * 가시성 (비공개 / 공개)
    * 필요한 환경 변수
    * 버전 이력 및 다운로드
    * 팀/역할 접근 권한

<Frame>
            <img src="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=1896ebecec784bc15411a0309a0cf973" alt="도구 설정" data-og-width="3648" width="3648" data-og-height="2266" height="2266" data-path="images/enterprise/tool-configs.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=280&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=fa0c14f9439ebad25474aa422f8b1bd7 280w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=560&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=d135d69d85a0ccb8d99403def21c8529 560w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=840&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=f65ac1de79956f4178a610be29c6e212 840w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=1100&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=3b13a8181819dbf6b07ed52f239f588a 1100w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=1650&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=0dc0e377941d126e06fa76cb176b70e2 1650w, https://mintcdn.com/crewai/VGZ5vPOL3DPMThlg/images/enterprise/tool-configs.png?w=2500&fit=max&auto=format&n=VGZ5vPOL3DPMThlg&q=85&s=53bf0fa4215eb47d5959d1c46a232db1 2500w" />
    </Frame>
  </Tab>
</Tabs>

<CardGroup cols={2}>
  <Card title="도구 저장소" href="/ko/enterprise/features/tool-repository" icon="toolbox">
    크루 기능을 확장할 수 있도록 도구를 게시하고 설치하세요.
  </Card>

<Card title="Webhook 자동화" href="/ko/enterprise/guides/webhook-automation" icon="bolt">
    워크플로를 자동화하고 외부 플랫폼/서비스와 통합하세요.
  </Card>
</CardGroup>

**Examples:**

Example 1 (unknown):
```unknown
### 환경 변수 설정

    <Note>
      `Agent(apps=[])`와 함께 통합을 사용하려면 Enterprise Token으로 `CREWAI_PLATFORM_INTEGRATION_TOKEN` 환경 변수를 설정해야 합니다.
    </Note>
```

Example 2 (unknown):
```unknown
또는 `.env` 파일에 추가하세요:
```

Example 3 (unknown):
```unknown
### 사용 예시

    <Tip>
      새로운 간소화된 접근 방식을 사용하여 엔터프라이즈 앱을 통합하세요. Agent 구성에서 앱과 해당 액션을 직접 지정하기만 하면 됩니다.
    </Tip>
```

Example 4 (unknown):
```unknown
### 도구 필터링
```

---

## Initialize the tool for website scraping capabilities

**URL:** llms-txt#initialize-the-tool-for-website-scraping-capabilities

tool = SerperScrapeWebsiteTool()

---

## Create an agent with Excel capabilities

**URL:** llms-txt#create-an-agent-with-excel-capabilities

excel_agent = Agent(
    role="Excel Data Manager",
    goal="Manage Excel workbooks and data efficiently",
    backstory="An AI assistant specialized in Excel data management and analysis.",
    apps=['microsoft_excel']  # All Excel actions will be available
)

---

## Create an agent with Zendesk capabilities

**URL:** llms-txt#create-an-agent-with-zendesk-capabilities

zendesk_agent = Agent(
    role="Support Manager",
    goal="Manage customer support tickets and provide excellent customer service",
    backstory="An AI assistant specialized in customer support operations and ticket management.",
    apps=['zendesk']
)

---

## Create an agent with Microsoft OneDrive capabilities

**URL:** llms-txt#create-an-agent-with-microsoft-onedrive-capabilities

onedrive_agent = Agent(
    role="File Manager",
    goal="Manage files and folders in OneDrive efficiently",
    backstory="An AI assistant specialized in Microsoft OneDrive file operations and organization.",
    apps=['microsoft_onedrive']  # All OneDrive actions will be available
)

---

## Bright Data Tools

**URL:** llms-txt#bright-data-tools

**Contents:**
- Installation
- Environment Variables
- Included Tools
- Examples
  - SERP Search
  - Web Unlocker
  - Dataset API
- Troubleshooting
- Example

This set of tools integrates Bright Data services for web extraction.

## Environment Variables

* `BRIGHT_DATA_API_KEY` (required)
* `BRIGHT_DATA_ZONE` (for SERP/Web Unlocker)

Create credentials at [https://brightdata.com/](https://brightdata.com/) (sign up, then create an API token and zone).
See their docs: [https://developers.brightdata.com/](https://developers.brightdata.com/)

* `BrightDataSearchTool`: SERP search (Google/Bing/Yandex) with geo/language/device options.
* `BrightDataWebUnlockerTool`: Scrape pages with anti-bot bypass and rendering.
* `BrightDataDatasetTool`: Run Dataset API jobs and fetch results.

* 401/403: verify `BRIGHT_DATA_API_KEY` and `BRIGHT_DATA_ZONE`.
* Empty/blocked content: enable rendering or try a different zone.

**Examples:**

Example 1 (unknown):
```unknown
## Environment Variables

* `BRIGHT_DATA_API_KEY` (required)
* `BRIGHT_DATA_ZONE` (for SERP/Web Unlocker)

Create credentials at [https://brightdata.com/](https://brightdata.com/) (sign up, then create an API token and zone).
See their docs: [https://developers.brightdata.com/](https://developers.brightdata.com/)

## Included Tools

* `BrightDataSearchTool`: SERP search (Google/Bing/Yandex) with geo/language/device options.
* `BrightDataWebUnlockerTool`: Scrape pages with anti-bot bypass and rendering.
* `BrightDataDatasetTool`: Run Dataset API jobs and fetch results.

## Examples

### SERP Search
```

Example 2 (unknown):
```unknown
### Web Unlocker
```

Example 3 (unknown):
```unknown
### Dataset API
```

Example 4 (unknown):
```unknown
## Troubleshooting

* 401/403: verify `BRIGHT_DATA_API_KEY` and `BRIGHT_DATA_ZONE`.
* Empty/blocked content: enable rendering or try a different zone.

## Example
```

---

## Google Calendar Trigger

**URL:** llms-txt#google-calendar-trigger

**Contents:**
- Overview
- Enabling the Google Calendar Trigger
- Example: Summarize meeting details
- Testando Localmente

Source: https://docs.crewai.com/pt-BR/enterprise/guides/google-calendar-trigger

Kick off crews when Google Calendar events are created, updated, or cancelled

Use the Google Calendar trigger to launch automations whenever calendar events change. Common use cases include briefing a team before a meeting, notifying stakeholders when a critical event is cancelled, or summarizing daily schedules.

<Tip>
  Make sure Google Calendar is connected in **Tools & Integrations** and enabled for the deployment you want to automate.
</Tip>

## Enabling the Google Calendar Trigger

1. Open your deployment in CrewAI AMP
2. Go to the **Triggers** tab
3. Locate **Google Calendar** and switch the toggle to enable

<Frame>
  <img src="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=e6594f439112ba76a399585e3e69e166" alt="Enable or disable triggers with toggle" data-og-width="2228" width="2228" data-og-height="1000" height="1000" data-path="images/enterprise/calendar-trigger.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=280&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=fa2e4f7da20c86c5ad7a6b7e2ab96116 280w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=560&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=c3f8a6638774eadefa5a5924328d5787 560w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=840&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=a2b8c83efc9a11a156877a8f061ca39c 840w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=1100&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=c772c71eda91c64d2db474c2ecb74159 1100w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=1650&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=35c5f5fe2de12a82aa0f1f798380def1 1650w, https://mintcdn.com/crewai/Grq_Qb7_m8o-TQ5O/images/enterprise/calendar-trigger.png?w=2500&fit=max&auto=format&n=Grq_Qb7_m8o-TQ5O&q=85&s=1fefaff8a0a2cf8e9d7d4c11203ed0eb 2500w" />
</Frame>

## Example: Summarize meeting details

The snippet below mirrors the `calendar-event-crew.py` example in the trigger repository. It parses the payload, analyses the attendees and timing, and produces a meeting brief for downstream tools.

Use `crewai_trigger_payload` exactly as it is delivered by the trigger so the crew can extract the proper fields.

## Testando Localmente

Teste sua integração de trigger do Google Calendar localmente usando a CLI da CrewAI:

```bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
Use `crewai_trigger_payload` exactly as it is delivered by the trigger so the crew can extract the proper fields.

## Testando Localmente

Teste sua integração de trigger do Google Calendar localmente usando a CLI da CrewAI:
```

---

## Create an agent with Google Contacts capabilities

**URL:** llms-txt#create-an-agent-with-google-contacts-capabilities

contacts_agent = Agent(
    role="Contact Manager",
    goal="Manage contacts and directory information efficiently",
    backstory="An AI assistant specialized in contact management and directory operations.",
    apps=['google_contacts']  # All Google Contacts actions will be available
)

---

## LangChain 도구

**URL:** llms-txt#langchain-도구

**Contents:**
- `LangChainTool`

Source: https://docs.crewai.com/ko/tools/ai-ml/langchaintool

LangChainTool은 LangChain 도구 및 쿼리 엔진을 위한 래퍼(wrapper)입니다.

<Info>
  CrewAI는 LangChain의 포괄적인 [도구 목록](https://python.langchain.com/docs/integrations/tools/)과 원활하게 통합되며, 이 모든 도구들은 CrewAI와 함께 사용할 수 있습니다.
</Info>

```python Code theme={null}
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew
from crewai.tools import BaseTool
from pydantic import Field
from langchain_community.utilities import GoogleSerperAPIWrapper

---

## Initialize the tool for internet searching capabilities

**URL:** llms-txt#initialize-the-tool-for-internet-searching-capabilities

**Contents:**
- Etapas para Começar
- Conclusão

tool = EXASearchTool()
```

## Etapas para Começar

Para usar o EXASearchTool de forma eficaz, siga estas etapas:

<Steps>
  <Step title="Instalação do Pacote">
    Confirme se o pacote `crewai[tools]` está instalado em seu ambiente Python.
  </Step>

<Step title="Obtenção da Chave de API">
    Adquira uma chave de API da [exa.ai](https://exa.ai/) registrando-se gratuitamente em [exa.ai](https://exa.ai/).
  </Step>

<Step title="Configuração de Ambiente">
    Armazene a chave de API obtida em uma variável de ambiente chamada `EXA_API_KEY` para facilitar o uso pela ferramenta.
  </Step>
</Steps>

Ao integrar o `EXASearchTool` em projetos Python, os usuários ganham a capacidade de realizar buscas relevantes e em tempo real pela internet diretamente de suas aplicações.
Seguindo as orientações de configuração e uso fornecidas, a incorporação desta ferramenta em projetos torna-se simples e direta.

---

## Each server's tools get unique prefixes based on the server name

**URL:** llms-txt#each-server's-tools-get-unique-prefixes-based-on-the-server-name

---

## Less efficient - gets all tools from server

**URL:** llms-txt#less-efficient---gets-all-tools-from-server

**Contents:**
  - 2. Handle Authentication Securely

mcps=["https://weather.api.com/mcp"]
python  theme={null}
import os

**Examples:**

Example 1 (unknown):
```unknown
### 2. Handle Authentication Securely
```

---

## 3. Continue with available tools

**URL:** llms-txt#3.-continue-with-available-tools

---

## Create an agent with Google Sheets capabilities

**URL:** llms-txt#create-an-agent-with-google-sheets-capabilities

sheets_agent = Agent(
    role="Data Manager",
    goal="Manage spreadsheet data and track information efficiently",
    backstory="An AI assistant specialized in data management and spreadsheet operations.",
    apps=['google_sheets']
)

---

## Create an agent with Salesforce capabilities

**URL:** llms-txt#create-an-agent-with-salesforce-capabilities

salesforce_agent = Agent(
    role="CRM Manager",
    goal="Manage customer relationships and sales processes efficiently",
    backstory="An AI assistant specialized in CRM operations and sales automation.",
    apps=['salesforce']
)

---

## Better solution: Use RAG tools for large data

**URL:** llms-txt#better-solution:-use-rag-tools-for-large-data

from crewai_tools import RagTool
agent.tools = [RagTool()]

---

## Create an agent with Google Drive capabilities

**URL:** llms-txt#create-an-agent-with-google-drive-capabilities

drive_agent = Agent(
    role="File Manager",
    goal="Manage files and folders in Google Drive efficiently",
    backstory="An AI assistant specialized in document and file management.",
    apps=['google_drive']  # All Google Drive actions will be available
)

---

## Create an agent with Clickup capabilities

**URL:** llms-txt#create-an-agent-with-clickup-capabilities

clickup_agent = Agent(
    role="Task Manager",
    goal="Manage tasks and projects in ClickUp efficiently",
    backstory="An AI assistant specialized in task management and productivity coordination.",
    apps=['clickup']  # All Clickup actions will be available
)

---

## First agent creation - discovers tools from server

**URL:** llms-txt#first-agent-creation---discovers-tools-from-server

agent1 = Agent(role="First", goal="Test", backstory="Test",
               mcps=["https://api.example.com/mcp"])

---

## Create an agent with Asana capabilities

**URL:** llms-txt#create-an-agent-with-asana-capabilities

asana_agent = Agent(
    role="Project Manager",
    goal="Manage tasks and projects in Asana efficiently",
    backstory="An AI assistant specialized in project management and task coordination.",
    apps=['asana']
)

---

## MCP tools are now automatically available!

**URL:** llms-txt#mcp-tools-are-now-automatically-available!

---

## Create an agent with Jira capabilities

**URL:** llms-txt#create-an-agent-with-jira-capabilities

jira_agent = Agent(
    role="Issue Manager",
    goal="Manage Jira issues and track project progress efficiently",
    backstory="An AI assistant specialized in issue tracking and project management.",
    apps=['jira']
)

---

## Gmail Trigger

**URL:** llms-txt#gmail-trigger

**Contents:**
- Overview
- Enabling the Gmail Trigger
- Example: Process new emails
  - Testando Localmente

Source: https://docs.crewai.com/pt-BR/enterprise/guides/gmail-trigger

Trigger automations when Gmail events occur (e.g., new emails, labels).

Use the Gmail Trigger to kick off your deployed crews when Gmail events happen in connected accounts, such as receiving a new email or messages matching a label/filter.

<Tip>
  Make sure Gmail is connected in Tools & Integrations and the trigger is enabled for your deployment.
</Tip>

## Enabling the Gmail Trigger

1. Open your deployment in CrewAI AMP
2. Go to the **Triggers** tab
3. Locate **Gmail** and switch the toggle to enable

<Frame>
  <img src="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=10b3ee6296f323168473593b64a1e4c8" alt="Enable or disable triggers with toggle" data-og-width="1984" width="1984" data-og-height="866" height="866" data-path="images/enterprise/trigger-selected.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=280&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=27137c8d8c072ece3319e9f4c8ee0185 280w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=560&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=842109fa147a6a91b9f9480e450a8ee0 560w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=840&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=5f2cbab1be7662c99854f88496f42b4b 840w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=1100&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=5fa4240b233d980059d3db96c493fda4 1100w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=1650&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=37f3001a39aab6400b8df45fad9b5cfa 1650w, https://mintcdn.com/crewai/Tp3HEbbp9mp-dy3H/images/enterprise/trigger-selected.png?w=2500&fit=max&auto=format&n=Tp3HEbbp9mp-dy3H&q=85&s=b2959938cb0f239a6113c9a8b7aa0356 2500w" />
</Frame>

## Example: Process new emails

When a new email arrives, the Gmail Trigger will send the payload to your Crew or Flow. Below is a Crew example that parses and processes the trigger payload.

The Gmail payload will be available via the standard context mechanisms.

### Testando Localmente

Teste sua integração de trigger do Gmail localmente usando a CLI da CrewAI:

```bash  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
The Gmail payload will be available via the standard context mechanisms.

### Testando Localmente

Teste sua integração de trigger do Gmail localmente usando a CLI da CrewAI:
```

---

## Create agent with Slack messaging capabilities

**URL:** llms-txt#create-agent-with-slack-messaging-capabilities

notification_agent = Agent(
    role="Notification Manager",
    goal="Create rich, interactive notifications and manage workspace communication",
    backstory="An AI assistant that specializes in creating engaging team notifications and updates.",
    apps=['slack/send_message']  # Specific action for sending messages
)

---

## Create agent with Gmail thread management capabilities

**URL:** llms-txt#create-agent-with-gmail-thread-management-capabilities

thread_manager = Agent(
    role="Thread Manager",
    goal="Organize and manage email threads efficiently",
    backstory="An AI assistant that specializes in email thread organization and management.",
    apps=[
        'gmail/fetch_thread',
        'gmail/modify_thread',
        'gmail/trash_thread'
    ]
)

---

## Create AI tools

**URL:** llms-txt#create-ai-tools

image_generator = DallETool()
vision_processor = VisionTool()
code_executor = CodeInterpreterTool()

---

## Additional API keys (optional)

**URL:** llms-txt#additional-api-keys-(optional)

**Contents:**
  - 전체 구현
  - 예제 실행하기
- LangDB에서 트레이스 보기
  - 볼 수 있는 내용
- 문제 해결
  - 일반적인 문제
- 리소스
- 다음 단계

export SERPER_API_KEY="<your_serper_api_key>"  # For web search capabilities
python  theme={null}
#!/usr/bin/env python3

import os
import sys
from pylangdb.crewai import init
init()  # Initialize LangDB before any CrewAI imports
from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process, LLM
from crewai_tools import SerperDevTool

def create_llm(model):
    return LLM(
        model=model,
        api_key=os.environ.get("LANGDB_API_KEY"),
        base_url=os.environ.get("LANGDB_API_BASE_URL"),
        extra_headers={"x-project-id": os.environ.get("LANGDB_PROJECT_ID")}
    )

class ResearchPlanningCrew:
    def researcher(self) -> Agent:
        return Agent(
            role="Research Specialist",
            goal="Research topics thoroughly and compile comprehensive information",
            backstory="Expert researcher with skills in finding and analyzing information from various sources",
            tools=[SerperDevTool()],
            llm=create_llm("openai/gpt-4o"),
            verbose=True
        )
    
    def planner(self) -> Agent:
        return Agent(
            role="Strategic Planner",
            goal="Create actionable plans based on research findings",
            backstory="Strategic planner who breaks down complex challenges into executable plans",
            reasoning=True,
            max_reasoning_attempts=3,
            llm=create_llm("openai/anthropic/claude-3.7-sonnet"),
            verbose=True
        )
    
    def research_task(self) -> Task:
        return Task(
            description="Research the topic thoroughly and compile comprehensive information",
            agent=self.researcher(),
            expected_output="Comprehensive research report with key findings and insights"
        )
    
    def planning_task(self) -> Task:
        return Task(
            description="Create a strategic plan based on the research findings",
            agent=self.planner(),
            expected_output="Strategic execution plan with phases, goals, and actionable steps",
            context=[self.research_task()]
        )
    
    def crew(self) -> Crew:
        return Crew(
            agents=[self.researcher(), self.planner()],
            tasks=[self.research_task(), self.planning_task()],
            verbose=True,
            process=Process.sequential
        )

def main():
        topic = sys.argv[1] if len(sys.argv) > 1 else "Artificial Intelligence in Healthcare"
        
        crew_instance = ResearchPlanningCrew()
        
        # Update task descriptions with the specific topic
        crew_instance.research_task().description = f"Research {topic} thoroughly and compile comprehensive information"
    crew_instance.planning_task().description = f"Create a strategic plan for {topic} based on the research findings"
    
    result = crew_instance.crew().kickoff()
    print(result)

if __name__ == "__main__":
    main()
bash  theme={null}
python main.py "Sustainable Energy Solutions"
```

CrewAI 애플리케이션을 실행한 후, LangDB 대시보드에서 자세한 트레이스를 확인할 수 있습니다:

<Frame caption="LangDB 트레이스 대시보드">
  <img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=74a88afefce3f84fb6f9482a1790b413" alt="LangDB 트레이스 대시보드에서 CrewAI 워크플로우 표시" data-og-width="1627" width="1627" data-og-height="890" height="890" data-path="images/langdb-2.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=8e43fd482dc80800788d7092a8e51f1c 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=02e4ddf9b1499b19d1e221628f5c21a4 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=31e9c94a264d2b33fc9bfbb6a744dc15 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=5de66fecea56248c974a91c918135e52 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=e03d206dd7c466cc5b9de55bab46daf1 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/langdb-2.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=4c16c2587ec6b48bf8cff71b9df17d07 2500w" />
</Frame>

* **에이전트 상호작용**: 에이전트 대화 및 작업 인계의 전체 흐름
* **도구 사용**: 호출된 도구, 입력값 및 출력값
* **모델 호출**: 프롬프트 및 응답과 함께하는 상세 LLM 상호작용
* **성능 지표**: 지연 시간, 토큰 사용량, 비용 추적
* **실행 타임라인**: 전체 워크플로우의 단계별 보기

* **추적이 나타나지 않음**: `init()`이 CrewAI 임포트 이전에 호출되었는지 확인하세요
* **인증 오류**: LangDB API 키와 프로젝트 ID를 확인하세요

<CardGroup cols={3}>
  <Card title="LangDB 문서" icon="book" href="https://docs.langdb.ai">
    공식 LangDB 문서 및 가이드
  </Card>

<Card title="LangDB 가이드" icon="graduation-cap" href="https://docs.langdb.ai/guides">
    AI 에이전트 구축을 위한 단계별 튜토리얼
  </Card>

<Card title="GitHub 예제" icon="github" href="https://github.com/langdb/langdb-samples/tree/main/examples/crewai">
    CrewAI 통합 전체 예제
  </Card>

<Card title="LangDB 대시보드" icon="chart-line" href="https://app.langdb.ai">
    트레이스 및 분석 액세스
  </Card>

<Card title="모델 카탈로그" icon="list" href="https://app.langdb.ai/models">
    350개 이상의 사용 가능한 언어 모델 살펴보기
  </Card>

<Card title="엔터프라이즈 기능" icon="building" href="https://docs.langdb.ai/enterprise">
    셀프 호스팅 옵션 및 엔터프라이즈 기능
  </Card>
</CardGroup>

이 가이드에서는 LangDB AI Gateway를 CrewAI와 통합하는 기본 사항을 다루었습니다. AI 워크플로우를 더욱 강화하려면 다음을 탐색해보세요:

* **Virtual Models**: 라우팅 전략을 사용한 맞춤형 모델 구성 만들기
* **Guardrails & Safety**: 콘텐츠 필터링 및 컴플라이언스 제어 구현
* **Production Deployment**: 폴백, 재시도, 로드 밸런싱 구성

보다 고급 기능 및 사용 사례에 대해서는 [LangDB Documentation](https://docs.langdb.ai)을 방문하거나, [Model Catalog](https://app.langdb.ai/models)를 탐색하여 사용 가능한 모든 모델을 확인해 보세요.

**Examples:**

Example 1 (unknown):
```unknown
### 전체 구현
```

Example 2 (unknown):
```unknown
### 예제 실행하기
```

---

## LangChain Tool

**URL:** llms-txt#langchain-tool

**Contents:**
- `LangChainTool`

Source: https://docs.crewai.com/en/tools/ai-ml/langchaintool

The `LangChainTool` is a wrapper for LangChain tools and query engines.

<Info>
  CrewAI seamlessly integrates with LangChain's comprehensive [list of tools](https://python.langchain.com/docs/integrations/tools/), all of which can be used with CrewAI.
</Info>

```python Code theme={null}
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew
from crewai.tools import BaseTool
from pydantic import Field
from langchain_community.utilities import GoogleSerperAPIWrapper

---
