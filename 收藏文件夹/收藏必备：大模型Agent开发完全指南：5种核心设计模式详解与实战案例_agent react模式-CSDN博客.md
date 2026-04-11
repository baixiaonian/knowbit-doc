---
title: 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例_agent react模式-CSDN博客
created_at: 2026-01-03T04:42:19.086941+00:00
updated_at: 2026-04-06T13:19:11.457167+00:00
excerpt: 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例_agent react模式-CSDN博客原文链接: https://blog.csdn.net/kaka0722ww/artic...
---

# 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例\_agent react模式-CSDN博客

**原文链接**: <https://blog.csdn.net/kaka0722ww/article/details/155453725>

**摘要**: 文章浏览阅读1k次，点赞12次，收藏19次。ReAct（Reasoning + Acting）是一种将推理（Reasoning）和行动（Acting）相结合的 Agent 设计模式。边思考、边行动、边观察结果，然后继续思考。这种模式特别适合处理需要外部信息或工具支持的任务。通过将复杂问题分解为多个"思考-行动-观察"的小步骤，Agent 能够逐步逼近最终答案，整个过程更加透明、可控。五种 Agent 设计模式各有侧重。ReAct 通过推理-行动循环适合处理需要外部工具的任务，CodeAct 通过代码生成解决复杂计算问题。\_agent react模式

**关键词**: agent react模式

**收藏时间**: 2026/1/3 12:42:17



---

# 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例

最新推荐文章于 2025-12-31 01:18:20 发布

原创 于 2025-12-01 15:51:14 发布 · 1k 阅读

· ![](https://csdnimg.cn/release/blogv2/dist/pc/img/newHeart2023Active.png) ![](https://csdnimg.cn/release/blogv2/dist/pc/img/newHeart2023Black.png) 12

· ![](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect2.png) ![](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollectionActive2.png) 19 ·

CC 4.0 BY-SA版权

版权声明：本文为博主原创文章，遵循 [CC 4.0 BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) 版权协议，转载请附上原文出处链接和本声明。

文章标签：

[#设计模式](https://so.csdn.net/so/search/s.do?q=%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#人工智能](https://so.csdn.net/so/search/s.do?q=%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#架构](https://so.csdn.net/so/search/s.do?q=%E6%9E%B6%E6%9E%84&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#transformer](https://so.csdn.net/so/search/s.do?q=transformer&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#大模型](https://so.csdn.net/so/search/s.do?q=%E5%A4%A7%E6%A8%A1%E5%9E%8B&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#大模型学习](https://so.csdn.net/so/search/s.do?q=%E5%A4%A7%E6%A8%A1%E5%9E%8B%E5%AD%A6%E4%B9%A0&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art) [#agent](https://so.csdn.net/so/search/s.do?q=agent&t=all&o=vip&s=&l=&f=&viparticle=&from_tracking_code=tag_word&from_code=app_blog_art)

部署运行你感兴趣的模型镜像一键部署

本文介绍5种AI Agent核心设计模式：ReAct模式通过推理与行动交替循环处理外部信息任务；CodeAct模式通过生成代码解决复杂计算；计划模式为结构化任务提供执行路径；反思模式通过迭代改进提升输出质量；人机协作模式在关键节点引入人工判断。每种模式均包含工作流程、实战案例和适用场景，帮助开发者构建高效可靠的Agent系统。

# 一、ReAct 模式

# 1.1 什么是 ReAct

ReAct（Reasoning + Acting）是一种将推理（Reasoning）和行动（Acting）相结合的 Agent 设计模式。它的核心思想是让 LLM 在解决问题时，不是一次性给出答案，而是模拟人类的思维过程：**边思考、边行动、边观察结果，然后继续思考**。

这种模式特别适合处理需要外部信息或工具支持的任务。通过将复杂问题分解为多个"思考-行动-观察"的小步骤，Agent 能够逐步逼近最终答案，整个过程更加透明、可控。

# 1.2 工作流程

ReAct 的核心流程可以概括为一个循环：Thought → Action → Observation → Thought。在每次循环中，Agent 首先进行思考阶段，分析当前问题和已有信息，决定下一步需要采取什么行动。例如，当需要查询股票价格时，Agent 会思考"我需要查询青岛啤酒的股票收盘价"。

接着进入行动阶段，Agent 选择合适的工具并指定参数，如 `Action: get_closing_price` 和 `Action Input: {"name": "青岛啤酒"}`。工具执行后进入观察阶段，将执行结果反馈给 Agent，例如 `Observation: 67.92`。Agent 收到观察结果后，会判断问题是否已经解决。如果未解决，则继续下一轮思考-行动-观察循环；如果已解决，则输出最终答案。

流程图展示了 ReAct 的完整执行过程。在底部的主流程中，Input 经过 LLM 推理后依次生成 Thought、Action、Action Input 和 PAUSE 标记。PAUSE 触发工具执行，执行结果形成 Observation 并返回给 LLM，由此形成一个闭环。当 LLM 判断已获得足够信息时，会从 Thought 节点输出 Final Answer，结束整个流程。

# 1.3 实战案例

# 案例：比较两个股票的收盘价

**任务：** 请比较青岛啤酒和贵州茅台的股票收盘价谁高？

# 核心代码实现

**1. 工具定义与注册**


```
// 工具定义（JSON Schema 格式）
const tools = [{
    name: 'get_closing_price',
    description: '使用该工具获取指定股票的收盘价',
    parameters: {
      type: 'object',
      properties: {
        name: {type: 'string', description: '股票名称'},
      },
      required: ['name'],
    },
  },
]

// 工具注册表（工具名 -> 实现函数）
const toolRegistry = {
  get_closing_price: (params) => getClosingPrice(params.name),
}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19

**2. Prompt 模板（关键部分）**


```
const REACT_PROMPT = `
You run in a loop of Thought, Action, Action Input, PAUSE, Observation.
At the end of the loop you output an Answer.

Your available actions are: {tools}

Example:
Question: 今天北京天气怎么样？
Thought: 我需要调用 get_weather 工具获取天气
Action: get_weather
Action Input: {"city": "BeiJing"}
PAUSE

Observation: 北京的气温是0度.
Final Answer: 北京的气温是0度.

New input: {input}`
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17

**3. Agent 主循环（核心逻辑）**


```
async function reactAgent(query: string) {
// 构建初始提示词
const prompt = REACT_PROMPT.replace('{tools}', JSON.stringify(tools)).replace(
    '{input}',
    query
  )

const messages = [{role: 'user', content: prompt}]

while (true) {
    // 1. 调用 LLM
    const response = await llm.chat(messages)
    const text = response.content

    // 2. 检查是否有最终答案
    if (text.includes('Final Answer:')) {
      return text.match(/Final Answer:\s*(.*)/)[1]
    }

    // 3. 解析 Action 和 Action Input
    const action = text.match(/Action:\s*(\w+)/)?.[1]
    const input = text.match(/Action Input:\s*({.*})/s)?.[1]

    if (!action || !input) break

    // 4. 执行工具
    const params = JSON.parse(input)
    const observation = await toolRegistry[action](params)

    // 5. 将 LLM 响应和 Observation 加入历史
    messages.push(
      {role: 'assistant', content: text},
      {role: 'user', content: `Observation: ${observation}`}
    )}}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36

Agent 的执行逻辑相对简单直接。首先用 Prompt 模板初始化消息，将工具列表和用户问题注入其中。然后进入主循环，不断调用 LLM 直到出现 `Final Answer` 标记。在每次循环中，解析 LLM 输出的 `Action` 和 `Action Input`，从工具注册表中找到对应的工具函数并执行，最后将执行结果作为 Observation 反馈给 LLM，开启下一轮循环。

# 运行结果示例


```
第一轮：
Thought: 我需要获取青岛啤酒的股票收盘价
Action: get_closing_price
Action Input: {"name": "青岛啤酒"}
→ Observation: 67.92

第二轮：
Thought: 现在需要获取贵州茅台的收盘价
Action: get_closing_price
Action Input: {"name": "贵州茅台"}
→ Observation: 1488.21

最终答案：
贵州茅台的股票收盘价（1488.21）比青岛啤酒（67.92）高得多

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14

# 1.4 使用 Function Call 来实现

前面展示的是经典的 ReAct 模式实现，需要通过 Prompt 让 LLM 输出特定格式（Thought/Action/Observation），然后手动解析这些文本。而现代 LLM API 都支持 **Function Calling**（函数调用），这让 ReAct 的实现变得更简单、更可靠。

# 核心代码实现

**1. 工具定义（标准 OpenAI 格式）**


```
import {ChatCompletionTool} from'openai/resources/chat/completions'

exportconst tools: ChatCompletionTool[] = [{
    type: 'function',
    function: {
      name: 'get_closing_price',
      description: '使用该工具获取指定股票的收盘价',
      parameters: {
        type: 'object',
        properties: {
          name: {
            type: 'string',
            description: '股票名称',
          },
        },
        required: ['name'],
      },
    },
  },
]

// 工具注册表
exportconst toolRegistry: Recordstring> = {
  get_closing_price: (params) => getClosingPrice(params.name),
}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27

**2. Agent 主循环（Function Call 版本）**


```
import {ChatCompletionTool} from'openai/resources/chat/completions'

exportconst tools: ChatCompletionTool[] = [{
    type: 'function',
    function: {
      name: 'get_closing_price',
      description: '使用该工具获取指定股票的收盘价',
      parameters: {
        type: 'object',
        properties: {
          name: {
            type: 'string',
            description: '股票名称',
          },
        },
        required: ['name'],
      },
    },
  },
]

// 工具注册表
exportconst toolRegistry: Recordstring> = {
  get_closing_price: (params) => getClosingPrice(params.name),
}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27

# 1.5 使用 LangGraph 实现

对于复杂的 Agent 场景（需要记忆、反思、人工介入等），LangGraph 提供了声明式的图结构定义，更易于维护和扩展。

LangGraph 将 Agent 建模为状态图，其中节点代表执行具体任务的函数，边定义节点之间的转换规则，而状态则是在各个节点之间传递的数据。这种抽象让 Agent 的执行流程更加清晰可控。

# 核心代码

**构建图：**


```
import {StateGraph, END} from'@langchain/langgraph'import {Annotation} from'@langchain/langgraph'

// 1. 定义状态
const GraphState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) => x.concat(y),
    default: () => [],
  }),
})

// 2. 定义节点
const llm = new ChatOpenAI({model: 'gpt-4o'}).bindTools(tools)

asyncfunction callModel(state: typeof GraphState.State) {
const response = await llm.invoke(state.messages)return {messages: [response]}}

asyncfunction callTools(state: typeof GraphState.State) {
const lastMessage = state.messages[state.messages.length - 1]
const toolMessages = awaitPromise.all(
    lastMessage.tool_calls.map(async (tc) => {
      const tool = tools.find((t) => t.name === tc.name)
      const result = await tool.invoke(tc.args)
      returnnew ToolMessage({content: String(result), tool_call_id: tc.id})
    }))return {messages: toolMessages}}

// 3. 路由函数
function shouldContinue(state: typeof GraphState.State) {
const lastMessage = state.messages[state.messages.length - 1]return lastMessage.tool_calls?.length > 0 ? 'tools' : END
}

// 4. 构建图
function buildGraph() {
returnnew StateGraph(GraphState)
    .addNode('agent', callModel)
    .addNode('tools', callTools)
    .addEdge('__start__', 'agent')
    .addConditionalEdges('agent', shouldContinue)
    .addEdge('tools', 'agent')
    .compile()}

// 5. 运行
const app = buildGraph()
await app.invoke({messages: [new HumanMessage('问题')]})
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50
- 51

其实 `@langchain/langgraph` 提供了 `createReactAgent`，可以更加方便的实现类似功能：


```
import {createReactAgent} from'@langchain/langgraph/prebuilt'import {ChatOpenAI} from'@langchain/openai'import {tool} from'@langchain/core/tools'import {z} from'zod'

// 定义工具
const getClosingPriceTool = tool((input) => {
    const name = (input as {name: string}).name
    if (name === '青岛啤酒') return'67.92'
    if (name === '贵州茅台') return'1488.21'
    return'未搜到该股票'},
  {
    name: 'get_closing_price',
    description: '获取指定股票的收盘价',
    schema: z.object({name: z.string().describe('股票名称')}),
  })

// 创建 Agent（一行代码）
const agent = createReactAgent({
  llm: new ChatOpenAI({model: 'gpt-4o'}),
  tools: [getClosingPriceTool],
})

// 运行
const result = await agent.invoke({
  messages: [{role: 'user', content: '比较青岛啤酒和贵州茅台的收盘价'}],
})
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30

# 1.6 适用场景

ReAct 模式特别适合需要外部信息或工具支持的任务。当问题无法仅凭 LLM 内部知识解决时，比如查询实时数据、调用 API、执行计算等，ReAct 通过工具调用弥补了 LLM 的能力边界。这种模式对于多步骤推理任务也很有效，Agent 可以逐步收集信息、分析结果、调整策略，最终得出答案。同时，ReAct 的透明性让整个推理过程可观察可调试，便于理解 Agent 的决策逻辑。

# 1.7 注意事项

实现 ReAct 模式时需要注意几个关键点。Prompt 设计至关重要，需要清晰地定义 Thought、Action、Observation 的格式，并提供足够的示例帮助 LLM 理解预期输出。工具描述要准确明确，让 LLM 能够正确选择和使用工具。同时要设置合理的迭代次数上限，避免陷入无限循环。错误处理机制也不可忽视，当工具调用失败或 LLM 输出格式错误时，需要有恰当的降级策略。此外，要注意 Token 消耗，因为每次迭代都会增加消息历史的长度。

# 二、CodeAct 模式

# 2.1 核心理念

CodeAct（Code as Action）让 Agent 通过生成并执行代码来完成任务。与 ReAct 调用预定义工具不同，CodeAct 赋予 Agent 更大的灵活性，特别适合复杂计算、数据处理或需要组合多个操作的场景。核心流程是：Thought → Code Generation → Code Execution → Observation。

# 2.2 工作流程

CodeAct 的执行流程从 LLM 分析用户问题开始，理解需要完成什么任务。接着 LLM 生成对应的代码（通常是 Python 或 JavaScript），这些代码会在沙箱环境中执行以保证安全性。执行结果作为 Observation 返回给 LLM，LLM 根据结果判断是继续生成新代码完善方案，还是已经得到满意答案可以结束流程。

# 2.3 实战案例

**需求：** 计算 1~100 的和

# 核心代码

**1. 提示词（Prompt）**


```
// prompts.ts
export const SYSTEM_PROMPT = `你是一个能够编写和执行代码的智能助手。
当用户提出问题时，你需要：
1. 分析问题并确定需要编写什么代码
2. 编写能解决问题的 JavaScript 代码
3. 代码必须将最终结果存储在 'result' 变量中
4. 将代码包裹在 \`\`\`javascript 代码块中
5. 分析执行结果，如果有错误则修改代码再次执行
6. 最终给用户提供答案`

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9

**2. 工具（代码执行器）**


```
// tools.ts
import {z} from'zod'import {tool} from'@langchain/core/tools'import vm from'vm'

exportconst executePythonTool = tool((input) => {
    const code = (input as {code: string}).code
    try {
      console.log('执行代码:\n', code)

      // 使用 vm 创建沙箱环境
      const context = {result: undefined, console}
      vm.createContext(context)
      vm.runInContext(code, context, {timeout: 5000})

      const result = context.result ?? '执行成功'
      console.log('执行结果:\n', result)
      returnString(result)
    } catch (error: any) {
      return`代码执行错误: ${error.message}`
    }},
  {
    name: 'execute_javascript',
    description: '执行 JavaScript 代码并返回结果',
    schema: z.object({
      code: z.string().describe('要执行的 JavaScript 代码'),
    }),
  })
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31

**3. Agent 逻辑（LangGraph）**


```
// graph.ts
import {StateGraph, END} from'@langchain/langgraph'import {Annotation} from'@langchain/langgraph'import {ChatOpenAI} from'@langchain/openai'import {AIMessage, HumanMessage, SystemMessage} from'@langchain/core/messages'import {SYSTEM_PROMPT} from'./prompts'import {executePythonTool} from'./tools'

// 定义状态
const CodeActState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) => x.concat(y),
    default: () => [],
  }),
  output: Annotation({default: () => ''}),
