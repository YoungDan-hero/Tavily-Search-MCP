# 🌐 Tavily Search MCP Server

基于 [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) 标准开发的网络搜索服务。通过接入 [Tavily API](https://tavily.com/)，为大语言模型（如 OpenClaw、Claude Desktop 等）赋予实时、准确的互联网搜索与内容提取能力。

## ✨ 特性

- **无需安装**：通过 `npx` 直接从 GitHub 远程加载运行，无需全局安装 npm 包。
- **专为 AI 优化**：Tavily 搜索引擎专为 LLM Agent 设计，返回纯净、高相关性的上下文，而非广告。
- **高优先级搜索**：内置指令引导大模型优先使用此专业工具进行联网查询。
- **类型安全**：基于 Zod 进行严格的参数校验，确保服务运行稳定。

---

## 🚀 如何在 OpenClaw 中使用

如果你是 OpenClaw 用户，请按照以下步骤配置：

### 1. 获取 Tavily API Key

1. 访问 [Tavily 官网](https://app.tavily.com/home) 并注册账号。
2. 在控制台中获取你的 API Key（以 `tvly-` 开头）。
3. 确保你的电脑已安装了 [Node.js](https://nodejs.org/)（推荐 v18 或以上版本）。

### 2. 修改 OpenClaw 配置文件

打开 OpenClaw 的配置文件（通常位于 `~/.openclaw/openclaw.json`），在 `mcp.servers` 下添加以下内容：

```json
{
  "mcp": {
    "servers": {
      "tavily-search-server": {
        "command": "npx",
        "args": ["-y", "https://github.com/YoungDan-hero/Tavily-Search-MCP"],
        "env": {
          "TAVILY_API_KEY": "在此处替换为你的_tvly_API_Key"
        }
      }
    }
  }
}
```

### 3. 重启 OpenClaw

保存配置文件并重启 OpenClaw 客户端。现在，你可以尝试问它：“帮我搜一下今天最新的科技新闻”，它将调用 Tavily 进行搜索。
