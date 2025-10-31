# Langchain - Core Components

**Pages:** 3

---

## 工具

**URL:** https://langchain-doc.cn/v1/python/langchain/tools.html

工具许多 AI 应用程序通过自然语言与用户交互。然而，某些用例要求模型使用结构化输入直接与外部系统（例如 API、数据库 或 文件系统）对接。工具 是 代理（agents） 调用来执行操作的组件。它们通过允许模型通过定义明确的输入和输出与世界交互来扩展模型的功能。工具封装了一个可调用的函数及其输入架构（schema）。这些可以传递给兼容的 聊天模型（chat models），让模型决定是否以及使用什么参数来调用工具。在这些场景中，工具调用 使模型能够生成符合指定输入架构的请求。服务器端工具使用 (Server-side tool use)某些聊天模型（例如 OpenAI、Anthropic 和 Gemini）具有 内置工具，这些工具在服务器端执行，例如网络搜索和代码解释器。请参阅 提供商概览（provider overview） 了解如何使用您的特定聊天模型访问这些工具。创建工具 (Create tools)基本工具定义 (Basic tool definition)创建工具最简单的方法是使用 @tool 装饰器。默认情况下，函数的 文档字符串（docstring）会成为工具的描述，帮助模型理解何时使用它：from langchain.tools import tool

@tool
def search_database(query: str, limit: int = 10) -> str:
    """Search the customer database for records matching the query.

    Args:
        query: Search terms to look for
        limit: Maximum number of results to return
    """
    return f"Found {limit} results for '{query}'"类型提示 是必需的，因为它们定义了工具的输入架构。文档字符串应该信息丰富且简洁，以帮助模型理解工具的用途。自定义工具属性 (Customize tool properties)自定义工具名称 (Custom tool name)默认情况下，工具名称来自函数名称。当您需要更具描述性的名称时，可以覆盖它：@tool("web_search")  # Custom name
def search(query: str) -> str:
    """Search the web for information."""
    return f"Results for: {query}"

print(search.name)  # web_search自定义工具描述 (Custom tool description)覆盖自动生成的工具描述，以提供更清晰的模型指导：@tool("calculator", description="Performs arithmetic calculations. Use this for any math problems.")
def calc(expression: str) -> str:
    """Evaluate mathematical expressions."""
    return str(eval(expression))高级架构定义 (Advanced schema definition)使用 Pydantic 模型 或 JSON 架构 定义复杂的输入：from pydantic import BaseModel, Field
from typing import Literal

class WeatherInput(BaseModel):
    """Input for weather queries."""
    location: str = Field(description="City name or coordinates")
    units: Literal["celsius", "fahrenheit"] = Field(
        default="celsius",
        description="Temperature unit preference"
    )
    include_forecast: bool = Field(
        default=False,
        description="Include 5-day forecast"
    )

@tool(args_schema=WeatherInput)
def get_weather(location: str, units: str = "celsius", include_forecast: bool = False) -> str:
    """Get current weather and optional forecast."""
    temp = 22 if units == "celsius" else 72
    result = f"Current weather in {location}: {temp} degrees {units[0].upper()}"
    if include_forecast:
        result += "\nNext 5 days: Sunny"
    return resultweather_schema = {
    "type": "object",
    "properties": {
        "location": {"type": "string"},
        "units": {"type": "string"},
        "include_forecast": {"type": "boolean"}
    },
    "required": ["location", "units", "include_forecast"]
}

@tool(args_schema=weather_schema)
def get_weather(location: str, units: str = "celsius", include_forecast: bool = False) -> str:
    """Get current weather and optional forecast."""
    temp = 22 if units == "celsius" else 72
    result = f"Current weather in {location}: {temp} degrees {units[0].upper()}"
    if include_forecast:
        result += "\nNext 5 days: Sunny"
    return result访问上下文 (Accessing Context)为什么这很重要： 当工具可以访问代理状态、运行时上下文和长期记忆时，它们的功能最强大。这使得工具能够做出上下文感知的决策、个性化响应并在对话中维护信息。工具可以通过 ToolRuntime 参数访问运行时信息，该参数提供：State（状态） - 流经执行的可变数据（消息、计数器、自定义字段）Context（上下文） - 不可变的配置，如用户 ID、会话详细信息或特定于应用程序的配置Store（存储） - 跨对话的持久长期记忆Stream Writer（流写入器） - 在工具执行时流式传输自定义更新Config（配置） - 执行的 RunnableConfigTool Call ID（工具调用 ID） - 当前工具调用的 IDToolRuntime使用 ToolRuntime 在一个参数中访问所有运行时信息。只需将 runtime: ToolRuntime 添加到您的工具签名中，它就会被自动注入，而不会暴露给 LLM。ToolRuntime: 一个统一的参数，为工具提供对状态、上下文、存储、流式传输、配置和工具调用 ID 的访问。这取代了使用单独的 InjectedState、InjectedStore、get_runtime 和 InjectedToolCallId 注释的旧模式。访问状态：工具可以使用 ToolRuntime 访问当前的图状态：from langchain.tools import tool, ToolRuntime

# Access the current conversation state
@tool
def summarize_conversation(
    runtime: ToolRuntime
) -> str:
    """Summarize the conversation so far."""
    messages = runtime.state["messages"]

    human_msgs = sum(1 for m in messages if m.__class__.__name__ == "HumanMessage")
    ai_msgs = sum(1 for m in messages if m.__class__.__name__ == "AIMessage")
    tool_msgs = sum(1 for m in messages if m.__class__.__name__ == "ToolMessage")

    return f"Conversation has {human_msgs} user messages, {ai_msgs} AI responses, and {tool_msgs} tool results"

# Access custom state fields
@tool
def get_user_preference(
    pref_name: str,
    runtime: ToolRuntime  # ToolRuntime parameter is not visible to the model
) -> str:
    """Get a user preference value."""
    preferences = runtime.state.get("user_preferences", {})
    return preferences.get(pref_name, "Not set")tool_runtime 参数对模型是隐藏的。对于上面的示例，模型在工具架构中只看到 pref_name - tool_runtime 不包含在请求中。更新状态：使用 Command 来更新代理的状态或控制图的执行流程：from langgraph.types import Command
from langchain.messages import RemoveMessage
from langgraph.graph.message import REMOVE_ALL_MESSAGES
from langchain.tools import tool, ToolRuntime

# Update the conversation history by removing all messages
@tool
def clear_conversation() -> Command:
    """Clear the conversation history."""

    return Command(
        update={
            "messages": [RemoveMessage(id=REMOVE_ALL_MESSAGES)],
        }
    )

# Update the user_name in the agent state
@tool
def update_user_name(
    new_name: str,
    runtime: ToolRuntime
) -> Command:
    """Update the user's name."""
    return Command(update={"user_name": new_name})上下文 (Context)通过 runtime.context 访问不可变的配置和上下文数据，例如用户 ID、会话详细信息或特定于应用程序的配置。工具可以通过 ToolRuntime 访问运行时上下文：from dataclasses import dataclass
from langchain_openai import ChatOpenAI
from langchain.agents import create_agent
from langchain.tools import tool, ToolRuntime


USER_DATABASE = {
    "user123": {
        "name": "Alice Johnson",
        "account_type": "Premium",
        "balance": 5000,
        "email": "alice@example.com"
    },
    "user456": {
        "name": "Bob Smith",
        "account_type": "Standard",
        "balance": 1200,
        "email": "bob@example.com"
    }
}