userPrompt: Annotation({default: () => ''}),
})

constllm = newChatOpenAI({model: 'gpt-4o'})

// 提取代码
functionextractCode(content: string) {if (content.includes('```javascript')) {
    constblocks = content.split('```javascript')
    constcode = blocks[1].split('```')[0].trim()
    returncode
  }
returnnull
}

// LLM 节点
asyncfunctionllmCall(state: typeof CodeActState.State) {
constmessages = [
    newSystemMessage(SYSTEM_PROMPT),
    newHumanMessage(state.userPrompt),
    ...state.messages,
  ]

constresponse = awaitllm.invoke(messages)
constcode = extractCode(response.content as string)

if (code) {
    return {
      messages: [response],
      output: '',
      code,
    }}

return {
    messages: [response],
    output: response.content,
  }}

// 路由函数
functionshouldExecute(state: typeof CodeActState.State) {
returnstate.output ? END : 'executeNode'}

// 执行节点
asyncfunctionexecuteNode(state: typeof CodeActState.State) {
constcode = (state as any).code
constresult = awaitexecutePythonTool.invoke({code})

return {
    messages: [newHumanMessage(`## 执行结果:\n${result}`)],}}

// 构建图
exportfunctionbuildCodeActGraph() {
returnnewStateGraph(CodeActState)
    .addNode('llmCall', llmCall)
    .addNode('executeNode', executeNode)
    .addEdge('__start__', 'llmCall')
    .addConditionalEdges('llmCall', shouldExecute)
    .addEdge('executeNode', 'llmCall')
    .compile()}
```
智能体编程bash

**4. 运行**


```
const agent = buildCodeActGraph()
const result = await agent.invoke({
  userPrompt: '请计算 1~100 的和',
})
console.log(result.output)
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5

# 运行效果


