---
title: 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例_agent react模式-CSDN博客
created_at: 2026-01-03T04:42:19.086941+00:00
updated_at: 2026-04-06T13:19:11.457167+00:00
excerpt: 收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例_agent react模式-CSDN博客原文链接: https://blog.csdn.net/kaka0722ww/artic...
---

<h1 id="heading-0">收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例_agent react模式-CSDN博客</h1><p><strong>原文链接</strong>: <a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/kaka0722ww/article/details/155453725">https://blog.csdn.net/kaka0722ww/article/details/155453725</a></p><p><strong>摘要</strong>: 文章浏览阅读1k次，点赞12次，收藏19次。ReAct（Reasoning + Acting）是一种将推理（Reasoning）和行动（Acting）相结合的 Agent 设计模式。边思考、边行动、边观察结果，然后继续思考。这种模式特别适合处理需要外部信息或工具支持的任务。通过将复杂问题分解为多个"思考-行动-观察"的小步骤，Agent 能够逐步逼近最终答案，整个过程更加透明、可控。五种 Agent 设计模式各有侧重。ReAct 通过推理-行动循环适合处理需要外部工具的任务，CodeAct 通过代码生成解决复杂计算问题。_agent react模式</p><p><strong>关键词</strong>: agent react模式</p><p><strong>收藏时间</strong>: 2026/1/3 12:42:17</p><hr><h1 id="articleContentId">收藏必备：大模型Agent开发完全指南：5种核心设计模式详解与实战案例</h1><p>最新推荐文章于&nbsp;2025-12-31 01:18:20&nbsp;发布</p><p>原创 于 2025-12-01 15:51:14 发布 · 1k 阅读</p><p>· <img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/newHeart2023Active.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"> <img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/newHeart2023Black.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"> 12</p><p>· <img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollect2.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"> <img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/tobarCollectionActive2.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"> 19 ·</p><p>CC 4.0 BY-SA版权</p><p>版权声明：本文为博主原创文章，遵循<a target="_blank" rel="noopener" class="editor-link" href="http://creativecommons.org/licenses/by-sa/4.0/"> CC 4.0 BY-SA </a>版权协议，转载请附上原文出处链接和本声明。</p><p>文章标签：</p><p><a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#设计模式</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#人工智能</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=%E6%9E%B6%E6%9E%84&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#架构</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=transformer&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#transformer</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=%E5%A4%A7%E6%A8%A1%E5%9E%8B&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#大模型</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=%E5%A4%A7%E6%A8%A1%E5%9E%8B%E5%AD%A6%E4%B9%A0&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#大模型学习</a> <a target="_blank" rel="nofollow" class="editor-link tag-link-new" href="https://so.csdn.net/so/search/s.do?q=agent&amp;t=all&amp;o=vip&amp;s=&amp;l=&amp;f=&amp;viparticle=&amp;from_tracking_code=tag_word&amp;from_code=app_blog_art">#agent</a></p><p>部署运行你感兴趣的模型镜像一键部署</p><p>本文介绍5种AI Agent核心设计模式：ReAct模式通过推理与行动交替循环处理外部信息任务；CodeAct模式通过生成代码解决复杂计算；计划模式为结构化任务提供执行路径；反思模式通过迭代改进提升输出质量；人机协作模式在关键节点引入人工判断。每种模式均包含工作流程、实战案例和适用场景，帮助开发者构建高效可靠的Agent系统。</p><h1 id="heading-894">一、ReAct 模式</h1><h1 id="heading-906">1.1 什么是 ReAct</h1><p>ReAct（Reasoning + Acting）是一种将推理（Reasoning）和行动（Acting）相结合的 Agent 设计模式。它的核心思想是让 LLM 在解决问题时，不是一次性给出答案，而是模拟人类的思维过程：<strong>边思考、边行动、边观察结果，然后继续思考</strong>。</p><p>这种模式特别适合处理需要外部信息或工具支持的任务。通过将复杂问题分解为多个"思考-行动-观察"的小步骤，Agent 能够逐步逼近最终答案，整个过程更加透明、可控。</p><h1 id="heading-1138">1.2 工作流程</h1><p>ReAct 的核心流程可以概括为一个循环：Thought → Action → Observation → Thought。在每次循环中，Agent 首先进行思考阶段，分析当前问题和已有信息，决定下一步需要采取什么行动。例如，当需要查询股票价格时，Agent 会思考"我需要查询青岛啤酒的股票收盘价"。</p><p>接着进入行动阶段，Agent 选择合适的工具并指定参数，如 <code>Action: get_closing_price</code> 和 <code>Action Input: {"name": "青岛啤酒"}</code>。工具执行后进入观察阶段，将执行结果反馈给 Agent，例如 <code>Observation: 67.92</code>。Agent 收到观察结果后，会判断问题是否已经解决。如果未解决，则继续下一轮思考-行动-观察循环；如果已解决，则输出最终答案。</p><p>流程图展示了 ReAct 的完整执行过程。在底部的主流程中，Input 经过 LLM 推理后依次生成 Thought、Action、Action Input 和 PAUSE 标记。PAUSE 触发工具执行，执行结果形成 Observation 并返回给 LLM，由此形成一个闭环。当 LLM 判断已获得足够信息时，会从 Thought 节点输出 Final Answer，结束整个流程。</p><h1 id="heading-1702">1.3 实战案例</h1><h1 id="heading-1712">案例：比较两个股票的收盘价</h1><p><strong>任务：</strong> 请比较青岛啤酒和贵州茅台的股票收盘价谁高？</p><h1 id="heading-1754">核心代码实现</h1><p><strong>1. 工具定义与注册</strong></p><pre class="code-block"><code class="language-bash">// 工具定义（JSON Schema 格式）
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

// 工具注册表（工具名 -&gt; 实现函数）
const toolRegistry = {
  get_closing_price: (params) =&gt; getClosingPrice(params.name),
}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li></ul><p><strong>2. Prompt 模板（关键部分）</strong></p><pre class="code-block"><code class="language-bash">const REACT_PROMPT = `
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

New input: {input}`</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li></ul><p><strong>3. Agent 主循环（核心逻辑）</strong></p><pre class="code-block"><code class="language-bash">async function reactAgent(query: string) {
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
    )}}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li></ul><p>Agent 的执行逻辑相对简单直接。首先用 Prompt 模板初始化消息，将工具列表和用户问题注入其中。然后进入主循环，不断调用 LLM 直到出现 <code>Final Answer</code> 标记。在每次循环中，解析 LLM 输出的 <code>Action</code> 和 <code>Action Input</code>，从工具注册表中找到对应的工具函数并执行，最后将执行结果作为 Observation 反馈给 LLM，开启下一轮循环。</p><h1 id="heading-4124">运行结果示例</h1><pre class="code-block"><code class="language-bash">第一轮：
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
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li></ul><h1 id="heading-4485">1.4 使用 Function Call 来实现</h1><p>前面展示的是经典的 ReAct 模式实现，需要通过 Prompt 让 LLM 输出特定格式（Thought/Action/Observation），然后手动解析这些文本。而现代 LLM API 都支持 <strong>Function Calling</strong>（函数调用），这让 ReAct 的实现变得更简单、更可靠。</p><h1 id="heading-4659">核心代码实现</h1><p><strong>1. 工具定义（标准 OpenAI 格式）</strong></p><pre class="code-block"><code class="language-bash">import {ChatCompletionTool} from'openai/resources/chat/completions'

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
exportconst toolRegistry: Recordstring&gt; = {
  get_closing_price: (params) =&gt; getClosingPrice(params.name),
}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li></ul><p><strong>2. Agent 主循环（Function Call 版本）</strong></p><pre class="code-block"><code class="language-bash">import {ChatCompletionTool} from'openai/resources/chat/completions'

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
exportconst toolRegistry: Recordstring&gt; = {
  get_closing_price: (params) =&gt; getClosingPrice(params.name),
}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li></ul><h1 id="heading-6236">1.5 使用 LangGraph 实现</h1><p>对于复杂的 Agent 场景（需要记忆、反思、人工介入等），LangGraph 提供了声明式的图结构定义，更易于维护和扩展。</p><p>LangGraph 将 Agent 建模为状态图，其中节点代表执行具体任务的函数，边定义节点之间的转换规则，而状态则是在各个节点之间传递的数据。这种抽象让 Agent 的执行流程更加清晰可控。</p><h1 id="heading-6422">核心代码</h1><p><strong>构建图：</strong></p><pre class="code-block"><code class="language-bash">import {StateGraph, END} from'@langchain/langgraph'import {Annotation} from'@langchain/langgraph'