@dataclass
class UserContext:
    user_id: str

@tool
def get_account_info(runtime: ToolRuntime[UserContext]) -> str:
    """Get the current user's account information."""
    user_id = runtime.context.user_id

    if user_id in USER_DATABASE:
        user = USER_DATABASE[user_id]
        return f"Account holder: {user['name']}\nType: {user['account_type']}\nBalance: ${user['balance']}"
    return "User not found"

model = ChatOpenAI(model="gpt-4o")
agent = create_agent(
    model,
    tools=[get_account_info],
    context_schema=UserContext,
    system_prompt="You are a financial assistant."
)

result = agent.invoke(
    {"messages": [{"role": "user", "content": "What's my current balance?"}]},
    context=UserContext(user_id="user123")
)内存（存储）(Memory (Store))使用 存储（store） 访问跨对话的持久数据。通过 runtime.store 访问存储，它允许您保存和检索特定于用户或特定于应用程序的数据。工具可以通过 ToolRuntime 访问和更新存储：from typing import Any
from langgraph.store.memory import InMemoryStore
from langchain.agents import create_agent
from langchain.tools import tool, ToolRuntime


# Access memory
@tool
def get_user_info(user_id: str, runtime: ToolRuntime) -> str:
    """Look up user info."""
    store = runtime.store
    user_info = store.get(("users",), user_id)
    return str(user_info.value) if user_info else "Unknown user"

# Update memory
@tool
def save_user_info(user_id: str, user_info: dict[str, Any], runtime: ToolRuntime) -> str:
    """Save user info."""
    store = runtime.store
    store.put(("users",), user_id, user_info)
    return "Successfully saved user info."

store = InMemoryStore()
agent = create_agent(
    model,
    tools=[get_user_info, save_user_info],
    store=store
)

# First session: save user info
agent.invoke({
    "messages": [{"role": "user", "content": "Save the following user: userid: abc123, name: Foo, age: 25, email: foo@langchain.dev"}]
})

# Second session: get user info
agent.invoke({
    "messages": [{"role": "user", "content": "Get user info for user with id 'abc123'"}]
})
# Here is the user info for user with ID "abc123":
# - Name: Foo
# - Age: 25
# - Email: foo@langchain.dev流写入器 (Stream Writer)使用 runtime.stream_writer 在工具执行时流式传输自定义更新。这对于向用户提供有关工具正在做什么的实时反馈很有用。from langchain.tools import tool, ToolRuntime

@tool
def get_weather(city: str, runtime: ToolRuntime) -> str:
    """Get weather for a given city."""
    writer = runtime.stream_writer

    # Stream custom updates as the tool executes
    writer(f"Looking up data for city: {city}")
    writer(f"Acquired data for city: {city}")

    return f"It's always sunny in {city}!"如果您在工具中使用 runtime.stream_writer，则必须在 LangGraph 执行上下文中调用该工具。有关更多详细信息，请参阅 流式传输（Streaming）。最近更新2025/10/25 19:51上一页消息下一页短期记忆

---

## 模型

**URL:** https://langchain-doc.cn/v1/python/langchain/models.html

模型大语言模型（LLMs） 是强大的 AI 工具，能够像人类一样理解和生成文本。它们用途广泛，可用于撰写内容、翻译语言、总结信息和回答问题，而无需针对每项任务进行专门训练。除了文本生成之外，许多模型还支持：工具调用 - 调用外部工具（如数据库查询或 API 调用）并将结果用于响应中。结构化输出 - 模型的响应被限制为遵循定义的格式。多模态 - 处理和返回非文本数据，如图像、音频和视频。推理 - 模型执行多步推理以得出结论。模型是 代理 的推理引擎。它们驱动代理的决策过程，决定调用哪些工具、如何解释结果以及何时提供最终答案。您选择的模型的质量和能力直接影响代理的可靠性和性能。不同模型在不同任务上表现出色——有些更擅长遵循复杂指令，有些更擅长结构化推理，有些支持更大的上下文窗口以处理更多信息。LangChain 的标准模型接口为您提供对众多不同提供商集成的访问，这使得实验和切换模型以找到最适合您用例的模型变得非常容易。信息 有关特定提供商的集成信息和功能，请参阅提供商的集成页面。基本用法模型可以通过两种方式使用：与代理一起使用 - 创建代理时可动态指定模型。独立使用 - 模型可直接调用（在代理循环之外），用于文本生成、分类或提取等任务，而无需代理框架。同一模型接口在两种上下文中均适用，这为您提供了从简单开始并根据需要扩展到更复杂基于代理的工作流程的灵活性。初始化模型在 LangChain 中开始使用独立模型的最简单方法是使用 init_chat_model 从您选择的提供商初始化一个模型（以下示例）：OpenAI👉 阅读 OpenAI 聊天模型集成文档pip install -U "langchain[openai]"import os
from langchain.chat_models import init_chat_model

os.environ["OPENAI_API_KEY"] = "sk-..."

model = init_chat_model("openai:gpt-4.1")import os
from langchain_openai import ChatOpenAI

os.environ["OPENAI_API_KEY"] = "sk-..."

model = ChatOpenAI(model="gpt-4.1")Anthropic👉 阅读 Anthropic 聊天模型集成文档pip install -U "langchain[anthropic]"import os
from langchain.chat_models import init_chat_model

os.environ["ANTHROPIC_API_KEY"] = "sk-..."

model = init_chat_model("anthropic:claude-sonnet-4-5")import os
from langchain_anthropic import ChatAnthropic

os.environ["ANTHROPIC_API_KEY"] = "sk-..."

model = ChatAnthropic(model="claude-sonnet-4-5")Azure👉 阅读 Azure 聊天模型集成文档pip install -U "langchain[openai]"import os
from langchain.chat_models import init_chat_model

os.environ["AZURE_OPENAI_API_KEY"] = "..."
os.environ["AZURE_OPENAI_ENDPOINT"] = "..."
os.environ["OPENAI_API_VERSION"] = "2025-03-01-preview"

model = init_chat_model(
    "azure_openai:gpt-4.1",
    azure_deployment=os.environ["AZURE_OPENAI_DEPLOYMENT_NAME"],
)import os
from langchain_openai import AzureChatOpenAI

os.environ["AZURE_OPENAI_API_KEY"] = "..."
os.environ["AZURE_OPENAI_ENDPOINT"] = "..."
os.environ["OPENAI_API_VERSION"] = "2025-03-01-preview"

model = AzureChatOpenAI(
    model="gpt-4.1",
    azure_deployment=os.environ["AZURE_OPENAI_DEPLOYMENT_NAME"]
)Google Gemini👉 阅读 Google GenAI 聊天模型集成文档pip install -U "langchain[google-genai]"import os
from langchain.chat_models import init_chat_model

os.environ["GOOGLE_API_KEY"] = "..."

model = init_chat_model("google_genai:gemini-2.5-flash-lite")import os
from langchain_google_genai import ChatGoogleGenerativeAI

os.environ["GOOGLE_API_KEY"] = "..."

model = ChatGoogleGenerativeAI(model="gemini-2.5-flash-lite")AWS Bedrock👉 阅读 AWS Bedrock 聊天模型集成文档pip install -U "langchain[aws]"from langchain.chat_models import init_chat_model