```
[启动 CodeAct Agent][用户问题] 请计算 1~100 的和


[LLM 节点] 分析问题...
[生成代码]

[执行节点] 运行代码...
## 执行代码:let n = 100;let result = (n * (n + 1)) / 2;
result;## 执行结果:
 执行成功

[LLM 节点] 分析问题...
[直接给出答案]

[完成]

[最终答案]
 很好！结果表明，1 到 100 的和是 5050。您是否还有其他数学问题或需要进一步的帮助？

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22

从结果可以看到，大模型并没有使用循环，而是用等差数列求和公式来实现的，有点聪明的样子。

# 2.4 适用场景

CodeAct 模式特别适合需要灵活处理数据或进行复杂计算的场景。当任务涉及数学计算、数据转换、文本处理、算法实现等需要编程逻辑的操作时，生成代码往往比调用预定义工具更加高效和灵活。同时，对于需要组合多个操作或处理非标准化数据的任务，CodeAct 也展现出明显优势。这种模式让 Agent 不再局限于现有工具的能力边界，可以根据具体需求动态生成解决方案。

# 2.5 注意事项

使用 CodeAct 模式时必须高度重视安全性问题。代码执行必须在沙箱环境中进行，避免恶意代码对系统造成破坏。建议使用 vm 模块或 Docker 容器等隔离机制，并设置执行超时限制防止无限循环。此外，生成的代码质量依赖于 LLM 的能力，可能存在语法错误或逻辑错误，需要完善的错误处理机制。对于生产环境，还应该记录所有执行的代码以便审计和调试。

# 三、计划模式（Plan Mode）

# 3.1 核心理念

计划模式采用"先计划，后执行"的策略。ReAct 每步都需重新思考，适合探索性任务；计划模式则在开始时制定完整方案再逐步执行，更适合结构化程度高的任务。优势在于执行路径清晰、便于监控进度和预测资源消耗。但灵活性较低，初始计划不准确时可能需要人工调整。

# 3.2 工作流程

# 3.3 实战案例:简单计划模式

**需求：** 比较茅台和青岛啤酒哪个贵？

# 核心代码

**1. 计划生成提示词**


```
// prompts.ts
export const PLAN_PROMPT = `你是一个金融分析师，擅长对股票的收盘价进行比较。
请为用户提出的问题创建分析方案步骤：

可调用工具列表：
get_closing_price: 根据股票名称获取收盘价

要求：
1. 用中文列出清晰步骤
2. 每个步骤标记序号
3. 明确说明需要分析和执行的内容
4. 只需输出计划内容，不要做任何额外的解释和说明`

export const PLAN_EXECUTE_PROMPT = `你是一个思路清晰，有条理的金融分析师，
必须严格按照以下计划执行：

当前计划：
{plan}

如果你认为计划已经执行到最后一步了，请在内容的末尾加上 Final Answer 字样`
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20

**2. 状态定义**


```
// types.ts
export const PlanState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) => x.concat(y),
    default: () => [],
  }),
  plan: Annotation({
    reducer: (x, y) => y ?? x,
    default: () => '',
  }),
})
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11

**3. 工作流构建**


```
// graph.ts
// 计划节点：生成执行计划
asyncfunction planNode(state: typeof PlanState.State) {
const response = await llm.invoke([
    new SystemMessage(PLAN_PROMPT),
    state.messages[0],
  ])

const plan = response.content asstring
console.log('[计划内容]\n', plan)

return {plan}}

// 执行节点：按计划执行并调用工具
asyncfunction executeNode(state: typeof PlanState.State) {
const messages = [
    new SystemMessage(PLAN_EXECUTE_PROMPT.replace('{plan}', state.plan)),
    ...state.messages,
  ]

const response = await llmWithTools.invoke(messages)return {messages: [response]}}

// 工具节点：执行工具调用
asyncfunction toolNode(state: typeof PlanState.State) {
const lastMessage = state.messages[state.messages.length - 1]
const toolCalls = lastMessage.tool_calls || []

const toolMessages = awaitPromise.all(
    toolCalls.map(async (tc) => {
      const tool = toolsByName[tc.name]
      const result = await tool.invoke(tc.args)
      returnnew ToolMessage({
        content: String(result),
        tool_call_id: tc.id,
      })
    }))

return {messages: toolMessages}}

// 路由函数
function shouldContinue(state: typeof PlanState.State): string {
const content = state.messages[state.messages.length - 1].content
return content.includes('Final Answer') ? END : 'toolNode'}

// 构建图
exportfunction buildPlanGraph() {
returnnew StateGraph(PlanState)
    .addNode('planNode', planNode)
    .addNode('executeNode', executeNode)
    .addNode('toolNode', toolNode)
    .addEdge('__start__', 'planNode')
    .addEdge('planNode', 'executeNode')
    .addConditionalEdges('executeNode', shouldContinue)
    .addEdge('toolNode', 'executeNode')
    .compile()}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50
- 51
- 52
- 53
- 54
- 55
- 56
- 57
- 58
- 59
- 60
- 61
- 62

# 运行效果


```
[启动计划模式 Agent][用户问题] 茅台和青岛啤酒哪个贵？

[计划节点] 生成执行计划...
[计划内容]1. 获取贵州茅台的股票收盘价
2. 获取青岛啤酒的股票收盘价
3. 比较两者的收盘价，确定哪个更贵

[执行节点] 按计划执行...
[工具节点] 执行工具...
   执行: get_closing_price({"name":"贵州茅台"})
   结果: 1488.21

[执行节点] 按计划执行...
[工具节点] 执行工具...
   执行: get_closing_price({"name":"青岛啤酒"})
   结果: 67.92

[执行节点] 按计划执行...
[完成]

[最终答案]
根据收盘价比较：
- 贵州茅台：1488.21 元
- 青岛啤酒：67.92 元

结论：贵州茅台更贵
Final Answer

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29

# 3.4 高级计划模式：动态调整

简单计划模式的局限是**计划一旦生成就固定不变**。高级计划模式引入了**动态重新规划**能力，可以根据执行结果调整剩余步骤，下面我们来改进一下。

# 工作流程

# 代码示例

**1. Prompt 设计**


```
// 执行助手 Prompt（用于 ReAct Agent）
export const SYSTEM_PROMPT = `你是一个任务执行助手`

// 计划评估 Prompt（核心：引导 LLM 动态调整计划）
export const PLAN_PROMPT = `你是一个计划评估助手，负责根据已完成的步骤评估任务进度，并动态调整后续计划。

你的目标:
{input}

原始计划:
{plan}

已完成的步骤及结果:
{past_steps}

核心规则：
1. 仔细分析已完成步骤的结果
2. 根据实际情况调整后续计划：
   - 如果发现需要补充新步骤，添加到计划中
   - 如果发现某些步骤不再需要，从计划中移除
   - 如果发现步骤顺序不合理，调整执行顺序

输出格式（必须严格遵守）：
- 如果任务已完成：直接输出答案，不要使用列表格式
- 如果还需继续：只输出步骤列表（每行一个，使用 "- " 开头）

注意：不要在步骤列表中混入解释性文字，只输出纯粹的步骤列表`
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27

**2. 执行节点（使用 ReAct Agent）**


```
import {createReactAgent} from'@langchain/langgraph/prebuilt'import {ChatOpenAI} from'@langchain/openai'

// 创建 LLM 实例
const llm = new ChatOpenAI({
  modelName: 'gpt-4o',
  apiKey: process.env.API_KEY || '',
})

// 创建 ReAct Agent 作为执行器
const executeAgent = createReactAgent({
  llm,
  tools, // 工具列表：getClosingPriceTool, calculatorTool 等
  messageModifier: SYSTEM_PROMPT,
})

// 执行节点：执行当前计划的第一步
asyncfunction executeStep(state: typeof PlanExecuteState.State) {
const plan = state.plan
if (!plan || plan.length === 0) {
    return {pastSteps: []}}

// 格式化任务描述
const planStr = plan.map((step, i) =>`${i + 1}. ${step}`).join('\n')
const task = plan[0]
const taskFormatted = `计划有以下几个步骤:\n${planStr}\n\n你需要执行 步骤1. ${task}.`

// 使用 ReAct Agent 执行
const agentResponse = await executeAgent.invoke({
    messages: [['user', taskFormatted]],
  })

// 提取执行结果
const lastMessage = agentResponse.messages[agentResponse.messages.length - 1]
const result = lastMessage?.content asstring

// 记录到执行历史
return {
    pastSteps: [[task, result]] asArray<[string, string]>,
  }}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42

**3. 规划评估节点（核心：动态调整）**


```
// 规划评估节点
asyncfunction planStep(state: typeof PlanExecuteState.State) {
// 格式化当前状态
const planStr = state.plan.map((step, i) =>`${i + 1}. ${step}`).join('\n')
const pastStepsStr = state.pastSteps
    .map(([task, result]) =>`- ${task}\n  结果: ${result}`)
    .join('\n')

// 构建评估提示词
const prompt = PLAN_PROMPT.replace('{input}', state.input)
    .replace('{plan}', planStr)
    .replace('{past_steps}', pastStepsStr || '无')

// 获取 LLM 评估结果
const response = await llm.invoke(prompt)
const content = response.content asstring

// 先尝试提取步骤列表
const newPlan = extractPlanFromResponse(content)

// 如果提取到步骤，说明需要继续执行
if (newPlan.length > 0) {
    // 对比原计划，检测是否有调整
    const originalRemaining = state.plan.slice(1)
    if (JSON.stringify(newPlan) !== JSON.stringify(originalRemaining)) {
      console.log('[计划调整] 检测到计划变更')
      console.log('[原计划]', originalRemaining)
      console.log('[调整后]', newPlan)
    }
    return {plan: newPlan}}

// 没有步骤列表，说明任务完成
return {response: content}}

// 辅助函数：从 LLM 响应中提取步骤列表
function extractPlanFromResponse(response: string): string[] {
const lines = response.split('\n')
const steps: string[] = []

for (const line of lines) {
    const trimmed = line.trim()
    // 匹配 "- 步骤" 或 "1. 步骤" 格式
    if (trimmed.match(/^[-*]\s+(.+)$/)) {
      const step = trimmed.replace(/^[-*]\s+/, '').trim()
      if (step) steps.push(step)
    } elseif (trimmed.match(/^\d+[\.)]\s+(.+)$/)) {
      const step = trimmed.replace(/^\d+[\.)]\s+/, '').trim()
      if (step) steps.push(step)
    }}