// 1. 定义状态
const GraphState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) =&gt; x.concat(y),
    default: () =&gt; [],
  }),
})

// 2. 定义节点
const llm = new ChatOpenAI({model: 'gpt-4o'}).bindTools(tools)

asyncfunction callModel(state: typeof GraphState.State) {
const response = await llm.invoke(state.messages)return {messages: [response]}}

asyncfunction callTools(state: typeof GraphState.State) {
const lastMessage = state.messages[state.messages.length - 1]
const toolMessages = awaitPromise.all(
    lastMessage.tool_calls.map(async (tc) =&gt; {
      const tool = tools.find((t) =&gt; t.name === tc.name)
      const result = await tool.invoke(tc.args)
      returnnew ToolMessage({content: String(result), tool_call_id: tc.id})
    }))return {messages: toolMessages}}

// 3. 路由函数
function shouldContinue(state: typeof GraphState.State) {
const lastMessage = state.messages[state.messages.length - 1]return lastMessage.tool_calls?.length &gt; 0 ? 'tools' : END
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
await app.invoke({messages: [new HumanMessage('问题')]})</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li><li><p>43</p></li><li><p>44</p></li><li><p>45</p></li><li><p>46</p></li><li><p>47</p></li><li><p>48</p></li><li><p>49</p></li><li><p>50</p></li><li><p>51</p></li></ul><p>其实 <code>@langchain/langgraph</code> 提供了 <code>createReactAgent</code>，可以更加方便的实现类似功能：</p><pre class="code-block"><code class="language-bash">import {createReactAgent} from'@langchain/langgraph/prebuilt'import {ChatOpenAI} from'@langchain/openai'import {tool} from'@langchain/core/tools'import {z} from'zod'

// 定义工具
const getClosingPriceTool = tool((input) =&gt; {
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
})</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li></ul><h1 id="heading-9174">1.6 适用场景</h1><p>ReAct 模式特别适合需要外部信息或工具支持的任务。当问题无法仅凭 LLM 内部知识解决时，比如查询实时数据、调用 API、执行计算等，ReAct 通过工具调用弥补了 LLM 的能力边界。这种模式对于多步骤推理任务也很有效，Agent 可以逐步收集信息、分析结果、调整策略，最终得出答案。同时，ReAct 的透明性让整个推理过程可观察可调试，便于理解 Agent 的决策逻辑。</p><h1 id="heading-9375">1.7 注意事项</h1><p>实现 ReAct 模式时需要注意几个关键点。Prompt 设计至关重要，需要清晰地定义 Thought、Action、Observation 的格式，并提供足够的示例帮助 LLM 理解预期输出。工具描述要准确明确，让 LLM 能够正确选择和使用工具。同时要设置合理的迭代次数上限，避免陷入无限循环。错误处理机制也不可忽视，当工具调用失败或 LLM 输出格式错误时，需要有恰当的降级策略。此外，要注意 Token 消耗，因为每次迭代都会增加消息历史的长度。</p><h1 id="heading-9614">二、CodeAct 模式</h1><h1 id="heading-9628">2.1 核心理念</h1><p>CodeAct（Code as Action）让 Agent 通过生成并执行代码来完成任务。与 ReAct 调用预定义工具不同，CodeAct 赋予 Agent 更大的灵活性，特别适合复杂计算、数据处理或需要组合多个操作的场景。核心流程是：Thought → Code Generation → Code Execution → Observation。</p><h1 id="heading-9817">2.2 工作流程</h1><p>CodeAct 的执行流程从 LLM 分析用户问题开始，理解需要完成什么任务。接着 LLM 生成对应的代码（通常是 Python 或 JavaScript），这些代码会在沙箱环境中执行以保证安全性。执行结果作为 Observation 返回给 LLM，LLM 根据结果判断是继续生成新代码完善方案，还是已经得到满意答案可以结束流程。</p><h1 id="heading-9998">2.3 实战案例</h1><p><strong>需求：</strong> 计算 1~100 的和</p><h1 id="heading-10025">核心代码</h1><p><strong>1. 提示词（Prompt）</strong></p><pre class="code-block"><code class="language-bash">// prompts.ts
export const SYSTEM_PROMPT = `你是一个能够编写和执行代码的智能助手。
当用户提出问题时，你需要：
1. 分析问题并确定需要编写什么代码
2. 编写能解决问题的 JavaScript 代码
3. 代码必须将最终结果存储在 'result' 变量中
4. 将代码包裹在 \`\`\`javascript 代码块中
5. 分析执行结果，如果有错误则修改代码再次执行
6. 最终给用户提供答案`
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li></ul><p><strong>2. 工具（代码执行器）</strong></p><pre class="code-block"><code class="language-bash">// tools.ts
import {z} from'zod'import {tool} from'@langchain/core/tools'import vm from'vm'

exportconst executePythonTool = tool((input) =&gt; {
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
  })</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li></ul><p><strong>3. Agent 逻辑（LangGraph）</strong></p><pre class="code-block"><code class="language-bash">// graph.ts
import {StateGraph, END} from'@langchain/langgraph'import {Annotation} from'@langchain/langgraph'import {ChatOpenAI} from'@langchain/openai'import {AIMessage, HumanMessage, SystemMessage} from'@langchain/core/messages'import {SYSTEM_PROMPT} from'./prompts'import {executePythonTool} from'./tools'

// 定义状态
const CodeActState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) =&gt; x.concat(y),
    default: () =&gt; [],
  }),
  output: Annotation({default: () =&gt; ''}),
userPrompt: Annotation({default: () =&gt; ''}),
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
    .compile()}</code></pre><p>智能体编程bash</p><p><strong>4. 运行</strong></p><pre class="code-block"><code class="language-bash">const agent = buildCodeActGraph()
const result = await agent.invoke({
  userPrompt: '请计算 1~100 的和',
})
console.log(result.output)</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li></ul><h1 id="heading-13872">运行效果</h1><pre class="code-block"><code class="language-bash">[启动 CodeAct Agent][用户问题] 请计算 1~100 的和


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
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li></ul><p>从结果可以看到，大模型并没有使用循环，而是用等差数列求和公式来实现的，有点聪明的样子。</p><h1 id="heading-14307">2.4 适用场景</h1><p>CodeAct 模式特别适合需要灵活处理数据或进行复杂计算的场景。当任务涉及数学计算、数据转换、文本处理、算法实现等需要编程逻辑的操作时，生成代码往往比调用预定义工具更加高效和灵活。同时，对于需要组合多个操作或处理非标准化数据的任务，CodeAct 也展现出明显优势。这种模式让 Agent 不再局限于现有工具的能力边界，可以根据具体需求动态生成解决方案。</p><h1 id="heading-14497">2.5 注意事项</h1><p>使用 CodeAct 模式时必须高度重视安全性问题。代码执行必须在沙箱环境中进行，避免恶意代码对系统造成破坏。建议使用 vm 模块或 Docker 容器等隔离机制，并设置执行超时限制防止无限循环。此外，生成的代码质量依赖于 LLM 的能力，可能存在语法错误或逻辑错误，需要完善的错误处理机制。对于生产环境，还应该记录所有执行的代码以便审计和调试。</p><h1 id="heading-14682">三、计划模式（Plan Mode）</h1><h1 id="heading-14701">3.1 核心理念</h1><p>计划模式采用"先计划，后执行"的策略。ReAct 每步都需重新思考，适合探索性任务；计划模式则在开始时制定完整方案再逐步执行，更适合结构化程度高的任务。优势在于执行路径清晰、便于监控进度和预测资源消耗。但灵活性较低，初始计划不准确时可能需要人工调整。</p><h1 id="heading-14838">3.2 工作流程</h1><h1 id="heading-14851">3.3 实战案例:简单计划模式</h1><p><strong>需求：</strong> 比较茅台和青岛啤酒哪个贵？</p><h1 id="heading-14887">核心代码</h1><p><strong>1. 计划生成提示词</strong></p><pre class="code-block"><code class="language-bash">// prompts.ts
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