# 请按照此处的步骤配置您的凭据：
# https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html

model = init_chat_model(
    "anthropic.claude-3-5-sonnet-20240620-v1:0",
    model_provider="bedrock_converse",
)from langchain_aws import ChatBedrock

model = ChatBedrock(model="anthropic.claude-3-5-sonnet-20240620-v1:0")response = model.invoke("为什么鹦鹉会说话？")有关更多详细信息，包括如何传递模型参数，请参阅 init_chat_model。关键方法方法说明Invoke模型接受消息作为输入，并在生成完整响应后输出消息。Stream调用模型，但实时流式传输生成的输出。Batch将多个请求批量发送给模型，以实现更高效的处理。信息 除了聊天模型之外，LangChain 还支持其他相关技术，如嵌入模型和向量存储。详情请参阅集成页面。参数聊天模型接受可用于配置其行为的一组参数。支持的参数集因模型和提供商而异，但标准参数包括：参数类型必填说明modelstring是您想使用的特定模型的名称或标识符。api_keystring否用于向模型提供商进行身份验证的密钥。通常在注册访问模型时颁发。通常通过设置环境变量访问。temperaturenumber否控制模型输出的随机性。值越高，响应越具创造性；值越低，响应越确定性。timeoutnumber否在取消请求之前等待模型响应的最大时间（秒）。max_tokensnumber否限制响应中的令牌总数，有效控制输出长度。max_retriesnumber否如果因网络超时或速率限制等问题而失败，系统将重新发送请求的最大尝试次数。使用 init_chat_model，将这些参数作为内联 **kwargs 传递：model = init_chat_model(
    "anthropic:claude-sonnet-4-5",
    # 传递给模型的 Kwargs：
    temperature=0.7,
    timeout=30,
    max_tokens=1000,
)信息 每个聊天模型集成可能具有用于控制提供商特定功能的额外参数。例如，ChatOpenAI 具有 use_responses_api 以决定是否使用 OpenAI Responses 或 Completions API。 要查找给定聊天模型支持的所有参数，请转到聊天模型集成页面。调用必须调用聊天模型以生成输出。主要有三种调用方法，每种方法适用于不同的用例。Invoke调用模型的最直接方法是使用 invoke() 传入单个消息或消息列表。response = model.invoke("为什么鹦鹉有五颜六色的羽毛？")
print(response)可以向模型提供消息列表以表示对话历史。每条消息都有一个角色，模型用它来指示对话中谁发送了消息。有关角色、类型和内容的更多详细信息，请参阅消息指南。from langchain.messages import HumanMessage, AIMessage, SystemMessage

conversation = [
    {"role": "system", "content": "你是一个将英语翻译成法语的有用助手。"},
    {"role": "user", "content": "翻译：我喜欢编程。"},
    {"role": "assistant", "content": "J'adore la programmation."},
    {"role": "user", "content": "翻译：我喜欢构建应用程序。"}
]

response = model.invoke(conversation)
print(response)  # AIMessage("J'adore créer des applications.")from langchain_core.messages import HumanMessage, AIMessage, SystemMessage

conversation = [
    SystemMessage("你是一个将英语翻译成法语的有用助手。"),
    HumanMessage("翻译：我喜欢编程。"),
    AIMessage("J'adore la programmation。"),
    HumanMessage("翻译：我喜欢构建应用程序。")
]

response = model.invoke(conversation)
print(response)  # AIMessage("J'adore créer des applications。")Stream大多数模型可以在生成时流式传输其输出内容。通过逐步显示输出，流式传输显著改善了用户体验，尤其是对于较长的响应。调用 stream() 返回一个迭代器，它在生成时逐块产生输出。您可以使用循环实时处理每个块：for chunk in model.stream("为什么鹦鹉有五颜六色的羽毛？"):
    print(chunk.text, end="|", flush=True)for chunk in model.stream("天空是什么颜色？"):
    for block in chunk.content_blocks:
        if block["type"] == "reasoning" and (reasoning := block.get("reasoning")):
            print(f"推理：{reasoning}")
        elif block["type"] == "tool_call_chunk":
            print(f"工具调用块：{block}")
        elif block["type"] == "text":
            print(block["text"])
        else:
            ...与返回单个 AIMessage 的 invoke() 不同，stream() 返回多个 AIMessageChunk 对象，每个对象包含一部分输出文本。重要的是，流中的每个块都设计为通过求和聚合成完整消息：full = None  # None | AIMessageChunk
for chunk in model.stream("天空是什么颜色？"):
    full = chunk if full is None else full + chunk
    print(full.text)

# 天空
# 天空是
# 天空通常
# 天空通常是蓝色
# ...

print(full.content_blocks)
# [{"type": "text", "text": "天空通常是蓝色..."}]生成的消息可以与使用 invoke() 生成的消息相同处理——例如，它可以聚合成消息历史并作为对话上下文传递回模型。警告 流式传输仅在程序的所有步骤都知道如何处理块流时才有效。例如，无法流式传输的应用程序是需要先将整个输出存储在内存中才能处理的情况。高级流式传输主题“自动流式传输”聊天模型LangChain 通过在某些情况下自动启用流式传输模式来简化从聊天模型进行流式传输，即使您未显式调用流式传输方法。这在您使用非流式传输的 invoke 方法但仍希望流式传输整个应用程序（包括聊天模型的中间结果）时特别有用。例如，在 LangGraph 代理 中，您可以在节点内调用 model.invoke()，但如果在流式传输模式下运行，LangChain 将自动委托给流式传输。工作原理当您 invoke() 一个聊天模型时，如果 LangChain 检测到您正在尝试流式传输整个应用程序，它将自动切换到内部流式传输模式。对于使用 invoke 的代码，结果是相同的；然而，在聊天模型流式传输时，LangChain 将负责在 LangChain 的回调系统中调用 on_llm_new_token 事件。回调事件允许 LangGraph 的 stream() 和 astream_events() 实时显示聊天模型的输出。流式传输事件LangChain 聊天模型还可以使用 astream_events() 流式传输语义事件。这简化了基于事件类型和其他元数据的过滤，并在后台聚合完整消息。请参阅以下示例。async for event in model.astream_events("你好"):

    if event["event"] == "on_chat_model_start":
        print(f"输入：{event['data']['input']}")

    elif event["event"] == "on_chat_model_stream":
        print(f"令牌：{event['data']['chunk'].text}")

    elif event["event"] == "on_chat_model_end":
        print(f"完整消息：{event['data']['output'].text}")

    else:
        pass输入：你好