return steps
}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50
- 51
- 52
- 53
- 54
- 55

**4. 构建 LangGraph 工作流**


```
import {StateGraph, END} from'@langchain/langgraph'

// 路由函数：决定继续还是结束
function shouldEnd(state: typeof PlanExecuteState.State): string {return state.response ? END : 'execute'}

// 构建工作流
const workflow = new StateGraph(PlanExecuteState)
  .addNode('execute', executeStep) // 执行节点
  .addNode('planstep', planStep) // 规划节点
  .addEdge('__start__', 'execute') // 开始 → 执行
  .addEdge('execute', 'planstep') // 执行 → 规划
  .addConditionalEdges('planstep', shouldEnd, {
    execute: 'execute', // 继续执行
    [END]: END, // 结束
  })

const app = workflow.compile()
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19

# 运行示例（体现动态调整）

故意给一个不完整的初始计划，让 Agent 根据中间结果动态补充步骤。


```
[启动高级计划模式 Agent][目标] 仅根据收盘价帮我分析一下青岛啤酒和贵州茅台的投资价值对比，低的更有价值
[初始计划]1. 获取青岛啤酒的股票收盘价

[执行节点] 执行当前步骤...
[任务]
计划有以下几个步骤:
1. 获取青岛啤酒的股票收盘价

你需要执行 步骤1. 获取青岛啤酒的股票收盘价.
[执行结果] 青岛啤酒的股票收盘价是67.92元。

[规划节点] 评估并调整计划...
[LLM 评估]
- 获取贵州茅台的股票收盘价
- 比较青岛啤酒和贵州茅台的股票收盘价
- 分析投资价值并确定哪一个更有价值

[计划调整] 检测到计划变更
[原计划剩余步骤][调整后的计划]1. 获取贵州茅台的股票收盘价
  2. 比较青岛啤酒和贵州茅台的股票收盘价
  3. 分析投资价值并确定哪一个更有价值

[执行节点] 执行当前步骤...
[任务]
计划有以下几个步骤:
1. 获取贵州茅台的股票收盘价
2. 比较青岛啤酒和贵州茅台的股票收盘价
3. 分析投资价值并确定哪一个更有价值

你需要执行 步骤1. 获取贵州茅台的股票收盘价.
[执行结果] 贵州茅台的股票收盘价是1488.21。接下来需要进行比较和分析投资价值的步骤。

[规划节点] 评估并调整计划...
[LLM 评估]
青岛啤酒的投资价值更高。

[决策] 无后续步骤，任务完成

[完成]

[最终答案]
 青岛啤酒的投资价值更高。

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46

# 3.5 适用场景

计划模式最适合需求明确、步骤可预测的结构化任务。当任务目标清晰、可分解为多个具体步骤时，先制定计划再执行能够提供更好的可控性和可预测性。这种模式特别适合数据分析、报告生成、多步骤查询等场景。对于需要监控执行进度或预估完成时间的任务，计划模式的优势更加明显。同时，当需要优化执行顺序或并行处理某些步骤时，有了明确的计划更容易进行调度优化。

# 3.6 注意事项

使用计划模式需要权衡灵活性和可控性。如果任务的不确定性较高，初始计划可能不够准确，需要考虑引入动态调整机制（如高级计划模式）。计划生成的质量直接影响最终效果，需要精心设计计划生成的 Prompt，提供清晰的指导和示例。执行过程中可能遇到计划中未预见的情况，需要有合适的异常处理策略。此外，过于详细的计划可能限制 Agent 的灵活性，而过于粗略的计划又可能起不到指导作用，需要根据具体任务找到平衡点。

# 四、反思模式（Reflection Mode）

# 4.1 核心理念

反思模式模拟人类"先写初稿，再反复修改"的创作过程，通过自我评估和迭代改进来提升输出质量。这种模式特别适合对输出质量要求较高的场景，通过引入一个独立的反思环节来审视当前方案的不足之处。

# 4.2 工作流程

反思模式包含三个阶段的循环：生成阶段根据需求和反思建议生成方案，反思阶段多维度检查方案并提出改进建议，决策阶段判断是否继续优化。循环持续进行直到达到质量标准或迭代次数上限。

# 4.3 核心代码

反思模式的实现包含状态定义、Prompt 设计、生成节点、反思节点和决策函数几个关键部分。

**状态定义：**


```
export const ReflectionState = Annotation.Root({
  userQuery: Annotation(), // 用户需求
  bestCommand: Annotation(), // 当前最优方案
  reflection: Annotation(), // 反思记录
  iterations: Annotation(), // 迭代次数
})
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6

**Prompt 设计：**

反思模式的核心在于两个高质量的 Prompt。生成 Prompt 用于根据需求和反思建议生成或改进方案：


```
export const COMMAND_PROMPT = `你是一个资深Linux运维专家，请根据用户需求生成最合适的Linux命令。

要求：
1. 只输出可直接执行的命令
2. 优先使用性能最好的方案

用户需求：{user_query}
当前方案：{best_command}
改进建议：{reflection}

请按以下格式输出：
命令：<生成的命令>`
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12

反思 Prompt 用于检查方案的合理性并提出改进建议：


```
export const REFLECTION_PROMPT = `请严格检查以下Linux命令的合理性：
{command}

检查维度：
1. 是否符合POSIX标准
2. 是否有更高效的替代方案
3. 是否完全解决用户需求
4. 是否好维护

用户原始需求：{user_query}

请返回结构化的检查结果：
- needsImprovement: 是否需要改进（true/false）
- suggestions: 改进建议（包含发现的问题和具体优化方向，如果无需改进则说明"已达最优"）`
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14

**结构化输出格式：**


```
import {z} from 'zod'

// 反思结果的结构化输出
const ReflectionResultSchema = z.object({
  needsImprovement: z.boolean().describe('是否需要改进'),
  suggestions: z.string().describe('改进建议，包含发现的问题和优化方向'),
})
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7

**生成节点：**


```
async function generateCommand(state: ReflectionStateType) {
const iter = state.iterations
console.log(`[生成] 第 ${iter + 1} 次命令生成`)

let prompt: string
if (iter === 0) {
    // 第一次生成
    prompt = COMMAND_PROMPT.replace('{user_query}', state.userQuery)
      .replace('{best_command}', '无')
      .replace('{reflection}', '无')} else {
    // 根据反思结果改进
    prompt = COMMAND_PROMPT.replace('{user_query}', state.userQuery)
      .replace('{best_command}', state.bestCommand)
      .replace('{reflection}', state.reflection)}

const response = await llm.invoke(prompt)
const content = response.content asstring

// 提取命令（处理"命令："前缀）
const commandParts = content.split('命令：')
const command =
    commandParts.length > 1
      ? commandParts[1]?.trim() || content.trim()
      : content.trim()

console.log(`[命令] ${command}`)

return {
    bestCommand: command,
    iterations: iter + 1,
  }}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34

**反思节点：**


```
async function reflectAndOptimize(state: ReflectionStateType) {
console.log('[反思] 执行检查...')

const prompt = REFLECTION_PROMPT.replace(
    '{command}',
    state.bestCommand
  ).replace('{user_query}', state.userQuery)

try {
    // 使用结构化输出
    const structuredLlm = llm.withStructuredOutput(ReflectionResultSchema)
    const result = await structuredLlm.invoke(prompt)

    // 检查是否需要改进
    if (!result.needsImprovement) {
      console.log('[评估] 已经最优，无需改进')
      return {reflection: '已经最优，无需优化'}
    }

    console.log(`[建议] ${result.suggestions}`)
    return {reflection: result.suggestions}} catch (error) {
    console.error('[反思失败]', error)
    return {reflection: '反思检查失败'}}}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26

**决策函数：**


```
// 停止标志：发现这些关键词时立即停止
const STOP_SIGNS = ['安全隐患', '木马', '攻击']

function checkReflection(state: ReflectionStateType): string {
// 1. 检查是否已最优
if (
    state.reflection.includes('无建议') ||
    state.reflection.includes('无需优化')) {
    console.log('\n[结束] 已达到最优方案')
    return END
  }

// 2. 检查停止标志（安全问题等）
for (const stopSign of STOP_SIGNS) {
    if (state.reflection.includes(stopSign)) {
      console.log(`\n[结束] 检测到停止标志: ${stopSign}`)
      return END
    }}

// 3. 检查迭代次数上限
if (state.iterations >= 3) {
    console.log('\n[结束] 达到最大迭代次数 (3次)')
    return END
  }

// 4. 继续优化
console.log('[决策] 继续优化...')return'generate'}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31

**构建工作流：**


```
const workflow = new StateGraph(ReflectionState)
  .addNode('generate', generateCommand)
  .addNode('reflect', reflectAndOptimize)
  .addEdge('__start__', 'generate')
  .addEdge('generate', 'reflect')
  .addConditionalEdges('reflect', checkReflection, {
    generate: 'generate',
    [END]: END,
  })

const app = workflow.compile()
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11

# 4.4 运行示例

**场景：生成 Docker 命令**


