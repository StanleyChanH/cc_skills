# Crewai - Guides

**Pages:** 3

---

## Example: Technical Documentation Agent

**URL:** llms-txt#example:-technical-documentation-agent

**Contents:**
- 실무 구현 체크리스트
  - 다양한 모델 유형을 사용할 시기
- CrewAI 모델 선택에서 흔히 발생하는 실수
- 테스트 및 반복 전략
  - 엔터프라이즈급 모델 검증
- 주요 원칙 요약
- 현재 모델 현황 (2025년 6월)
  - 카테고리별 주요 모델
  - 현재 모델을 위한 선택 프레임워크
  - 모델 선택을 위한 주요 고려사항

tech_writer = Agent(
    role="API Documentation Specialist",  # Specific role for clear LLM requirements
    goal="Create comprehensive, developer-friendly API documentation",
    backstory="""
    You're a technical writer with 8+ years documenting REST APIs, GraphQL endpoints,
    and SDK integration guides. You've worked with developer tools companies and
    understand what developers need: clear examples, comprehensive error handling,
    and practical use cases. You prioritize accuracy and usability over marketing fluff.
    """,
    llm=LLM(
        model="claude-3-5-sonnet",  # Excellent for technical writing
        temperature=0.1  # Low temperature for accuracy
    ),
    tools=[code_analyzer_tool, api_scanner_tool],
    verbose=True
)
python  theme={null}
    # crew에 신뢰할 수 있는 기본값으로 시작합니다
    default_crew_llm = LLM(model="gpt-4o-mini")  # 비용 효율적인 기준점

crew = Crew(
        agents=[...],
        tasks=[...],
        memory=True
    )
    python  theme={null}
    # Manager 또는 coordination agent
    manager_agent = Agent(
        role="Project Manager",
        llm=LLM(model="gemini-2.5-flash-preview-05-20"),  # 조율을 위한 프리미엄
        # ... 나머지 설정
    )

# Creative 또는 고객 대응 agent
    content_agent = Agent(
        role="Content Creator",
        llm=LLM(model="claude-3-5-sonnet"),  # 글쓰기에 최적
        # ... 나머지 설정
    )
    python  theme={null}
    # 전략 agent는 프리미엄 모델 사용
    manager = Agent(role="Strategy Manager", llm=LLM(model="gpt-4o"))

# 처리 agent는 효율적인 모델 사용
    processor = Agent(role="Data Processor", llm=LLM(model="gpt-4o-mini"))
    python  theme={null}
    crew = Crew(
        agents=[agent1, agent2],
        tasks=[task1, task2],
        manager_llm=LLM(model="gpt-4o"),  # crew 조정용
        process=Process.hierarchical  # manager_llm 사용 시
    )

# agent는 특별히 지정하지 않으면 crew LLM을 상속받음
    agent1 = Agent(llm=LLM(model="claude-3-5-sonnet"))  # 특정 요구에 따라 오버라이드
    python  theme={null}
    # 다양한 도구를 사용하는 agent의 경우
    tool_agent = Agent(
        role="API Integration Specialist",
        tools=[search_tool, api_tool, data_tool],
        llm=LLM(model="gpt-4o"),  # 함수 호출에 우수
        # OR
        llm=LLM(model="claude-3-5-sonnet")  # 도구 사용에 강점
    )
    python  theme={null}
    # 이렇게 시작
    crew = Crew(agents=[...], tasks=[...], llm=LLM(model="gpt-4o-mini"))