如果你认为计划已经执行到最后一步了，请在内容的末尾加上 Final Answer 字样`</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li></ul><p><strong>2. 状态定义</strong></p><pre class="code-block"><code class="language-bash">// types.ts
export const PlanState = Annotation.Root({
  messages: Annotation({
    reducer: (x, y) =&gt; x.concat(y),
    default: () =&gt; [],
  }),
  plan: Annotation({
    reducer: (x, y) =&gt; y ?? x,
    default: () =&gt; '',
  }),
})</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li></ul><p><strong>3. 工作流构建</strong></p><pre class="code-block"><code class="language-bash">// graph.ts
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
    toolCalls.map(async (tc) =&gt; {
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
    .compile()}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li><li><p>43</p></li><li><p>44</p></li><li><p>45</p></li><li><p>46</p></li><li><p>47</p></li><li><p>48</p></li><li><p>49</p></li><li><p>50</p></li><li><p>51</p></li><li><p>52</p></li><li><p>53</p></li><li><p>54</p></li><li><p>55</p></li><li><p>56</p></li><li><p>57</p></li><li><p>58</p></li><li><p>59</p></li><li><p>60</p></li><li><p>61</p></li><li><p>62</p></li></ul><h1 id="heading-17701">运行效果</h1><pre class="code-block"><code class="language-bash">[启动计划模式 Agent][用户问题] 茅台和青岛啤酒哪个贵？

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
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li></ul><h1 id="heading-18269">3.4 高级计划模式：动态调整</h1><p>简单计划模式的局限是<strong>计划一旦生成就固定不变</strong>。高级计划模式引入了<strong>动态重新规划</strong>能力，可以根据执行结果调整剩余步骤，下面我们来改进一下。</p><h1 id="heading-18353">工作流程</h1><h1 id="heading-18362">代码示例</h1><p><strong>1. Prompt 设计</strong></p><pre class="code-block"><code class="language-bash">// 执行助手 Prompt（用于 ReAct Agent）
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

注意：不要在步骤列表中混入解释性文字，只输出纯粹的步骤列表`</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li></ul><p><strong>2. 执行节点（使用 ReAct Agent）</strong></p><pre class="code-block"><code class="language-bash">import {createReactAgent} from'@langchain/langgraph/prebuilt'import {ChatOpenAI} from'@langchain/openai'

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
const planStr = plan.map((step, i) =&gt;`${i + 1}. ${step}`).join('\n')
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
    pastSteps: [[task, result]] asArray&lt;[string, string]&gt;,
  }}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li></ul><p><strong>3. 规划评估节点（核心：动态调整）</strong></p><pre class="code-block"><code class="language-bash">// 规划评估节点
asyncfunction planStep(state: typeof PlanExecuteState.State) {
// 格式化当前状态
const planStr = state.plan.map((step, i) =&gt;`${i + 1}. ${step}`).join('\n')
const pastStepsStr = state.pastSteps
    .map(([task, result]) =&gt;`- ${task}\n  结果: ${result}`)
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
if (newPlan.length &gt; 0) {
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
}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li><li><p>43</p></li><li><p>44</p></li><li><p>45</p></li><li><p>46</p></li><li><p>47</p></li><li><p>48</p></li><li><p>49</p></li><li><p>50</p></li><li><p>51</p></li><li><p>52</p></li><li><p>53</p></li><li><p>54</p></li><li><p>55</p></li></ul><p><strong>4. 构建 LangGraph 工作流</strong></p><pre class="code-block"><code class="language-bash">import {StateGraph, END} from'@langchain/langgraph'

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

const app = workflow.compile()</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li></ul><h1 id="heading-22912">运行示例（体现动态调整）</h1><p>故意给一个不完整的初始计划，让 Agent 根据中间结果动态补充步骤。</p><pre class="code-block"><code class="language-bash">[启动高级计划模式 Agent][目标] 仅根据收盘价帮我分析一下青岛啤酒和贵州茅台的投资价值对比，低的更有价值
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
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li><li><p>43</p></li><li><p>44</p></li><li><p>45</p></li><li><p>46</p></li></ul><h1 id="heading-23855">3.5 适用场景</h1><p>计划模式最适合需求明确、步骤可预测的结构化任务。当任务目标清晰、可分解为多个具体步骤时，先制定计划再执行能够提供更好的可控性和可预测性。这种模式特别适合数据分析、报告生成、多步骤查询等场景。对于需要监控执行进度或预估完成时间的任务，计划模式的优势更加明显。同时，当需要优化执行顺序或并行处理某些步骤时，有了明确的计划更容易进行调度优化。</p><h1 id="heading-24035">3.6 注意事项</h1><p>使用计划模式需要权衡灵活性和可控性。如果任务的不确定性较高，初始计划可能不够准确，需要考虑引入动态调整机制（如高级计划模式）。计划生成的质量直接影响最终效果，需要精心设计计划生成的 Prompt，提供清晰的指导和示例。执行过程中可能遇到计划中未预见的情况，需要有合适的异常处理策略。此外，过于详细的计划可能限制 Agent 的灵活性，而过于粗略的计划又可能起不到指导作用，需要根据具体任务找到平衡点。</p><h1 id="heading-24247">四、反思模式（Reflection Mode）</h1><h1 id="heading-24272">4.1 核心理念</h1><p>反思模式模拟人类"先写初稿，再反复修改"的创作过程，通过自我评估和迭代改进来提升输出质量。这种模式特别适合对输出质量要求较高的场景，通过引入一个独立的反思环节来审视当前方案的不足之处。</p><h1 id="heading-24376">4.2 工作流程</h1><p>反思模式包含三个阶段的循环：生成阶段根据需求和反思建议生成方案，反思阶段多维度检查方案并提出改进建议，决策阶段判断是否继续优化。循环持续进行直到达到质量标准或迭代次数上限。</p><h1 id="heading-24477">4.3 核心代码</h1><p>反思模式的实现包含状态定义、Prompt 设计、生成节点、反思节点和决策函数几个关键部分。</p><p><strong>状态定义：</strong></p><pre class="code-block"><code class="language-bash">export const ReflectionState = Annotation.Root({
  userQuery: Annotation(), // 用户需求
  bestCommand: Annotation(), // 当前最优方案
  reflection: Annotation(), // 反思记录
  iterations: Annotation(), // 迭代次数
})</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li></ul><p><strong>Prompt 设计：</strong></p><p>反思模式的核心在于两个高质量的 Prompt。生成 Prompt 用于根据需求和反思建议生成或改进方案：</p><pre class="code-block"><code class="language-bash">export const COMMAND_PROMPT = `你是一个资深Linux运维专家，请根据用户需求生成最合适的Linux命令。

要求：
1. 只输出可直接执行的命令
2. 优先使用性能最好的方案

用户需求：{user_query}
当前方案：{best_command}
改进建议：{reflection}

请按以下格式输出：
命令：&lt;生成的命令&gt;`</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li></ul><p>反思 Prompt 用于检查方案的合理性并提出改进建议：</p><pre class="code-block"><code class="language-bash">export const REFLECTION_PROMPT = `请严格检查以下Linux命令的合理性：
{command}

检查维度：
1. 是否符合POSIX标准
2. 是否有更高效的替代方案
3. 是否完全解决用户需求
4. 是否好维护

用户原始需求：{user_query}

请返回结构化的检查结果：
- needsImprovement: 是否需要改进（true/false）
- suggestions: 改进建议（包含发现的问题和具体优化方向，如果无需改进则说明"已达最优"）`</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li></ul><p><strong>结构化输出格式：</strong></p><pre class="code-block"><code class="language-bash">import {z} from 'zod'

// 反思结果的结构化输出
const ReflectionResultSchema = z.object({
  needsImprovement: z.boolean().describe('是否需要改进'),
  suggestions: z.string().describe('改进建议，包含发现的问题和优化方向'),
})</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li></ul><p><strong>生成节点：</strong></p><pre class="code-block"><code class="language-bash">async function generateCommand(state: ReflectionStateType) {
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
    commandParts.length &gt; 1
      ? commandParts[1]?.trim() || content.trim()
      : content.trim()

console.log(`[命令] ${command}`)

return {
    bestCommand: command,
    iterations: iter + 1,
  }}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li></ul><p><strong>反思节点：</strong></p><pre class="code-block"><code class="language-bash">async function reflectAndOptimize(state: ReflectionStateType) {
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
    return {reflection: '反思检查失败'}}}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li></ul><p><strong>决策函数：</strong></p><pre class="code-block"><code class="language-bash">// 停止标志：发现这些关键词时立即停止
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
if (state.iterations &gt;= 3) {
    console.log('\n[结束] 达到最大迭代次数 (3次)')
    return END
  }

