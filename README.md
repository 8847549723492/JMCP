JMCP

JMCP is a remote Linux / VPS MCP Server for AI clients.

JMCP allows compatible AI clients to interact with a remote Linux/VPS through MCP, including command execution, file operations, workspace management, and optional GUI control.

JMCP provides:

* MCP Server
* OAuth 2.1 authentication
* Passkey authentication
* Web Dashboard
* Remote command execution
* File operations
* Workspace management
* Connection and token management
* Optional GUI control

Language: 中文⁠￼ · English⁠￼

⸻

中文

JMCP 是什么？

JMCP 是一个运行在 Linux/VPS 上的 MCP Server，用于让支持 MCP 的 AI 客户端连接并操作远程服务器。

AI 客户端可以通过 JMCP：

* 执行 Linux 命令
* 读取和修改文件
* 操作 MCP 工作区
* 查看服务器状态
* 使用可选的 GUI 操控功能

JMCP 同时提供 OAuth 2.1、Passkey 和 Web Dashboard，用于管理连接和服务器访问。

⸻

⚠️ 使用前必须知道

必须拥有域名

JMCP 必须使用域名。

你的 VPS / 服务器必须满足以下条件之一：

* VPS 服务商已经提供可使用的域名
* 你在部署 JMCP 后自行配置域名

域名必须解析到你的 VPS / 服务器，并且必须能够通过 HTTPS 访问。

正确示例：

https://example.com

不支持：

http://123.123.123.123:3000

在使用 JMCP 前，请确保：

* 域名已经解析到 VPS
* DNS 配置正常
* HTTPS 证书已经配置
* 必要的反向代理已经配置
* 域名可以从公网正常访问

JMCP 的 BASE_URL 必须使用 HTTPS 域名：

BASE_URL=https://example.com

AI 操作导致的服务器损坏

JMCP 允许连接的 AI 客户端在 VPS / 服务器上执行命令和进行其他操作。

用户需要自行承担允许 AI 执行操作所产生的风险。

如果 AI 客户端执行危险指令导致：

* VPS / 服务器损坏
* 文件或数据被删除
* 系统服务损坏
* 系统配置被修改
* 服务器无法正常运行
* 数据丢失
* 服务中断
* 服务器无法访问
* 其他任何服务器损坏或异常

项目作者不对由此产生的任何损失、损坏、停机或其他后果承担责任。

请在允许 AI 执行危险操作之前仔细确认操作内容。

🔐 绝对不要向 Agent 提供 sudo 密码

不要把你的 sudo password 提供给 AI Agent。

不要通过以下任何方式提供：

* 聊天消息
* MCP 参数
* 环境变量
* 配置文件
* Tool 参数
* 其他任何方式

JMCP 不需要 AI Agent 知道你的 sudo 密码。

⸻

🚀 快速开始

1. 进入 JMCP 目录

cd JMCP

2. 赋予安装脚本执行权限

chmod +x install.sh

3. 运行安装程序

./install.sh

安装程序会引导你完成：

* 中文 / English
* BASE_URL
* 管理员密码
* 可选 GUI 支持

4. 启动 JMCP

安装完成后：

npm start

完整流程：

cd JMCP
chmod +x install.sh
./install.sh
npm start

启动后：

Dashboard:
https://你的域名/dashboard
MCP:
https://你的域名/mcp

默认 AI 工作区：

$HOME/mcp-workspace

⸻

🌐 Dashboard

打开：

https://你的域名/dashboard

Dashboard 支持中文和 English。

可以在 Dashboard 中：

* 查看 CPU 使用情况
* 查看内存使用情况
* 查看磁盘使用情况
* 查看服务器运行时间
* 查看 MCP 工作区
* 查看授权连接
* 重命名连接
* 永久撤销 Token
* 管理 Passkey
* 修改管理员密码
* 清空工作区
* 查看 GUI 状态
* 创建 ChatGPT / 手动接入凭据

清空工作区需要 JMCP 登录密码或 Dashboard Passkey 二次验证。

⸻

🔌 MCP

JMCP 的 MCP 地址：

https://你的域名/mcp

将此地址配置到支持 MCP 的 AI 客户端即可连接 JMCP。

⸻

🤖 ChatGPT / 手动接入

对于不支持自动客户端注册的平台，可以进入：

Dashboard
→ ChatGPT / Manual Client

生成：

client_id
client_secret

然后配置：