```
[启动反思模式 Agent][需求] 使用docker创建nginx容器，端口映射8080:80


[生成] 第 1 次命令生成
[命令] docker run -d -p 8080:80 nginx

[反思] 执行检查...
[建议] ### 检查结果：

1. **是否符合POSIX标准**
   - Docker命令本身不在POSIX标准的范围内。POSIX主要用于异类系统的兼容性与命令行工具，而Docker作为一个应用层次的技术，自成一套工具集。因此，此项不适用。

2. **是否有更高效的替代方案**
   - **问题**：缺少对容器生命周期管理的基础设置。
   - **建议**：
     - 使用容器名：便于管理和识别。
       ```bash
       docker run -d --name my_nginx -p 8080:80 nginx
       ```

3. **是否完全解决用户需求**
   - **问题**：基本需求虽然实现，但缺少扩展性设置。
   - **建议**：
     - 定义具体的版本和配置映射：确保相同环境的一致性。
       ```bash
       docker run -d --name my_nginx -p 8080:80 -v /my/local/nginx.conf:/etc/nginx/nginx.conf nginx:1.21.6
       ```
     - 添加自动重启设置，提高容器的可用性。
       ```bash
       docker run -d --name my_nginx --restart unless-stopped -p 8080:80 nginx
       ```

4. **是否好维护**
   - **问题**：需要通过容器ID执行维护命令，不利于日常操作。
   - **建议**：
     - 使用可识别的容器名称：简化运维。
       ```bash
       docker run -d --name my_nginx -p 8080:80 nginx
       ```
     - 考虑使用 Docker Compose 管理复杂项目，提升可维护性。

### 综合结论：
- **需要改进**：True
- **改进建议**：通过增加容器名称、版本控制和配置映射等方式提高管理效率，增强容器运行的稳定性和可扩展性。同时，建议考虑使用 Docker Compose 简化多容器环境的管理。
[决策] 继续优化...

[生成] 第 2 次命令生成
[命令] docker run -d --name my_nginx -p 8080:80 -v /my/local/nginx.conf:/etc/nginx/nginx.conf nginx:1.21.6

[反思] 执行检查...
[评估] 已经最优，无需改进

[结束] 已达到最优方案

[完成]
最终命令: docker run -d --name my_nginx -p 8080:80 -v /my/local/nginx.conf:/etc/nginx/nginx.conf nginx:1.21.6

```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34
- 35
- 36
- 37
- 38
- 39
- 40
- 41
- 42
- 43
- 44
- 45
- 46
- 47
- 48
- 49
- 50
- 51
- 52
- 53
- 54
- 55
- 56
- 57

# 4.5 适用场景

反思模式最适合对输出质量有较高要求的场景。当需要生成文档、代码、配置文件、命令等关键输出时，通过反思机制可以显著提升方案的完整性和可靠性。这种模式特别适合技术方案设计、代码审查、内容创作等需要经过多次打磨才能达到专业标准的任务。同时，对于那些有明确质量评估标准的任务，反思模式能够系统性地检查各个维度是否达标。

# 4.6 注意事项

使用反思模式时需要注意控制迭代次数，避免过度优化导致效率低下或陷入无限循环。建议设置合理的迭代上限（通常 2-3 次即可），并定义清晰的停止条件。反思 Prompt 的设计至关重要，需要明确具体的检查维度和评估标准，避免模糊的评价导致反思效果不佳。此外，反思模式会增加 LLM 调用次数和 Token 消耗，需要在质量和成本之间做好平衡。对于某些已经足够好的初始方案，过度的反思可能反而引入不必要的修改。



---

# 五、人机协作模式（Human-in-the-Loop）

# 5.1 核心理念

人机协作模式将 Agent 的自动化能力与人类判断力相结合。适用于关键决策（高风险操作需人工确认）、信息补全（缺少参数时询问用户）和质量控制（重要输出需人工审核）等场景。通过在关键节点暂停执行、等待人工输入、然后恢复执行，实现效率与可控性的平衡。

# 5.2 工作流程

流程图展示了一个核心循环和三条分支路径：

**核心循环：**


```
Input → LLM 推理 → 路由判断

```
智能体编程plaintext

- 1

**分支 1：人工交互路径（橙色）**


```
路由判断 → 暂停等待 → 用户输入 → LLM 推理（循环）

```
智能体编程plaintext

- 1
- **触发条件**：LLM 调用 `ask_user` 工具
- **核心机制**：`interrupt()` 暂停，等待用户输入，`resume` 恢复
- **应用场景**：缺少参数、需要用户确认、多选项决策

**分支 2：工具执行路径（紫色）**


```
路由判断 → 工具执行 → LLM 推理（循环）

```
智能体编程plaintext

- 1
- **触发条件**：LLM 调用普通工具
- **核心机制**：自动执行工具，结果反馈给 LLM
- **应用场景**：查询数据、计算处理、API 调用

**分支 3：完成路径（绿色虚线）**


```
路由判断 → Final Answer（结束）

```
智能体编程plaintext

- 1
- **触发条件**：LLM 判断已获得足够信息
- **核心机制**：返回最终结果，结束执行
- **应用场景**：问题解决、任务完成

实现依赖三个核心机制：中断机制通过 `interrupt()` 暂停执行并等待人工输入，状态保存机制使用 Checkpointer 保留所有上下文信息，恢复执行机制通过 `Command({ resume: userInput })` 从暂停点继续执行。

# 5.3 实战案例：购物助手

**场景：** 用户询问购买商品的总价，但没有说明数量，需要询问用户。

# 核心代码实现

**1. 工具定义**


```
import {tool} from'@langchain/core/tools'import {z} from'zod'

// 普通工具：获取商品价格
exportconst getPriceTool = tool(
async (input) => {
    const {product} = input as {product: string}
    const price = (Math.random() * 90 + 10).toFixed(2)
    return`商品${product}的价格为${price}元`},
  {
    name: 'get_price',
    description: '获取商品价格',
    schema: z.object({
      product: z.string().describe('商品名称'),
    }),
  })

// 特殊工具：询问用户（触发人工介入）
exportconst askUserTool = tool(
async (input) => {
    const {question} = input as {question: string}
    console.log('[需要询问用户]', question)
    return question
  },
  {
    name: 'ask_user',
    description: '询问用户进一步的需求，如用户要多少件商品、要什么商品等',
    schema: z.object({
      question: z.string().describe('需要询问用户的问题'),
    }),
  })
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34

**关键点：**

- `ask_user` 是一个特殊工具，用于触发人工介入
- LLM 会在需要用户信息时自动调用这个工具

**2. 人工节点（核心）**


```
import {tool} from'@langchain/core/tools'import {z} from'zod'

// 普通工具：获取商品价格
exportconst getPriceTool = tool(
async (input) => {
    const {product} = input as {product: string}
    const price = (Math.random() * 90 + 10).toFixed(2)
    return`商品${product}的价格为${price}元`},
  {
    name: 'get_price',
    description: '获取商品价格',
    schema: z.object({
      product: z.string().describe('商品名称'),
    }),
  })

// 特殊工具：询问用户（触发人工介入）
exportconst askUserTool = tool(
async (input) => {
    const {question} = input as {question: string}
    console.log('[需要询问用户]', question)
    return question
  },
  {
    name: 'ask_user',
    description: '询问用户进一步的需求，如用户要多少件商品、要什么商品等',
    schema: z.object({
      question: z.string().describe('需要询问用户的问题'),
    }),
  })
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21
- 22
- 23
- 24
- 25
- 26
- 27
- 28
- 29
- 30
- 31
- 32
- 33
- 34

**关键点：**

- `interrupt()` 会暂停整个工作流的执行
- 返回的值会在恢复执行时作为 `resume` 参数传入
- 用户输入被封装成 `ToolMessage` 返回给 LLM

**3. 路由函数（识别触发时机）**


```
function enterTools(state: HumanLoopStateType): string {
const lastMessage = state.messages[state.messages.length - 1]
const toolCalls = lastMessage.tool_calls

if (!toolCalls || toolCalls.length === 0) {
    return END
  }

const toolName = toolCalls[0].name

// 如果是 ask_user，进入人工节点
if (toolName === 'ask_user') {
    return'humanNode'}

// 否则进入工具节点
return'toolNode'}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18

**4. 构建 LangGraph（必须使用 Checkpointer）**


```
import {StateGraph, START, END} from'@langchain/langgraph'import {MemorySaver} from'@langchain/langgraph'

function buildHumanLoopGraph() {
const workflow = new StateGraph(HumanLoopState)
    .addNode('llmNode', llmNode)
    .addNode('humanNode', humanNode)
    .addNode('toolNode', toolNode)
    .addEdge(START, 'llmNode')
    .addConditionalEdges('llmNode', enterTools, {
      humanNode: 'humanNode',
      toolNode: 'toolNode',
      [END]: END,
    })
    .addEdge('toolNode', 'llmNode')
    .addEdge('humanNode', 'llmNode')

// 必须使用 checkpointer 来保存状态
const memory = new MemorySaver()return workflow.compile({checkpointer: memory})}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13
- 14
- 15
- 16
- 17
- 18
- 19
- 20
- 21

**关键点：**

- 人机协作模式**必须**配置 `checkpointer`
- `MemorySaver` 将状态保存在内存中（生产环境可用数据库）

**5. 运行 Agent（两阶段执行）**


```
export asyncfunction runHumanLoopAgent(
  query: string,
  getUserInput: () => Promise): Promise {
const app = buildHumanLoopGraph()
const threadConfig = {configurable: {thread_id: '123'}}

// 第一次启动
let result = await app.invoke({query, messages: []}, threadConfig)

// 检查是否需要人工输入
const lastMessage = result.messages[result.messages.length - 1]if (lastMessage.tool_calls?.[0]?.name === 'ask_user') {
    console.log('\n[等待用户输入...]')
    const userInput = await getUserInput()

    // 恢复执行（关键：使用 Command + resume）
    result = await app.invoke(new Command({resume: userInput}), threadConfig)}

return result.messages[result.messages.length - 1].content
}
```
智能体编程bash