令牌：你
令牌：好
令牌：！
令牌：我
令牌：能
令牌：如
...
完整消息：你好！今天我能如何帮助您？提示 请参阅 astream_events() 参考，了解事件类型和其他详细信息。Batch将一组独立请求批量处理给模型可以显著提高性能并降低成本，因为处理可以并行进行：responses = model.batch([
    "为什么鹦鹉有五颜六色的羽毛？",
    "飞机是如何飞行的？",
    "什么是量子计算？"
])
for response in responses:
    print(response)注意 本节描述的是聊天模型方法 batch()，它在客户端并行化模型调用。 它不同于推理提供商支持的批量 API，例如 OpenAI 或 Anthropic。默认情况下，batch() 仅返回整个批次的最终输出。如果您希望在每个单独输入完成生成时接收输出，可以使用 batch_as_completed() 流式传输结果：for response in model.batch_as_completed([
    "为什么鹦鹉有五颜六色的羽毛？",
    "飞机是如何飞行的？",
    "什么是量子计算？"
]):
    print(response)注意 使用 batch_as_completed() 时，结果可能无序到达。每个结果包括输入索引，以便根据需要匹配和重建原始顺序。提示 在使用 batch() 或 batch_as_completed() 处理大量输入时，您可能希望控制最大并行调用数。这可以通过在 RunnableConfig 字典中设置 max_concurrency 属性来完成。model.batch(
    list_of_inputs,
    config={
        'max_concurrency': 5,  # 限制为 5 个并行调用
    }
)有关批处理的更多详细信息，请参阅参考。工具调用模型可以请求调用执行任务的工具，例如从数据库获取数据、搜索网络或运行代码。工具是以下内容的配对：架构，包括工具的名称、描述和/或参数定义（通常是 JSON 架构）要执行的函数或协程注意 您可能会听到“函数调用”一词。我们将此与“工具调用”互换使用。要使您定义的工具可供模型使用，您必须使用 bind_tools() 绑定它们。在后续调用中，模型可以根据需要选择调用任何绑定的工具。一些模型提供商提供内置工具，可通过模型或调用参数启用（例如 ChatOpenAI、ChatAnthropic）。请查看相应的提供商参考以了解详细信息。提示 有关创建工具的详细信息和其他选项，请参阅工具指南。from langchain.tools import tool

@tool
def get_weather(location: str) -> str:
    """获取某个位置的天气。"""
    return f"{location} 天气晴朗。"

model_with_tools = model.bind_tools([get_weather])  # [!code highlight]

response = model_with_tools.invoke("波士顿的天气怎么样？")
for tool_call in response.tool_calls:
    # 查看模型发出的工具调用
    print(f"工具：{tool_call['name']}")
    print(f"参数：{tool_call['args']}")绑定用户定义的工具时，模型的响应包括请求执行工具。当将模型与代理分开使用时，您需要执行请求的操作并将结果返回给模型以用于后续推理。请注意，当使用代理时，代理循环将为您处理工具执行循环。下面展示了一些使用工具调用的常见方法。工具执行循环当模型返回工具调用时，您需要执行工具并将结果传递回模型。这会创建一个对话循环，模型可以使用工具结果生成其最终响应。LangChain 包含代理抽象来为您处理此协调。以下是一个简单示例：# 将（可能多个）工具绑定到模型
model_with_tools = model.bind_tools([get_weather])

# 步骤 1：模型生成工具调用
messages = [{"role": "user", "content": "波士顿的天气怎么样？"}]
ai_msg = model_with_tools.invoke(messages)
messages.append(ai_msg)

# 步骤 2：执行工具并收集结果
for tool_call in ai_msg.tool_calls:
    # 使用生成的参数执行工具
    tool_result = get_weather.invoke(tool_call)
    messages.append(tool_result)

# 步骤 3：将结果传递回模型以获取最终响应
final_response = model_with_tools.invoke(messages)
print(final_response.text)
# "波士顿当前天气为 72°F，晴朗。"每个由工具返回的 ToolMessage 包含一个与原始工具调用匹配的 tool_call_id，帮助模型将结果与请求相关联。强制工具调用默认情况下，模型可以根据用户输入自由选择使用哪个绑定的工具。但是，您可能希望强制选择工具，确保模型使用特定工具或给定列表中的任何工具：model_with_tools = model.bind_tools([tool_1], tool_choice="any")model_with_tools = model.bind_tools([tool_1], tool_choice="tool_1")并行工具调用许多模型支持在适当时并行调用多个工具。这允许模型同时从不同来源收集信息。model_with_tools = model.bind_tools([get_weather])

response = model_with_tools.invoke(
    "波士顿和东京的天气怎么样？"
)

# 模型可能会生成多个工具调用
print(response.tool_calls)
# [
#   {'name': 'get_weather', 'args': {'location': 'Boston'}, 'id': 'call_1'},
#   {'name': 'get_weather', 'args': {'location': 'Tokyo'}, 'id': 'call_2'},
# ]

# 执行所有工具（可以使用 async 并行执行）
results = []
for tool_call in response.tool_calls:
    if tool_call['name'] == 'get_weather':
        result = get_weather.invoke(tool_call)
    ...
    results.append(result)模型根据请求操作的独立性智能地确定何时适合并行执行。提示 大多数支持工具调用的模型默认启用并行工具调用。某些模型（包括 OpenAI 和 Anthropic）允许您禁用此功能。要执行此操作，请设置 parallel_tool_calls=False：model.bind_tools([get_weather], parallel_tool_calls=False)流式传输工具调用在流式传输响应时，工具调用通过 ToolCallChunk 逐步构建。这允许您在生成工具调用时查看它们，而不是等待完整响应。for chunk in model_with_tools.stream(
    "波士顿和东京的天气怎么样？"
):
    # 工具调用块逐步到达
    for tool_chunk in chunk.tool_call_chunks:
        if name := tool_chunk.get("name"):
            print(f"工具：{name}")
        if id_ := tool_chunk.get("id"):
            print(f"ID：{id_}")
        if args := tool_chunk.get("args"):
            print(f"参数：{args}")

# 输出：
# 工具：get_weather
# ID：call_SvMlU1TVIZugrFLckFE2ceRE
# 参数：{"lo
# 参数：catio
# 参数：n": "B
# 参数：osto
# 参数：n"}
# 工具：get_weather
# ID：call_QMZdy6qInx13oWKE7KhuhOLR
# 参数：{"lo
# 参数：catio
# 参数：n": "T
# 参数：okyo
# 参数："}您可以累积块以构建完整的工具调用：gathered = None
for chunk in model_with_tools.stream("波士顿的天气怎么样？"):
    gathered = chunk if gathered is None else gathered + chunk
    print(gathered.tool_calls)结构化输出可以请求模型以匹配给定架构的格式提供其响应。这对于确保输出易于解析并用于后续处理非常有用。LangChain 支持多种架构类型和强制执行结构化输出的方法。PydanticPydantic 模型 提供最丰富的功能集，包括字段验证、描述和嵌套结构。from pydantic import BaseModel, Field

class Movie(BaseModel):
    """一部带有详细信息的电影。"""
    title: str = Field(..., description="电影标题")
    year: int = Field(..., description="电影上映年份")
    director: str = Field(..., description="电影导演")
    rating: float = Field(..., description="电影评分，满分 10 分")

model_with_structure = model.with_structured_output(Movie)
response = model_with_structure.invoke("提供关于电影《盗梦空间》的详细信息")
print(response)  # Movie(title="Inception", year=2010, director="Christopher Nolan", rating=8.8)TypedDictTypedDict 提供使用 Python 内置类型的更简单替代方案，适用于不需要运行时验证的情况。from typing_extensions import TypedDict, Annotated

class MovieDict(TypedDict):
    """一部带有详细信息的电影。"""
    title: Annotated[str, ..., "电影标题"]
    year: Annotated[int, ..., "电影上映年份"]
    director: Annotated[str, ..., "电影导演"]
    rating: Annotated[float, ..., "电影评分，满分 10 分"]