# 성능을 테스트하고, 필요에 따라 특정 agent만 최적화
    # Enterprise 플랫폼 테스트를 통해 개선 사항 검증
    ```
  </Accordion>

<Accordion title="컨텍스트·메모리 한계 간과" icon="brain">
    **문제점**: 모델의 컨텍스트 윈도(window)와 CrewAI의 메모리, agent 간 컨텍스트 공유 방식을 고려하지 않는 실수.

**실제 예시**: 여러 차례 반복되는 업무나 agent 간 활발한 소통이 필요한 crew에 대화 내역을 오래 유지해야 하는데, 짧은 컨텍스트 모델을 사용한 경우.

**CrewAI 솔루션**: crew의 소통 패턴에 맞춰 컨텍스트 처리 능력을 갖춘 모델을 선택.
  </Accordion>
</AccordionGroup>

<Steps>
  <Step title="간단하게 시작하기" icon="play">
    신뢰할 수 있고, 잘 알려져 있으며, 널리 지원되는 범용 모델로 시작하세요. 이것은 최적화된 특수한 필요에 집중하기 전에 귀하의 특정 요구사항과 성능 기대치를 이해할 수 있는 안정적인 기초를 제공합니다.
  </Step>

<Step title="중요한 것 측정하기" icon="chart-line">
    일반적인 벤치마크에만 의존하지 말고, 귀하의 특정 사용 사례와 비즈니스 요구에 부합하는 지표를 개발하세요. 이론적 성능 지표가 아니라 성공에 직접적으로 영향을 미치는 결과 측정에 집중하세요.
  </Step>

<Step title="결과에 기반한 반복" icon="arrows-rotate">
    이론적 고려사항이나 일반적인 권장사항이 아니라, 귀하의 특정 상황에서 관찰된 성능에 따라 모델을 변경하세요. 실제 성능은 벤치마크 결과나 일반적인 평판과는 크게 다를 수 있습니다.
  </Step>

<Step title="총 비용 고려하기" icon="calculator">
    모델 비용, 개발 시간, 유지 보수 오버헤드, 운영 복잡성 등 소유에 드는 전체 비용을 평가하세요. 토큰당 가장 저렴한 모델이 모든 요소를 고려했을 때 반드시 가장 비용 효율적이지는 않을 수 있습니다.
  </Step>
</Steps>

<Tip>
  먼저 귀하의 요구사항을 이해하는 데 집중한 후, 그 요구와 가장 잘 맞는 모델을 선택하세요. 최상의 LLM 선택은 운영상의 제약 조건 내에서 꾸준히 원하는 결과를 제공하는 것입니다.
</Tip>

LLM 선택을 최적화하고자 하는 팀을 위해 **CrewAI AMP 플랫폼**은 기본적인 CLI 테스트를 훨씬 능가하는 정교한 테스트 기능을 제공합니다. 이 플랫폼은 데이터 기반의 LLM 전략 의사결정을 지원하는 종합적인 모델 평가를 가능하게 합니다.

<Frame>
    <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=08580e93186b6563adca8b75da805805" alt="엔터프라이즈 테스트 인터페이스" data-og-width="2238" width="2238" data-og-height="1700" height="1700" data-path="images/enterprise/enterprise-testing.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=d7ced6158ec4dd0b5a9928edcfc4a38d 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=0bf0f3d7110c1ac4ae4139a80e28b9c2 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=27a38bf115431233bfb9849629dc125e 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=5d73aad5c4af3e62a82044f80add8ac1 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=a91a7198392462683371a28e799943a0 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=78aaf8869525c5633d5f06655cc46c5e 2500w" />
</Frame>

* **다중 모델 비교**: 동일한 작업과 입력에 대해 여러 LLM을 동시에 테스트할 수 있습니다. GPT-4o, Claude, Llama, Groq, Cerebras 및 기타 선도적인 모델의 성능을 병렬로 비교하여 특정 사용 사례에 가장 적합한 모델을 식별할 수 있습니다.

* **통계적 엄밀성**: 일관된 입력값으로 여러 번 테스트를 구성하여 신뢰성과 성능 편차를 측정할 수 있습니다. 이를 통해 단순히 잘하는 모델이 아닌, 여러 번 실행해도 안정적으로 동작하는 모델을 식별할 수 있습니다.

* **실제 환경 검증**: 합성 벤치마크가 아닌 실제 crew 입력값과 시나리오를 사용할 수 있습니다. 플랫폼을 통해 산업 환경, 회사 정보, 실제 사용 사례 등 특정 맥락에 맞는 테스트가 가능하여 보다 정확한 평가가 이뤄집니다.

* **종합 분석 도구**: 테스트한 모든 모델의 세부 성능 지표, 실행 시간, 비용 분석을 확인할 수 있습니다. 이로써 모델의 일반적인 평판이나 이론적 능력에 기대지 않고 데이터 기반으로 의사결정을 내릴 수 있습니다.

* **팀 협업**: 팀 내에서 테스트 결과와 모델 성능 데이터를 공유할 수 있어, 협업적 의사결정과 프로젝트 전반에서 일관된 모델 선택 전략을 수립할 수 있습니다.

지금 [app.crewai.com](https://app.crewai.com)에서 시작하세요!

<Info>
  Enterprise 플랫폼은 모델 선택을 단순한 추측이 아닌 데이터 기반 프로세스로 혁신하여, 본 가이드의 원칙을 실제 사용 사례와 요구 사항에 맞게 검증할 수 있도록 해줍니다.
</Info>

<CardGroup cols={2}>
  <Card title="작업 중심 선택" icon="bullseye">
    이론적 능력이나 일반적인 평판이 아니라, 작업에 실제로 필요한 것에 따라 모델을 선택하세요.
  </Card>

<Card title="능력 일치" icon="puzzle-piece">
    최적의 성능을 위해 모델의 강점을 agent의 역할 및 책임과 일치시키세요.
  </Card>

<Card title="전략적 일관성" icon="link">
    관련 구성 요소와 워크플로 전반에 걸쳐 일관된 모델 선택 전략을 유지하세요.
  </Card>

<Card title="실용적 테스트" icon="flask">
    벤치마크에만 의존하지 말고 실제 사용을 통해 선택을 검증하세요.
  </Card>

<Card title="반복적 개선" icon="arrow-up">
    단순하게 시작하고 실제 성능과 필요에 따라 최적화하세요.
  </Card>

<Card title="운영적 균형" icon="scale-balanced">
    성능 요구사항과 비용 및 복잡성 제약을 균형 있게 맞추세요.
  </Card>
</CardGroup>

<Check>
  기억하세요: 최고의 LLM 선택이란 운영상의 제약 내에서 일관되게 필요한 결과를 제공하는 모델입니다. 먼저 요구사항을 정확히 이해하는 데 집중한 후, 그에 가장 잘 맞는 모델을 선택하세요.
</Check>

## 현재 모델 현황 (2025년 6월)

<Warning>
  **특정 시점의 스냅샷**: 아래 모델 순위는 2025년 6월 기준으로, [LMSys Arena](https://arena.lmsys.org/), [Artificial Analysis](https://artificialanalysis.ai/) 및 기타 주요 벤치마크에서 집계된 최신 리더보드 결과입니다. LLM의 성능, 가용성, 가격은 빠르게 변동됩니다. 항상 귀하의 특정 사용 사례와 데이터로 직접 평가를 진행하시기 바랍니다.
</Warning>

아래 표는 다양한 카테고리에서 현재 최고의 성능을 보이는 대표적인 모델들을 보여주며, CrewAI 에이전트에 적합한 모델 선택에 대한 가이드를 제공합니다:

<Note>
  이 표와 지표는 각 카테고리에서 선별된 주요 모델을 보여주기 위한 것으로, 전체를 포괄하지 않습니다. 여기 소개되지 않은 훌륭한 모델들도 많이 존재합니다. 이 표의 목적은 완전한 목록을 제공하는 것이 아니라, 어떤 능력을 갖춘 모델을 찾아야 하는지 예시를 제시하는 것입니다.
</Note>

<Tabs>
  <Tab title="Reasoning & Planning">
    **매니저 LLM 및 복잡한 분석에 최적**

| Model                      | Intelligence Score | Cost (\$/M tokens) | Speed | Best Use in CrewAI              |
    | :------------------------- | :----------------- | :----------------- | :---- | :------------------------------ |
    | **o3**                     | 70                 | \$17.50            | 빠름    | 복잡한 멀티 에이전트 조정용 매니저 LLM         |
    | **Gemini 2.5 Pro**         | 69                 | \$3.44             | 빠름    | 전략 기획 에이전트, 연구 조정               |
    | **DeepSeek R1**            | 68                 | \$0.96             | 보통    | 예산을 중시하는 팀을 위한 비용 효율적 reasoning |
    | **Claude 4 Sonnet**        | 53                 | \$6.00             | 빠름    | 세밀한 이해가 필요한 분석 에이전트             |
    | **Qwen3 235B (Reasoning)** | 62                 | \$2.63             | 보통    | reasoning 작업을 위한 오픈소스 대안        |

이 모델들은 다단계 reasoning에 뛰어나며, 전략을 개발하거나 다른 에이전트를 조정하거나 복잡한 정보를 분석해야 하는 에이전트에 이상적입니다.
  </Tab>

<Tab title="Coding & Technical">
    **개발 및 도구 중심의 워크플로우에 최적**

| Model                 | Coding Performance | Tool Use Score | Cost (\$/M tokens) | Best Use in CrewAI                       |
    | :-------------------- | :----------------- | :------------- | :----------------- | :--------------------------------------- |
    | **Claude 4 Sonnet**   | 우수                 | 72.7%          | \$6.00             | 주력 코딩 에이전트, 기술 문서화                       |
    | **Claude 4 Opus**     | 우수                 | 72.5%          | \$30.00            | 복잡한 소프트웨어 아키텍처, 코드 리뷰                    |
    | **DeepSeek V3**       | 매우 좋음              | 높음             | \$0.48             | 일상적 개발을 위한 비용 효율적 코딩                     |
    | **Qwen2.5 Coder 32B** | 매우 좋음              | 보통             | \$0.15             | 예산 친화적 코딩 에이전트                           |
    | **Llama 3.1 405B**    | 좋음                 | 81.1%          | \$3.50             | 도구 사용이 많은 워크플로우를 위한 function calling LLM |

이 모델들은 코드 생성, 디버깅, 기술 문제 해결에 최적화되어 있어, 개발 중심 팀에 적합합니다.
  </Tab>

<Tab title="Speed & Efficiency">
    **대량 처리 및 실시간 애플리케이션에 최적**

| Model                   | Speed (tokens/s) | Latency (TTFT) | Cost (\$/M tokens) | Best Use in CrewAI |
    | :---------------------- | :--------------- | :------------- | :----------------- | :----------------- |
    | **Llama 4 Scout**       | 2,600            | 0.33s          | \$0.27             | 대량 처리 에이전트         |
    | **Gemini 2.5 Flash**    | 376              | 0.30s          | \$0.26             | 실시간 응답 에이전트        |
    | **DeepSeek R1 Distill** | 383              | 가변             | \$0.04             | 비용 최적화 고속 처리       |
    | **Llama 3.3 70B**       | 2,500            | 0.52s          | \$0.60             | 균형 잡힌 속도와 기능       |
    | **Nova Micro**          | 높음               | 0.30s          | \$0.04             | 단순·빠른 작업 처리        |

이 모델들은 속도와 효율을 우선시하며, 일상적 운영 또는 신속한 응답이 필요한 에이전트에게 최적입니다. **팁**: 이러한 모델을 Groq와 같은 빠른 추론 제공자와 함께 사용하면 더욱 우수한 성능을 낼 수 있습니다. 특히 Llama와 같은 오픈소스 모델에 적합합니다.
  </Tab>

<Tab title="Balanced Performance">
    **일반 팀을 위한 최고의 다목적 모델**

| Model                 | Overall Score | Versatility | Cost (\$/M tokens) | Best Use in CrewAI    |
    | :-------------------- | :------------ | :---------- | :----------------- | :-------------------- |
    | **GPT-4.1**           | 53            | 탁월          | \$3.50             | 범용 팀 LLM              |
    | **Claude 3.7 Sonnet** | 48            | 매우 좋음       | \$6.00             | 균형 잡힌 reasoning 및 창의력 |
    | **Gemini 2.0 Flash**  | 48            | 좋음          | \$0.17             | 비용 효율적인 범용 용도         |
    | **Llama 4 Maverick**  | 51            | 좋음          | \$0.37             | 오픈소스 범용 모델            |
    | **Qwen3 32B**         | 44            | 좋음          | \$1.23             | 예산 친화적 다재다능성          |

이 모델들은 다양한 측면에서 우수한 성능을 제공하며, 여러 작업이 혼합된 팀에 적합합니다.
  </Tab>
</Tabs>

### 현재 모델을 위한 선택 프레임워크

<AccordionGroup>
  <Accordion title="High-Performance Crews" icon="rocket">
    **퍼포먼스가 우선 순위일 때**: 매니저 LLM 또는 중요한 에이전트 역할에는 **o3**, **Gemini 2.5 Pro**, **Claude 4 Sonnet**과 같은 최상위 모델을 사용하세요. 이 모델들은 복잡한 reasoning 및 coordination에 탁월하지만 비용이 더 높습니다.

**전략**: 프리미엄 모델이 전략적 사고를 담당하고, 효율적인 모델이 일상적 operation을 처리하는 멀티 모델 접근법을 구현하세요.
  </Accordion>

<Accordion title="Cost-Conscious Crews" icon="dollar-sign">
    **예산이 주요 제약일 때**: **DeepSeek R1**, **Llama 4 Scout**, **Gemini 2.0 Flash**와 같은 모델에 집중하세요. 이 모델들은 훨씬 낮은 비용으로 강력한 퍼포먼스를 제공합니다.

**전략**: 대부분의 에이전트에는 비용 효율이 높은 모델을 사용하고, 가장 중요한 decision-making 역할에만 프리미엄 모델을 남겨두세요.
  </Accordion>

<Accordion title="Specialized Workflows" icon="screwdriver-wrench">
    **특정 도메인 전문성이 필요할 때**: 주된 사용 사례에 최적화된 모델을 선택하세요. 코딩에는 **Claude 4** 시리즈, 리서치에는 **Gemini 2.5 Pro**, function calling에는 **Llama 405B**를 사용하세요.

**전략**: crew의 주요 기능에 따라 모델을 선택해, 핵심 역량이 모델의 강점과 일치하도록 하세요.
  </Accordion>

<Accordion title="Enterprise & Privacy" icon="shield">
    **데이터 민감한 operation의 경우**: 로컬에서 배포 가능하면서 경쟁력 있는 퍼포먼스를 유지하는 오픈 소스 모델인 **Llama 4** 시리즈, **DeepSeek V3**, **Qwen3** 등을 고려하세요.

**전략**: 사설 인프라에 오픈 소스 모델을 배포하여, 데이터 제어를 위해 필요한 퍼포먼스 손실을 감수하세요.
  </Accordion>
</AccordionGroup>

### 모델 선택을 위한 주요 고려사항

* **성능 동향**: 현재 시장에서는 reasoning에 초점을 맞춘 모델(o3, Gemini 2.5 Pro)과 균형 잡힌 모델(Claude 4, GPT-4.1) 간의 치열한 경쟁이 있습니다. DeepSeek R1과 같은 특화 모델은 우수한 비용-성능 비율을 제공합니다.

* **속도와 지능 간의 트레이드오프**: Llama 4 Scout와 같은 모델은 합리적인 지능을 유지하면서도 빠른 속도(2,600 tokens/s)를 우선시하며, o3와 같은 모델은 속도와 가격을 희생해 reasoning 능력을 극대화합니다.

* **오픈 소스의 실효성**: 오픈 소스와 독점 모델 간의 격차가 계속 좁혀지고 있으며, Llama 4 Maverick 및 DeepSeek V3와 같은 모델이 매력적인 가격대에서 경쟁력 있는 성능을 제공합니다. 특히 빠른 추론을 제공하는 업체들은 오픈 소스 모델과 함께 탁월한 속도-비용 비율을 제공하는 경우가 많아 독점 모델보다 우위에 서기도 합니다.

<Info>
  **테스트는 필수입니다**: 리더보드 순위는 일반적인 가이드라인을 제공하지만, 귀하의 특정 사용 사례, 프롬프트 스타일, 평가 기준에 따라 결과가 달라질 수 있습니다. 최종 결정을 내리기 전에 반드시 실제 작업과 데이터로 후보 모델을 테스트해 보세요.
</Info>

<Steps>
  <Step title="검증된 모델로 시작하기">
    여러 차원에서 우수한 성능을 제공하며 실제 환경에서 광범위하게 검증된 **GPT-4.1**, **Claude 3.7 Sonnet**, **Gemini 2.0 Flash**와 같은 잘 알려진 모델부터 시작하십시오.
  </Step>

<Step title="특화된 요구 사항 식별">
    crew에 코드 작성, reasoning, 속도 등 특정 요구가 있는지 확인하고, 이러한 요구에 부합하는 **Claude 4 Sonnet**(개발용) 또는 **o3**(복잡한 분석용)과 같은 특화 모델을 고려하십시오. 속도가 중요한 애플리케이션의 경우, 모델 선택과 더불어 **Groq**와 같은 빠른 추론 제공자를 고려할 수 있습니다.
  </Step>

<Step title="다중 모델 전략 구현">
    각 에이전트의 역할에 따라 다양한 모델을 사용하세요. 관리자와 복잡한 작업에는 고성능 모델을, 일상적 운영에는 효율적인 모델을 적용합니다.
  </Step>

<Step title="모니터링 및 최적화">
    사용 사례와 관련된 성능 지표를 추적하고, 새로운 모델이 출시되거나 가격이 변동될 때 모델 선택을 조정할 준비를 하십시오.
  </Step>
</Steps>

**Examples:**

Example 1 (unknown):
```unknown
**정렬 체크리스트:**

