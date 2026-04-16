# 🌐 Tavily Search MCP Server

基于 [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) 标准开发的网络搜索服务。通过接入 [Tavily API](https://app.tavily.com/home)，为大语言模型（如 OpenClaw、Claude Desktop 等）赋予实时、准确的互联网搜索与内容提取能力。

## ✨ 特性

- **单文件即可运行**：下载一个 `index.js` 即可，无需克隆仓库、无需本地构建。
- **专为 AI 优化**：Tavily 搜索引擎专为 LLM Agent 设计，返回纯净、高相关性的上下文，而非广告。
- **高优先级搜索**：内置指令引导大模型优先使用此专业工具进行联网查询。
- **类型安全**：基于 Zod 进行严格的参数校验，确保服务运行稳定。

---

## Tavily Search MCP 服务器安装教程（OpenClaw）

本教程旨在帮助小白用户以最简单的方式，在 OpenClaw 中集成 Tavily 搜索功能。无需克隆代码，无需安装开发环境，仅需一个文件。

### 🛠️ 第一步：下载核心运行文件

你需要把仓库里的 `dist/index.js` 保存到本机任意位置（建议改名为 `tavily-mcp.js`，便于识别）。任选下面一种方式即可。

**前置条件**：已安装 [Node.js](https://nodejs.org/)（推荐 v18 或以上），并已获取 [Tavily API Key](https://app.tavily.com/home)（以 `tvly-` 开头）。

#### 方式一：在 GitHub 网页下载（无需命令行）

1. 在浏览器中打开本仓库的 **`dist/index.js`** 页面：  
   [在 GitHub 中查看 dist/index.js](https://github.com/YoungDan-hero/Tavily-Search-MCP/blob/main/dist/index.js)
2. 点击右上角的 **`Raw`**（原始文件），浏览器会打开纯文本页面。
3. 使用浏览器的 **另存为**（`Ctrl+S` / `Cmd+S`）保存到你想放的位置，例如保存为 `tavily-mcp.js`。  
   - 若浏览器直接下载了文件，请确认文件名是 `.js`，不要变成 `.txt`。
4. 记下该文件的 **完整路径**，下一步配置 `args` 时要填这个路径。

> 也可直接打开 [原始文件直链](https://github.com/YoungDan-hero/Tavily-Search-MCP/raw/main/dist/index.js)，多数浏览器会触发下载；若只显示代码，同样用 **另存为** 保存为 `tavily-mcp.js` 即可。

#### 方式二：使用命令行下载（MacOS / Linux）

打开 **终端 (Terminal)**，复制并运行：

```bash
curl -L -o ~/tavily-mcp.js https://github.com/YoungDan-hero/Tavily-Search-MCP/raw/main/dist/index.js && echo -e "\n✅ 安装完成！\n文件路径为: $HOME/tavily-mcp.js"
```

#### Windows 用户

打开 **PowerShell**（开始菜单搜索 PowerShell），复制并运行：

```powershell
curl.exe -L -o "$HOME\tavily-mcp.js" https://github.com/YoungDan-hero/Tavily-Search-MCP/raw/main/dist/index.js; Write-Host "`n✅ 安装完成！`n文件路径为: $HOME\tavily-mcp.js" -ForegroundColor Green
```

### ⚙️ 第二步：配置 OpenClaw

打开你的 OpenClaw 配置文件（通常是 `config.json`，也可能为 `openclaw.json` 等，以你本机为准）。

在 `mcp` → `servers` 下添加以下配置。

**注意**：请将 `args` 中的路径替换为你上一步命令输出的真实路径。

```json
{
  "mcp": {
    "servers": {
      "tavily-search": {
        "command": "node",
        "args": ["/Users/你的用户名/tavily-mcp.js"],
        "env": {
          "TAVILY_API_KEY": "这里填入你的_TAVILY_API_KEY"
        }
      }
    }
  }
}
```

> [!IMPORTANT]
> **Windows 用户**：路径请使用双反斜杠或正斜杠，例如：`"C:\\Users\\YourName\\tavily-mcp.js"` 或 `"C:/Users/YourName/tavily-mcp.js"`。

### 第三步：重启 OpenClaw

保存配置文件并重启 OpenClaw。之后可以尝试提问：「帮我搜一下今天最新的科技新闻」，客户端将调用 Tavily 进行搜索。