model_with_structure = model.with_structured_output(MovieDict)
response = model_with_structure.invoke("提供关于电影《盗梦空间》的详细信息")
print(response)  # {'title': 'Inception', 'year': 2010, 'director': 'Christopher Nolan', 'rating': 8.8}JSON Schema为了获得最大控制或互操作性，您可以提供原始 JSON 架构。import json

json_schema = {
    "title": "Movie",
    "description": "一部带有详细信息的电影",
    "type": "object",
    "properties": {
        "title": {
            "type": "string",
            "description": "电影标题"
        },
        "year": {
            "type": "integer",
            "description": "电影上映年份"
        },
        "director": {
            "type": "string",
            "description": "电影导演"
        },
        "rating": {
            "type": "number",
            "description": "电影评分，满分 10 分"
        }
    },
    "required": ["title", "year", "director", "rating"]
}

model_with_structure = model.with_structured_output(
    json_schema,
    method="json_schema",
)
response = model_with_structure.invoke("提供关于电影《盗梦空间》的详细信息")
print(response)  # {'title': 'Inception', 'year': 2010, ...}注意结构化输出的关键考虑因素：方法参数：某些提供商支持不同的方法（'json_schema'、'function_calling'、'json_mode'） 'json_schema' 通常指提供商提供的专用结构化输出功能'function_calling' 通过强制工具调用遵循给定架构来派生结构化输出'json_mode' 是某些提供商提供的 'json_schema' 的前身——它生成有效的 JSON，但架构必须在提示中描述包含原始：使用 include_raw=True 以同时获取已解析的输出和原始 AI 消息验证：Pydantic 模型提供自动验证，而 TypedDict 和 JSON Schema 需要手动验证示例：消息输出与解析结构并存返回原始 AIMessage 对象与解析表示一起以访问响应元数据（如令牌计数）可能很有用。为此，在调用 with_structured_output 时设置 include_raw=True：from pydantic import BaseModel, Field

class Movie(BaseModel):
    """一部带有详细信息的电影。"""
    title: str = Field(..., description="电影标题")
    year: int = Field(..., description="电影上映年份")
    director: str = Field(..., description="电影导演")
    rating: float = Field(..., description="电影评分，满分 10 分")

model_with_structure = model.with_structured_output(Movie, include_raw=True)  # [!code highlight]
response = model_with_structure.invoke("提供关于电影《盗梦空间》的详细信息")
response
# {
#     "raw": AIMessage(...),
#     "parsed": Movie(title=..., year=..., ...),
#     "parsing_error": None,
# }示例：嵌套结构架构可以嵌套：from pydantic import BaseModel, Field

class Actor(BaseModel):
    name: str
    role: str

class MovieDetails(BaseModel):
    title: str
    year: int
    cast: list[Actor]
    genres: list[str]
    budget: float | None = Field(None, description="预算（百万美元）")

model_with_structure = model.with_structured_output(MovieDetails)from typing_extensions import Annotated, TypedDict

class Actor(TypedDict):
    name: str
    role: str

class MovieDetails(TypedDict):
    title: str
    year: int
    cast: list[Actor]
    genres: list[str]
    budget: Annotated[float | None, ..., "预算（百万美元）"]

model_with_structure = model.with_structured_output(MovieDetails)支持的模型LangChain 支持所有主要模型提供商，包括 OpenAI、Anthropic、Google、Azure、AWS Bedrock 等。每个提供商提供具有不同功能的各种模型。有关 LangChain 中支持的模型完整列表，请参阅集成页面。高级主题多模态某些模型可以处理和返回非文本数据，如图像、音频和视频。您可以通过提供内容块将非文本数据传递给模型。提示 所有具有底层多模态功能的 LangChain 聊天模型都支持：跨提供商标准格式的数据（请参阅我们的消息指南）OpenAI 聊天完成格式特定于该提供商的任何格式（例如，Anthropic 模型接受 Anthropic 原生格式）有关详细信息，请参阅消息指南的多模态部分。提示 并非所有 LLM 都是平等的！ 某些模型可以作为其响应的一部分返回多模态数据。如果调用它们这样做，则生成的 AIMessage 将具有多模态类型的内容块。response = model.invoke("创建一张猫的图片")
print(response.content_blocks)
# [
#     {"type": "text", "text": "这是一张猫的图片"},
#     {"type": "image", "base64": "...", "mime_type": "image/jpeg"},
# ]有关特定提供商的详细信息，请参阅集成页面。推理较新的模型能够执行多步推理以得出结论。这涉及将复杂问题分解为更小、更易管理的步骤。如果底层模型支持，您可以显示此推理过程以更好地理解模型如何得出其最终答案。for chunk in model.stream("为什么鹦鹉有五颜六色的羽毛？"):
    reasoning_steps = [r for r in chunk.content_blocks if r["type"] == "reasoning"]
    print(reasoning_steps if reasoning_steps else chunk.text)response = model.invoke("为什么鹦鹉有五颜六色的羽毛？")
reasoning_steps = [b for b in response.content_blocks if b["type"] == "reasoning"]
print(" ".join(step["reasoning"] for step in reasoning_steps))根据模型，您有时可以指定它应投入推理的努力程度。同样，您可以请求模型完全关闭推理。这可能采用“层级”（例如 'low' 或 'high'）或整数令牌预算的形式。有关详细信息，请参阅集成页面或您相应聊天模型的参考。本地模型LangChain 支持在您自己的硬件上本地运行模型。这对于数据隐私至关重要、您想调用自定义模型或希望避免使用基于云的模型所产生的成本的场景非常有用。Ollama 是本地运行模型的最简单方法之一。请参阅集成页面上的本地集成完整列表。提示缓存许多提供商提供提示缓存功能，以减少对相同令牌重复处理的延迟和成本。这些功能可以是隐式或显式：隐式提示缓存： 如果请求命中缓存，提供商将自动传递成本节省。示例：OpenAI 和 Gemini（Gemini 2.5 及以上）。显式缓存： 提供商允许您手动指示缓存点以获得更大控制或保证成本节省。示例：ChatOpenAI（通过 prompt_cache_key）、Anthropic 的 AnthropicPromptCachingMiddleware 和 cache_control 选项、AWS Bedrock、Gemini。警告 提示缓存通常仅在超过最小输入令牌阈值时才会启用。请参阅提供商页面以了解详细信息。缓存使用情况将反映在模型响应的使用元数据中。服务器端工具使用某些提供商支持服务器端工具调用循环：模型可以在单个对话轮次中与网络搜索、代码解释器和其他工具交互并分析结果。如果模型在服务器端调用工具，则响应消息的内容将包括表示工具调用和结果的内容。访问响应的内容块将以提供商无关的格式返回服务器端工具调用和结果：from langchain.chat_models import init_chat_model

model = init_chat_model("openai:gpt-4.1-mini")

tool = {"type": "web_search"}
model_with_tools = model.bind_tools([tool])

