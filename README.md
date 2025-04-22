过程记录 
1. 实现一个简单的LLM应用 
- 创建对话模板ChatTemplate 
- 创建基于Ark的chatmodel，调用火山引擎的模型服务 
- 创建generate和stream两种输出模式

2. content部分
- 将传入的会议内容，转换成json，并分别提取各部分信息。
- 确定meeting组成部分
- 确定prompt提示词
- participants、start_time、end_time、content直接截取，title、description由llm生成 

3. summary部分
- 确定summary组成部分
- 每个meeting对应一个summary
- 确定prompt提示词
- 以json格式输出 

4. chat部分 
- 在缓存中存储历史记录，每个meeting对应一个历史记录
- 确定prompt提示词
- 创建SSE 流对象，llm采用stream输出方式，并构建一个通道当流输出到结尾时控制关闭 

5. todo部分
- 基于Summary给出的关键任务进行分割，得到 todos 列表
- 引入 todo-list-mcp 服务，封装为 MCP Tool 实现对数据库的操作
- 将 todos 列表通过 template 组装为 Agent 的 Prompt，调用MCP完成操作