* ✅ **역할 특이성**: 명확한 도메인과 책임
* ✅ **LLM 적합도**: 모델의 강점이 역할 요구사항과 일치
* ✅ **백스토리 깊이**: LLM이 활용할 수 있는 도메인 맥락 제공
* ✅ **도구 통합**: 도구가 agent의 특수 기능을 지원
* ✅ **파라미터 튜닝**: 온도 및 설정이 역할에 최적화

핵심은 모든 구성 선택이 LLM 선택 전략을 강화하여 성능을 극대화하면서 비용을 최적화하는 agent를 만드는 것입니다.

## 실무 구현 체크리스트

전략적 프레임워크를 반복하는 대신, CrewAI에서 LLM 선택 결정을 실행하는 데 사용할 수 있는 전술적 체크리스트를 제공합니다:

<Steps>
  <Step title="현재 셋업 점검" icon="clipboard-check">
    **검토할 사항:**

    * 모든 agent가 기본적으로 동일한 LLM을 사용하고 있습니까?
    * 어떤 agent가 가장 복잡한 reasoning 작업을 처리합니까?
    * 어떤 agent가 주로 데이터 처리 또는 포매팅을 담당합니까?
    * 도구에 크게 의존하는 agent가 있습니까?

    **Action**: 현재 agent 역할을 문서화하고 최적화 기회를 식별하세요.
  </Step>

  <Step title="Crew 수준 전략 구현" icon="users-gear">
    **기본값 설정:**