response = model_with_tools.invoke("今天有什么正面新闻？")
response.content_blocks[
    {
        "type": "server_tool_call",
        "name": "web_search",
        "args": {
            "query": "positive news stories today",
            "type": "search"
        },
        "id": "ws_abc123"
    },
    {
        "type": "server_tool_result",
        "tool_call_id": "ws_abc123",
        "status": "success"
    },
    {
        "type": "text",
        "text": "以下是今天的一些正面新闻...",
        "annotations": [
            {
                "end_index": 410,
                "start_index": 337,
                "title": "文章标题",
                "type": "citation",
                "url": "..."
            }
        ]
    }
]这表示单个对话轮次；没有需要作为客户端工具调用传入的关联 ToolMessage 对象。有关可用工具和使用详细信息的给定提供商，请参阅集成页面。速率限制许多聊天模型提供商对给定时间段内可以发出的调用次数施加限制。如果您达到速率限制，通常会从提供商收到速率限制错误响应，并且需要等待才能发出更多请求。为了帮助管理速率限制，聊天模型集成在初始化期间接受 rate_limiter 参数，以控制发出请求的速率。初始化和使用速率限制器LangChain 内置（可选）InMemoryRateLimiter。此限制器是线程安全的，可以由同一进程中的多个线程共享。from langchain_core.rate_limiters import InMemoryRateLimiter

rate_limiter = InMemoryRateLimiter(
    requests_per_second=0.1,  # 每 10 秒 1 个请求
    check_every_n_seconds=0.1,  # 每 100 毫秒检查是否允许发出请求
    max_bucket_size=10,  # 控制最大突发大小。
)

model = init_chat_model(
    model="gpt-5",
    model_provider="openai",
    rate_limiter=rate_limiter  # [!code highlight]
)警告 提供的速率限制器只能限制每单位时间的请求数。如果您还需要根据请求大小进行限制，它将无济于事。基础 URL 或代理对于许多聊天模型集成，您可以配置 API 请求的基础 URL，这允许您使用具有 OpenAI 兼容 API 的模型提供商或使用代理服务器。基础 URL许多模型提供商提供 OpenAI 兼容的 API（例如，Together AI、vLLM）。您可以通过指定适当的 base_url 参数使用 init_chat_model 与这些提供商一起使用：model = init_chat_model(
    model="MODEL_NAME",
    model_provider="openai",
    base_url="BASE_URL",
    api_key="YOUR_API_KEY",
)注意 使用直接聊天模型类实例化时，参数名称可能因提供商而异。请查看相应的参考以了解详细信息。代理配置对于需要 HTTP 代理的部署，某些模型集成支持代理配置：from langchain_openai import ChatOpenAI

model = ChatOpenAI(
    model="gpt-4o",
    openai_proxy="http://proxy.example.com:8080"
)注意 代理支持因集成而异。请查看特定模型提供商的参考以了解代理配置选项。对数概率某些模型可以通过在初始化模型时设置 logprobs 参数来配置为返回表示给定令牌可能性的令牌级对数概率：model = init_chat_model(
    model="gpt-4o",
    model_provider="openai"
).bind(logprobs=True)

response = model.invoke("为什么鹦鹉会说话？")
print(response.response_metadata["logprobs"])令牌使用情况许多模型提供商将令牌使用信息作为调用响应的一部分返回。当可用时，此信息将包含在相应模型生成的 AIMessage 对象上。有关更多详细信息，请参阅消息指南。注意 某些提供商 API，特别是在流式传输上下文中 OpenAI 和 Azure OpenAI 聊天完成，要求用户选择接收令牌使用数据。请参阅集成指南的流式传输使用元数据部分以了解详细信息。您可以使用回调或上下文管理器跟踪应用程序中跨模型的聚合令牌计数，如下所示：回调处理程序from langchain.chat_models import init_chat_model
from langchain_core.callbacks import UsageMetadataCallbackHandler

model_1 = init_chat_model(model="openai:gpt-4o-mini")
model_2 = init_chat_model(model="anthropic:claude-3-5-haiku-latest")

callback = UsageMetadataCallbackHandler()
result_1 = model_1.invoke("你好", config={"callbacks": [callback]})
result_2 = model_2.invoke("你好", config={"callbacks": [callback]})
callback.usage_metadata{
    'gpt-4o-mini-2024-07-18': {
        'input_tokens': 8,
        'output_tokens': 10,
        'total_tokens': 18,
        'input_token_details': {'audio': 0, 'cache_read': 0},
        'output_token_details': {'audio': 0, 'reasoning': 0}
    },
    'claude-3-5-haiku-20241022': {
        'input_tokens': 8,
        'output_tokens': 21,
        'total_tokens': 29,
        'input_token_details': {'cache_read': 0, 'cache_creation': 0}
    }
}上下文管理器from langchain.chat_models import init_chat_model
from langchain_core.callbacks import get_usage_metadata_callback

model_1 = init_chat_model(model="openai:gpt-4o-mini")
model_2 = init_chat_model(model="anthropic:claude-3-5-haiku-latest")

with get_usage_metadata_callback() as cb:
    model_1.invoke("你好")
    model_2.invoke("你好")
    print(cb.usage_metadata){
    'gpt-4o-mini-2024-07-18': {
        'input_tokens': 8,
        'output_tokens': 10,
        'total_tokens': 18,
        'input_token_details': {'audio': 0, 'cache_read': 0},
        'output_token_details': {'audio': 0, 'reasoning': 0}
    },
    'claude-3-5-haiku-20241022': {
        'input_tokens': 8,
        'output_tokens': 21,
        'total_tokens': 29,
        'input_token_details': {'cache_read': 0, 'cache_creation': 0}
    }
}调用配置调用模型时，您可以使用 RunnableConfig 字典通过 config 参数传递额外配置。这提供了对执行行为、回调和元数据跟踪的运行时控制。常见配置选项包括：response = model.invoke(
    "讲个笑话",
    config={
        "run_name": "joke_generation",      # 此运行的自定义名称
        "tags": ["humor", "demo"],          # 用于分类的标签
        "metadata": {"user_id": "123"},     # 自定义元数据
        "callbacks": [my_callback_handler], # 回调处理程序
    }
)这些配置值在以下情况下特别有用：使用 LangSmith 跟踪进行调试实现自定义日志或监控在生产中控制资源使用在复杂管道中跟踪调用关键配置属性属性类型说明run_namestring在日志和跟踪中标识此特定调用。不由子调用继承。tagsstring[]由所有子调用继承的标签，用于在调试工具中过滤和组织。metadataobject用于跟踪额外上下文的自定义键值对，由所有子调用继承。max_concurrencynumber在使用 batch() 或 batch_as_completed() 时控制最大并行调用数。callbacksarray用于在执行期间监控和响应事件的处理程序。recursion_limitnumber链的最大递归深度，以防止复杂管道中的无限循环。提示 请参阅完整的 RunnableConfig 参考，了解所有支持的属性。可配置模型您还可以通过指定 configurable_fields 创建运行时可配置模型。如果您未指定模型值，则默认情况下 'model' 和 'model_provider' 将是可配置的。from langchain.chat_models import init_chat_model

configurable_model = init_chat_model(temperature=0)

configurable_model.invoke(
    "你叫什么名字",
    config={"configurable": {"model": "gpt-5-nano"}},  # 使用 GPT-5-Nano 运行
)
configurable_model.invoke(
    "你叫什么名字",
    config={"configurable": {"model": "claude-sonnet-4-5"}},  # 使用 Claude 运行
)具有默认值的可配置模型我们可以创建具有默认模型值的可配置模型，指定哪些参数是可配置的，并为可配置参数添加前缀：first_model = init_chat_model(
        model="gpt-4.1-mini",
        temperature=0,
        configurable_fields=("model", "model_provider", "temperature", "max_tokens"),
        config_prefix="first",  # 当链中有多个模型时很有用
)

