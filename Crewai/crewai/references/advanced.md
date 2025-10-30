# Crewai - Advanced

**Pages:** 5

---

## Create an agent for advanced document operations

**URL:** llms-txt#create-an-agent-for-advanced-document-operations

document_formatter = Agent(
    role="Document Formatter",
    goal="Apply advanced formatting and structure to Google Docs",
    backstory="An AI assistant that handles complex document formatting and organization.",
    apps=['google_docs/batch_update', 'google_docs/insert_page_break', 'google_docs/create_named_range']
)

---

## Example with multiple URLs and advanced extraction

**URL:** llms-txt#example-with-multiple-urls-and-advanced-extraction

multi_extract_task = Task(
    description='Extract content from https://example.com and https://anotherexample.org using advanced extraction.',
    expected_output='A JSON string containing the extracted content from both URLs.',
    agent=extractor_agent
)

---

## Advanced OpenAI configuration

**URL:** llms-txt#advanced-openai-configuration

**Contents:**
  - Azure OpenAI 임베딩
  - Google AI 임베딩
  - Vertex AI 임베딩
  - Ollama 임베딩 (로컬)

crew = Crew(
    memory=True,
    embedder={
        "provider": "openai",
        "config": {
            "api_key": "your-openai-api-key",  # Optional: override env var
            "model": "text-embedding-3-large",
            "dimensions": 1536,  # Optional: reduce dimensions for smaller storage
            "organization_id": "your-org-id"  # Optional: for organization accounts
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "openai",  # Use openai provider for Azure
        "config": {
            "api_key": "your-azure-api-key",
            "api_base": "https://your-resource.openai.azure.com/",
            "api_type": "azure",
            "api_version": "2023-05-15",
            "model": "text-embedding-3-small",
            "deployment_id": "your-deployment-name"  # Azure deployment name
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "google",
        "config": {
            "api_key": "your-google-api-key",
            "model": "text-embedding-004"  # or "text-embedding-preview-0409"
        }
    }
)
python  theme={null}
crew = Crew(
    memory=True,
    embedder={
        "provider": "vertexai",
        "config": {
            "project_id": "your-gcp-project-id",
            "region": "us-central1",  # 또는 원하는 리전
            "api_key": "your-service-account-key",
            "model_name": "textembedding-gecko"
        }
    }
)
python  theme={null}

**Examples:**

Example 1 (unknown):
```unknown
### Azure OpenAI 임베딩

Azure OpenAI 배포를 사용하는 엔터프라이즈 사용자용.
```

Example 2 (unknown):
```unknown
### Google AI 임베딩

Google의 텍스트 임베딩 모델을 사용하여 Google Cloud 서비스와 연동할 수 있습니다.
```

Example 3 (unknown):
```unknown
### Vertex AI 임베딩

Vertex AI 액세스 권한이 있는 Google Cloud 사용자용.
```

Example 4 (unknown):
```unknown
### Ollama 임베딩 (로컬)

개인 정보 보호 및 비용 절감을 위해 임베딩을 로컬에서 실행하세요.
```

---

## For Advanced MCPServerAdapter usage

**URL:** llms-txt#for-advanced-mcpserveradapter-usage

**Contents:**
- Quick Start: Simple DSL Integration

uv pip install 'crewai-tools[mcp]'
python  theme={null}
from crewai import Agent, Task, Crew

**Examples:**

Example 1 (unknown):
```unknown
## Quick Start: Simple DSL Integration

The easiest way to integrate MCP servers is using the `mcps` field on your agents:
```

---

## Initialize the agent with advanced options

**URL:** llms-txt#initialize-the-agent-with-advanced-options

**Contents:**
- 위임 및 자율성
  - 예시: 에이전트에 대한 위임 비활성화
- 결론

agent = Agent(
  role='Research Analyst',
  goal='Provide up-to-date market analysis',
  backstory='An expert analyst with a keen eye for market trends.',
  tools=[search_tool],
  memory=True, # Enable memory
  verbose=True,
  max_rpm=None, # No limit on requests per minute
  max_iter=25, # Default value for maximum iterations
)
python Code theme={null}
agent = Agent(
  role='Content Writer',
  goal='Write engaging content on market trends',
  backstory='A seasoned writer with expertise in market analysis.',
  allow_delegation=True # Enabling delegation
)
```

CrewAI에서 에이전트의 역할, 목표, 배경 이야기, 도구를 설정하고, 언어 모델 커스터마이징, 메모리, 성능 설정, 위임 선호도와 같은 고급 옵션을 함께 활용하면 복잡한 과제에 대응할 준비가 된 세밀하고 유능한 AI 팀을 구성할 수 있습니다.

**Examples:**

Example 1 (unknown):
```unknown
## 위임 및 자율성

에이전트가 작업을 위임하거나 질문을 할 수 있는 능력을 제어하는 것은 CrewAI 프레임워크 내에서 자율성과 협업 역학을 맞춤화하는 데 매우 중요합니다. 기본적으로\
`allow_delegation` 속성은 이제 `False`로 설정되어 있어, 에이전트가 필요에 따라 도움을 요청하거나 작업을 위임하는 것이 비활성화됩니다. 이 기본 동작은 CrewAI 생태계 내에서 협동적 문제 해결과\
효율성을 촉진하기 위해 변경될 수 있습니다. 필요할 경우, 특정 운영 요구 사항에 맞게 위임을 활성화할 수 있습니다.

### 예시: 에이전트에 대한 위임 비활성화
```

---
