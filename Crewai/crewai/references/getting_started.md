# Crewai - Getting Started

**Pages:** 12

---

## Azure OpenAI Setup

**URL:** llms-txt#azure-openai-setup

**Contents:**
- Setup Process
- Verification
- Troubleshooting

Source: https://docs.crewai.com/en/enterprise/guides/azure-openai-setup

Configure Azure OpenAI with Crew Studio for enterprise LLM connections

This guide walks you through connecting Azure OpenAI with Crew Studio for seamless enterprise AI operations.

<Steps>
  <Step title="Access Azure AI Foundry">
    1. In Azure, go to [Azure AI Foundry](https://ai.azure.com/) > select your Azure OpenAI deployment.
    2. On the left menu, click `Deployments`. If you don't have one, create a deployment with your desired model.
    3. Once created, select your deployment and locate the `Target URI` and `Key` on the right side of the page. Keep this page open, as you'll need this information.
       <Frame>
         <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=a7136eae05529c674ddbda6e8f58eee8" alt="Azure AI Foundry" data-og-width="670" width="670" data-og-height="502" height="502" data-path="images/enterprise/azure-openai-studio.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=79abbdeb76fa4f38ef6614438651744c 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=c60da2c7f702a15162111d45996d97ff 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=46d5ab75f601b9a14c53c93e51aa57b4 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=67e2c20ec9785d24bf69279102f564a7 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=342a5e6abe1f0a4b1dadf7865ac4cf27 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/azure-openai-studio.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=44d5e6cf8120262a1637a4e24858dfcb 2500w" />
       </Frame>
  </Step>

<Step title="Configure CrewAI AMP Connection">
    4. In another tab, open `CrewAI AMP > LLM Connections`. Name your LLM Connection, select Azure as the provider, and choose the same model you selected in Azure.
    5. On the same page, add environment variables from step 3:
       * One named `AZURE_DEPLOYMENT_TARGET_URL` (using the Target URI). The URL should look like this: [https://your-deployment.openai.azure.com/openai/deployments/gpt-4o/chat/completions?api-version=2024-08-01-preview](https://your-deployment.openai.azure.com/openai/deployments/gpt-4o/chat/completions?api-version=2024-08-01-preview)
       * Another named `AZURE_API_KEY` (using the Key).
    6. Click `Add Connection` to save your LLM Connection.
  </Step>

<Step title="Set Default Configuration">
    7. In `CrewAI AMP > Settings > Defaults > Crew Studio LLM Settings`, set the new LLM Connection and model as defaults.
  </Step>

<Step title="Configure Network Access">
    8. Ensure network access settings:
       * In Azure, go to `Azure OpenAI > select your deployment`.
       * Navigate to `Resource Management > Networking`.
       * Ensure that `Allow access from all networks` is enabled. If this setting is restricted, CrewAI may be blocked from accessing your Azure OpenAI endpoint.
  </Step>
</Steps>

You're all set! Crew Studio will now use your Azure OpenAI connection. Test the connection by creating a simple crew or task to ensure everything is working properly.

If you encounter issues:

* Verify the Target URI format matches the expected pattern
* Check that the API key is correct and has proper permissions
* Ensure network access is configured to allow CrewAI connections
* Confirm the deployment model matches what you've configured in CrewAI

---

## Guia Rápido

**URL:** llms-txt#guia-rápido

**Contents:**
- Construa seu primeiro Agente CrewAI
  - Observação sobre Consistência nos Nomes
- Fazendo o Deploy da Sua Tripulação

Source: https://docs.crewai.com/pt-BR/quickstart

Construa seu primeiro agente de IA com a CrewAI em menos de 5 minutos.

## Construa seu primeiro Agente CrewAI

Vamos criar uma tripulação simples que nos ajudará a `pesquisar` e `relatar` sobre os `últimos avanços em IA` para um determinado tópico ou assunto.

Antes de prosseguir, certifique-se de ter concluído a instalação da CrewAI.
Se ainda não instalou, faça isso seguindo o [guia de instalação](/pt-BR/installation).

Siga os passos abaixo para começar a tripular! 🚣‍♂️

<Steps>
  <Step title="Crie sua tripulação">
    Crie um novo projeto de tripulação executando o comando abaixo em seu terminal.
    Isso criará um novo diretório chamado `latest-ai-development` com a estrutura básica para sua tripulação.

<CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="Navegue até o novo projeto da sua tripulação">
    <CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="Modifique seu arquivo `agents.yaml`">
    <Tip>
      Você também pode modificar os agentes conforme necessário para atender ao seu caso de uso ou copiar e colar como está para seu projeto.
      Qualquer variável interpolada nos seus arquivos `agents.yaml` e `tasks.yaml`, como `{topic}`, será substituída pelo valor da variável no arquivo `main.py`.
    </Tip>

<Step title="Modifique seu arquivo `tasks.yaml`">
    '
      agent: reporting_analyst
      output_file: report.md
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task
    from crewai_tools import SerperDevTool
    from crewai.agents.agent_builder.base_agent import BaseAgent
    from typing import List

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

agents: List[BaseAgent]
      tasks: List[Task]

@agent
      def researcher(self) -> Agent:
        return Agent(
          config=self.agents_config['researcher'], # type: ignore[index]
          verbose=True,
          tools=[SerperDevTool()]
        )

@agent
      def reporting_analyst(self) -> Agent:
        return Agent(
          config=self.agents_config['reporting_analyst'], # type: ignore[index]
          verbose=True
        )

@task
      def research_task(self) -> Task:
        return Task(
          config=self.tasks_config['research_task'], # type: ignore[index]
        )

@task
      def reporting_task(self) -> Task:
        return Task(
          config=self.tasks_config['reporting_task'], # type: ignore[index]
          output_file='output/report.md' # Este é o arquivo que conterá o relatório final.
        )

@crew
      def crew(self) -> Crew:
        """Creates the LatestAiDevelopment crew"""
        return Crew(
          agents=self.agents, # Criado automaticamente pelo decorador @agent
          tasks=self.tasks, # Criado automaticamente pelo decorador @task
          process=Process.sequential,
          verbose=True,
        )
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task, before_kickoff, after_kickoff
    from crewai_tools import SerperDevTool

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

@before_kickoff
      def before_kickoff_function(self, inputs):
        print(f"Before kickoff function with inputs: {inputs}")
        return inputs # You can return the inputs or modify them as needed

@after_kickoff
      def after_kickoff_function(self, result):
        print(f"After kickoff function with result: {result}")
        return result # You can return the result or modify it as needed

# ... remaining code
    python main.py theme={null}
    #!/usr/bin/env python
    # src/latest_ai_development/main.py
    import sys
    from latest_ai_development.crew import LatestAiDevelopmentCrew

def run():
      """
      Run the crew.
      """
      inputs = {
        'topic': 'AI Agents'
      }
      LatestAiDevelopmentCrew().crew().kickoff(inputs=inputs)
    shell Terminal theme={null}
        crewai install
        shell Terminal theme={null}
        uv add <package-name>
        bash Terminal theme={null}
        crewai run
        markdown output/report.md theme={null}
      # Relatório Abrangente sobre a Ascensão e o Impacto dos Agentes de IA em 2025

## 1. Introduction to AI Agents
      In 2025, Artificial Intelligence (AI) agents are at the forefront of innovation across various industries. As intelligent systems that can perform tasks typically requiring human cognition, AI agents are paving the way for significant advancements in operational efficiency, decision-making, and overall productivity within sectors like Human Resources (HR) and Finance. This report aims to detail the rise of AI agents, their frameworks, applications, and potential implications on the workforce.

## 2. Benefits of AI Agents
      AI agents bring numerous advantages that are transforming traditional work environments. Key benefits include:

- **Task Automation**: AI agents can carry out repetitive tasks such as data entry, scheduling, and payroll processing without human intervention, greatly reducing the time and resources spent on these activities.
      - **Improved Efficiency**: By quickly processing large datasets and performing analyses that would take humans significantly longer, AI agents enhance operational efficiency. This allows teams to focus on strategic tasks that require higher-level thinking.
      - **Enhanced Decision-Making**: AI agents can analyze trends and patterns in data, provide insights, and even suggest actions, helping stakeholders make informed decisions based on factual data rather than intuition alone.

## 3. Popular AI Agent Frameworks
      Several frameworks have emerged to facilitate the development of AI agents, each with its own unique features and capabilities. Some of the most popular frameworks include:

- **Autogen**: A framework designed to streamline the development of AI agents through automation of code generation.
      - **Semantic Kernel**: Focuses on natural language processing and understanding, enabling agents to comprehend user intentions better.
      - **Promptflow**: Provides tools for developers to create conversational agents that can navigate complex interactions seamlessly.
      - **Langchain**: Specializes in leveraging various APIs to ensure agents can access and utilize external data effectively.
      - **CrewAI**: Aimed at collaborative environments, CrewAI strengthens teamwork by facilitating communication through AI-driven insights.
      - **MemGPT**: Combines memory-optimized architectures with generative capabilities, allowing for more personalized interactions with users.

These frameworks empower developers to build versatile and intelligent agents that can engage users, perform advanced analytics, and execute various tasks aligned with organizational goals.

## 4. AI Agents in Human Resources
      AI agents are revolutionizing HR practices by automating and optimizing key functions:

- **Recruiting**: AI agents can screen resumes, schedule interviews, and even conduct initial assessments, thus accelerating the hiring process while minimizing biases.
      - **Succession Planning**: AI systems analyze employee performance data and potential, helping organizations identify future leaders and plan appropriate training.
      - **Employee Engagement**: Chatbots powered by AI can facilitate feedback loops between employees and management, promoting an open culture and addressing concerns promptly.

As AI continues to evolve, HR departments leveraging these agents can realize substantial improvements in both efficiency and employee satisfaction.

## 5. AI Agents in Finance
      The finance sector is seeing extensive integration of AI agents that enhance financial practices:

- **Expense Tracking**: Automated systems manage and monitor expenses, flagging anomalies and offering recommendations based on spending patterns.
      - **Risk Assessment**: AI models assess credit risk and uncover potential fraud by analyzing transaction data and behavioral patterns.
      - **Investment Decisions**: AI agents provide stock predictions and analytics based on historical data and current market conditions, empowering investors with informative insights.

The incorporation of AI agents into finance is fostering a more responsive and risk-aware financial landscape.

## 6. Market Trends and Investments
      The growth of AI agents has attracted significant investment, especially amidst the rising popularity of chatbots and generative AI technologies. Companies and entrepreneurs are eager to explore the potential of these systems, recognizing their ability to streamline operations and improve customer engagement.

Conversely, corporations like Microsoft are taking strides to integrate AI agents into their product offerings, with enhancements to their Copilot 365 applications. This strategic move emphasizes the importance of AI literacy in the modern workplace and indicates the stabilizing of AI agents as essential business tools.

## 7. Future Predictions and Implications
      Experts predict that AI agents will transform essential aspects of work life. As we look toward the future, several anticipated changes include:

- Enhanced integration of AI agents across all business functions, creating interconnected systems that leverage data from various departmental silos for comprehensive decision-making.
      - Continued advancement of AI technologies, resulting in smarter, more adaptable agents capable of learning and evolving from user interactions.
      - Increased regulatory scrutiny to ensure ethical use, especially concerning data privacy and employee surveillance as AI agents become more prevalent.

To stay competitive and harness the full potential of AI agents, organizations must remain vigilant about latest developments in AI technology and consider continuous learning and adaptation in their strategic planning.

## 8. Conclusion
      The emergence of AI agents is undeniably reshaping the workplace landscape in 5. With their ability to automate tasks, enhance efficiency, and improve decision-making, AI agents are critical in driving operational success. Organizations must embrace and adapt to AI developments to thrive in an increasingly digital business environment.
      yaml agents.yaml theme={null}
email_summarizer:
    role: >
      Email Summarizer
    goal: >
      Summarize emails into a concise and clear summary
    backstory: >
      You will create a 5 bullet point summary of the report
    llm: provider/model-id  # Add your choice of model here
yaml tasks.yaml theme={null}
email_summarizer_task:
    description: >
      Summarize the email into a 5 bullet point summary
    expected_output: >
      A 5 bullet point summary of the email
    agent: email_summarizer
    context:
      - reporting_task
      - research_task
```

## Fazendo o Deploy da Sua Tripulação

A forma mais fácil de fazer deploy da sua tripulação em produção é através da [CrewAI AMP](http://app.crewai.com).

Assista a este vídeo tutorial para uma demonstração detalhada de como fazer deploy da sua tripulação na [CrewAI AMP](http://app.crewai.com) usando a CLI.

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/3EqSV-CYDZA" title="CrewAI Deployment Guide" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

<CardGroup cols={2}>
  <Card title="Deploy no Enterprise" icon="rocket" href="http://app.crewai.com">
    Comece com o CrewAI AMP e faça o deploy da sua tripulação em ambiente de produção com apenas alguns cliques.
  </Card>

<Card title="Junte-se à Comunidade" icon="comments" href="https://community.crewai.com">
    Participe da nossa comunidade open source para discutir ideias, compartilhar seus projetos e conectar-se com outros desenvolvedores CrewAI.
  </Card>
</CardGroup>

**Examples:**

Example 1 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="Navegue até o novo projeto da sua tripulação">
    <CodeGroup>
```

Example 2 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="Modifique seu arquivo `agents.yaml`">
    <Tip>
      Você também pode modificar os agentes conforme necessário para atender ao seu caso de uso ou copiar e colar como está para seu projeto.
      Qualquer variável interpolada nos seus arquivos `agents.yaml` e `tasks.yaml`, como `{topic}`, será substituída pelo valor da variável no arquivo `main.py`.
    </Tip>
```

Example 3 (unknown):
```unknown
</Step>

  <Step title="Modifique seu arquivo `tasks.yaml`">
```

Example 4 (unknown):
```unknown
</Step>

  <Step title="Modifique seu arquivo `crew.py`">
```

---

## Setup custom model for vectorizer and generative model

**URL:** llms-txt#setup-custom-model-for-vectorizer-and-generative-model

**Contents:**
- 문서 미리 로드하기

tool = WeaviateVectorSearchTool(
    collection_name='example_collections',
    limit=3,
    vectorizer=Configure.Vectorizer.text2vec_openai(model="nomic-embed-text"),
    generative_model=Configure.Generative.openai(model="gpt-4o-mini"),
    weaviate_cluster_url="https://your-weaviate-cluster-url.com",
    weaviate_api_key="your-weaviate-api-key",
)
python Code theme={null}
import os
from crewai_tools import WeaviateVectorSearchTool
import weaviate
from weaviate.classes.init import Auth

**Examples:**

Example 1 (unknown):
```unknown
## 문서 미리 로드하기

도구를 사용하기 전에 Weaviate 데이터베이스에 문서를 미리 로드할 수 있습니다:
```

---

## For custom Ollama installations

**URL:** llms-txt#for-custom-ollama-installations

**Contents:**
  - Cohere Embeddings
  - VoyageAI Embeddings
  - AWS Bedrock Embeddings
  - Hugging Face Embeddings
  - IBM Watson Embeddings
  - Mem0 Provider
  - Choosing the Right Embedding Provider
  - Environment Variable Configuration

crew = Crew(
    memory=True,
    embedder={
        "provider": "ollama",
        "config": {
            "model": "mxbai-embed-large",
            "url": "http://your-ollama-server:11434/api/embeddings"
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "cohere",
        "config": {
            "api_key": "your-cohere-api-key",
            "model": "embed-english-v3.0"  # or "embed-multilingual-v3.0"
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "voyageai",
        "config": {
            "api_key": "your-voyage-api-key",
            "model": "voyage-large-2",  # or "voyage-code-2" for code
            "input_type": "document"  # or "query"
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "bedrock",
        "config": {
            "aws_access_key_id": "your-access-key",
            "aws_secret_access_key": "your-secret-key",
            "region_name": "us-east-1",
            "model": "amazon.titan-embed-text-v1"
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "huggingface",
        "config": {
            "api_key": "your-hf-token",  # Optional for public models
            "model": "sentence-transformers/all-MiniLM-L6-v2",
            "api_url": "https://api-inference.huggingface.co"  # or your custom endpoint
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "watson",
        "config": {
            "api_key": "your-watson-api-key",
            "url": "your-watson-instance-url",
            "model": "ibm/slate-125m-english-rtrvr"
        }
    }
)
python  theme={null}
from crewai.memory.short_term.short_term_memory import ShortTermMemory
from crewai.memory.entity_entity_memory import EntityMemory

mem0_oss_embedder_config = {
        "provider": "mem0",
        "config": {
            "user_id": "john",
            "local_mem0_config": {
                "vector_store": {"provider": "qdrant","config": {"host": "localhost", "port": 6333}},
                "llm": {"provider": "openai","config": {"api_key": "your-api-key", "model": "gpt-4"}},
                "embedder": {"provider": "openai","config": {"api_key": "your-api-key", "model": "text-embedding-3-small"}}
            },
            "infer": True # Optional defaults to True
        },
    }

mem0_client_embedder_config = {
        "provider": "mem0",
        "config": {
            "user_id": "john",
            "org_id": "my_org_id",        # Optional
            "project_id": "my_project_id", # Optional
            "api_key": "custom-api-key"    # Optional - overrides env var
            "run_id": "my_run_id",        # Optional - for short-term memory
            "includes": "include1",       # Optional 
            "excludes": "exclude1",       # Optional
            "infer": True                 # Optional defaults to True
            "custom_categories": new_categories  # Optional - custom categories for user memory
        },
    }

short_term_memory_mem0_oss = ShortTermMemory(embedder_config=mem0_oss_embedder_config) # Short Term Memory with Mem0 OSS
short_term_memory_mem0_client = ShortTermMemory(embedder_config=mem0_client_embedder_config) # Short Term Memory with Mem0 Client
entity_memory_mem0_oss = EntityMemory(embedder_config=mem0_oss_embedder_config) # Entity Memory with Mem0 OSS
entity_memory_mem0_client = EntityMemory(embedder_config=mem0_client_embedder_config) # Short Term Memory with Mem0 Client

crew = Crew(
    memory=True,
    short_term_memory=short_term_memory_mem0_oss, # or short_term_memory_mem0_client
    entity_memory=entity_memory_mem0_oss # or entity_memory_mem0_client
)
python  theme={null}
import os

**Examples:**

Example 1 (unknown):
```unknown
### Cohere Embeddings

Use Cohere's embedding models for multilingual support.
```

Example 2 (unknown):
```unknown
### VoyageAI Embeddings

High-performance embeddings optimized for retrieval tasks.
```

Example 3 (unknown):
```unknown
### AWS Bedrock Embeddings

For AWS users with Bedrock access.
```

Example 4 (unknown):
```unknown
### Hugging Face Embeddings

Use open-source models from Hugging Face.
```

---

## setup monitoring for your crew

**URL:** llms-txt#setup-monitoring-for-your-crew

tracer_provider = register(
    endpoint="http://localhost:6006/v1/traces")
CrewAIInstrumentor().instrument(skip_dep_check=True, tracer_provider=tracer_provider)
search_tool = SerperDevTool()

---

## 퀵스타트

**URL:** llms-txt#퀵스타트

**Contents:**
- 첫 번째 CrewAI Agent 만들기
  - 명명 일관성에 대한 참고
- Crew 배포하기

Source: https://docs.crewai.com/ko/quickstart

5분 이내에 CrewAI로 첫 번째 AI 에이전트를 구축해보세요.

## 첫 번째 CrewAI Agent 만들기

이제 주어진 주제나 항목에 대해 `최신 AI 개발 동향`을 `연구`하고 `보고`하는 간단한 crew를 만들어보겠습니다.

진행하기 전에 CrewAI 설치를 완료했는지 확인하세요.
아직 설치하지 않았다면, [설치 가이드](/ko/installation)를 참고해 설치할 수 있습니다.

아래 단계를 따라 Crewing을 시작하세요! 🚣‍♂️

<Steps>
  <Step title="crew 생성하기">
    터미널에서 아래 명령어를 실행하여 새로운 crew 프로젝트를 만드세요.
    이 작업은 `latest-ai-development`라는 새 디렉터리와 기본 구조를 생성합니다.

<CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="새로운 crew 프로젝트로 이동하기">
    <CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="`agents.yaml` 파일 수정하기">
    <Tip>
      프로젝트에 맞게 agent를 수정하거나 복사/붙여넣기를 할 수 있습니다.
      `agents.yaml` 및 `tasks.yaml` 파일에서 `{topic}`과 같은 변수를 사용하면, 이는 `main.py` 파일의 변수 값으로 대체됩니다.
    </Tip>

<Step title="`tasks.yaml` 파일 수정하기">
    '
      agent: reporting_analyst
      output_file: report.md
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task
    from crewai_tools import SerperDevTool
    from crewai.agents.agent_builder.base_agent import BaseAgent
    from typing import List

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

agents: List[BaseAgent]
      tasks: List[Task]

@agent
      def researcher(self) -> Agent:
        return Agent(
          config=self.agents_config['researcher'], # type: ignore[index]
          verbose=True,
          tools=[SerperDevTool()]
        )

@agent
      def reporting_analyst(self) -> Agent:
        return Agent(
          config=self.agents_config['reporting_analyst'], # type: ignore[index]
          verbose=True
        )

@task
      def research_task(self) -> Task:
        return Task(
          config=self.tasks_config['research_task'], # type: ignore[index]
        )

@task
      def reporting_task(self) -> Task:
        return Task(
          config=self.tasks_config['reporting_task'], # type: ignore[index]
          output_file='output/report.md' # This is the file that will be contain the final report.
        )

@crew
      def crew(self) -> Crew:
        """Creates the LatestAiDevelopment crew"""
        return Crew(
          agents=self.agents, # Automatically created by the @agent decorator
          tasks=self.tasks, # Automatically created by the @task decorator
          process=Process.sequential,
          verbose=True,
        )
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task, before_kickoff, after_kickoff
    from crewai_tools import SerperDevTool

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

@before_kickoff
      def before_kickoff_function(self, inputs):
        print(f"Before kickoff function with inputs: {inputs}")
        return inputs # You can return the inputs or modify them as needed

@after_kickoff
      def after_kickoff_function(self, result):
        print(f"After kickoff function with result: {result}")
        return result # You can return the result or modify it as needed

# ... remaining code
    python main.py theme={null}
    #!/usr/bin/env python
    # src/latest_ai_development/main.py
    import sys
    from latest_ai_development.crew import LatestAiDevelopmentCrew

def run():
      """
      Run the crew.
      """
      inputs = {
        'topic': 'AI Agents'
      }
      LatestAiDevelopmentCrew().crew().kickoff(inputs=inputs)
    shell Terminal theme={null}
        crewai install
        shell Terminal theme={null}
        uv add <package-name>
        bash Terminal theme={null}
        crewai run
        markdown output/report.md theme={null}
      # Comprehensive Report on the Rise and Impact of AI Agents in 2025

## 1. Introduction to AI Agents
      In 2025, Artificial Intelligence (AI) agents are at the forefront of innovation across various industries. As intelligent systems that can perform tasks typically requiring human cognition, AI agents are paving the way for significant advancements in operational efficiency, decision-making, and overall productivity within sectors like Human Resources (HR) and Finance. This report aims to detail the rise of AI agents, their frameworks, applications, and potential implications on the workforce.

## 2. Benefits of AI Agents
      AI agents bring numerous advantages that are transforming traditional work environments. Key benefits include:

- **Task Automation**: AI agents can carry out repetitive tasks such as data entry, scheduling, and payroll processing without human intervention, greatly reducing the time and resources spent on these activities.
      - **Improved Efficiency**: By quickly processing large datasets and performing analyses that would take humans significantly longer, AI agents enhance operational efficiency. This allows teams to focus on strategic tasks that require higher-level thinking.
      - **Enhanced Decision-Making**: AI agents can analyze trends and patterns in data, provide insights, and even suggest actions, helping stakeholders make informed decisions based on factual data rather than intuition alone.

## 3. Popular AI Agent Frameworks
      Several frameworks have emerged to facilitate the development of AI agents, each with its own unique features and capabilities. Some of the most popular frameworks include:

- **Autogen**: A framework designed to streamline the development of AI agents through automation of code generation.
      - **Semantic Kernel**: Focuses on natural language processing and understanding, enabling agents to comprehend user intentions better.
      - **Promptflow**: Provides tools for developers to create conversational agents that can navigate complex interactions seamlessly.
      - **Langchain**: Specializes in leveraging various APIs to ensure agents can access and utilize external data effectively.
      - **CrewAI**: Aimed at collaborative environments, CrewAI strengthens teamwork by facilitating communication through AI-driven insights.
      - **MemGPT**: Combines memory-optimized architectures with generative capabilities, allowing for more personalized interactions with users.

These frameworks empower developers to build versatile and intelligent agents that can engage users, perform advanced analytics, and execute various tasks aligned with organizational goals.

## 4. AI Agents in Human Resources
      AI agents are revolutionizing HR practices by automating and optimizing key functions:

- **Recruiting**: AI agents can screen resumes, schedule interviews, and even conduct initial assessments, thus accelerating the hiring process while minimizing biases.
      - **Succession Planning**: AI systems analyze employee performance data and potential, helping organizations identify future leaders and plan appropriate training.
      - **Employee Engagement**: Chatbots powered by AI can facilitate feedback loops between employees and management, promoting an open culture and addressing concerns promptly.

As AI continues to evolve, HR departments leveraging these agents can realize substantial improvements in both efficiency and employee satisfaction.

## 5. AI Agents in Finance
      The finance sector is seeing extensive integration of AI agents that enhance financial practices:

- **Expense Tracking**: Automated systems manage and monitor expenses, flagging anomalies and offering recommendations based on spending patterns.
      - **Risk Assessment**: AI models assess credit risk and uncover potential fraud by analyzing transaction data and behavioral patterns.
      - **Investment Decisions**: AI agents provide stock predictions and analytics based on historical data and current market conditions, empowering investors with informative insights.

The incorporation of AI agents into finance is fostering a more responsive and risk-aware financial landscape.

## 6. Market Trends and Investments
      The growth of AI agents has attracted significant investment, especially amidst the rising popularity of chatbots and generative AI technologies. Companies and entrepreneurs are eager to explore the potential of these systems, recognizing their ability to streamline operations and improve customer engagement.

Conversely, corporations like Microsoft are taking strides to integrate AI agents into their product offerings, with enhancements to their Copilot 365 applications. This strategic move emphasizes the importance of AI literacy in the modern workplace and indicates the stabilizing of AI agents as essential business tools.

## 7. Future Predictions and Implications
      Experts predict that AI agents will transform essential aspects of work life. As we look toward the future, several anticipated changes include:

- Enhanced integration of AI agents across all business functions, creating interconnected systems that leverage data from various departmental silos for comprehensive decision-making.
      - Continued advancement of AI technologies, resulting in smarter, more adaptable agents capable of learning and evolving from user interactions.
      - Increased regulatory scrutiny to ensure ethical use, especially concerning data privacy and employee surveillance as AI agents become more prevalent.

To stay competitive and harness the full potential of AI agents, organizations must remain vigilant about latest developments in AI technology and consider continuous learning and adaptation in their strategic planning.

## 8. Conclusion
      The emergence of AI agents is undeniably reshaping the workplace landscape in 5. With their ability to automate tasks, enhance efficiency, and improve decision-making, AI agents are critical in driving operational success. Organizations must embrace and adapt to AI developments to thrive in an increasingly digital business environment.
      yaml agents.yaml theme={null}
email_summarizer:
    role: >
      Email Summarizer
    goal: >
      Summarize emails into a concise and clear summary
    backstory: >
      You will create a 5 bullet point summary of the report
    llm: provider/model-id  # Add your choice of model here
yaml tasks.yaml theme={null}
email_summarizer_task:
    description: >
      Summarize the email into a 5 bullet point summary
    expected_output: >
      A 5 bullet point summary of the email
    agent: email_summarizer
    context:
      - reporting_task
      - research_task
```

production 환경에 crew를 배포하는 가장 쉬운 방법은 [CrewAI AMP](http://app.crewai.com)를 통해서입니다.

CLI를 사용하여 [CrewAI AMP](http://app.crewai.com)에 crew를 배포하는 단계별 시연은 이 영상 튜토리얼을 참고하세요.

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/3EqSV-CYDZA" title="CrewAI Deployment Guide" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

<CardGroup cols={2}>
  <Card title="Enterprise에 배포" icon="rocket" href="http://app.crewai.com">
    CrewAI AMP로 시작하여 몇 번의 클릭만으로 production 환경에 crew를 배포하세요.
  </Card>

<Card title="커뮤니티 참여하기" icon="comments" href="https://community.crewai.com">
    오픈 소스 커뮤니티에 참여하여 아이디어를 나누고, 프로젝트를 공유하며, 다른 CrewAI 개발자들과 소통하세요.
  </Card>
</CardGroup>

**Examples:**

Example 1 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="새로운 crew 프로젝트로 이동하기">
    <CodeGroup>
```

Example 2 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="`agents.yaml` 파일 수정하기">
    <Tip>
      프로젝트에 맞게 agent를 수정하거나 복사/붙여넣기를 할 수 있습니다.
      `agents.yaml` 및 `tasks.yaml` 파일에서 `{topic}`과 같은 변수를 사용하면, 이는 `main.py` 파일의 변수 값으로 대체됩니다.
    </Tip>
```

Example 3 (unknown):
```unknown
</Step>

  <Step title="`tasks.yaml` 파일 수정하기">
```

Example 4 (unknown):
```unknown
</Step>

  <Step title="`crew.py` 파일 수정하기">
```

---

## Task to coordinate project setup

**URL:** llms-txt#task-to-coordinate-project-setup

**Contents:**
  - 이슈 계층 구조 및 하위 작업 관리

project_coordination = Task(
    description="""
    1. Search for engineering teams in Linear
    2. Create a new project for Q2 feature development
    3. Associate the project with relevant teams
    4. Create initial project milestones as issues
    """,
    agent=project_coordinator,
    expected_output="Q2 project created with teams assigned and initial milestones established"
)

crew = Crew(
    agents=[project_coordinator],
    tasks=[project_coordination]
)

crew.kickoff()
python  theme={null}
from crewai import Agent, Task, Crew

task_organizer = Agent(
    role="Task Organizer",
    goal="Organize complex issues into manageable sub-tasks",
    backstory="An AI assistant that breaks down complex development work into organized sub-tasks.",
    apps=['linear']
)

**Examples:**

Example 1 (unknown):
```unknown
### 이슈 계층 구조 및 하위 작업 관리
```

---

## Introduction

**URL:** llms-txt#introduction

**Contents:**
- Why use Neatlogs?
- Core Features
- Quick Setup with CrewAI
- Under the Hood
- Watch It Work
  - 🔍 Full Demo (4 min)
  - ⚙️ CrewAI Integration (30 s)
- Links & Support
- TL;DR

Neatlogs helps you **see what your agent did**, **why**, and **share it**.

It captures every step: thoughts, tool calls, responses, evaluations. No raw logs. Just clear, structured traces. Great for debugging and collaboration.

CrewAI agents use multiple tools and reasoning steps. When something goes wrong, you need context — not just errors.

* Follow the full decision path
* Add feedback directly on steps
* Chat with the trace using AI assistant
* Share runs publicly for feedback
* Turn insights into tasks

Manage your traces effortlessly

<img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=d01a5ce64066c6c7387b238068e71369" alt="Traces" data-og-width="1999" width="1999" data-og-height="763" height="763" data-path="images/neatlogs-1.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=ee62fda86fa566c25c133bcab4749395 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=5cb6eaca0429f7e70bb5c8d98a489a97 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=cb664845151f8e54c0e0b9fba753f383 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=fb471833d13ba8718ebd37cc6f557697 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=e470693ab78a2cce5b34570b328c6939 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-1.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=2211c7cdbf87f4e96de3aa5a51927b1d 2500w" />
<img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=5b737699468781be25098c33040d2125" alt="Trace Response" data-og-width="1999" width="1999" data-og-height="1128" height="1128" data-path="images/neatlogs-2.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=020336c536f38ce54dfc04854acac7d4 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=8a40138ff848d453607b8e4cf6d0af31 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=411d496952511260f03dcf703cf40402 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=ce7a99a7d6752ae77706cde411104694 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=e943a0308341c59d6b4d17e29e17126c 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-2.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=61b95cdb68c4c5cbdd349e802db3f2cb 2500w" />

The best UX to view a CrewAI trace. Post comments anywhere you want. Use AI to debug.

<img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=43cda9bcd83376dda4523ff0596b2043" alt="Trace Details" data-og-width="1999" width="1999" data-og-height="1125" height="1125" data-path="images/neatlogs-3.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=b412fc1111d110fba24398449f86c8a6 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=bc9a8210c617335893a0b9e94b9dcede 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=bca4c7758110744a457e3e635ba86e1c 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=c259898ac4cbe4835a0df33f161c7840 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=74f03053e7cc5b98b3e568417de3a319 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-3.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=b90e2b8fcadb097c82a60e6522533386 2500w" />
<img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=c9e7ad0653cae7bfaad2dd448d90eda0" alt="Ai Chat Bot With A Trace" data-og-width="1999" width="1999" data-og-height="751" height="751" data-path="images/neatlogs-4.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=eb0debf5272db5db3729d8b4b4634d94 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=9ebccf5654ad590f1d231118b4a29037 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=a7987df251bd7085c86535c31c3bc8fe 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=113e589438936a55df794a60faec5ff7 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=469f0ab2f09cdd65c18e925ebd88be11 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-4.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=55115f959b3f2e49231e9ed273e6d11c 2500w" />
<img src="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=a977655abb8cd26d9ed4cef5fdd7d859" alt="Comments Drawer" data-og-width="1999" width="1999" data-og-height="1388" height="1388" data-path="images/neatlogs-5.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=280&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=51ad567b077e31082ed8f2a1c53be446 280w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=560&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=b4c663fe1527dc74a13e8c7a7ae955d2 560w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=840&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=fdddfe615d4098db90f694707d70ec87 840w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=1100&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=15cefd5838432e622844dced45f2f6b6 1100w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=1650&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=18b726e6b4bf38ee419f2a50be1e748a 1650w, https://mintcdn.com/crewai/qVjgZHKAyEOgSSUS/images/neatlogs-5.png?w=2500&fit=max&auto=format&n=qVjgZHKAyEOgSSUS&q=85&s=52fcf26f16e0d4177dbcb9c0da5d1bb9 2500w" />

* **Trace Viewer**: Track thoughts, tools, and decisions in sequence
* **Inline Comments**: Tag teammates on any trace step
* **Feedback & Evaluation**: Mark outputs as correct or incorrect
* **Error Highlighting**: Automatic flagging of API/tool failures
* **Task Conversion**: Convert comments into assigned tasks
* **Ask the Trace (AI)**: Chat with your trace using Neatlogs AI bot
* **Public Sharing**: Publish trace links to your community

## Quick Setup with CrewAI

<Steps>
  <Step title="Sign Up & Get API Key">
    Visit [neatlogs.com](https://neatlogs.com/?utm_source=crewAI-docs), create a project, copy the API key.
  </Step>

<Step title="Install SDK">

(Latest version 0.8.0, Python 3.8+; MIT license)
  </Step>

<Step title="Initialize Neatlogs">
    Before starting Crew agents, add:

Agents run as usual. Neatlogs captures everything automatically.
  </Step>
</Steps>

According to GitHub, Neatlogs:

* Captures thoughts, tool calls, responses, errors, and token stats
* Supports AI-powered task generation and robust evaluation workflows

All with just two lines of code.

### 🔍 Full Demo (4 min)

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/8KDme9T2I7Q?si=b8oHteaBwFNs_Duk" title="NeatLogs overview" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

### ⚙️ CrewAI Integration (30 s)

<iframe className="w-full aspect-video rounded-xl" src="https://www.loom.com/embed/9c78b552af43452bb3e4783cb8d91230?sid=e9d7d370-a91a-49b0-809e-2f375d9e801d" title="Loom video player" frameBorder="0" allowFullScreen />

* 📘 [Neatlogs Docs](https://docs.neatlogs.com/)
* 🔐 [Dashboard & API Key](https://app.neatlogs.com/)
* 🐦 [Follow on Twitter](https://twitter.com/neatlogs)
* 📧 Contact: [hello@neatlogs.com](mailto:hello@neatlogs.com)
* 🛠 [GitHub SDK](https://github.com/NeatLogs/neatlogs)

**Examples:**

Example 1 (unknown):
```unknown
(Latest version 0.8.0, Python 3.8+; MIT license)
  </Step>

  <Step title="Initialize Neatlogs">
    Before starting Crew agents, add:
```

Example 2 (unknown):
```unknown
Agents run as usual. Neatlogs captures everything automatically.
  </Step>
</Steps>

## Under the Hood

According to GitHub, Neatlogs:

* Captures thoughts, tool calls, responses, errors, and token stats
* Supports AI-powered task generation and robust evaluation workflows

All with just two lines of code.

## Watch It Work

### 🔍 Full Demo (4 min)

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/8KDme9T2I7Q?si=b8oHteaBwFNs_Duk" title="NeatLogs overview" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

### ⚙️ CrewAI Integration (30 s)

<iframe className="w-full aspect-video rounded-xl" src="https://www.loom.com/embed/9c78b552af43452bb3e4783cb8d91230?sid=e9d7d370-a91a-49b0-809e-2f375d9e801d" title="Loom video player" frameBorder="0" allowFullScreen />

## Links & Support

* 📘 [Neatlogs Docs](https://docs.neatlogs.com/)
* 🔐 [Dashboard & API Key](https://app.neatlogs.com/)
* 🐦 [Follow on Twitter](https://twitter.com/neatlogs)
* 📧 Contact: [hello@neatlogs.com](mailto:hello@neatlogs.com)
* 🛠 [GitHub SDK](https://github.com/NeatLogs/neatlogs)

## TL;DR

With just:
```

---

## Maxim 개요

**URL:** llms-txt#maxim-개요

**Contents:**
- 특징
  - 프롬프트 관리
  - 관찰 가능성 & 평가
- 시작하기
  - 사전 준비 사항
  - 설치
  - 기본 설정
  - 1. 환경 변수 설정
  - Environment Variables Setup

Maxim AI는 귀하의 CrewAI 애플리케이션을 위한 포괄적인 에이전트 모니터링, 평가 및 가시성을 제공합니다. Maxim의 원라인 통합을 통해 에이전트 상호작용, 성능 지표 등을 손쉽게 추적하고 분석할 수 있습니다.

Maxim의 프롬프트 관리 기능을 통해 CrewAI 에이전트를 위한 프롬프트를 생성, 조직, 최적화할 수 있습니다. 지침을 하드코딩하는 대신, Maxim의 SDK를 활용하여 버전 관리가 되는 프롬프트를 동적으로 가져오고 적용하세요.

<Tabs>
  <Tab title="프롬프트 플레이그라운드">
    플레이그라운드를 통해 프롬프트를 생성, 정제, 실험 및 배포할 수 있습니다. 폴더와 버전을 활용하여 프롬프트를 정리하고, 도구 및 컨텍스트를 연결하여 실제 사례로 실험해 보며, 맞춤형 로직을 기반으로 배포할 수 있습니다.

[**모델 구성**](https://www.getmaxim.ai/docs/introduction/quickstart/setting-up-workspace#add-model-api-keys)을 통해 여러 모델을 손쉽게 실험하고, 프롬프트 플레이그라운드 상단 드롭다운에서 원하는 모델을 선택하세요.

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_playground.png" />
  </Tab>

<Tab title="프롬프트 버전">
    팀이 AI 애플리케이션을 개발할 때, 실험의 중요한 부분은 프롬프트 구조를 반복적으로 개선하는 것입니다. 효과적으로 협업하고 변경 사항을 명확히 정리할 수 있도록 Maxim은 프롬프트 버전 관리와 버전 간 비교 실행을 지원합니다.

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_versions.png" />
  </Tab>

<Tab title="프롬프트 비교">
    AI 애플리케이션을 발전시켜 나가면서 프롬프트를 반복 개선하기 위해서는 모델, 프롬프트 구조 등 다양한 요소로 실험이 필요합니다. 버전 간 비교 및 변화에 대한 정보에 기반한 결정을 위해, 비교 플레이그라운드는 결과를 나란히 볼 수 있게 해줍니다.

## **프롬프트 비교를 왜 사용해야 하나요?**

프롬프트 비교는 여러 개의 단일 프롬프트를 하나의 뷰에서 볼 수 있도록 하여 다양한 워크플로에 streamlined 접근을 제공합니다:

1. **모델 비교**: 동일한 프롬프트에서 서로 다른 모델의 성능을 평가합니다.
    2. **프롬프트 최적화**: 여러 버전의 프롬프트를 비교하여 가장 효과적인 구성을 식별합니다.
    3. **교차 모델 일관성**: 동일한 프롬프트에 대해 여러 모델에서 일관된 출력을 보장합니다.
    4. **성능 벤치마킹**: 다양한 모델과 프롬프트에 대해 지연 시간, 비용, 토큰 수 등의 지표를 분석합니다.
  </Tab>
</Tabs>

Maxim AI는 CrewAI 에이전트에 대한 포괄적인 관찰 가능성과 평가 기능을 제공하여, 각 실행 과정에서 무슨 일이 일어나고 있는지 정확히 파악할 수 있도록 지원합니다.

<Tabs>
  <Tab title="Agent Tracing">
    에이전트의 전체 라이프사이클(도구 호출, 에이전트 궤적, 결정 플로우 등)을 손쉽게 추적할 수 있습니다.

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_agent_tracking.png" />
  </Tab>

<Tab title="Analytics + Evals">
    전체 트레이스 또는 개별 노드에 대해 상세 평가를 실행할 수 있으며, 다음 기능을 지원합니다:

* 다중 단계 상호작용 및 세분화된 트레이스 분석
    * 세션 수준 평가
    * 실제 환경 시뮬레이션 테스트

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_trace_eval.png" />

<CardGroup cols={3}>
      <Card title="로그 자동 평가" icon="e" href="https://www.getmaxim.ai/docs/observe/how-to/evaluate-logs/auto-evaluation">
        <p>
          필터 및 샘플링을 기준으로 UI에서 캡처된 로그를 자동으로 평가할 수 있습니다.
        </p>
      </Card>

<Card title="로그 수동 평가" icon="hand" href="https://www.getmaxim.ai/docs/observe/how-to/evaluate-logs/human-evaluation">
        <p>
          로그의 품질을 평가하고, 사람의 평가 또는 등급을 이용해 로그를 검토할 수 있습니다.
        </p>
      </Card>

<Card title="노드 수준 평가" icon="road" href="https://www.getmaxim.ai/docs/observe/how-to/evaluate-logs/node-level-evaluation">
        <p>
          트레이스 또는 로그의 모든 컴포넌트를 평가하여 에이전트의 행동에 대한 통찰을 얻을 수 있습니다.
        </p>
      </Card>
    </CardGroup>

<Tab title="Alerting">
    **오류**, **비용, 토큰 사용량, 사용자 피드백, 지연 시간**에 임계값을 설정하고, Slack 또는 PagerDuty를 통해 실시간 알림을 받아보세요.

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_alerts_1.png" />
  </Tab>

<Tab title="Dashboards">
    시간 경과에 따른 트레이스, 사용량 측정지표, 지연 시간 및 오류율을 손쉽게 시각화할 수 있습니다.

<img src="https://raw.githubusercontent.com/akmadan/crewAI/docs_maxim_observability/docs/images/maxim_dashboard_1.png" />
  </Tab>
</Tabs>

* Python 버전 >=3.10
* Maxim 계정 ([여기에서 가입](https://getmaxim.ai/))
* Maxim API 키 생성
* CrewAI 프로젝트

Maxim SDK를 pip을 통해 설치하세요:

또는 `requirements.txt`에 추가하세요:

```python  theme={null}
### Environment Variables Setup

**Examples:**

Example 1 (unknown):
```unknown
또는 `requirements.txt`에 추가하세요:
```

Example 2 (unknown):
```unknown
### 기본 설정

### 1. 환경 변수 설정
```

---

## This setup allows the agent to only search the given CSV file.

**URL:** llms-txt#this-setup-allows-the-agent-to-only-search-the-given-csv-file.

tool = CSVSearchTool(csv='path/to/your/csvfile.csv')

---

## Installation

**URL:** llms-txt#installation

**Contents:**
- Video Tutorial
- Text Tutorial

Source: https://docs.crewai.com/en/installation

Get started with CrewAI - Install, configure, and build your first AI crew

Watch this video tutorial for a step-by-step demonstration of the installation process:

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/-kSOTtYzgEw" title="CrewAI Installation Guide" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

<Note>
  **Python Version Requirements**

CrewAI requires `Python >=3.10 and <3.14`. Here's how to check your version:

If you need to update Python, visit [python.org/downloads](https://python.org/downloads)
</Note>

<Note>
  **OpenAI SDK Requirement**

CrewAI 0.175.0 requires `openai >= 1.13.3`. If you manage dependencies yourself, ensure your environment satisfies this constraint to avoid import/runtime issues.
</Note>

CrewAI uses the `uv` as its dependency management and package handling tool. It simplifies project setup and execution, offering a seamless experience.

If you haven't installed `uv` yet, follow **step 1** to quickly get it set up on your system, else you can skip to **step 2**.

<Steps>
  <Step title="Install uv">
    * **On macOS/Linux:**

Use `curl` to download the script and execute it with `sh`:

If your system doesn't have `curl`, you can use `wget`:

Use `irm` to download the script and `iex` to execute it:

If you run into any issues, refer to [UV's installation guide](https://docs.astral.sh/uv/getting-started/installation/) for more information.
  </Step>

<Step title="Install CrewAI 🚀">
    * Run the following command to install `crewai` CLI:

<Warning>
        If you encounter a `PATH` warning, run this command to update your shell:

<Warning>
        If you encounter the `chroma-hnswlib==0.7.6` build error (`fatal error C1083: Cannot open include file: 'float.h'`) on Windows, install [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/) with *Desktop development with C++*.
      </Warning>

* To verify that `crewai` is installed, run:

* You should see something like:

* If you need to update `crewai`, run:

<Check>Installation successful! You're ready to create your first crew! 🎉</Check>
  </Step>
</Steps>

**Examples:**

Example 1 (unknown):
```unknown
If you need to update Python, visit [python.org/downloads](https://python.org/downloads)
</Note>

<Note>
  **OpenAI SDK Requirement**

  CrewAI 0.175.0 requires `openai >= 1.13.3`. If you manage dependencies yourself, ensure your environment satisfies this constraint to avoid import/runtime issues.
</Note>

CrewAI uses the `uv` as its dependency management and package handling tool. It simplifies project setup and execution, offering a seamless experience.

If you haven't installed `uv` yet, follow **step 1** to quickly get it set up on your system, else you can skip to **step 2**.

<Steps>
  <Step title="Install uv">
    * **On macOS/Linux:**

      Use `curl` to download the script and execute it with `sh`:
```

Example 2 (unknown):
```unknown
If your system doesn't have `curl`, you can use `wget`:
```

Example 3 (unknown):
```unknown
* **On Windows:**

      Use `irm` to download the script and `iex` to execute it:
```

Example 4 (unknown):
```unknown
If you run into any issues, refer to [UV's installation guide](https://docs.astral.sh/uv/getting-started/installation/) for more information.
  </Step>

  <Step title="Install CrewAI 🚀">
    * Run the following command to install `crewai` CLI:
```

---

## Quickstart

**URL:** llms-txt#quickstart

**Contents:**
- Build your first CrewAI Agent
  - Note on Consistency in Naming
- Deploying Your Crew

Source: https://docs.crewai.com/en/quickstart

Build your first AI agent with CrewAI in under 5 minutes.

## Build your first CrewAI Agent

Let's create a simple crew that will help us `research` and `report` on the `latest AI developments` for a given topic or subject.

Before we proceed, make sure you have finished installing CrewAI.
If you haven't installed them yet, you can do so by following the [installation guide](/en/installation).

Follow the steps below to get Crewing! 🚣‍♂️

<Steps>
  <Step title="Create your crew">
    Create a new crew project by running the following command in your terminal.
    This will create a new directory called `latest-ai-development` with the basic structure for your crew.

<CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="Navigate to your new crew project">
    <CodeGroup>
      
    </CodeGroup>
  </Step>

<Step title="Modify your `agents.yaml` file">
    <Tip>
      You can also modify the agents as needed to fit your use case or copy and paste as is to your project.
      Any variable interpolated in your `agents.yaml` and `tasks.yaml` files like `{topic}` will be replaced by the value of the variable in the `main.py` file.
    </Tip>

<Step title="Modify your `tasks.yaml` file">
    '
      agent: reporting_analyst
      output_file: report.md
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task
    from crewai_tools import SerperDevTool
    from crewai.agents.agent_builder.base_agent import BaseAgent
    from typing import List

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

agents: List[BaseAgent]
      tasks: List[Task]

@agent
      def researcher(self) -> Agent:
        return Agent(
          config=self.agents_config['researcher'], # type: ignore[index]
          verbose=True,
          tools=[SerperDevTool()]
        )

@agent
      def reporting_analyst(self) -> Agent:
        return Agent(
          config=self.agents_config['reporting_analyst'], # type: ignore[index]
          verbose=True
        )

@task
      def research_task(self) -> Task:
        return Task(
          config=self.tasks_config['research_task'], # type: ignore[index]
        )

@task
      def reporting_task(self) -> Task:
        return Task(
          config=self.tasks_config['reporting_task'], # type: ignore[index]
          output_file='output/report.md' # This is the file that will be contain the final report.
        )

@crew
      def crew(self) -> Crew:
        """Creates the LatestAiDevelopment crew"""
        return Crew(
          agents=self.agents, # Automatically created by the @agent decorator
          tasks=self.tasks, # Automatically created by the @task decorator
          process=Process.sequential,
          verbose=True,
        )
    python crew.py theme={null}
    # src/latest_ai_development/crew.py
    from crewai import Agent, Crew, Process, Task
    from crewai.project import CrewBase, agent, crew, task, before_kickoff, after_kickoff
    from crewai_tools import SerperDevTool

@CrewBase
    class LatestAiDevelopmentCrew():
      """LatestAiDevelopment crew"""

@before_kickoff
      def before_kickoff_function(self, inputs):
        print(f"Before kickoff function with inputs: {inputs}")
        return inputs # You can return the inputs or modify them as needed

@after_kickoff
      def after_kickoff_function(self, result):
        print(f"After kickoff function with result: {result}")
        return result # You can return the result or modify it as needed

# ... remaining code
    python main.py theme={null}
    #!/usr/bin/env python
    # src/latest_ai_development/main.py
    import sys
    from latest_ai_development.crew import LatestAiDevelopmentCrew

def run():
      """
      Run the crew.
      """
      inputs = {
        'topic': 'AI Agents'
      }
      LatestAiDevelopmentCrew().crew().kickoff(inputs=inputs)
    shell Terminal theme={null}
        crewai install
        shell Terminal theme={null}
        uv add <package-name>
        bash Terminal theme={null}
        crewai run
        markdown output/report.md theme={null}
      # Comprehensive Report on the Rise and Impact of AI Agents in 2025

## 1. Introduction to AI Agents
      In 2025, Artificial Intelligence (AI) agents are at the forefront of innovation across various industries. As intelligent systems that can perform tasks typically requiring human cognition, AI agents are paving the way for significant advancements in operational efficiency, decision-making, and overall productivity within sectors like Human Resources (HR) and Finance. This report aims to detail the rise of AI agents, their frameworks, applications, and potential implications on the workforce.

## 2. Benefits of AI Agents
      AI agents bring numerous advantages that are transforming traditional work environments. Key benefits include:

- **Task Automation**: AI agents can carry out repetitive tasks such as data entry, scheduling, and payroll processing without human intervention, greatly reducing the time and resources spent on these activities.
      - **Improved Efficiency**: By quickly processing large datasets and performing analyses that would take humans significantly longer, AI agents enhance operational efficiency. This allows teams to focus on strategic tasks that require higher-level thinking.
      - **Enhanced Decision-Making**: AI agents can analyze trends and patterns in data, provide insights, and even suggest actions, helping stakeholders make informed decisions based on factual data rather than intuition alone.

## 3. Popular AI Agent Frameworks
      Several frameworks have emerged to facilitate the development of AI agents, each with its own unique features and capabilities. Some of the most popular frameworks include:

- **Autogen**: A framework designed to streamline the development of AI agents through automation of code generation.
      - **Semantic Kernel**: Focuses on natural language processing and understanding, enabling agents to comprehend user intentions better.
      - **Promptflow**: Provides tools for developers to create conversational agents that can navigate complex interactions seamlessly.
      - **Langchain**: Specializes in leveraging various APIs to ensure agents can access and utilize external data effectively.
      - **CrewAI**: Aimed at collaborative environments, CrewAI strengthens teamwork by facilitating communication through AI-driven insights.
      - **MemGPT**: Combines memory-optimized architectures with generative capabilities, allowing for more personalized interactions with users.

These frameworks empower developers to build versatile and intelligent agents that can engage users, perform advanced analytics, and execute various tasks aligned with organizational goals.

## 4. AI Agents in Human Resources
      AI agents are revolutionizing HR practices by automating and optimizing key functions:

- **Recruiting**: AI agents can screen resumes, schedule interviews, and even conduct initial assessments, thus accelerating the hiring process while minimizing biases.
      - **Succession Planning**: AI systems analyze employee performance data and potential, helping organizations identify future leaders and plan appropriate training.
      - **Employee Engagement**: Chatbots powered by AI can facilitate feedback loops between employees and management, promoting an open culture and addressing concerns promptly.

As AI continues to evolve, HR departments leveraging these agents can realize substantial improvements in both efficiency and employee satisfaction.

## 5. AI Agents in Finance
      The finance sector is seeing extensive integration of AI agents that enhance financial practices:

- **Expense Tracking**: Automated systems manage and monitor expenses, flagging anomalies and offering recommendations based on spending patterns.
      - **Risk Assessment**: AI models assess credit risk and uncover potential fraud by analyzing transaction data and behavioral patterns.
      - **Investment Decisions**: AI agents provide stock predictions and analytics based on historical data and current market conditions, empowering investors with informative insights.

The incorporation of AI agents into finance is fostering a more responsive and risk-aware financial landscape.

## 6. Market Trends and Investments
      The growth of AI agents has attracted significant investment, especially amidst the rising popularity of chatbots and generative AI technologies. Companies and entrepreneurs are eager to explore the potential of these systems, recognizing their ability to streamline operations and improve customer engagement.

Conversely, corporations like Microsoft are taking strides to integrate AI agents into their product offerings, with enhancements to their Copilot 365 applications. This strategic move emphasizes the importance of AI literacy in the modern workplace and indicates the stabilizing of AI agents as essential business tools.

## 7. Future Predictions and Implications
      Experts predict that AI agents will transform essential aspects of work life. As we look toward the future, several anticipated changes include:

- Enhanced integration of AI agents across all business functions, creating interconnected systems that leverage data from various departmental silos for comprehensive decision-making.
      - Continued advancement of AI technologies, resulting in smarter, more adaptable agents capable of learning and evolving from user interactions.
      - Increased regulatory scrutiny to ensure ethical use, especially concerning data privacy and employee surveillance as AI agents become more prevalent.

To stay competitive and harness the full potential of AI agents, organizations must remain vigilant about latest developments in AI technology and consider continuous learning and adaptation in their strategic planning.

## 8. Conclusion
      The emergence of AI agents is undeniably reshaping the workplace landscape in 5. With their ability to automate tasks, enhance efficiency, and improve decision-making, AI agents are critical in driving operational success. Organizations must embrace and adapt to AI developments to thrive in an increasingly digital business environment.
      yaml agents.yaml theme={null}
email_summarizer:
    role: >
      Email Summarizer
    goal: >
      Summarize emails into a concise and clear summary
    backstory: >
      You will create a 5 bullet point summary of the report
    llm: provider/model-id  # Add your choice of model here
yaml tasks.yaml theme={null}
email_summarizer_task:
    description: >
      Summarize the email into a 5 bullet point summary
    expected_output: >
      A 5 bullet point summary of the email
    agent: email_summarizer
    context:
      - reporting_task
      - research_task
```

## Deploying Your Crew

The easiest way to deploy your crew to production is through [CrewAI AMP](http://app.crewai.com).

Watch this video tutorial for a step-by-step demonstration of deploying your crew to [CrewAI AMP](http://app.crewai.com) using the CLI.

<iframe className="w-full aspect-video rounded-xl" src="https://www.youtube.com/embed/3EqSV-CYDZA" title="CrewAI Deployment Guide" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowFullScreen />

<CardGroup cols={2}>
  <Card title="Deploy on Enterprise" icon="rocket" href="http://app.crewai.com">
    Get started with CrewAI AMP and deploy your crew in a production environment with just a few clicks.
  </Card>

<Card title="Join the Community" icon="comments" href="https://community.crewai.com">
    Join our open source community to discuss ideas, share your projects, and connect with other CrewAI developers.
  </Card>
</CardGroup>

**Examples:**

Example 1 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="Navigate to your new crew project">
    <CodeGroup>
```

Example 2 (unknown):
```unknown
</CodeGroup>
  </Step>

  <Step title="Modify your `agents.yaml` file">
    <Tip>
      You can also modify the agents as needed to fit your use case or copy and paste as is to your project.
      Any variable interpolated in your `agents.yaml` and `tasks.yaml` files like `{topic}` will be replaced by the value of the variable in the `main.py` file.
    </Tip>
```

Example 3 (unknown):
```unknown
</Step>

  <Step title="Modify your `tasks.yaml` file">
```

Example 4 (unknown):
```unknown
</Step>

  <Step title="Modify your `crew.py` file">
```

---