// 4. 继续优化
console.log('[决策] 继续优化...')return'generate'}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li></ul><p><strong>构建工作流：</strong></p><pre class="code-block"><code class="language-bash">const workflow = new StateGraph(ReflectionState)
  .addNode('generate', generateCommand)
  .addNode('reflect', reflectAndOptimize)
  .addEdge('__start__', 'generate')
  .addEdge('generate', 'reflect')
  .addConditionalEdges('reflect', checkReflection, {
    generate: 'generate',
    [END]: END,
  })

const app = workflow.compile()</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li></ul><h1 id="heading-28954">4.4 运行示例</h1><p><strong>场景：生成 Docker 命令</strong></p><pre class="code-block"><code class="language-bash">[启动反思模式 Agent][需求] 使用docker创建nginx容器，端口映射8080:80


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
</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li><li><p>35</p></li><li><p>36</p></li><li><p>37</p></li><li><p>38</p></li><li><p>39</p></li><li><p>40</p></li><li><p>41</p></li><li><p>42</p></li><li><p>43</p></li><li><p>44</p></li><li><p>45</p></li><li><p>46</p></li><li><p>47</p></li><li><p>48</p></li><li><p>49</p></li><li><p>50</p></li><li><p>51</p></li><li><p>52</p></li><li><p>53</p></li><li><p>54</p></li><li><p>55</p></li><li><p>56</p></li><li><p>57</p></li></ul><h1 id="heading-30714">4.5 适用场景</h1><p>反思模式最适合对输出质量有较高要求的场景。当需要生成文档、代码、配置文件、命令等关键输出时，通过反思机制可以显著提升方案的完整性和可靠性。这种模式特别适合技术方案设计、代码审查、内容创作等需要经过多次打磨才能达到专业标准的任务。同时，对于那些有明确质量评估标准的任务，反思模式能够系统性地检查各个维度是否达标。</p><h1 id="heading-30881">4.6 注意事项</h1><p>使用反思模式时需要注意控制迭代次数，避免过度优化导致效率低下或陷入无限循环。建议设置合理的迭代上限（通常 2-3 次即可），并定义清晰的停止条件。反思 Prompt 的设计至关重要，需要明确具体的检查维度和评估标准，避免模糊的评价导致反思效果不佳。此外，反思模式会增加 LLM 调用次数和 Token 消耗，需要在质量和成本之间做好平衡。对于某些已经足够好的初始方案，过度的反思可能反而引入不必要的修改。</p><hr><h1 id="heading-31096">五、人机协作模式（Human-in-the-Loop）</h1><h1 id="heading-31125">5.1 核心理念</h1><p>人机协作模式将 Agent 的自动化能力与人类判断力相结合。适用于关键决策（高风险操作需人工确认）、信息补全（缺少参数时询问用户）和质量控制（重要输出需人工审核）等场景。通过在关键节点暂停执行、等待人工输入、然后恢复执行，实现效率与可控性的平衡。</p><h1 id="heading-31260">5.2 工作流程</h1><p>流程图展示了一个核心循环和三条分支路径：</p><p><strong>核心循环：</strong></p><pre class="code-block"><code class="language-plaintext">Input → LLM 推理 → 路由判断
</code></pre><p>智能体编程plaintext</p><ul><li><p>1</p></li></ul><p><strong>分支 1：人工交互路径（橙色）</strong></p><pre class="code-block"><code class="language-plaintext">路由判断 → 暂停等待 → 用户输入 → LLM 推理（循环）
</code></pre><p>智能体编程plaintext</p><ul><li><p>1</p></li></ul><ul><li><p><strong>触发条件</strong>：LLM 调用 <code>ask_user</code> 工具</p></li><li><p><strong>核心机制</strong>：<code>interrupt()</code> 暂停，等待用户输入，<code>resume</code> 恢复</p></li><li><p><strong>应用场景</strong>：缺少参数、需要用户确认、多选项决策</p></li></ul><p><strong>分支 2：工具执行路径（紫色）</strong></p><pre class="code-block"><code class="language-plaintext">路由判断 → 工具执行 → LLM 推理（循环）
</code></pre><p>智能体编程plaintext</p><ul><li><p>1</p></li></ul><ul><li><p><strong>触发条件</strong>：LLM 调用普通工具</p></li><li><p><strong>核心机制</strong>：自动执行工具，结果反馈给 LLM</p></li><li><p><strong>应用场景</strong>：查询数据、计算处理、API 调用</p></li></ul><p><strong>分支 3：完成路径（绿色虚线）</strong></p><pre class="code-block"><code class="language-plaintext">路由判断 → Final Answer（结束）
</code></pre><p>智能体编程plaintext</p><ul><li><p>1</p></li></ul><ul><li><p><strong>触发条件</strong>：LLM 判断已获得足够信息</p></li><li><p><strong>核心机制</strong>：返回最终结果，结束执行</p></li><li><p><strong>应用场景</strong>：问题解决、任务完成</p></li></ul><p>实现依赖三个核心机制：中断机制通过 <code>interrupt()</code> 暂停执行并等待人工输入，状态保存机制使用 Checkpointer 保留所有上下文信息，恢复执行机制通过 <code>Command({ resume: userInput })</code> 从暂停点继续执行。</p><h1 id="heading-31909">5.3 实战案例：购物助手</h1><p><strong>场景：</strong> 用户询问购买商品的总价，但没有说明数量，需要询问用户。</p><h1 id="heading-31957">核心代码实现</h1><p><strong>1. 工具定义</strong></p><pre class="code-block"><code class="language-bash">import {tool} from'@langchain/core/tools'import {z} from'zod'