Authorization URL:
https://你的域名/authorize
Token URL:
https://你的域名/token
MCP URL:
https://你的域名/mcp

具体配置方式取决于所使用的 AI 客户端。

⸻

⚠️ 危险命令确认

JMCP 对危险 MCP 命令提供额外确认机制。

危险命令必须先获得用户明确确认，然后客户端才能使用：

confirmed: true

执行。

即使 JMCP 提供了确认机制，用户仍然需要自行判断 AI 即将执行的命令是否安全。

确认机制不是服务器损坏的保险。

⸻

🔑 Token 安全

JMCP 的授权 Token 是永久有效的。

Token 不会因为长时间没有使用而自动失效。

如果某个连接不再使用，请在 Dashboard 中撤销对应连接。

不要公开以下信息：

Token
client_secret
管理员密码
.env



⸻

🖥️ GUI 操控

GUI 操控属于可选功能。

JMCP 可以使用：

Xvfb
xdotool
scrot

或者服务器已有的：

VNC / X Desktop

部分 VPS 服务商可能没有安装系统软件所需的权限，因此 GUI 功能可能无法使用。

GUI 操控不是 JMCP 基础 MCP 功能正常运行的必要条件。

⸻

🔄 VPS 保活

JMCP 主程序和 Dashboard 都必须保持正常运行。

不同 VPS 服务商提供的运行环境不同，因此可能需要分别配置：

* Node.js 应用保活
* 反向代理
* 网站入口
* 端口映射

不要只保证：

npm start

一直运行，却让 Dashboard 的 Web 服务入口停止。

正常运行时应确保：

JMCP Server     ✓
Dashboard       ✓
HTTPS           ✓
Domain          ✓
Reverse Proxy   ✓

⸻

📁 项目结构

基本项目结构：

JMCP/
├── server.js
├── install.sh
├── README.md
├── package.json
├── package-lock.json
└── data/

默认 AI 工作区：

$HOME/mcp-workspace

⸻

🔒 安全检查

部署 JMCP 前，请确认：

* 已配置域名
* 域名已经解析到 VPS
* HTTPS 正常工作
* BASE_URL 使用 HTTPS 域名
* 不要向 AI Agent 提供 sudo 密码
* 不要上传 .env
* 不要上传密码
* 不要上传 Token
* 不要公开 client_secret
* 不使用的连接及时撤销
* 执行危险命令前仔细检查

⸻

📜 免责声明

JMCP 允许 AI 客户端在用户授权后执行服务器操作。

用户对允许 AI 执行的操作自行负责。

如果 AI 客户端执行任何危险、错误或具有破坏性的操作，并导致 VPS / 服务器发生任何形式的损坏、数据丢失、配置错误、服务中断、系统故障或其他后果，项目作者不承担任何责任。

用户在使用 JMCP 前，应充分了解 AI 客户端拥有的操作权限以及可能产生的风险。

⸻

English

What is JMCP?

JMCP is a remote Linux / VPS MCP Server for AI clients.

It allows compatible AI clients to interact with a remote Linux/VPS through MCP, including:

* Linux command execution
* File operations
* Workspace management
* Server status
* Optional GUI control

JMCP also provides:

* OAuth 2.1 authentication
* Passkey authentication
* Web Dashboard
* Connection management
* Token management

⸻

⚠️ Important

A domain name is required

JMCP requires a domain name.

Your VPS/server must either:

* Already have a usable domain provided by your VPS provider, or
* Have a domain configured by you after deployment.

The domain must point to your VPS/server and must be accessible through HTTPS.

Supported:

https://example.com

Not supported:

http://123.123.123.123:3000

Before using JMCP, make sure that:

* The domain points to your VPS
* DNS is configured correctly
* HTTPS is configured
* The required reverse proxy is configured
* The domain is publicly accessible

BASE_URL must use your HTTPS domain:

BASE_URL=https://example.com

AI operations and server damage

JMCP allows connected AI clients to execute commands and perform other operations on your VPS/server.

You are responsible for the operations you allow an AI client to perform.

If an AI client executes a dangerous command that causes:

* VPS/server damage
* Deleted files or data
* Broken system services
* Modified system configuration
* Server downtime
* Data loss
* Service interruption
* Server unavailability
* Any other damage or disruption

the project author assumes no responsibility for any resulting damage, loss, downtime, or other consequences.

Review dangerous operations carefully before allowing an AI client to execute them.

🔐 Never provide your sudo password to an Agent