**关键点：**

1. 第一次 `invoke` 会执行到 `interrupt` 处暂停
2. 获取用户输入后，通过 `Command({ resume: userInput })` 恢复
3. **必须使用相同的** `threadConfig` 才能恢复到正确的状态

# 运行效果


```
[启动人机协作模式 Agent][用户问题] 我想买一些苹果，总共需要多少钱

[LLM 分析] 需要知道用户要买多少苹果
[进入工具] ask_user
[参数] {question: '您想购买多少个苹果？'}

[需要询问用户] 您想购买多少个苹果？
[等待用户输入...]

请输入: 5个

[用户输入] 5个
[用户回答] 5个

[调用工具] get_price {product: '苹果'}
→ 商品苹果的价格为52.30元

[LLM 计算] 5个 × 52.30元 = 261.50元

[完成][最终答案] 您想购买5个苹果，总共需要261.50元

```
智能体编程bash

# 5.4 适用场景

人机协作模式在多种场景下都能发挥重要作用。对于敏感操作，比如删除数据、修改配置、执行系统命令等高风险动作，在执行前需要用户明确确认。可以通过定义 `confirm_operation` 工具，在执行前暂停并向用户展示即将执行的操作内容，等待用户审核通过后再继续。

在信息补全场景中，当 Agent 发现缺少必需参数、需要用户在多个选项中选择、或参数含义不明确时，可以暂停执行并向用户询问。这种交互式的信息收集方式比让 Agent 自行猜测要可靠得多。

质量控制是另一个重要应用场景。当 Agent 生成文档、代码、方案等内容后，可以暂停执行让用户审核输出质量。在关键决策点，人工判断往往比 LLM 的判断更可靠。此外，对于重要结果，在使用前进行人工验证可以避免潜在风险。

异常处理场景也很常见。当 Agent 遇到无法自动处理的情况时，与其直接失败不如暂停并请求人工帮助。用户可以提供额外信息、调整策略或从多个备选方案中选择，然后 Agent 继续执行。

# 5.5 高级用法

**1. 支持多轮人工介入**


```
async function runWithMultipleInterrupts(query: string) {
const app = buildHumanLoopGraph()
const config = {configurable: {thread_id: '123'}}

let input: any = {query, messages: []}

while (true) {
    const result = await app.invoke(input, config)

    // 检查是否完成
    if (!needsHumanInput(result)) {
      return result.messages[result.messages.length - 1].content
    }

    // 获取用户输入
    const userInput = await getUserInput()

    // 准备下一次调用
    input = new Command({resume: userInput})}}
```
智能体编程bash

**2. 支持用户取消**


```
const userInput = await getUserInput()

if (userInput === 'cancel' || userInput === '取消') {return '操作已取消'}

result = await app.invoke(new Command({resume: userInput}), config)
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7

**3. 添加超时处理**


```
const timeout = (ms: number) =>
newPromise((_, reject) => setTimeout(() => reject(newError('Timeout')), ms))

try {
const userInput = awaitPromise.race([
    getUserInput(),
    timeout(60000), // 60秒超时
  ])

  result = await app.invoke(new Command({resume: userInput}), config)} catch (error) {return'等待超时，操作已取消'}
