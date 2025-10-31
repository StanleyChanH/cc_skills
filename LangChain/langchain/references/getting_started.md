# Langchain - Getting Started

**Pages:** 2

---

## 快速入门

**URL:** https://langchain-doc.cn/v1/python/langchain/quickstart.html

快速入门本快速入门将带您从简单设置到构建一个功能完整的 AI 代理，仅需几分钟。构建基本代理首先创建一个简单的代理，它可以回答问题并调用工具。该代理将使用 Claude Sonnet 4.5 作为语言模型，一个基本的天气函数作为工具，以及一个简单的提示来指导其行为。from langchain.agents import create_agent


def get_weather(city: str) -> str:
    """获取指定城市的天气。"""
    return f"{city}总是阳光明媚！"

agent = create_agent(
    model="anthropic:claude-sonnet-4-5",
    tools=[get_weather],
    system_prompt="你是一个乐于助人的助手",
)

# 运行代理
agent.invoke(
    {"messages": [{"role": "user", "content": "旧金山的天气怎么样"}]}
)注意 对于此示例，您需要设置一个 Claude (Anthropic) 账户并获取 API 密钥。然后在终端中设置 ANTHROPIC_API_KEY 环境变量。构建真实世界的代理接下来，构建一个实用的天气预报代理，展示关键的生产概念：详细的系统提示 以获得更好的代理行为创建工具 与外部数据集成模型配置 以确保响应一致性结构化输出 以获得可预测的结果对话记忆 以实现类似聊天的交互创建并运行代理 构建一个功能完整的代理让我们逐步完成每一步：定义系统提示系统提示定义了代理的角色和行为。保持其具体且可操作：SYSTEM_PROMPT = """你是一位擅长用双关语表达的专家天气预报员。

你可以使用两个工具：

- get_weather_for_location：用于获取特定地点的天气
- get_user_location：用于获取用户的位置

如果用户询问天气，请确保你知道具体位置。如果从问题中可以判断他们指的是自己所在的位置，请使用 get_user_location 工具来查找他们的位置。"""创建工具工具 允许模型通过调用您定义的函数与外部系统交互。 工具可以依赖于运行时上下文，也可以与代理记忆交互。请注意下面的 get_user_location 工具如何使用运行时上下文：from dataclasses import dataclass
from langchain.tools import tool, ToolRuntime

@tool
def get_weather_for_location(city: str) -> str:
    """获取指定城市的天气。"""
    return f"{city}总是阳光明媚！"

@dataclass
class Context:
    """自定义运行时上下文模式。"""
    user_id: str

@tool
def get_user_location(runtime: ToolRuntime[Context]) -> str:
    """根据用户 ID 获取用户信息。"""
    user_id = runtime.context.user_id
    return "Florida" if user_id == "1" else "SF"提示 工具应有良好的文档说明：其名称、描述和参数名称将成为模型提示的一部分。 LangChain 的 @tool 装饰器 会添加元数据，并通过 ToolRuntime 参数启用运行时注入。配置模型使用适合您用例的语言模型和参数进行设置：from langchain.chat_models import init_chat_model

model = init_chat_model(
    "anthropic:claude-sonnet-4-5",
    temperature=0.5,
    timeout=10,
    max_tokens=1000
)定义响应格式（可选）如果需要代理响应符合特定模式，请定义结构化响应格式。from dataclasses import dataclass

# 这里使用 dataclass，但也支持 Pydantic 模型。
@dataclass
class ResponseFormat:
    """代理的响应模式。"""
    # 带双关语的回应（始终必需）
    punny_response: str
    # 天气的任何有趣信息（如果有）
    weather_conditions: str | None = None添加记忆向代理添加记忆，以在多次交互中保持状态。这允许代理记住之前的对话和上下文。from langgraph.checkpoint.memory import InMemorySaver

checkpointer = InMemorySaver()注意 在生产环境中，请使用持久化的检查点保存到数据库。 详见 添加和管理记忆。创建并运行代理现在将所有组件组装成代理并运行它！agent = create_agent(
    model=model,
    system_prompt=SYSTEM_PROMPT,
    tools=[get_user_location, get_weather_for_location],
    context_schema=Context,
    response_format=ResponseFormat,
    checkpointer=checkpointer
)

# `thread_id` 是给定对话的唯一标识符。
config = {"configurable": {"thread_id": "1"}}

response = agent.invoke(
    {"messages": [{"role": "user", "content": "外面的天气怎么样？"}]},
    config=config,
    context=Context(user_id="1")
)

print(response['structured_response'])
# ResponseFormat(
#     punny_response="佛罗里达今天依然是'阳光灿烂'的一天！阳光正在播放'rey-dio'热门歌曲！我得说，这是进行'solar-bration'的完美天气！如果你希望下雨，恐怕这个想法已经'被冲走'了——预报仍然'清晰地'灿烂！",
#     weather_conditions="佛罗里达总是阳光明媚！"
# )

# 注意，我们可以使用相同的 `thread_id` 继续对话。
response = agent.invoke(
    {"messages": [{"role": "user", "content": "谢谢！"}]},
    config=config,
    context=Context(user_id="1")
)