first_model.invoke("你叫什么名字")first_model.invoke(
    "你叫什么名字",
    config={
        "configurable": {
            "first_model": "claude-sonnet-4-5",
            "first_temperature": 0.5,
            "first_max_tokens": 100,
        }
    },
)以声明方式使用可配置模型我们可以在可配置模型上调用声明性操作，如 bind_tools、with_structured_output、with_configurable 等，并以与常规实例化聊天模型对象相同的方式链接可配置模型。from pydantic import BaseModel, Field

class GetWeather(BaseModel):
    """获取给定位置的当前天气"""
    location: str = Field(..., description="城市和州，例如 San Francisco, CA")

class GetPopulation(BaseModel):
    """获取给定位置的当前人口"""
    location: str = Field(..., description="城市和州，例如 San Francisco, CA")

model = init_chat_model(temperature=0)
model_with_tools = model.bind_tools([GetWeather, GetPopulation])

model_with_tools.invoke(
    "2024 年洛杉矶和纽约哪个更大", config={"configurable": {"model": "gpt-4.1-mini"}}
).tool_calls[
    {
        'name': 'GetPopulation',
        'args': {'location': 'Los Angeles, CA'},
        'id': 'call_Ga9m8FAArIyEjItHmztPYA22',
        'type': 'tool_call'
    },
    {
        'name': 'GetPopulation',
        'args': {'location': 'New York, NY'},
        'id': 'call_jh2dEvBaAHRaw5JUDthOs7rt',
        'type': 'tool_call'
    }
]model_with_tools.invoke(
    "2024 年洛杉矶和纽约哪个更大",
        config={"configurable": {"model": "claude-sonnet-4-5"}},
).tool_calls[
    {
        'name': 'GetPopulation',
        'args': {'location': 'Los Angeles, CA'},
        'id': 'toolu_01JMufPf4F4t2zLj7miFeqXp',
        'type': 'tool_call'
    },
    {
        'name': 'GetPopulation',
        'args': {'location': 'New York City, NY'},
        'id': 'toolu_01RQBHcE8kEEbYTuuS8WqY1u',
        'type': 'tool_call'
    }
]最近更新2025/10/25 19:51上一页智能体下一页消息

---

## 智能体

**URL:** https://langchain-doc.cn/v1/python/langchain/agents.html

智能体智能体将语言模型与工具结合，创建能够对任务进行推理、决定使用哪些工具并迭代寻求解决方案的系统。create_agent 提供了一个生产就绪的智能体实现。LLM 智能体在循环中运行工具以实现目标。 智能体会一直运行，直到满足停止条件——即模型输出最终结果或达到迭代次数限制。信息create_agent 使用 LangGraph 构建了一个基于图的智能体运行时。图由节点（步骤）和边（连接）组成，定义了智能体如何处理信息。智能体在图中移动，执行节点，如模型节点（调用模型）、工具节点（执行工具）或中间件。了解更多关于 Graph API 的信息。核心组件模型模型 是智能体的推理引擎。它可以通过多种方式指定，支持静态和动态模型选择。静态模型静态模型在创建智能体时配置一次，并在整个执行过程中保持不变。这是最常见且直接的方法。从  初始化静态模型：from langchain.agents import create_agent

agent = create_agent(
    "openai:gpt-5",
    tools=tools
)提示 模型标识符字符串支持自动推断（例如 "gpt-5" 将被推断为 "openai:gpt-5"）。请参考参考文档 查看完整的模型标识符字符串映射列表。为了对模型配置进行更多控制，可以直接使用提供商包初始化模型实例。在此示例中，我们使用 ChatOpenAI。请参阅 聊天模型 以了解其他可用的聊天模型类。from langchain.agents import create_agent
from langchain_openai import ChatOpenAI

model = ChatOpenAI(
    model="gpt-5",
    temperature=0.1,
    max_tokens=1000,
    timeout=30
    # ...（其他参数）
)
agent = create_agent(model, tools=tools)模型实例为您提供对配置的完全控制。当您需要设置特定参数，如 temperature、max_tokens、timeouts、base_url 和其他提供商特定设置时，请使用它们。请参考参考文档 查看模型上可用的参数和方法。动态模型动态模型在  根据当前  和上下文进行选择。这支持复杂的路由逻辑和成本优化。要使用动态模型，请使用 @wrap_model_call 装饰器创建中间件，以修改请求中的模型：from langchain_openai import ChatOpenAI
from langchain.agents import create_agent
from langchain.agents.middleware import wrap_model_call, ModelRequest, ModelResponse


basic_model = ChatOpenAI(model="gpt-4o-mini")
advanced_model = ChatOpenAI(model="gpt-4o")

@wrap_model_call
def dynamic_model_selection(request: ModelRequest, handler) -> ModelResponse:
    """根据对话复杂性选择模型。"""
    message_count = len(request.state["messages"])

    if message_count > 10:
        # 对较长的对话使用高级模型
        model = advanced_model
    else:
        model = basic_model

    request.model = model
    return handler(request)

agent = create_agent(
    model=basic_model,  # 默认模型
    tools=tools,
    middleware=[dynamic_model_selection]
)警告 在使用结构化输出时，不支持预绑定模型（已调用 bind_tools 的模型）。如果您需要使用结构化输出的动态模型选择，请确保传递给中间件的模型未预绑定。提示 有关模型配置详细信息，请参阅 模型。有关动态模型选择模式，请参阅 中间件中的动态模型。工具工具赋予智能体执行行动的能力。智能体超越了简单的仅模型工具绑定，实现了：序列中的多个工具调用（由单个提示触发）适当的并行工具调用基于先前结果的动态工具选择工具重试逻辑和错误处理工具调用之间的状态持久化有关更多信息，请参阅 工具。定义工具将工具列表传递给智能体。from langchain.tools import tool
from langchain.agents import create_agent


@tool
def search(query: str) -> str:
    """搜索信息。"""
    return f"结果：{query}"

@tool
def get_weather(location: str) -> str:
    """获取位置的天气信息。"""
    return f"{location} 的天气：晴朗，72°F"

agent = create_agent(model, tools=[search, get_weather])如果提供空工具列表，智能体将仅包含一个 LLM 节点，不具备工具调用能力。工具错误处理要自定义工具错误的处理方式，请使用 @wrap_tool_call 装饰器创建中间件：from langchain.agents import create_agent
from langchain.agents.middleware import wrap_tool_call
from langchain_core.messages import ToolMessage


@wrap_tool_call
def handle_tool_errors(request, handler):
    """使用自定义消息处理工具执行错误。"""
    try:
        return handler(request)
    except Exception as e:
        # 向模型返回自定义错误消息
        return ToolMessage(
            content=f"工具错误：请检查您的输入并重试。({str(e)})",
            tool_call_id=request.tool_call["id"]
        )