```

Example 2 (unknown):
```unknown
**Action**: 개별 agent 최적화 전에 crew의 기본 LLM을 설정하세요.
  </Step>

  <Step title="고임팩트 agent 최적화" icon="star">
    **핵심 agent 식별 및 업그레이드:**
```

Example 3 (unknown):
```unknown
**Action**: 복잡도의 80%를 처리하는 agent 20%를 업그레이드하세요.
  </Step>

  <Step title="엔터프라이즈 테스트로 검증" icon="test-tube">
    **agent를 프로덕션에 배포한 후:**

    * [CrewAI AMP platform](https://app.crewai.com)을 활용하여 모델 선택을 A/B 테스트하세요
    * 실제 입력으로 여러 번 반복 테스트하여 일관성과 성능을 측정하세요
    * 최적화된 셋업 전반의 비용과 성능을 비교하세요
    * 팀과 결과를 공유하여 협업 의사결정을 지원하세요

    **Action**: 테스트 플랫폼을 활용해 추측이 아닌 데이터 기반 검증을 실행하세요.
  </Step>
</Steps>

### 다양한 모델 유형을 사용할 시기

<Tabs>
  <Tab title="Reasoning Models">
    reasoning 모델은 진정한 다단계 논리적 사고, 전략적 계획 수립, 또는 체계적인 분석이 필요한 고수준의 의사결정이 요구되는 작업에서 필수적입니다. 이러한 모델은 문제를 구성 요소로 분해하고 체계적으로 분석해야 할 때, 단순한 패턴 매칭이나 지시 사항 이행만으로는 해결할 수 없는 경우에 뛰어난 성능을 발휘합니다.

    예를 들어, 비즈니스 전략 개발, 여러 출처에서 인사이트를 도출해야 하는 복잡한 데이터 분석, 각 단계가 이전 분석을 기반으로 해야 하는 다단계 문제 해결, 다양한 변수 및 이들의 상호작용을 고려해야 하는 전략적 계획 수립 업무에 reasoning 모델을 고려해 보세요.

    그러나 reasoning 모델은 일반적으로 더 높은 비용과 느린 응답 시간을 수반하므로, 복잡한 사고가 필요한 작업에서 실질적인 가치를 제공할 때에만 사용하는 것이 좋으며, 복잡한 reasoning이 필요하지 않은 단순한 작업에는 권장되지 않습니다.
  </Tab>

  <Tab title="Creative Models">
    creative 모델은 콘텐츠 생성이 주요 결과물이고 콘텐츠의 품질, 스타일, 참여도가 성공에 직접적으로 영향을 미칠 때 유용합니다. 이 모델들은 글의 질과 스타일이 매우 중요하거나, 창의적인 아이디어 창출 또는 브레인스토밍이 필요하거나, 브랜드의 목소리와 톤이 중요한 경우에 특히 뛰어납니다.

    creative 모델은 블로그 포스트 작성 및 기사 생성, 독자를 끌어들이고 설득해야 하는 마케팅 카피, 창의적인 스토리텔링 및 내러티브 개발, 목소리와 톤이 중요한 브랜드 커뮤니케이션 등에 적합합니다. 이 모델은 일반 목적 모델보다 뉘앙스와 맥락을 더 잘 이해할 수 있습니다.

    creative 모델은 정밀성과 사실적 정확성이 스타일이나 참여도보다 더 중요한 기술적 또는 분석적 작업에는 덜 적합할 수 있습니다. 결과물의 창의적·의사소통적 측면이 성공의 주요 요인일 때 사용하는 것이 가장 좋습니다.
  </Tab>

  <Tab title="Efficient Models">
    efficient 모델은 빠른 속도와 비용 최적화가 우선순위인 고빈도, 반복 작업에 이상적입니다. 이러한 모델은 작업의 매개변수가 명확하고 잘 정의되어 있으며, 복잡한 reasoning이나 창의적인 능력이 필요하지 않을 때 가장 잘 작동합니다.

    efficient 모델은 데이터 처리 및 변환 작업, 단순한 서식 지정 및 정리 작업, 정밀성이 중요하고 복잡함보다는 정확성이 필요한 함수 호출 및 도구 사용, 1회 작업당 비용이 중대한 고볼륨 작업에 적합합니다.

    efficient 모델에서는 해당 모델의 역량이 작업 요구 사항과 일치하는지 확인하는 것이 핵심입니다. 다양한 반복 작업을 효과적으로 처리할 수 있지만, 뉘앙스 이해, 복잡한 reasoning, 고도화된 콘텐츠 생성이 필요한 작업에서는 한계가 있을 수 있습니다.
  </Tab>

  <Tab title="Open Source Models">
    open source 모델은 예산 제약이 크거나, 데이터 프라이버시 요구 사항이 있거나, 맞춤화가 중요하거나, 운영·컴플라이언스 목적상 로컬 배포가 필요한 경우에 매력적인 선택이 됩니다.

    예를 들어, 데이터 프라이버시가 최우선인 사내 도구, 외부 API를 사용할 수 없는 프라이버시 민감형 애플리케이션, 토큰 단위 가격이 부담스러운 비용 최적화 배포, 모델 수정 또는 파인튜닝이 필요한 상황에서 open source 모델을 고려해 보세요.

    단, open source 모델은 효과적으로 배포하고 유지하기 위해 더 많은 기술 전문성이 요구됩니다. 인프라, 기술적 오버헤드, 지속적인 유지보수를 포함한 전체 소유 비용을 종합적으로 평가해야 합니다.
  </Tab>
</Tabs>

## CrewAI 모델 선택에서 흔히 발생하는 실수

<AccordionGroup>
  <Accordion title="‘하나의 모델로 모두 해결’ 함정" icon="triangle-exclamation">
    **문제점**: 각 agent의 역할과 책임과 상관없이 모든 agent에 동일한 LLM을 사용하는 것. 대부분 기본적으로 선택되는 접근 방식이지만, 최적의 결과가 나오지 않는 경우가 많음.

    **실제 예시**: 전략 기획 매니저와 데이터 추출 agent 모두에게 GPT-4o를 사용하는 경우. 매니저는 높은 추론 성능이 필요해 프리미엄 모델이 적합하나, 데이터 추출 업무는 저렴한 GPT-4o-mini만으로도 충분한 성능을 낼 수 있음.

    **CrewAI 솔루션**: agent별 LLM 설정을 활용해, agent의 역할에 맞는 모델 역량을 매칭:
```

Example 4 (unknown):
```unknown
</Accordion>

  <Accordion title="Crew 수준과 Agent 수준 LLM 계층 혼동" icon="shuffle">
    **문제점**: CrewAI의 LLM 계층 구조(crew LLM, manager LLM, agent LLM)를 이해하지 못해 설정이 충돌하거나 적절히 조정되지 않음.

    **실제 예시**: crew에는 Claude를, agent에는 GPT 모델을 설정해 일관성 없는 동작과 불필요한 모델 전환 오버헤드가 발생하는 경우.

    **CrewAI 솔루션**: LLM 계층 구조를 전략적으로 설계:
```

---

## OpenAI Agent Adapter

**URL:** llms-txt#openai-agent-adapter

link_finder_agent = OpenAIAgentAdapter(
    role="Link Finder",
    goal="Find the most relevant and high-quality resources for coding tasks.",
    backstory="You are a research specialist with a talent for finding the most helpful resources. You're skilled at using search tools to discover documentation, tutorials, and examples that directly address the user's coding needs.",
    tools=[SerperDevTool()],
    allow_delegation=False,
    verbose=True,
)

---

## Exemplo: Agente de Documentação Técnica

**URL:** llms-txt#exemplo:-agente-de-documentação-técnica

**Contents:**
- Checklist Prático de Implementação
  - Quando Usar Tipos Diferentes de Modelos
- Armadilhas Comuns na Seleção de Modelos CrewAI
- Estratégia de Teste e Iteração
  - Validação de Modelos em Nível Enterprise
- Resumo dos Princípios-Chave
- Panorama Atual dos Modelos (Junho/2025)
  - Principais Modelos por Categoria
  - Framework de Seleção para Modelos Atuais
  - Considerações-Chave na Seleção de Modelos

tech_writer = Agent(
    role="API Documentation Specialist",
    goal="Create comprehensive, developer-friendly API documentation",
    backstory="""
    You're a technical writer with 8+ years documenting REST APIs, GraphQL endpoints,
    and SDK integration guides. You've worked with developer tools companies and
    understand what developers need: clear examples, comprehensive error handling,
    and practical use cases. You prioritize accuracy and usability over marketing fluff.
    """,
    llm=LLM(
        model="claude-3-5-sonnet",
        temperature=0.1
    ),
    tools=[code_analyzer_tool, api_scanner_tool],
    verbose=True
)
python  theme={null}
    # Comece com um padrão confiável para a crew
    default_crew_llm = LLM(model="gpt-4o-mini")  # Base econômica

crew = Crew(
        agents=[...],
        tasks=[...],
        memory=True
    )
    python  theme={null}
    # Agentes gerenciadores ou de coordenação
    manager_agent = Agent(
        role="Project Manager",
        llm=LLM(model="gemini-2.5-flash-preview-05-20"),
        # ... demais configs
    )

# Agentes criativos ou customer-facing
    content_agent = Agent(
        role="Content Creator",
        llm=LLM(model="claude-3-5-sonnet"),
        # ... demais configs
    )
    python  theme={null}
    # Agente estratégico recebe modelo premium
    manager = Agent(role="Strategy Manager", llm=LLM(model="gpt-4o"))

# Agente de processamento recebe modelo eficiente
    processor = Agent(role="Data Processor", llm=LLM(model="gpt-4o-mini"))
    python  theme={null}
    crew = Crew(
        agents=[agent1, agent2],
        tasks=[task1, task2],
        manager_llm=LLM(model="gpt-4o"),
        process=Process.hierarchical
    )

# Agentes herdam o LLM da crew, salvo sobrescrita
    agent1 = Agent(llm=LLM(model="claude-3-5-sonnet"))
    python  theme={null}
    # Para agentes com muitas ferramentas
    tool_agent = Agent(
        role="API Integration Specialist",
        tools=[search_tool, api_tool, data_tool],
        llm=LLM(model="gpt-4o"),
        # OU
        llm=LLM(model="claude-3-5-sonnet")
    )
    python  theme={null}
    # Comece assim
    crew = Crew(agents=[...], tasks=[...], llm=LLM(model="gpt-4o-mini"))

# Teste a performance e só depois otimize agentes específicos
    # Use testes Enterprise para validar melhorias
    ```
  </Accordion>

<Accordion title="Ignorar Limites de Contexto e Memória" icon="brain">
    **O problema**: Não considerar como janela de contexto dos modelos interage com memória e compartilhamento de contexto entre agentes CrewAI.

**Exemplo real**: Usar modelo de contexto curto para agentes que precisam manter histórico ao longo de múltiplas iterações ou equipes com comunicação extensiva agent-to-agent.

**Solução CrewAI**: Alinhe capacidades de contexto ao padrão de comunicação da crew.
  </Accordion>
</AccordionGroup>

## Estratégia de Teste e Iteração

<Steps>
  <Step title="Comece Simples" icon="play">
    Comece com modelos de uso geral, confiáveis e amplamente suportados. Isso estabelece base estável para entender necessidades e expectativas de desempenho antes de otimizar para demandas especializadas.
  </Step>

<Step title="Meça o que Importa" icon="chart-line">
    Desenvolva métricas alinhadas ao seu caso de uso e metas de negócio, não apenas benchmarks gerais. Foque na mensuração de resultados relevantes ao seu sucesso.
  </Step>

<Step title="Itere Baseado em Resultados" icon="arrows-rotate">
    Faça mudanças baseadas no desempenho observado no seu contexto, não apenas considerações teóricas ou recomendações genéricas. O desempenho prático costuma ser bem diferente dos benchmarks.
  </Step>

<Step title="Considere o Custo Total" icon="calculator">
    Avalie todo custo de operação, incluindo modelo, tempo de desenvolvimento, manutenção e complexidade. O modelo mais barato por token pode não ser o mais econômico ao considerar todos os fatores.
  </Step>
</Steps>

<Tip>
  Foque em entender seus requisitos primeiro, e então escolha modelos que melhor correspondam a essas necessidades. O melhor LLM é aquele que consistentemente entrega os resultados esperados dentro das suas restrições.
</Tip>

### Validação de Modelos em Nível Enterprise

Para equipes sérias sobre otimização, a **plataforma CrewAI AMP** oferece testes sofisticados que vão além do CLI. Ela permite avaliação completa para decisões orientadas por dados na estratégia de LLM.

<Frame>
    <img src="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=08580e93186b6563adca8b75da805805" alt="Enterprise Testing Interface" data-og-width="2238" width="2238" data-og-height="1700" height="1700" data-path="images/enterprise/enterprise-testing.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=280&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=d7ced6158ec4dd0b5a9928edcfc4a38d 280w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=560&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=0bf0f3d7110c1ac4ae4139a80e28b9c2 560w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=840&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=27a38bf115431233bfb9849629dc125e 840w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=1100&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=5d73aad5c4af3e62a82044f80add8ac1 1100w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=1650&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=a91a7198392462683371a28e799943a0 1650w, https://mintcdn.com/crewai/5SZbe87tsCWZY09V/images/enterprise/enterprise-testing.png?w=2500&fit=max&auto=format&n=5SZbe87tsCWZY09V&q=85&s=78aaf8869525c5633d5f06655cc46c5e 2500w" />
</Frame>

**Funcionalidades Avançadas de Teste:**

* **Comparação Multi-Modelo**: Teste diversos LLMs simultaneamente nas mesmas tarefas e entradas. Compare desempenho entre GPT-4o, Claude, Llama, Groq, Cerebras, e outros líderes em paralelo para identificar a melhor opção para você.

* **Rigor Estatístico**: Configure múltiplas iterações com inputs consistentes para medir confiabilidade e variação no desempenho. Assim, identifica modelos que performam bem e de modo consistente.

* **Validação no Mundo Real**: Use os inputs e cenários reais da sua crew, e não apenas benchmarks sintéticos. A plataforma permite testar no contexto da sua indústria, empresa e casos de uso.

* **Analytics Completo**: Acesse métricas detalhadas de desempenho, tempos de execução e análise de custos para todos os modelos testados. Decisões baseadas em dados reais, não apenas reputação.

* **Colaboração em Equipe**: Compartilhe resultados e análises com seu time, favorecendo decisões coletivas e estratégias alinhadas.

Acesse [app.crewai.com](https://app.crewai.com) para começar!

<Info>
  A plataforma Enterprise transforma a seleção de modelos de um "palpite" para um processo orientado por dados, permitindo validar os princípios deste guia com seus próprios casos de uso.
</Info>

## Resumo dos Princípios-Chave

<CardGroup cols={2}>
  <Card title="Seleção Orientada à Tarefa" icon="bullseye">
    Escolha os modelos pelo que sua tarefa realmente requer, não por reputação ou capacidades teóricas.
  </Card>

<Card title="Combinação de Capacidades" icon="puzzle-piece">
    Alinhe forças do modelo a papéis e responsabilidades dos agentes para melhor desempenho.
  </Card>

<Card title="Consistência Estratégica" icon="link">
    Mantenha uma estratégia coerente de seleção de modelos em fluxos e componentes relacionados.
  </Card>

<Card title="Testes Práticos" icon="flask">
    Valide escolhas em uso real, não apenas em benchmarks.
  </Card>

<Card title="Iteração Contínua" icon="arrow-up">
    Comece simples e otimize com base na performance e necessidade práticas.
  </Card>

<Card title="Equilíbrio Operacional" icon="scale-balanced">
    Equilibre performance requerida, custo e complexidade.
  </Card>
</CardGroup>

<Check>
  Lembre-se: o melhor LLM é o que entrega consistentemente os resultados de que você precisa dentro de suas restrições. Conheça seu requisito primeiro, depois selecione o modelo mais adequado.
</Check>

## Panorama Atual dos Modelos (Junho/2025)

<Warning>
  **Retrato do Momento**: Os rankings a seguir representam o estado da arte em Junho de 2025, compilados do [LMSys Arena](https://arena.lmsys.org/), [Artificial Analysis](https://artificialanalysis.ai/) e outros benchmarks líderes. Performance, disponibilidade e preço mudam rapidamente. Sempre valide com seus dados e casos reais.
</Warning>

### Principais Modelos por Categoria

As tabelas abaixo mostram uma amostra dos modelos de maior destaque em cada categoria, junto de orientação sobre aplicação em agentes CrewAI:

<Note>
  Estas tabelas exibem apenas alguns modelos líderes por categoria. Existem muitos outros excelentes. O objetivo é ilustrar exemplos de capacidades buscadas em vez de apresentar um catálogo completo.
</Note>

<Tabs>
  <Tab title="Raciocínio & Planejamento">
    **Melhores para LLMs Manager e Análises Complexas**

| Modelo                     | Score de Inteligência | Custo (\$/M tokens) | Velocidade | Melhor Uso em CrewAI                                         |
    | :------------------------- | :-------------------- | :------------------ | :--------- | :----------------------------------------------------------- |
    | **o3**                     | 70                    | \$17.50             | Rápido     | Manager LLM para coordenação multi-agente                    |
    | **Gemini 2.5 Pro**         | 69                    | \$3.44              | Rápido     | Agentes de planejamento estratégico, coordenação de pesquisa |
    | **DeepSeek R1**            | 68                    | \$0.96              | Moderada   | Raciocínio com bom custo-benefício                           |
    | **Claude 4 Sonnet**        | 53                    | \$6.00              | Rápido     | Agentes de análise que precisam de nuance                    |
    | **Qwen3 235B (Reasoning)** | 62                    | \$2.63              | Moderada   | Alternativa open source para raciocínio                      |

Esses modelos se destacam em raciocínio multi-etapas e são ideais para agentes que desenvolvem estratégias, coordenam outros agentes ou analisam informações complexas.
  </Tab>

<Tab title="Codificação & Técnica">
    **Melhores para Desenvolvimento e Workflows com Ferramentas**

| Modelo                | Performance em Coding | Tool Use Score | Custo (\$/M tokens) | Melhor Uso em CrewAI                                             |
    | :-------------------- | :-------------------- | :------------- | :------------------ | :--------------------------------------------------------------- |
    | **Claude 4 Sonnet**   | Excelente             | 72.7%          | \$6.00              | Agente principal de código/documentação técnica                  |
    | **Claude 4 Opus**     | Excelente             | 72.5%          | \$30.00             | Arquitetura complexa, code review                                |
    | **DeepSeek V3**       | Muito bom             | Alto           | \$0.48              | Coding econômico para desenvolvimentos rotineiros                |
    | **Qwen2.5 Coder 32B** | Muito bom             | Médio          | \$0.15              | Agente de código econômico                                       |
    | **Llama 3.1 405B**    | Bom                   | 81.1%          | \$3.50              | LLM para function calling em workflows intensivos em ferramentas |

Otimizados para geração de código, debugging e solução técnica, ideais para equipes de desenvolvimento.
  </Tab>

<Tab title="Velocidade & Eficiência">
    **Melhores para Operações em Massa e Aplicações em Tempo Real**

| Modelo                  | Velocidade (tokens/s) | Latência (TTFT) | Custo (\$/M tokens) | Melhor Uso em CrewAI                     |
    | :---------------------- | :-------------------- | :-------------- | :------------------ | :--------------------------------------- |
    | **Llama 4 Scout**       | 2.600                 | 0.33s           | \$0.27              | Agentes de processamento de alto volume  |
    | **Gemini 2.5 Flash**    | 376                   | 0.30s           | \$0.26              | Agentes de resposta em tempo real        |
    | **DeepSeek R1 Distill** | 383                   | Variável        | \$0.04              | Processamento rápido de baixo custo      |
    | **Llama 3.3 70B**       | 2.500                 | 0.52s           | \$0.60              | Equilíbrio entre velocidade e capacidade |
    | **Nova Micro**          | Alto                  | 0.30s           | \$0.04              | Execução rápida de tarefas simples       |

Priorizam velocidade e eficiência, perfeitos para agentes em operações de rotina ou resposta ágil. **Dica:** Usar provedores de inference rápidos como Groq potencializa open source como Llama.
  </Tab>

<Tab title="Performance Equilibrada">
    **Melhores Modelos Coringa para Crews Diversos**

| Modelo                | Score Global | Versatilidade | Custo (\$/M tokens) | Melhor Uso em CrewAI                  |
    | :-------------------- | :----------- | :------------ | :------------------ | :------------------------------------ |
    | **GPT-4.1**           | 53           | Excelente     | \$3.50              | LLM generalista para equipes variadas |
    | **Claude 3.7 Sonnet** | 48           | Muito boa     | \$6.00              | Raciocínio e criatividade balanceados |
    | **Gemini 2.0 Flash**  | 48           | Boa           | \$0.17              | Generalista de bom custo benefício    |
    | **Llama 4 Maverick**  | 51           | Boa           | \$0.37              | Open source para usos gerais          |
    | **Qwen3 32B**         | 44           | Boa           | \$1.23              | Versatilidade econômica               |

Oferecem bom desempenho geral, adequados para crews com demandas amplas.
  </Tab>
</Tabs>

### Framework de Seleção para Modelos Atuais

<AccordionGroup>
  <Accordion title="Crews de Alta Performance" icon="rocket">
    **Priorizando performance**: Use modelos topo de linha como **o3**, **Gemini 2.5 Pro** ou **Claude 4 Sonnet** para managers e agentes críticos. Excelentes em raciocínio e coordenação, porém mais caros.

**Estratégia**: Implemente abordagem multi-modelo, reservando premium para raciocínio estratégico e eficientes para operações rotineiras.
  </Accordion>

<Accordion title="Crews de Baixo Custo" icon="dollar-sign">
    **Foco no orçamento**: Foque em modelos como **DeepSeek R1**, **Llama 4 Scout** ou **Gemini 2.0 Flash**, que trazem ótimo desempenho com investimento reduzido.

**Estratégia**: Use modelos econômicos para maioria dos agentes, reservando premium apenas para funções críticas.
  </Accordion>

<Accordion title="Workflows Especializados" icon="screwdriver-wrench">
    **Para expertise específica**: Escolha modelos otimizados para seu principal caso de uso: **Claude 4** em código, **Gemini 2.5 Pro** em pesquisa, **Llama 405B** em function calling.

**Estratégia**: Selecione conforme a principal função da crew, garantindo alinhamento de capacidade e modelo.
  </Accordion>

<Accordion title="Empresa & Privacidade" icon="shield">
    **Para operações sensíveis**: Avalie modelos open source como **Llama 4** series, **DeepSeek V3** ou **Qwen3** para deployment privado, mantendo performance competitiva.

**Estratégia**: Use open source em infraestrutura própria e aceite possíveis trade-offs por controle dos dados.
  </Accordion>
</AccordionGroup>

### Considerações-Chave na Seleção de Modelos

* **Tendências de Performance**: O cenário atual mostra competição forte entre modelos de raciocínio (o3, Gemini 2.5 Pro) e equilibrados (Claude 4, GPT-4.1). Modelos como DeepSeek R1 entregam excelente custo/performance.
* **Trade-off Velocidade x Inteligência**: Modelos como Llama 4 Scout priorizam velocidade (2.600 tokens/s) e inteligência razoável, enquanto outros como o3 maximizam raciocínio em detrimento de velocidade/preço.
* **Viabilidade Open Source**: A distância entre open source e proprietários diminui a cada mês, com Llama 4 Maverick e DeepSeek V3 entregando performance competitiva a preços atrativos. Inferência rápida via Groq maximiza custo-benefício nesses casos.

<Info>
  **Testes são essenciais**: Rankings servem de orientação geral, mas seu caso de uso, prompt e critério podem gerar resultados distintos. Sempre teste modelos candidatos com suas tarefas e dados reais antes de decidir.
</Info>

### Estratégia Prática de Implementação

<Steps>
  <Step title="Comece por Modelos Validados">
    Inicie com opções consagradas como **GPT-4.1**, **Claude 3.7 Sonnet** ou **Gemini 2.0 Flash**, que oferecem bom desempenho e ampla validação.
  </Step>

<Step title="Identifique Demandas Especializadas">
    Descubra se sua crew possui requisitos específicos (código, raciocínio, velocidade) que justifiquem modelos como **Claude 4 Sonnet** para desenvolvimento ou **o3** para análise. Para aplicações críticas em velocidade, considere Groq aliado à seleção do modelo.
  </Step>

<Step title="Implemente Estratégia Multi-Modelo">
    Use modelos diferentes para agentes distintos conforme o papel. Modelos de alta capacidade para managers e tarefas complexas, eficientes para rotinas.
  </Step>

<Step title="Monitore e Otimize">
    Acompanhe métricas relevantes ao seu caso e esteja pronto para ajustar modelos conforme lançamentos ou mudanças de preços.
  </Step>
</Steps>

**Examples:**

Example 1 (unknown):
```unknown
**Checklist de Alinhamento:**

* ✅ **Função Específica**: Domínio e responsabilidades claras
* ✅ **Correspondência do LLM**: Forças do modelo conectadas à função
* ✅ **Profundidade do Backstory**: Contexto de domínio disponível pro modelo
* ✅ **Integração de Ferramentas**: Ferramentas fortalecem a função do agente
* ✅ **Ajuste de Parâmetros**: Temperatura e configs otimizadas para a função

O segredo é criar agentes onde cada configuração reforça sua estratégia de escolha do LLM, maximizando rendimento e otimizando custos.

## Checklist Prático de Implementação

Em vez de repetir o framework estratégico, segue um checklist tático para implementar as decisões de seleção de LLM em CrewAI:

<Steps>
  <Step title="Audite Sua Configuração Atual" icon="clipboard-check">
    **O que analisar:**

    * Todos os agentes usam o mesmo LLM por padrão?
    * Quais agentes lidam com tarefas mais complexas?
    * Quais agentes só processam ou formatam dados?
    * Algum agente depende fortemente de ferramentas?

    **Ação**: Documente funções dos agentes e identifique oportunidades de otimização.
  </Step>

  <Step title="Implemente Estratégia no Nível da Crew" icon="users-gear">
    **Defina sua Base:**
```

Example 2 (unknown):
```unknown
**Ação**: Defina o LLM padrão da crew antes de otimizar agentes individuais.
  </Step>

  <Step title="Otimize Agentes de Maior Impacto" icon="star">
    **Identifique e Aprimore Agentes-Chave:**
```

Example 3 (unknown):
```unknown
**Ação**: Faça upgrade dos 20% dos agentes que tratam 80% da complexidade.
  </Step>

  <Step title="Valide com Testes Empresariais" icon="test-tube">
    **Após colocar os agentes em produção:**

    * Use [CrewAI AMP platform](https://app.crewai.com) para testar seleções de modelo A/B
    * Execute múltiplas iterações com inputs reais para medir consistência e performance
    * Compare custo vs performance na configuração otimizada
    * Compartilhe resultados com o time para tomada coletiva de decisão

    **Ação**: Substitua achismos por validação com dados reais usando a plataforma de testes.
  </Step>
</Steps>

### Quando Usar Tipos Diferentes de Modelos

<Tabs>
  <Tab title="Modelos de Raciocínio">
    Modelos de raciocínio tornam-se essenciais quando tarefas exigem pensamento lógico genuíno em múltiplas etapas, planejamento estratégico ou decisões complexas beneficiadas por análise sistemática. Brilham na decomposição de problemas e análise estruturada, não no simples seguimento de padrões.

    Considere-os para desenvolvimento de estratégias de negócios, análise de dados combinados de múltiplas fontes, resolução de problemas dependente de etapas sucessivas e planejamento estratégico envolvendo múltiplas variáveis.

    Entretanto, esses modelos são mais caros e lentos, devendo ser reservados para tarefas onde suas capacidades agregam valor real — evite usá-los apenas para operações simples.
  </Tab>

  <Tab title="Modelos Criativos">
    Modelos criativos são valiosos quando a principal entrega é geração de conteúdo e a qualidade, estilo e engajamento desse conteúdo impactam o sucesso. Se destacam quando redação e estilo importam, ideação criativa é necessária, ou voz de marca é fundamental.

    Use-os em redação de posts, criação de artigos, textos de marketing com viés persuasivo, storytelling e comunicações da marca. Costumam captar nuances e contexto melhor do que generalistas.

    Podem ser menos adequados para tarefas técnicas ou analíticas, onde precisão supera criatividade. Use-os quando aspectos comunicativos são fatores críticos de sucesso.
  </Tab>

  <Tab title="Modelos Eficientes">
    Modelos eficientes são ideais para operações frequentes e rotineiras, onde velocidade e custo são prioridade. Trabalham melhor em tarefas com parâmetros bem definidos, sem necessidade de raciocínio avançado ou criatividade.

    Considere-os para processamento e transformação de dados, formatação simples, chamadas de funções (function calling) e operações em alto volume onde custo importa mais.

    O ponto crítico é verificar adequação à tarefa. Funcionam para muitos fluxos rotineiros, mas podem falhar se a tarefa exigir compreensão técnica ou raciocínio.
  </Tab>

  <Tab title="Modelos Open Source">
    Modelos open source são atraentes quando há restrição orçamentária, necessidade de privacidade, personalização especial ou exigência de deployment local.

    Considere para ferramentas internas de empresas, aplicações sensíveis, projetos onde não é possível usar APIs externas, casos com orçamento apertado ou requisitos de customização.

    Mas lembre-se: exigem mais expertise, manutenção e investimentos em infraestrutura. Avalie o custo total da operação ao avaliar esses modelos.
  </Tab>
</Tabs>

## Armadilhas Comuns na Seleção de Modelos CrewAI

<AccordionGroup>
  <Accordion title="A Armadilha do 'Um Modelo Serve para Tudo'" icon="triangle-exclamation">
    **O problema**: Usar o mesmo LLM para todos os agentes, independentemente das funções. Prática padrão, mas raramente ótima.

    **Exemplo real**: Usar GPT-4o tanto para planejamento estratégico quanto para extração simples de dados. O manager precisa do raciocínio premium, mas o extrator poderia usar o GPT-4o-mini, muito mais barato.

    **Solução CrewAI**: Configure modelos específicos por agente:
```

Example 4 (unknown):
```unknown
</Accordion>

  <Accordion title="Ignorar Hierarquia de LLM entre Crew e Agente" icon="shuffle">
    **O problema**: Não entender como funciona a hierarquia LLM da CrewAI — configurações conflitam entre crew, manager e agentes.

    **Exemplo real**: Configurar crew com Claude, mas agentes com GPT, gerando comportamento inconsistente e trocas desnecessárias.

    **Solução CrewAI**: Planeje a hierarquia estrategicamente:
```

---