print(response['structured_response'])
# ResponseFormat(
#     punny_response="你真是'雷'厉风行地欢迎！帮助你保持'当前'天气总是'轻而易举'。我只是'云'游四方，等待随时'淋浴'你更多预报。祝你在佛罗里达的阳光下度过'sun-sational'的一天！",
#     weather_conditions=None
# )完整示例代码from dataclasses import dataclass

from langchain.agents import create_agent
from langchain.chat_models import init_chat_model
from langchain.tools import tool, ToolRuntime
from langgraph.checkpoint.memory import InMemorySaver


# 定义系统提示
SYSTEM_PROMPT = """你是一位擅长用双关语表达的专家天气预报员。

你可以使用两个工具：

- get_weather_for_location：用于获取特定地点的天气
- get_user_location：用于获取用户的位置

如果用户询问天气，请确保你知道具体位置。如果从问题中可以判断他们指的是自己所在的位置，请使用 get_user_location 工具来查找他们的位置。"""

# 定义上下文模式
@dataclass
class Context:
    """自定义运行时上下文模式。"""
    user_id: str

# 定义工具
@tool
def get_weather_for_location(city: str) -> str:
    """获取指定城市的天气。"""
    return f"{city}总是阳光明媚！"

@tool
def get_user_location(runtime: ToolRuntime[Context]) -> str:
    """根据用户 ID 获取用户信息。"""
    user_id = runtime.context.user_id
    return "Florida" if user_id == "1" else "SF"

# 配置模型
model = init_chat_model(
    "anthropic:claude-sonnet-4-5",
    temperature=0
)

# 定义响应格式
@dataclass
class ResponseFormat:
    """代理的响应模式。"""
    # 带双关语的回应（始终必需）
    punny_response: str
    # 天气的任何有趣信息（如果有）
    weather_conditions: str | None = None

# 设置记忆
checkpointer = InMemorySaver()

# 创建代理
agent = create_agent(
    model=model,
    system_prompt=SYSTEM_PROMPT,
    tools=[get_user_location, get_weather_for_location],
    context_schema=Context,
    response_format=ResponseFormat,
    checkpointer=checkpointer
)

# 运行代理
# `thread_id` 是给定对话的唯一标识符。
config = {"configurable": {"thread_id": "1"}}

response = agent.invoke(
    {"messages": [{"role": "user", "content": "外面的天气怎么样？"}]},
    config=config,
    context=Context(user_id="1")
)

print(response['structured_response'])
# ResponseFormat(
#     punny_response="佛罗里达今天依然是'阳光灿烂'的一天！阳光正在播放'rey-dio'热门歌曲！我得说，这是进行'solar-bration'的完美天气！如果你希望下雨，恐怕这个想法已经'被冲走'了——预报仍然'清晰地'灿烂！",
#     weather_conditions="佛罗里达总是阳光明媚！"
# )

# 注意，我们可以使用相同的 `thread_id` 继续对话。
response = agent.invoke(
    {"messages": [{"role": "user", "content": "谢谢！"}]},
    config=config,
    context=Context(user_id="1")
)

print(response['structured_response'])
# ResponseFormat(
#     punny_response="你真是'雷'厉风行地欢迎！帮助你保持'当前'天气总是'轻而易举'。我只是'云'游四方，等待随时'淋浴'你更多预报。祝你在佛罗里达的阳光下度过'sun-sational'的一天！",
#     weather_conditions=None
# )恭喜！您现在拥有一个 AI 代理，它可以：理解上下文 并记住对话智能使用多个工具提供结构化响应，格式一致通过上下文处理用户特定信息跨交互维护对话状态最近更新2025/10/25 19:51上一页安装下一页理念

---

## LangChain 概述

**URL:** https://langchain-doc.cn/v1/python/langchain/overview.html

**Contents:**
- LangChain 概述
- 安装
  - Python
  - JavaScript / TypeScript
- 创建代理
  - Python 示例
  - JavaScript / TypeScript 示例
- 核心优势

有关完整的更新内容和升级指南，请查看 发布说明 和 迁移指南。 如果遇到问题或有反馈，请 提交 issue 以帮助我们改进。 若需查看 v0.x 文档，请访问 存档网站。

LangChain 是最快速入门构建基于 LLM 的智能代理和应用的方法。不到 10 行代码，你就可以连接 OpenAI、Anthropic、Google 以及更多提供商（详见）。LangChain 提供预构建的代理架构和模型集成，帮助你快速启动并无缝将 LLM 集成到你的应用中。

如果你想快速构建代理和自主应用，建议使用 LangChain。 当你有更复杂的需求，需要结合确定性与智能工作流、高度自定义以及精确延迟控制时，可使用 LangGraph，这是我们提供的低级代理编排框架和运行时。

LangChain agents 构建在 LangGraph 之上，提供持久化执行、流式处理、人类参与、数据持久化等功能。基础使用无需了解 LangGraph。

**Examples:**

Example 1 (bash):
```bash
pip install -U langchain
```

Example 2 (unknown):
```unknown
pip install -U langchain
```

Example 3 (bash):
```bash
pip install -U langchain
```

Example 4 (bash):
```bash
uv add langchain
```

---