DO NOT give your sudo password to an AI Agent.

Never provide it through:

* Chat messages
* MCP parameters
* Environment variables
* Configuration files
* Tool arguments
* Any other method

JMCP does not require the AI Agent to know your sudo password.

⸻

🚀 Quick Start

1. Enter the JMCP directory

cd JMCP

2. Make the installer executable

chmod +x install.sh

3. Run the installer

./install.sh

The installer will guide you through:

* Chinese / English
* BASE_URL
* Admin password
* Optional GUI support

4. Start JMCP

After installation:

npm start

Complete setup:

cd JMCP
chmod +x install.sh
./install.sh
npm start

After JMCP starts:

Dashboard:
https://your-domain/dashboard
MCP:
https://your-domain/mcp

Default AI workspace:

$HOME/mcp-workspace

⸻

🌐 Dashboard

Open:

https://your-domain/dashboard

The Dashboard supports both Chinese and English.

It provides:

* CPU usage
* Memory usage
* Disk usage
* Server uptime
* MCP workspace information
* Authorized connection management
* Connection renaming
* Permanent token revocation
* Passkey management
* Admin password management
* Workspace clearing
* GUI status
* ChatGPT / manual integration credentials

Clearing the workspace requires the JMCP login password or Dashboard Passkey step-up verification.

⸻

🔌 MCP

The JMCP MCP endpoint is:

https://your-domain/mcp

Configure this URL in an MCP-compatible AI client.

⸻

🤖 ChatGPT / Manual Integration

For platforms that do not support automatic client registration, open:

Dashboard
→ ChatGPT / Manual Client

Generate:

client_id
client_secret

Then configure:

Authorization URL:
https://your-domain/authorize
Token URL:
https://your-domain/token
MCP URL:
https://your-domain/mcp

The exact configuration process depends on the AI client.

⸻

⚠️ Dangerous Command Confirmation

JMCP provides an additional confirmation mechanism for dangerous MCP commands.

A dangerous command must receive explicit user confirmation before the client can execute it with:

confirmed: true

Even with this mechanism, users are responsible for determining whether an operation is safe.

The confirmation mechanism is not a guarantee against server damage.

⸻

🔑 Token Security

JMCP authorization tokens are permanent.

Tokens do not automatically expire simply because they have not been used for a long time.

If a connection is no longer needed, revoke it from the Dashboard.

Never publish:

Token
client_secret
Admin password
.env

Do not upload authentication credentials or other sensitive information to GitHub.

⸻

🖥️ GUI Control

GUI control is optional.

JMCP can use:

Xvfb
xdotool
scrot

or an existing:

VNC / X Desktop

Some VPS providers may not allow users to install the required system packages, so GUI control may be unavailable.

GUI control is not required for the basic MCP functionality.

⸻

🔄 VPS Keep-Alive

Both the JMCP application and Dashboard must remain available.

Depending on your VPS provider, you may need to configure:

* Node.js process keep-alive
* Reverse proxy
* Website entry
* Port mapping

Do not keep:

npm start

running while allowing the Dashboard web entry to stop working.

A working deployment should keep:

JMCP Server     ✓
Dashboard       ✓
HTTPS           ✓
Domain          ✓
Reverse Proxy   ✓

available.

⸻

📁 Project Structure

A basic JMCP project contains:

JMCP/
├── server.js
├── install.sh
├── README.md
├── package.json
├── package-lock.json
└── data/

The default AI workspace is:

$HOME/mcp-workspace

⸻

🔒 Security Checklist

Before deploying JMCP, make sure that:

* A domain has been configured
* The domain points to the VPS
* HTTPS is working
* BASE_URL uses an HTTPS domain
* You never provide your sudo password to an AI Agent
* .env is not uploaded
* Passwords are not uploaded
* Tokens are not uploaded
* client_secret is not exposed
* Unused connections are revoked
* Dangerous commands are reviewed before execution

⸻

📜 Disclaimer

JMCP allows AI clients to perform server operations after user authorization.

Users are responsible for the operations they allow AI clients to perform.

If an AI client performs any dangerous, incorrect, or destructive operation that causes any form of VPS/server damage, data loss, configuration failure, service interruption, system failure, or other consequence, the project author assumes no responsibility for the result.

Users should understand the permissions available to the connected AI client and the risks involved before using JMCP.

⸻

License

JMCP is distributed under the license included in the repository’s LICENSE file.