// 普通工具：获取商品价格
exportconst getPriceTool = tool(
async (input) =&gt; {
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
async (input) =&gt; {
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
  })</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li></ul><p><strong>关键点：</strong></p><ul><li><p><code>ask_user</code> 是一个特殊工具，用于触发人工介入</p></li><li><p>LLM 会在需要用户信息时自动调用这个工具</p></li></ul><p><strong>2. 人工节点（核心）</strong></p><pre class="code-block"><code class="language-bash">import {tool} from'@langchain/core/tools'import {z} from'zod'

// 普通工具：获取商品价格
exportconst getPriceTool = tool(
async (input) =&gt; {
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
async (input) =&gt; {
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
  })</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li><li><p>22</p></li><li><p>23</p></li><li><p>24</p></li><li><p>25</p></li><li><p>26</p></li><li><p>27</p></li><li><p>28</p></li><li><p>29</p></li><li><p>30</p></li><li><p>31</p></li><li><p>32</p></li><li><p>33</p></li><li><p>34</p></li></ul><p><strong>关键点：</strong></p><ul><li><p><code>interrupt()</code> 会暂停整个工作流的执行</p></li><li><p>返回的值会在恢复执行时作为 <code>resume</code> 参数传入</p></li><li><p>用户输入被封装成 <code>ToolMessage</code> 返回给 LLM</p></li></ul><p><strong>3. 路由函数（识别触发时机）</strong></p><pre class="code-block"><code class="language-bash">function enterTools(state: HumanLoopStateType): string {
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
return'toolNode'}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li></ul><p><strong>4. 构建 LangGraph（必须使用 Checkpointer）</strong></p><pre class="code-block"><code class="language-bash">import {StateGraph, START, END} from'@langchain/langgraph'import {MemorySaver} from'@langchain/langgraph'

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
const memory = new MemorySaver()return workflow.compile({checkpointer: memory})}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li><li><p>14</p></li><li><p>15</p></li><li><p>16</p></li><li><p>17</p></li><li><p>18</p></li><li><p>19</p></li><li><p>20</p></li><li><p>21</p></li></ul><p><strong>关键点：</strong></p><ul><li><p>人机协作模式<strong>必须</strong>配置 <code>checkpointer</code></p></li><li><p><code>MemorySaver</code> 将状态保存在内存中（生产环境可用数据库）</p></li></ul><p><strong>5. 运行 Agent（两阶段执行）</strong></p><pre class="code-block"><code class="language-bash">export asyncfunction runHumanLoopAgent(
  query: string,
  getUserInput: () =&gt; Promise): Promise {
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
}</code></pre><p>智能体编程bash</p><p><strong>关键点：</strong></p><ol><li><p>第一次 <code>invoke</code> 会执行到 <code>interrupt</code> 处暂停</p></li><li><p>获取用户输入后，通过 <code>Command({ resume: userInput })</code> 恢复</p></li><li><p><strong>必须使用相同的 </strong><code>threadConfig</code> 才能恢复到正确的状态</p></li></ol><h1 id="heading-36415">运行效果</h1><pre class="code-block"><code class="language-bash">[启动人机协作模式 Agent][用户问题] 我想买一些苹果，总共需要多少钱

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
</code></pre><p>智能体编程bash</p><h1 id="heading-36849">5.4 适用场景</h1><p>人机协作模式在多种场景下都能发挥重要作用。对于敏感操作，比如删除数据、修改配置、执行系统命令等高风险动作，在执行前需要用户明确确认。可以通过定义 <code>confirm_operation</code> 工具，在执行前暂停并向用户展示即将执行的操作内容，等待用户审核通过后再继续。</p><p>在信息补全场景中，当 Agent 发现缺少必需参数、需要用户在多个选项中选择、或参数含义不明确时，可以暂停执行并向用户询问。这种交互式的信息收集方式比让 Agent 自行猜测要可靠得多。</p><p>质量控制是另一个重要应用场景。当 Agent 生成文档、代码、方案等内容后，可以暂停执行让用户审核输出质量。在关键决策点，人工判断往往比 LLM 的判断更可靠。此外，对于重要结果，在使用前进行人工验证可以避免潜在风险。</p><p>异常处理场景也很常见。当 Agent 遇到无法自动处理的情况时，与其直接失败不如暂停并请求人工帮助。用户可以提供额外信息、调整策略或从多个备选方案中选择，然后 Agent 继续执行。</p><h1 id="heading-37289">5.5 高级用法</h1><p><strong>1. 支持多轮人工介入</strong></p><pre class="code-block"><code class="language-bash">async function runWithMultipleInterrupts(query: string) {
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
    input = new Command({resume: userInput})}}</code></pre><p>智能体编程bash</p><p><strong>2. 支持用户取消</strong></p><pre class="code-block"><code class="language-bash">const userInput = await getUserInput()

if (userInput === 'cancel' || userInput === '取消') {return '操作已取消'}

result = await app.invoke(new Command({resume: userInput}), config)</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li></ul><p><strong>3. 添加超时处理</strong></p><pre class="code-block"><code class="language-bash">const timeout = (ms: number) =&gt;
newPromise((_, reject) =&gt; setTimeout(() =&gt; reject(newError('Timeout')), ms))