agent = create_agent(
    model="openai:gpt-4o",
    tools=[search, get_weather],
    middleware=[handle_tool_errors]
)当工具失败时，智能体将返回带有自定义错误消息的 ToolMessage：[
    ...
    ToolMessage(
        content="工具错误：请检查您的输入并重试。(division by zero)",
        tool_call_id="..."
    ),
    ...
]ReAct 循环中的工具使用智能体遵循 ReAct（“推理 + 行动”）模式，在简短的推理步骤与针对性的工具调用之间交替，并将结果观察反馈到后续决策中，直到能够提供最终答案。提示 要了解更多关于工具的信息，请参阅 工具。系统提示您可以通过提供提示来塑造智能体处理任务的方式。system_prompt 参数可以作为字符串提供：agent = create_agent(
    model,
    tools,
    system_prompt="你是一个有帮助的助手。请简洁准确。"
)当未提供 system_prompt 时，智能体将直接从消息中推断其任务。动态系统提示对于需要根据运行时上下文或智能体状态修改系统提示的高级用例，您可以使用 中间件。@dynamic_prompt 装饰器创建中间件，根据模型请求动态生成系统提示：from typing import TypedDict

from langchain.agents import create_agent
from langchain.agents.middleware import dynamic_prompt, ModelRequest


class Context(TypedDict):
    user_role: str

@dynamic_prompt
def user_role_prompt(request: ModelRequest) -> str:
    """根据用户角色生成系统提示。"""
    user_role = request.runtime.context.get("user_role", "user")
    base_prompt = "你是一个有帮助的助手。"

    if user_role == "expert":
        return f"{base_prompt} 提供详细的技术响应。"
    elif user_role == "beginner":
        return f"{base_prompt} 简单解释概念，避免使用行话。"

    return base_prompt

agent = create_agent(
    model="openai:gpt-4o",
    tools=[web_search],
    middleware=[user_role_prompt],
    context_schema=Context
)

# 系统提示将根据上下文动态设置
result = agent.invoke(
    {"messages": [{"role": "user", "content": "解释机器学习"}]},
    context={"user_role": "expert"}
)提示 有关消息类型和格式化的更多详细信息，请参阅 消息。有关全面的中间件文档，请参阅 中间件。调用您可以通过向其 State 传递更新来调用智能体。所有智能体在其状态中包含消息序列；要调用智能体，请传递一条新消息：result = agent.invoke(
    {"messages": [{"role": "user", "content": "旧金山天气如何？"}]}
)有关从智能体流式传输步骤和/或令牌的信息，请参阅流式传输指南。否则，智能体遵循 LangGraph Graph API 并支持所有相关方法。高级概念结构化输出在某些情况下，您可能希望智能体以特定格式返回输出。LangChain 通过 response_format 参数提供结构化输出策略。ToolStrategyToolStrategy 使用人工工具调用生成结构化输出。这适用于任何支持工具调用的模型：from pydantic import BaseModel
from langchain.agents import create_agent
from langchain.agents.structured_output import ToolStrategy


class ContactInfo(BaseModel):
    name: str
    email: str
    phone: str

agent = create_agent(
    model="openai:gpt-4o-mini",
    tools=[search_tool],
    response_format=ToolStrategy(ContactInfo)
)

result = agent.invoke({
    "messages": [{"role": "user", "content": "从以下内容提取联系信息：John Doe, john@example.com, (555) 123-4567"}]
})

result["structured_response"]
# ContactInfo(name='John Doe', email='john@example.com', phone='(555) 123-4567')ProviderStrategyProviderStrategy 使用模型提供商的原生结构化输出生成。这更可靠，但仅适用于支持原生结构化输出的提供商（例如 OpenAI）：from langchain.agents.structured_output import ProviderStrategy

agent = create_agent(
    model="openai:gpt-4o",
    response_format=ProviderStrategy(ContactInfo)
)注意 从 langchain 1.0 开始，不再支持直接传递模式（例如 response_format=ContactInfo）。您必须明确使用 ToolStrategy 或 ProviderStrategy。提示 要了解结构化输出，请参阅 结构化输出。记忆智能体通过消息状态自动维护对话历史。您还可以配置智能体使用自定义状态模式，在对话期间记住额外信息。存储在状态中的信息可以被视为智能体的短期记忆：自定义状态模式必须扩展 AgentState 作为 TypedDict。定义自定义状态有两种方式：通过 中间件（推荐）通过 create_agent 上的 state_schema注意 推荐通过中间件定义自定义状态，而不是通过 create_agent 上的 state_schema，因为它允许您将状态扩展概念上限定在相关中间件和工具的范围内。state_schema 仍支持用于向后兼容，在 create_agent 上。通过中间件定义状态当您的自定义状态需要被特定中间件钩子和附加到该中间件的工具访问时，使用中间件定义自定义状态。from langchain.agents import AgentState
from langchain.agents.middleware import AgentMiddleware


class CustomState(AgentState):
    user_preferences: dict

class CustomMiddleware(AgentMiddleware):
    state_schema = CustomState
    tools = [tool1, tool2]

    def before_model(self, state: CustomState, runtime) -> dict[str, Any] | None:
        ...

agent = create_agent(
    model,
    tools=tools,
    middleware=[CustomMiddleware()]
)

# 智能体现在可以跟踪消息之外的额外状态
result = agent.invoke({
    "messages": [{"role": "user", "content": "我更喜欢技术性解释"}],
    "user_preferences": {"style": "technical", "verbosity": "detailed"},
})通过 state_schema 定义状态使用 state_schema 参数作为快捷方式，定义仅在工具中使用的自定义状态。from langchain.agents import AgentState


class CustomState(AgentState):
    user_preferences: dict

agent = create_agent(
    model,
    tools=[tool1, tool2],
    state_schema=CustomState
)
# 智能体现在可以跟踪消息之外的额外状态
result = agent.invoke({
    "messages": [{"role": "user", "content": "我更喜欢技术性解释"}],
    "user_preferences": {"style": "technical", "verbosity": "detailed"},
})注意 从 langchain 1.0 开始，自定义状态模式必须是 TypedDict 类型。不再支持 Pydantic 模型和数据类。有关更多详细信息，请参阅 v1 迁移指南。提示 要了解更多关于记忆的信息，请参阅 记忆。有关实现跨会话持久化的长期记忆的信息，请参阅 长期记忆。流式传输我们已经看到如何使用 invoke 调用智能体以获取最终响应。如果智能体执行多个步骤，这可能需要一段时间。为了显示中间进度，我们可以随着消息的发生而流式传回。for chunk in agent.stream({
    "messages": [{"role": "user", "content": "搜索 AI 新闻并总结发现"}]
}, stream_mode="values"):
    # 每个块包含该时间点的完整状态
    latest_message = chunk["messages"][-1]
    if latest_message.content:
        print(f"智能体：{latest_message.content}")
    elif latest_message.tool_calls:
        print(f"正在调用工具：{[tc['name'] for tc in latest_message.tool_calls]}")提示 有关流式传输的更多详细信息，请参阅 流式传输。中间件中间件 为在执行的不同阶段自定义智能体行为提供了强大的扩展性。您可以使用中间件来：在调用模型之前处理状态（例如消息裁剪、上下文注入）修改或验证模型的响应（例如防护栏、内容过滤）使用自定义逻辑处理工具执行错误基于状态或上下文实现动态模型选择添加自定义日志、监控或分析中间件无缝集成到智能体的执行图中，允许您在关键点拦截和修改数据流，而无需更改核心智能体逻辑。提示 有关全面的中间件文档，包括装饰器如 @before_model、@after_model 和 @wrap_tool_call，请参阅 中间件。最近更新2025/10/25 19:51下一页模型

---