```
智能体编程bash

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10
- 11
- 12
- 13

# 5.6 注意事项

实现人机协作模式时需要注意几个关键点。首先，必须配置 Checkpointer 来保存状态，这是整个模式的技术基础。可以选择 `MemorySaver` 用于开发和简单场景，或使用 `SqliteSaver` 等持久化方案用于生产环境。

Thread ID 的一致性至关重要。恢复执行时必须使用与暂停时相同的 `thread_id`，否则会导致状态丢失。在多用户场景下，务必为每个用户会话分配独立的 `thread_id` 以隔离状态，避免数据混淆。

输入验证不可忽视。用户可能输入无效内容、格式错误或超出预期范围的数据，需要实现完善的验证和错误处理机制。同时，应该设置合理的超时机制，避免 Agent 无限期等待用户输入。提供取消操作的选项也很重要，让用户可以随时中止流程。

# 六、总结

五种 Agent 设计模式各有侧重。ReAct 通过推理-行动循环适合处理需要外部工具的任务，CodeAct 通过代码生成解决复杂计算问题。计划模式提供结构化执行路径，简单版适合明确任务，高级版支持动态调整。反思模式通过迭代优化提升输出质量，人机协作模式在关键节点引入人工判断确保可控性。

实际应用中往往需要组合使用。建议从简单模式开始验证核心逻辑，逐步引入高级特性。根据任务特点权衡性能与准确性，同时做好日志监控和安全防护。通过理解这些模式的特点和适用场景，你可以构建高效可靠的 Agent 系统。

# 那么，如何系统的去学习大模型LLM？

作为一名从业五年的资深大模型算法工程师，我经常会收到一些评论和私信，我是小白，学习大模型该从哪里入手呢？我自学没有方向怎么办？这个地方我不会啊。如果你也有类似的经历，一定要继续看下去！这些问题啊，也不是三言两语啊就能讲明白的。

所以我综合了大模型的所有知识点，给大家带来一套**全网最全最细的大模型零基础教程**。在做这套教程之前呢，我就曾放空大脑，以一个大模型小白的角度去重新解析它，采用基础知识和实战项目相结合的教学方式，历时3个月，终于完成了这样的课程，让你真正体会到什么是每一秒都在疯狂输出知识点。

由于篇幅有限，⚡️ 朋友们如果有需要全套 《**2025全新制作的大模型全套资料**》，**扫码获取~**  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d14cb33bff1e46ebb618651bfeba7a3b.jpeg#pic_center)

# 为什么要学习大模型？

我国在A大模型领域面临人才短缺,数量与质量均落后于发达国家。2023年，人才缺口已超百万，凸显培养不足。随着AI技术飞速发展，预计到2025年,这一缺口将急剧扩大至400万,严重制约我国AI产业的创新步伐。加强人才培养,优化教育体系,国际合作并进是破解困局、推动AI发展的关键。

# 👉大模型学习指南+路线汇总👈

我们这套大模型资料呢，会从**基础篇、进阶篇和项目实战篇**等三大方面来讲解。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/718e40e9489741139c25f2d7941ec7db.png#pic_center)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/direct/d59f942c9a924dc2b1b529134fecd2fb.jpeg#pic_center)

# 👉①.基础篇👈

基础篇里面包括了Python快速入门、AI开发环境搭建及提示词工程，带你学习大模型核心原理、prompt使用技巧、Transformer架构和预训练、SFT、RLHF等一些基础概念，用最易懂的方式带你入门大模型。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/f857e19ae4c14237a544bdba8cd3521b.png#pic_center)

# 👉②.进阶篇👈

接下来是进阶篇，你将掌握RAG、Agent、Langchain、大模型微调和私有化部署，学习如何构建外挂知识库并和自己的企业相结合，学习如何使用langchain框架提高开发效率和代码质量、学习如何选择合适的基座模型并进行数据集的收集预处理以及具体的模型微调等等。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/709c908f5c7c4dce8e685c92fbf93a9b.png#pic_center)

# 👉③.实战篇👈

实战篇会手把手带着大家练习企业级的落地项目（已脱敏），比如RAG医疗问答系统、Agent智能电商客服系统、数字人项目实战、教育行业智能助教等等，从而帮助大家更好的应对大模型时代的挑战。  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/56c8d5ed017044d2abcd92354227bc51.png#pic_center)

# 👉④.福利篇👈

最后呢，会给大家一个小福利，课程视频中的所有素材，有搭建AI开发环境资料包，还有学习计划表，几十上百G素材、电子书和课件等等，只要你能想到的素材，我这里几乎都有。我已经全部上传到CSDN，朋友们如果需要可以微信扫描下方CSDN官方认证二维码免费领取【`保证100%免费`】  
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2bd8cd10ce6742ef823f73617bfdcbb3.jpeg#pic_center)  
`相信我，这套大模型系统教程将会是全网最齐全 最易懂的小白专用课！！`

您可能感兴趣的与本文相关的镜像

Seed-Coder-8B-Base

文本生成

Seed-Coder

Seed-Coder是一个功能强大、透明、参数高效的 8B 级开源代码模型系列，包括基础变体、指导变体和推理变体，由字节团队开源

一键部署运行  


  
确定要放弃本次机会？  


福利倒计时  


*:*  
  
*:*  
  


  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/vip-limited-close-roup.png)  
立减 ¥  
  


普通VIP年卡可用  


[立即使用](https://mall.csdn.net/vip)

[![](https://i-avatar.csdnimg.cn/ac028661e3c8470bbe2f7b3354687a32_kaka0722ww.jpg!1)  
  
deepseek大模型](https://blog.csdn.net/kaka0722ww)  


关注  
关注  


- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUpactive.png)  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/like-active.png)  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/like.png)  
  
12  
  
  


点赞
- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/unlike-active.png)  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/unlike.png)  
  
  


踩
- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/collect-active.png)  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/collect.png)  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/newCollectActive.png)  
  
19  
  
  


  
收藏  
  


  
觉得还不错?  
  
一键收藏  
  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/collectionCloseWhite.png)
- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward01.png)  
知道了  


[![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/comment.png)  
  
0](https://blog.csdn.net/kaka0722ww/article/details/155453725#commentBox)  


评论
- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/share.png)  
分享  
  


复制链接  


分享到 QQ  


分享到新浪微博  


![](https://csdnimg.cn/release/blogv2/dist/pc/img/share/icon-wechat.png)扫一扫
- ![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/more.png)  
  
  


![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/report.png)  
举报  
  


![](https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/report.png)  
举报

[详细解释什么叫*agent*中的*ReAct模式*](https://blog.csdn.net/weixin_39756314/article/details/144384491)

[AI生成曾小健3](https://blog.csdn.net/weixin_39756314)  


12-10  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1638  
  


[答案*ReAct模式*，即Reasoning and Acting的结合，是一种在*人工智能*代理（*Agent*）*开发*中广泛应用的设计思想。它强调推理（Reasoning）*与*行动（Acting）的有机结合，使得*Agent*能够在复杂和动态的环境中更有效地执行任务。](https://blog.csdn.net/weixin_39756314/article/details/144384491)

参与评论  
您还未登录，请先  
登录  
后发表或查看评论  


[【光子AI 】探索AI *Agent* *架构*师的30项*必备*修炼：一本全面*指南*](https://dreamit.blog.csdn.net/article/details/156435171)

[最新发布](https://dreamit.blog.csdn.net/article/details/156435171)

[AI天才研究院](https://blog.csdn.net/universsky2015)  


12-31  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
415  
  


[摘要 《探索AI *Agent架构*师的30项*必备*修炼》是一本面向AI *Agent架构*师的*实战指南*，基于作者团队在腾讯云等大厂的20多个AI *Agent*项目经验编写而成。全书从认知层、工程层和高阶层三个维度系统性地构建了AI *Agent架构*师的能力模型，包含30项针对性修炼内容。 书中首先通过一个电商售后AI *Agent*失败*案例*，揭示了行业痛点：大多数项目失败源于缺乏对AI *Agent核心*本质的理解。随后详细阐述了AI *Agent*的定义、边界分类、发展痛点和解决思路，并*与*传统Chatbot进行了多维度对比。全书](https://dreamit.blog.csdn.net/article/details/156435171)

[智能体AI *Agent*的极速入门：从*ReAct*、AutoGPT到AutoGen、Qwen*Agent*、X*Agent*、MetaGPT](https://devpress.csdn.net/v1/article/detail/135868163)

[热门推荐](https://devpress.csdn.net/v1/article/detail/135868163)

[结构之法 算法之道](https://blog.csdn.net/v_JULY_v)  


01-26  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1万+  
  


[*ReAct*其实不是一个刚出来的概念，它于2022年10月份便由Google Research 的 Brain Team 通过此篇论文《》提出来了，没错，又是Google的建设性工作之一，曾一度感觉，没有Google(毕竟*transformer*、指令微调、CoT等哪个不是Google的杰作，包括RLHF也是Google deepmind和OpenAI联合推出来的)，就没有后来的ChatGPT，^\_^考虑一个智能体*与*环境交互以解决任务的一般设置。](https://devpress.csdn.net/v1/article/detail/135868163)

[大厂*大模型*必知的*5*种*agent模式*](https://devpress.csdn.net/v1/article/detail/147722142)

[m0\_59235945的博客](https://blog.csdn.net/m0_59235945)  


05-05  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1247  
  


[该阶段让大家对*大模型* AI有一个最前沿的认识，对*大模型* AI 的理解超过 9*5*% 的人，可以在相关讨论时发表高级、不跟风、又接地气的见解，别人只会和 AI 聊天，而你能调教 AI，并能用代码将*大模型*和业务衔接。对全球*大模型*从性能、吞吐量、成本等方面有一定的认知，可以在云端和本地等多种环境下部署*大模型*，找到适合自己的项目/创业方向，做一名被 AI 武装的产品经理。由于新岗位的生产效率，要优于被取代岗位的生产效率，所以实际上整个社会的生产效率是提升的。天道酬勤，你越努力，就会成为越优秀的自己。](https://devpress.csdn.net/v1/article/detail/147722142)

[产品经理研读：*Agent*的九种*设计模式*(图解+代码)](https://devpress.csdn.net/v1/article/detail/140035898)

[zhishi0000的博客](https://blog.csdn.net/zhishi0000)  


06-28  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1180  
  


[好了，以上就是目前所总结的 *Agent* 九大*设计模式*，其实 *Agent* 中。](https://devpress.csdn.net/v1/article/detail/140035898)

[手把手教你！*Agent设计模式*，从入门到*实战*，一次搞定！](https://devpress.csdn.net/v1/article/detail/149742300)

[2401\_84494441的博客](https://blog.csdn.net/2401_84494441)  


07-29  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1000  
  


[本文系统梳理了五种主流*Agent设计模式*：1. *ReAct*（2022）：结合推理*与*行动的闭环系统，通过"思考-行动-观察"循环提升环境适应性，但存在延迟高、易漂移等问题；2. Plan-and-Execute：经典的两阶段"规划-执行"开环*模式*，适合结构化任务但缺乏灵活性；3. ReWoo（2023）：改进版规划*模式*，通过并行执行和独立求解模块提升效率；4. Reflexion（2023）：引入执行轨迹评估和反思机制的闭环系统，具备持续优化能力；*5*. ReflAct（202*5*）：实时目标对齐的微反思*模式*，将](https://devpress.csdn.net/v1/article/detail/149742300)

[AI应用*架构*师*必备*：智能数字资产流转平台的跨链交互*架构*设计*指南*（附协议*详解*）](https://blog.csdn.net/2501_91912247/article/details/150223307)

[AI 算法实战派](https://blog.csdn.net/2501_91912247)  


08-11  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1070  
  


[智能数字资产是指通过区块链技术确权、流转的AI相关无形资产，其*核心*特征是“可编程性”和“价值*与*功能绑定”——不仅可交易，还能通过智能合约触发特定功能（如调用AI模型推理、授权数据访问）。类型定义示例跨链需求AI模型资产以代码/参数形式存在的AI模型，通过NFT/Token化确权GPT-4模型参数NFT、Stable Diffusion权重Token跨链传输时需验证参数完整性、推理性能一致性训练数据资产标注数据、数据集的使用权或所有权凭证医疗影像标注数据集NFT、金融时序数据Token。](https://blog.csdn.net/2501_91912247/article/details/150223307)

[AIGC领域多模态*大模型*在游戏AI中的应用创新*案例*](https://dreamit.blog.csdn.net/article/details/147652993)

[AI天才研究院](https://blog.csdn.net/universsky2015)  


05-01  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
965  
  


[随着《塞尔达传说：王国之泪》《博德之门3》等现象级游戏的成功，游戏行业对AI技术的需求已从简单的路径规划升级为具备创意生成、自然交互和动态决策能力的智能系统。传统单模态AI（如纯文本对话模型或图像生成模型）难以处理游戏中复杂的多维度输入（如玩家语音、手势、场景图像），而多模态*大模型*通过融合文本、图像、语音、视频等多维度数据，为构建沉浸式游戏体验提供了革命性解决方案。智能NPC交互动态内容生成和玩家行为分析，结合具体技术*案例*解析其技术*架构*、算法实现和工程落地经验。*核心*概念。](https://dreamit.blog.csdn.net/article/details/147652993)

[【ESP32 Wi-Fi调试终极*指南*】：10大常见连接问题深度解析*与实战*解决方案](https://wenku.csdn.net/column/43s6pzof6e)

[ESP32 Wi-Fi连接的*核心*机制*与*工作原理 ## 1.1 ESP32 Wi-Fi协议栈*架构*解析 ESP32的Wi-Fi功能基于IEEE 802.11 b/g/n标准，集成于自研的PHY和MAC层硬件模块，并通过乐鑫专有的TCP/IP协议栈（LWIP）*与*上层应用交互。...](https://wenku.csdn.net/column/43s6pzof6e)

[Big Data 原理*与*代码*实战案例*讲解](https://blog.csdn.net/2401_85133351/article/details/141441204)

[AI大模型应用之禅](https://blog.csdn.net/2401_85133351)  


08-23  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
221  
  


[Big Data 原理*与*代码*实战案例*讲解  
作者：禅*与*计算机程序设计艺术 / Zen and the Art of Computer Programming  
1. 背景介绍  
1.1 问题的由来  
随着互联网、物联网、移动设备等](https://blog.csdn.net/2401_85133351/article/details/141441204)

[产品经理研读：*Agent*的九种*设计模式*(图解+代码)建议人手一份，*收藏*起来慢慢学！！](https://devpress.csdn.net/v1/article/detail/146499710)

[Gaga246的博客](https://blog.csdn.net/Gaga246)  


03-25  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1183  
  


[接下来讲讲每个*模式*的原理，以及代码实现(看代码能帮助产品经理加深理解，因为这些*设计模式*都是以结构化 prompt 的方式藏在代码里)。](https://devpress.csdn.net/v1/article/detail/146499710)

[每日论文速递 | *ReAct* Meets ActRe*:* *Agent*规划自主解释](https://blog.csdn.net/qq_27590277/article/details/137259140)

[zenRRan的博客](https://blog.csdn.net/qq_27590277)  


04-01  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
434  
  


[深度*学习*自然语言处理 分享整理：pp摘要：语言代理通过对基础模型进行推理，展示了自主决策能力。最近，人们开始利用多步骤推理和行动轨迹作为训练数据，努力训练语言代理以提高其性能。然而，收集这些轨迹仍然需要大量人力，要么需要人工注释，要么需要实现各种提示框架。在这项工作中，我们提出了 AT，这是一个能以 *ReAct* 风格实现代理轨迹自主注释的框架。其*核心*角色是一个 ActRe 提示代理，负责解释任意行...](https://blog.csdn.net/qq_27590277/article/details/137259140)

[*大模型Agent*五大工作*模式*深度解析](https://blog.csdn.net/qq_45066628/article/details/152372823)

[kuokay的博客](https://blog.csdn.net/qq_45066628)  


10-01  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1201  
  


[要理解一个*大模型Agent*如何工作，*核心*在于它背后所依赖的 工作*模式*。目前主流的*Agent*大多围绕五种关键*模式*：反射*模式*（Reflection pattern ）：让模型通过自我检视和修正提升推理能力；工具使用*模式*（ Tool use pattern）：赋予模型调用外部工具*与*系统的能力；*ReAct模式*（Reason and Act）：在推理*与*行动之间动态切换，实现更高效的决策；规划*模式*（Planning pattern）：让模型具备长期目标分解*与*任务执行的能力；](https://blog.csdn.net/qq_45066628/article/details/152372823)

[深度讲解智能体：*ReACT* *Agent*](https://devpress.csdn.net/v1/article/detail/150921347)

[Peter\_Changyb的博客](https://blog.csdn.net/Peter_Changyb)  


08-27  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1456  
  


[通过将推理*与*行动紧密结合，*ReACT* *Agent* 让大语言模型能交替生成推理轨迹（Thought）*与*特定任务行动（Action），开启了两者协同工作的新*模式*。  
MCP 服务器提供具体功能服务，包括暴露资源、提示模板和工具等能力。工作时，主机中的*大模型*通过客户端向服务器发送请求，服务器依据请求返回相应结果。](https://devpress.csdn.net/v1/article/detail/150921347)

[*收藏必备*！AI *Agent*五大*核心设计模式详解*：从*ReAct*到人机协作，助你构建智能系统](https://devpress.csdn.net/v1/article/detail/155229889)

[2401\_85327249的博客](https://blog.csdn.net/2401_85327249)  


11-25  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
864  
  


[本文系统介绍了五种AI *Agent核心设计模式*：*ReAct模式*通过推理-行动循环处理外部信息任务；CodeAct*模式*通过生成代码解决复杂计算；计划*模式*提供结构化执行路径；反思*模式*通过迭代优化提升输出质量；人机协作*模式*在关键节点引入人工判断。各*模式*有不同适用场景，实际应用中可组合使用，帮助*开发*者构建高效可靠的*Agent*系统。](https://devpress.csdn.net/v1/article/detail/155229889)

[*Agent*九种*设计模式*有哪些？看完你的AI*大模型*就很牛了！](https://blog.csdn.net/javatiange/article/details/151223724)

[javatiange的博客](https://blog.csdn.net/javatiange)  


09-05  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
1125  
  


[AI *Agent设计模式*概览 AI *Agent*通过感知、规划、行动三步骤动态完成任务，需具备推理、记忆、工具和行动四大模块。目前主流有9种*设计模式*，其中*5*种*核心模式*如下： *ReAct模式*：结合推理*与*行动，通过"行动-观察"循环动态调整策略，提升任务执行的连贯性和准确性。 Plan and Solve*模式*：先规划再执行，适用于多阶段任务（如烹饪），支持动态调整计划（如缺食材时新增步骤）。 REWOO*模式*：隐式观察依赖关系，适用于审批流等环环相扣的任务，通过链式计划自动传递上一步输出。 LL](https://blog.csdn.net/javatiange/article/details/151223724)

[*Agent*的九种*设计模式* 介绍](https://zhangjq.blog.csdn.net/article/details/147336474)

[ZJQ的博客](https://blog.csdn.net/qq_38998213)  


04-18  
![](https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png)  
432  
  


[原理：将推理（Reasoning）和行动（Acting）相结合，使*Agent*能够在推理的指导下采取行动，并根据行动的结果进一步推理，形成一个循环。*Agent*通过生成一系列的思维链（Thought Chains）来明确推理步骤，并根据推理结果执行相应的动作，*与*环境进行交互，获取反馈后再进行下一轮的推理和行动。应用场景：广泛应用于需要*与*外部环境进行交互并解决问题的场景，如知识问答、信息检索、任务规划等。](https://zhangjq.blog.csdn.net/article/details/147336474)

- [关于我们](https://www.csdn.net/company/index.html#about)
- [招贤纳士](https://www.csdn.net/company/index.html#recruit)
- [商务合作](https://fsc-p05.txscrm.com/T8PN8SFII7W)
- [寻求报道](https://marketing.csdn.net/questions/Q2202181748074189855)
- ![](https://g.csdnimg.cn/common/csdn-footer/images/tel.png)  
400-660-0108
- ![](https://g.csdnimg.cn/common/csdn-footer/images/email.png)  
[kefu@csdn.net](mailto:webmaster@csdn.net)
- ![](https://g.csdnimg.cn/common/csdn-footer/images/cs.png)  
[在线客服](https://csdn.s2.udesk.cn/im_client/?web_plugin_id=29181)
- 工作时间 8:30-22:00
- ![](https://g.csdnimg.cn/common/csdn-footer/images/badge.png)[公安备案号11010502030143](http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11010502030143)
- [京ICP备19004658号](http://beian.miit.gov.cn/publish/query/indexFirst.action)
- [京网文〔2020〕1039-165号](https://csdnimg.cn/release/live_fe/culture_license.png)
- [经营性网站备案信息](https://csdnimg.cn/cdn/content-toolbar/csdn-ICP.png)
- [北京互联网违法和不良信息举报中心](http://www.bjjubao.org/)
- [家长监护](https://download.csdn.net/tutelage/home)
- [网络110报警服务](https://cyberpolice.mps.gov.cn/)
- [中国互联网举报中心](http://www.12377.cn/)
- [Chrome商店下载](https://chrome.google.com/webstore/detail/csdn%E5%BC%80%E5%8F%91%E8%80%85%E5%8A%A9%E6%89%8B/kfkdboecolemdjodhmhmcibjocfopejo?hl=zh-CN)
- [账号管理规范](https://blog.csdn.net/blogdevteam/article/details/126135357)
- [版权与免责声明](https://www.csdn.net/company/index.html#statement)
- [版权申诉](https://blog.csdn.net/blogdevteam/article/details/90369522)
- [出版物许可证](https://img-home.csdnimg.cn/images/20250103023206.png)
- [营业执照](https://img-home.csdnimg.cn/images/20250103023201.png)
- ©1999-2026北京创新乐知网络技术有限公司

登录后您可以享受以下权益：

- 免费复制代码
- 和博主大V互动
- 下载海量资源
- 发动态/写文章/加入社区

×立即登录

评论   
![](https://csdnimg.cn/release/blogv2/dist/pc/img/closeBt.png)

![](https://csdnimg.cn/release/blogv2/dist/pc/img/commentArrowLeftWhite.png)被折叠的  条评论  
[为什么被折叠?](https://blogdev.blog.csdn.net/article/details/122245662)  
 [![](https://csdnimg.cn/release/blogv2/dist/pc/img/iconPark.png)到【灌水乐园】发言](https://bbs.csdn.net/forums/FreeZone)   


查看更多评论![](https://csdnimg.cn/release/blogv2/dist/pc/img/commentArrowDownWhite.png)

  
添加红包  
  


祝福语  


请填写红包祝福语或标题

红包数量  


个  


红包个数最小为10个

红包总金额  


元  


红包金额最低5元

余额支付  


  
当前余额3.43元  
[前往充值 >](https://i.csdn.net/#/wallet/balance/recharge)  


  
需支付：10.00元  


取消  
确定  


![](https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward02.png)  
下一步

![](https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward03.png)  
知道了

实付元

使用余额支付

![](https://csdnimg.cn/release/blogv2/dist/pc/img/pay-time-out.png)  
点击重新获取  


![](https://csdnimg.cn/release/blogv2/dist/pc/img/weixin.png)![](https://csdnimg.cn/release/blogv2/dist/pc/img/zhifubao.png)![](https://csdnimg.cn/release/blogv2/dist/pc/img/jingdong.png)扫码支付

钱包余额  
0  


抵扣说明：

1.余额是钱包充值的虚拟货币，按照1:1的比例进行支付金额的抵扣。  
2.余额无法直接购买下载，可以购买VIP、付费专栏及课程。

[![](https://csdnimg.cn/release/blogv2/dist/pc/img/recharge.png)余额充值](https://i.csdn.net/#/wallet/balance/recharge)  


确定取消![](https://csdnimg.cn/release/blogv2/dist/pc/img/closeBt.png)

举报

选择你想要举报的内容（必选）

- 内容涉黄
- 政治相关
- 内容抄袭
- 涉嫌广告
- 内容侵权
- 侮辱谩骂
- 样式问题
- 其他

原文链接（必填）

请选择具体原因（必选）

- 包含不实信息
- 涉及个人隐私

请选择具体原因（必选）

- 侮辱谩骂
- 诽谤

请选择具体原因（必选）

- 搬家样式
- 博文样式

补充说明（选填）

取消

确定

下载APP  


程序员都在用的中文IT技术交流社区

公众号  


专业的中文 IT 技术社区，与千万技术人共成长

视频号  


关注【CSDN】视频号，行业资讯、技术分享精彩不断，直播好礼送不停！

![](https://g.csdnimg.cn/side-toolbar/3.6/images/customer.png)  
客服  
  
  
  
  
![](https://g.csdnimg.cn/side-toolbar/3.6/images/totop.png)  
返回顶部  
  
  