try {
const userInput = awaitPromise.race([
    getUserInput(),
    timeout(60000), // 60秒超时
  ])

  result = await app.invoke(new Command({resume: userInput}), config)} catch (error) {return'等待超时，操作已取消'}</code></pre><p>智能体编程bash</p><ul><li><p>1</p></li><li><p>2</p></li><li><p>3</p></li><li><p>4</p></li><li><p>5</p></li><li><p>6</p></li><li><p>7</p></li><li><p>8</p></li><li><p>9</p></li><li><p>10</p></li><li><p>11</p></li><li><p>12</p></li><li><p>13</p></li></ul><h1 id="heading-38586">5.6 注意事项</h1><p>实现人机协作模式时需要注意几个关键点。首先，必须配置 Checkpointer 来保存状态，这是整个模式的技术基础。可以选择 <code>MemorySaver</code> 用于开发和简单场景，或使用 <code>SqliteSaver</code> 等持久化方案用于生产环境。</p><p>Thread ID 的一致性至关重要。恢复执行时必须使用与暂停时相同的 <code>thread_id</code>，否则会导致状态丢失。在多用户场景下，务必为每个用户会话分配独立的 <code>thread_id</code> 以隔离状态，避免数据混淆。</p><p>输入验证不可忽视。用户可能输入无效内容、格式错误或超出预期范围的数据，需要实现完善的验证和错误处理机制。同时，应该设置合理的超时机制，避免 Agent 无限期等待用户输入。提供取消操作的选项也很重要，让用户可以随时中止流程。</p><h1 id="heading-38930">六、总结</h1><p>五种 Agent 设计模式各有侧重。ReAct 通过推理-行动循环适合处理需要外部工具的任务，CodeAct 通过代码生成解决复杂计算问题。计划模式提供结构化执行路径，简单版适合明确任务，高级版支持动态调整。反思模式通过迭代优化提升输出质量，人机协作模式在关键节点引入人工判断确保可控性。</p><p>实际应用中往往需要组合使用。建议从简单模式开始验证核心逻辑，逐步引入高级特性。根据任务特点权衡性能与准确性，同时做好日志监控和安全防护。通过理解这些模式的特点和适用场景，你可以构建高效可靠的 Agent 系统。</p><h1 id="heading-39189">那么，如何系统的去学习大模型LLM？</h1><p>作为一名从业五年的资深大模型算法工程师，我经常会收到一些评论和私信，我是小白，学习大模型该从哪里入手呢？我自学没有方向怎么办？这个地方我不会啊。如果你也有类似的经历，一定要继续看下去！这些问题啊，也不是三言两语啊就能讲明白的。</p><p>所以我综合了大模型的所有知识点，给大家带来一套<strong>全网最全最细的大模型零基础教程</strong>。在做这套教程之前呢，我就曾放空大脑，以一个大模型小白的角度去重新解析它，采用基础知识和实战项目相结合的教学方式，历时3个月，终于完成了这样的课程，让你真正体会到什么是每一秒都在疯狂输出知识点。</p><p>由于篇幅有限，⚡️ 朋友们如果有需要全套 《<strong>2025全新制作的大模型全套资料</strong>》，<strong><mark>扫码获取</mark>~</strong><br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/d14cb33bff1e46ebb618651bfeba7a3b.jpeg#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><h1 id="heading-39510">为什么要学习大模型？</h1><p>我国在A大模型领域面临人才短缺,数量与质量均落后于发达国家。2023年，人才缺口已超百万，凸显培养不足。随着AI技术飞速发展，预计到2025年,这一缺口将急剧扩大至400万,严重制约我国AI产业的创新步伐。加强人才培养,优化教育体系,国际合作并进是破解困局、推动AI发展的关键。</p><h1 id="heading-39669">👉大模型学习指南+路线汇总👈</h1><p>我们这套大模型资料呢，会从<strong>基础篇、进阶篇和项目实战篇</strong>等三大方面来讲解。<br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/718e40e9489741139c25f2d7941ec7db.png#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://img-blog.csdnimg.cn/direct/d59f942c9a924dc2b1b529134fecd2fb.jpeg#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><h1 id="heading-39728">👉①.基础篇👈</h1><p>基础篇里面包括了Python快速入门、AI开发环境搭建及提示词工程，带你学习大模型核心原理、prompt使用技巧、Transformer架构和预训练、SFT、RLHF等一些基础概念，用最易懂的方式带你入门大模型。<br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/f857e19ae4c14237a544bdba8cd3521b.png#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><h1 id="heading-39849">👉②.进阶篇👈</h1><p>接下来是进阶篇，你将掌握RAG、Agent、Langchain、大模型微调和私有化部署，学习如何构建外挂知识库并和自己的企业相结合，学习如何使用langchain框架提高开发效率和代码质量、学习如何选择合适的基座模型并进行数据集的收集预处理以及具体的模型微调等等。<br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/709c908f5c7c4dce8e685c92fbf93a9b.png#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><h1 id="heading-39996">👉③.实战篇👈</h1><p>实战篇会手把手带着大家练习企业级的落地项目（已脱敏），比如RAG医疗问答系统、Agent智能电商客服系统、数字人项目实战、教育行业智能助教等等，从而帮助大家更好的应对大模型时代的挑战。<br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/56c8d5ed017044d2abcd92354227bc51.png#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><h1 id="heading-40103">👉④.福利篇👈</h1><p>最后呢，会给大家一个小福利，课程视频中的所有素材，有搭建AI开发环境资料包，还有学习计划表，几十上百G素材、电子书和课件等等，只要你能想到的素材，我这里几乎都有。我已经全部上传到CSDN，朋友们如果需要可以微信扫描下方CSDN官方认证二维码免费领取【<code>保证100%免费</code>】<br><img class="editor-image" src="https://i-blog.csdnimg.cn/direct/2bd8cd10ce6742ef823f73617bfdcbb3.jpeg#pic_center" alt="在这里插入图片描述" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><code>相信我，这套大模型系统教程将会是全网最齐全 最易懂的小白专用课！！</code></p><p>您可能感兴趣的与本文相关的镜像</p><p>Seed-Coder-8B-Base</p><p>文本生成</p><p>Seed-Coder</p><p>Seed-Coder是一个功能强大、透明、参数高效的 8B 级开源代码模型系列，包括基础变体、指导变体和推理变体，由字节团队开源</p><p>一键部署运行<br></p><p><br>确定要放弃本次机会？<br></p><p>福利倒计时<br></p><p><em>:</em><br><br><em>:</em><br><br></p><p><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/vip-limited-close-roup.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>立减 ¥<br><br></p><p>普通VIP年卡可用<br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link limited-time-btn-new" href="https://mall.csdn.net/vip">立即使用</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link profile-href" href="https://blog.csdn.net/kaka0722ww"><img class="editor-image" src="https://i-avatar.csdnimg.cn/ac028661e3c8470bbe2f7b3354687a32_kaka0722ww.jpg!1" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br>deepseek大模型<br><br></a><br></p><p>关注<br>关注<br></p><ul><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/tobarThumbUpactive.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/like-active.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/like.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br>12<br><br><br></p><p>点赞</p></li><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/unlike-active.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/unlike.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br><br></p><p>踩</p></li><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/collect-active.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/collect.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/newCollectActive.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br>19<br><br><br></p><p><br>收藏<br><br></p><p><br>觉得还不错?<br><br>一键收藏<br><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/collectionCloseWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br></p></li><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward01.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>知道了<br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tool-item-href" href="https://blog.csdn.net/kaka0722ww/article/details/155453725#commentBox"><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/comment.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br>0<br><br></a><br></p><p>评论</p></li><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/share.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>分享<br><br></p><p>复制链接<br></p><p>分享到 QQ<br></p><p>分享到新浪微博<br></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/share/icon-wechat.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;">扫一扫<br></p></li><li><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/more.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><br><br></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/report.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>举报<br><br></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/toolbar/report.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>举报<br><br></p></li></ul><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/weixin_39756314/article/details/144384491">详细解释什么叫<em>agent</em>中的<em>ReAct模式</em></a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/weixin_39756314">AI生成曾小健3</a><br></p><p>12-10<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1638<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/weixin_39756314/article/details/144384491">答案<em>ReAct模式</em>，即Reasoning and Acting的结合，是一种在<em>人工智能</em>代理（<em>Agent</em>）<em>开发</em>中广泛应用的设计思想。它强调推理（Reasoning）<em>与</em>行动（Acting）的有机结合，使得<em>Agent</em>能够在复杂和动态的环境中更有效地执行任务。</a></p><p>参与评论<br>您还未登录，请先<br>登录<br>后发表或查看评论<br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://dreamit.blog.csdn.net/article/details/156435171">【光子AI 】探索AI <em>Agent</em> <em>架构</em>师的30项<em>必备</em>修炼：一本全面<em>指南</em></a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://dreamit.blog.csdn.net/article/details/156435171">最新发布</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/universsky2015">AI天才研究院</a><br></p><p>12-31<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>415<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://dreamit.blog.csdn.net/article/details/156435171">摘要 《探索AI <em>Agent架构</em>师的30项<em>必备</em>修炼》是一本面向AI <em>Agent架构</em>师的<em>实战指南</em>，基于作者团队在腾讯云等大厂的20多个AI <em>Agent</em>项目经验编写而成。全书从认知层、工程层和高阶层三个维度系统性地构建了AI <em>Agent架构</em>师的能力模型，包含30项针对性修炼内容。 书中首先通过一个电商售后AI <em>Agent</em>失败<em>案例</em>，揭示了行业痛点：大多数项目失败源于缺乏对AI <em>Agent核心</em>本质的理解。随后详细阐述了AI <em>Agent</em>的定义、边界分类、发展痛点和解决思路，并<em>与</em>传统Chatbot进行了多维度对比。全书</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/135868163">智能体AI <em>Agent</em>的极速入门：从<em>ReAct</em>、AutoGPT到AutoGen、Qwen<em>Agent</em>、X<em>Agent</em>、MetaGPT</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/135868163">热门推荐</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/v_JULY_v">结构之法 算法之道</a><br></p><p>01-26<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1万+<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/135868163"><em>ReAct</em>其实不是一个刚出来的概念，它于2022年10月份便由Google Research 的 Brain Team 通过此篇论文《》提出来了，没错，又是Google的建设性工作之一，曾一度感觉，没有Google(毕竟<em>transformer</em>、指令微调、CoT等哪个不是Google的杰作，包括RLHF也是Google deepmind和OpenAI联合推出来的)，就没有后来的ChatGPT，^_^考虑一个智能体<em>与</em>环境交互以解决任务的一般设置。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/147722142">大厂<em>大模型</em>必知的<em>5</em>种<em>agent模式</em></a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/m0_59235945">m0_59235945的博客</a><br></p><p>05-05<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1247<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/147722142">该阶段让大家对<em>大模型</em> AI有一个最前沿的认识，对<em>大模型</em> AI 的理解超过 9<em>5</em>% 的人，可以在相关讨论时发表高级、不跟风、又接地气的见解，别人只会和 AI 聊天，而你能调教 AI，并能用代码将<em>大模型</em>和业务衔接。对全球<em>大模型</em>从性能、吞吐量、成本等方面有一定的认知，可以在云端和本地等多种环境下部署<em>大模型</em>，找到适合自己的项目/创业方向，做一名被 AI 武装的产品经理。由于新岗位的生产效率，要优于被取代岗位的生产效率，所以实际上整个社会的生产效率是提升的。天道酬勤，你越努力，就会成为越优秀的自己。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/140035898">产品经理研读：<em>Agent</em>的九种<em>设计模式</em>(图解+代码)</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/zhishi0000">zhishi0000的博客</a><br></p><p>06-28<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1180<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/140035898">好了，以上就是目前所总结的 <em>Agent</em> 九大<em>设计模式</em>，其实 <em>Agent</em> 中。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/149742300">手把手教你！<em>Agent设计模式</em>，从入门到<em>实战</em>，一次搞定！</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2401_84494441">2401_84494441的博客</a><br></p><p>07-29<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1000<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/149742300">本文系统梳理了五种主流<em>Agent设计模式</em>：1. <em>ReAct</em>（2022）：结合推理<em>与</em>行动的闭环系统，通过"思考-行动-观察"循环提升环境适应性，但存在延迟高、易漂移等问题；2. Plan-and-Execute：经典的两阶段"规划-执行"开环<em>模式</em>，适合结构化任务但缺乏灵活性；3. ReWoo（2023）：改进版规划<em>模式</em>，通过并行执行和独立求解模块提升效率；4. Reflexion（2023）：引入执行轨迹评估和反思机制的闭环系统，具备持续优化能力；<em>5</em>. ReflAct（202<em>5</em>）：实时目标对齐的微反思<em>模式</em>，将</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/2501_91912247/article/details/150223307">AI应用<em>架构</em>师<em>必备</em>：智能数字资产流转平台的跨链交互<em>架构</em>设计<em>指南</em>（附协议<em>详解</em>）</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2501_91912247">AI 算法实战派</a><br></p><p>08-11<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1070<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2501_91912247/article/details/150223307">智能数字资产是指通过区块链技术确权、流转的AI相关无形资产，其<em>核心</em>特征是“可编程性”和“价值<em>与</em>功能绑定”——不仅可交易，还能通过智能合约触发特定功能（如调用AI模型推理、授权数据访问）。类型定义示例跨链需求AI模型资产以代码/参数形式存在的AI模型，通过NFT/Token化确权GPT-4模型参数NFT、Stable Diffusion权重Token跨链传输时需验证参数完整性、推理性能一致性训练数据资产标注数据、数据集的使用权或所有权凭证医疗影像标注数据集NFT、金融时序数据Token。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://dreamit.blog.csdn.net/article/details/147652993">AIGC领域多模态<em>大模型</em>在游戏AI中的应用创新<em>案例</em></a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/universsky2015">AI天才研究院</a><br></p><p>05-01<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>965<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://dreamit.blog.csdn.net/article/details/147652993">随着《塞尔达传说：王国之泪》《博德之门3》等现象级游戏的成功，游戏行业对AI技术的需求已从简单的路径规划升级为具备创意生成、自然交互和动态决策能力的智能系统。传统单模态AI（如纯文本对话模型或图像生成模型）难以处理游戏中复杂的多维度输入（如玩家语音、手势、场景图像），而多模态<em>大模型</em>通过融合文本、图像、语音、视频等多维度数据，为构建沉浸式游戏体验提供了革命性解决方案。智能NPC交互动态内容生成和玩家行为分析，结合具体技术<em>案例</em>解析其技术<em>架构</em>、算法实现和工程落地经验。<em>核心</em>概念。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://wenku.csdn.net/column/43s6pzof6e">【ESP32 Wi-Fi调试终极<em>指南</em>】：10大常见连接问题深度解析<em>与实战</em>解决方案</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://wenku.csdn.net/column/43s6pzof6e">ESP32 Wi-Fi连接的<em>核心</em>机制<em>与</em>工作原理 ## 1.1 ESP32 Wi-Fi协议栈<em>架构</em>解析 ESP32的Wi-Fi功能基于IEEE 802.11 b/g/n标准，集成于自研的PHY和MAC层硬件模块，并通过乐鑫专有的TCP/IP协议栈（LWIP）<em>与</em>上层应用交互。...</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/2401_85133351/article/details/141441204">Big Data 原理<em>与</em>代码<em>实战案例</em>讲解</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2401_85133351">AI大模型应用之禅</a><br></p><p>08-23<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>221<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2401_85133351/article/details/141441204">Big Data 原理<em>与</em>代码<em>实战案例</em>讲解<br>作者：禅<em>与</em>计算机程序设计艺术 / Zen and the Art of Computer Programming<br>1. 背景介绍<br>1.1 问题的由来<br>随着互联网、物联网、移动设备等</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/146499710">产品经理研读：<em>Agent</em>的九种<em>设计模式</em>(图解+代码)建议人手一份，<em>收藏</em>起来慢慢学！！</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/Gaga246">Gaga246的博客</a><br></p><p>03-25<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1183<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/146499710">接下来讲讲每个<em>模式</em>的原理，以及代码实现(看代码能帮助产品经理加深理解，因为这些<em>设计模式</em>都是以结构化 prompt 的方式藏在代码里)。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/qq_27590277/article/details/137259140">每日论文速递 | <em>ReAct</em> Meets ActRe<em>:</em> <em>Agent</em>规划自主解释</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/qq_27590277">zenRRan的博客</a><br></p><p>04-01<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>434<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/qq_27590277/article/details/137259140">深度<em>学习</em>自然语言处理 分享整理：pp摘要：语言代理通过对基础模型进行推理，展示了自主决策能力。最近，人们开始利用多步骤推理和行动轨迹作为训练数据，努力训练语言代理以提高其性能。然而，收集这些轨迹仍然需要大量人力，要么需要人工注释，要么需要实现各种提示框架。在这项工作中，我们提出了 AT，这是一个能以 <em>ReAct</em> 风格实现代理轨迹自主注释的框架。其<em>核心</em>角色是一个 ActRe 提示代理，负责解释任意行...</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/qq_45066628/article/details/152372823"><em>大模型Agent</em>五大工作<em>模式</em>深度解析</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/qq_45066628">kuokay的博客</a><br></p><p>10-01<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1201<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/qq_45066628/article/details/152372823">要理解一个<em>大模型Agent</em>如何工作，<em>核心</em>在于它背后所依赖的 工作<em>模式</em>。目前主流的<em>Agent</em>大多围绕五种关键<em>模式</em>：反射<em>模式</em>（Reflection pattern ）：让模型通过自我检视和修正提升推理能力；工具使用<em>模式</em>（ Tool use pattern）：赋予模型调用外部工具<em>与</em>系统的能力；<em>ReAct模式</em>（Reason and Act）：在推理<em>与</em>行动之间动态切换，实现更高效的决策；规划<em>模式</em>（Planning pattern）：让模型具备长期目标分解<em>与</em>任务执行的能力；</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/150921347">深度讲解智能体：<em>ReACT</em> <em>Agent</em></a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/Peter_Changyb">Peter_Changyb的博客</a><br></p><p>08-27<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1456<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/150921347">通过将推理<em>与</em>行动紧密结合，<em>ReACT</em> <em>Agent</em> 让大语言模型能交替生成推理轨迹（Thought）<em>与</em>特定任务行动（Action），开启了两者协同工作的新<em>模式</em>。<br>MCP 服务器提供具体功能服务，包括暴露资源、提示模板和工具等能力。工作时，主机中的<em>大模型</em>通过客户端向服务器发送请求，服务器依据请求返回相应结果。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://devpress.csdn.net/v1/article/detail/155229889"><em>收藏必备</em>！AI <em>Agent</em>五大<em>核心设计模式详解</em>：从<em>ReAct</em>到人机协作，助你构建智能系统</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/2401_85327249">2401_85327249的博客</a><br></p><p>11-25<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>864<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://devpress.csdn.net/v1/article/detail/155229889">本文系统介绍了五种AI <em>Agent核心设计模式</em>：<em>ReAct模式</em>通过推理-行动循环处理外部信息任务；CodeAct<em>模式</em>通过生成代码解决复杂计算；计划<em>模式</em>提供结构化执行路径；反思<em>模式</em>通过迭代优化提升输出质量；人机协作<em>模式</em>在关键节点引入人工判断。各<em>模式</em>有不同适用场景，实际应用中可组合使用，帮助<em>开发</em>者构建高效可靠的<em>Agent</em>系统。</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://blog.csdn.net/javatiange/article/details/151223724"><em>Agent</em>九种<em>设计模式</em>有哪些？看完你的AI<em>大模型</em>就很牛了！</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/javatiange">javatiange的博客</a><br></p><p>09-05<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>1125<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/javatiange/article/details/151223724">AI <em>Agent设计模式</em>概览 AI <em>Agent</em>通过感知、规划、行动三步骤动态完成任务，需具备推理、记忆、工具和行动四大模块。目前主流有9种<em>设计模式</em>，其中<em>5</em>种<em>核心模式</em>如下： <em>ReAct模式</em>：结合推理<em>与</em>行动，通过"行动-观察"循环动态调整策略，提升任务执行的连贯性和准确性。 Plan and Solve<em>模式</em>：先规划再执行，适用于多阶段任务（如烹饪），支持动态调整计划（如缺食材时新增步骤）。 REWOO<em>模式</em>：隐式观察依赖关系，适用于审批流等环环相扣的任务，通过链式计划自动传递上一步输出。 LL</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tit" href="https://zhangjq.blog.csdn.net/article/details/147336474"><em>Agent</em>的九种<em>设计模式</em> 介绍</a></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://blog.csdn.net/qq_38998213">ZJQ的博客</a><br></p><p>04-18<br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/readCountWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>432<br><br></p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link" href="https://zhangjq.blog.csdn.net/article/details/147336474">原理：将推理（Reasoning）和行动（Acting）相结合，使<em>Agent</em>能够在推理的指导下采取行动，并根据行动的结果进一步推理，形成一个循环。<em>Agent</em>通过生成一系列的思维链（Thought Chains）来明确推理步骤，并根据推理结果执行相应的动作，<em>与</em>环境进行交互，获取反馈后再进行下一轮的推理和行动。应用场景：广泛应用于需要<em>与</em>外部环境进行交互并解决问题的场景，如知识问答、信息检索、任务规划等。</a></p><ul><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://www.csdn.net/company/index.html#about">关于我们</a><br></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://www.csdn.net/company/index.html#recruit">招贤纳士</a><br></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://fsc-p05.txscrm.com/T8PN8SFII7W">商务合作</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://marketing.csdn.net/questions/Q2202181748074189855">寻求报道</a></p></li><li><p><img class="editor-image" src="https://g.csdnimg.cn/common/csdn-footer/images/tel.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>400-660-0108<br></p></li><li><p><img class="editor-image" src="https://g.csdnimg.cn/common/csdn-footer/images/email.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><a target="_blank" rel="nofollow" class="editor-link" href="mailto:webmaster@csdn.net">kefu@csdn.net</a><br></p></li><li><p><img class="editor-image" src="https://g.csdnimg.cn/common/csdn-footer/images/cs.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br><a target="_blank" rel="nofollow" class="editor-link" href="https://csdn.s2.udesk.cn/im_client/?web_plugin_id=29181">在线客服</a><br></p></li><li><p><br>工作时间&nbsp;8:30-22:00<br></p></li></ul><ul><li><p><img class="editor-image" src="https://g.csdnimg.cn/common/csdn-footer/images/badge.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><a target="_blank" rel="nofollow" class="editor-link" href="http://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11010502030143">公安备案号11010502030143</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="http://beian.miit.gov.cn/publish/query/indexFirst.action">京ICP备19004658号</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://csdnimg.cn/release/live_fe/culture_license.png">京网文〔2020〕1039-165号</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://csdnimg.cn/cdn/content-toolbar/csdn-ICP.png">经营性网站备案信息</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="http://www.bjjubao.org/">北京互联网违法和不良信息举报中心</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://download.csdn.net/tutelage/home">家长监护</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://cyberpolice.mps.gov.cn/">网络110报警服务</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="http://www.12377.cn/">中国互联网举报中心</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://chrome.google.com/webstore/detail/csdn%E5%BC%80%E5%8F%91%E8%80%85%E5%8A%A9%E6%89%8B/kfkdboecolemdjodhmhmcibjocfopejo?hl=zh-CN">Chrome商店下载</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://blog.csdn.net/blogdevteam/article/details/126135357">账号管理规范</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://www.csdn.net/company/index.html#statement">版权与免责声明</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://blog.csdn.net/blogdevteam/article/details/90369522">版权申诉</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://img-home.csdnimg.cn/images/20250103023206.png">出版物许可证</a></p></li><li><p><a target="_blank" rel="nofollow" class="editor-link" href="https://img-home.csdnimg.cn/images/20250103023201.png">营业执照</a></p></li><li><p>©1999-2026北京创新乐知网络技术有限公司</p></li></ul><p>登录后您可以享受以下权益：</p><ul><li><p>免费复制代码</p></li><li><p>和博主大V互动</p></li><li><p>下载海量资源</p></li><li><p>发动态/写文章/加入社区</p></li></ul><p><span style="font-size: 22px; color: rgb(153, 153, 153);">×</span>立即登录</p><p>评论 <br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/closeBt.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/commentArrowLeftWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;">被折叠的&nbsp;&nbsp;条评论<br><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link tip" href="https://blogdev.blog.csdn.net/article/details/122245662">为什么被折叠?</a><br><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link park" href="https://bbs.csdn.net/forums/FreeZone"><br><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/iconPark.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;">到【灌水乐园】发言</a> <br></p><p>查看更多评论<img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/commentArrowDownWhite.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><p><br>添加红包<br><br></p><p>祝福语<br></p><p>请填写红包祝福语或标题</p><p>红包数量<br></p><p>个<br></p><p>红包个数最小为10个</p><p>红包总金额<br></p><p>元<br></p><p>红包金额最低5元</p><p>余额支付<br></p><p><br>当前余额3.43元<br><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link link-charge" href="https://i.csdn.net/#/wallet/balance/recharge">前往充值 &gt;</a><br></p><p><br>需支付：10.00元<br></p><p>取消<br>确定<br></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward02.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>下一步</p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/guideRedReward03.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>知道了</p><p>实付元</p><p>使用余额支付</p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/pay-time-out.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>点击重新获取<br></p><p><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/weixin.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/zhifubao.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/jingdong.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;">扫码支付</p><p>钱包余额<br><span style="font-size: 14px; color: rgb(252, 85, 49);">0</span><br></p><p>抵扣说明：</p><p>1.余额是钱包充值的虚拟货币，按照1:1的比例进行支付金额的抵扣。<br>2.余额无法直接购买下载，可以购买VIP、付费专栏及课程。</p><p><a target="_blank" rel="noopener noreferrer nofollow" class="editor-link pay-balance-con" href="https://i.csdn.net/#/wallet/balance/recharge"><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/recharge.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;">余额充值</a><br></p><p><span style="color: rgb(255, 255, 255);">确定</span><span style="color: rgb(34, 34, 38);">取消</span><img class="editor-image" src="https://csdnimg.cn/release/blogv2/dist/pc/img/closeBt.png" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"></p><p>举报</p><p>选择你想要举报的内容（必选）</p><ul><li><p>内容涉黄</p></li><li><p>政治相关</p></li><li><p>内容抄袭</p></li><li><p>涉嫌广告</p></li><li><p>内容侵权</p></li><li><p>侮辱谩骂</p></li><li><p>样式问题</p></li><li><p>其他</p></li></ul><p>原文链接（必填）</p><p>请选择具体原因（必选）</p><ul><li><p>包含不实信息</p></li><li><p>涉及个人隐私</p></li></ul><p>请选择具体原因（必选）</p><ul><li><p>侮辱谩骂</p></li><li><p>诽谤</p></li></ul><p>请选择具体原因（必选）</p><ul><li><p>搬家样式</p></li><li><p>博文样式</p></li></ul><p>补充说明（选填）</p><p>取消</p><p>确定</p><p>下载APP<br></p><p>程序员都在用的中文IT技术交流社区</p><p>公众号<br></p><p>专业的中文 IT 技术社区，与千万技术人共成长</p><p>视频号<br></p><p>关注【CSDN】视频号，行业资讯、技术分享精彩不断，直播好礼送不停！</p><p><img class="editor-image" src="https://g.csdnimg.cn/side-toolbar/3.6/images/customer.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>客服<br><br><br><br><br><img class="editor-image" src="https://g.csdnimg.cn/side-toolbar/3.6/images/totop.png" alt="" containerstyle="" wrapperstyle="display: inline-block; float: left; padding-right: 8px;"><br>返回顶部<br><br><br></p>