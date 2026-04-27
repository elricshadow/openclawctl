# OpenClaw CTL / MoltBot 管理脚本 (Elric 增强版)

> **🚀 提示：此版本由 Elric 深度定制，完美适配多 Profile 隔离环境及自动化管理。**
> 
> 本脚本是在 [byJoey/openclawctl](https://github.com/byJoey/openclawctl) 基础上进行的二次开发与增强。

---

## 🚀 Elric 版新增/修改亮点 (Change Log)
1.  **原生多环境支持**：优化了对 OpenClaw 多实例（如 `--profile test_lobster`）的路径识别，避免主 Agent 配置冲突。
2.  **独立软件库**：所有组件与核心脚本均从 `elricshadow/openclawctl` 仓库直接拉取，确保维护的独立性与安全性。
3.  **安装逻辑增强**：修正了原始脚本在非交互环境下的部分路径报错，提升了在不同服务器环境下的兼容性。

---

## 📥 快速安装指令 (一键脚本)

在你的服务器终端运行以下命令即可（已自动适配 Elric 仓库）：

### macOS / Linux
```bash
curl -fsSL https://raw.githubusercontent.com/elricshadow/openclawctl/main/openclaw.sh -o openclaw.sh && chmod +x openclaw.sh && ./openclaw.sh
```

### Windows (PowerShell)
```powershell
powershell -ExecutionPolicy Bypass -Command "irm https://raw.githubusercontent.com/elricshadow/openclawctl/main/openclaw.ps1 | iex"
```

---

## 📖 原版本功能性说明 (by Joey)

OpenClaw CTL / MoltBot 的管理脚本，把常用操作都包进了一个交互式菜单里，省得每次手打命令。

支持 macOS（Intel / Apple Silicon）、主流 Linux 发行版和 Windows 11。

### 能做什么

- 一键安装全套（OpenClaw + CLIProxyAPI + OAuth + 自动配置）
- OpenClaw 的启动、停止、更新、卸载
- API 提供商管理，模型同步，延迟检测，模型切换
- CLIProxyAPI 的完整管理（服务控制、账号登录、Key 管理、日志查看）
- 对接机器人（Telegram、飞书、WhatsApp、Discord、Slack）
- 插件和技能安装
- 备份与还原（记忆 / 项目）
- 健康检测与修复
- WebUI 访问与设备配对
- 开机自启动管理

### 系统要求

| 系统 | 支持情况 |
|------|---------|
| Windows 11 | 完整支持，PowerShell 5.1+，依赖通过 winget 自动安装 |
| macOS Apple Silicon | 完整支持，依赖通过 Homebrew 自动安装 |
| macOS Intel | 完整支持，依赖通过 Homebrew 自动安装 |
| Ubuntu / Debian | 完整支持 |
| CentOS / Rocky / RHEL | 完整支持 |
| Alpine | 支持 |
| Arch Linux | 支持 |

### 依赖

所有依赖在首次运行时自动安装，无需手动操作：

- Windows：通过 winget 自动安装 Node.js 和 Git
- macOS：脚本会自动安装 Homebrew（如未安装），然后通过 brew 装其余依赖
- Linux：通过系统包管理器（apt / dnf / yum / apk / pacman）自动安装
- 依赖包括：Node.js、curl、git、nano、jq、python3、gum、fzf

### 小白模式

主菜单第一项，适合第一次安装。按顺序完成：

1. 安装 Node.js 和构建工具
2. 安装 OpenClaw（Windows 使用官方安装脚本，macOS/Linux 用 npm）
3. `openclaw onboard`（交互式向导）
4. 安装 CLIProxyAPI（macOS 用 brew，Linux 用一键脚本，Windows 从 GitHub 下载二进制）
5. OAuth 登录（支持 Claude / Gemini / OpenAI / Qwen / iFlow）
6. 启动 CLIProxyAPI 服务
7. 注册 CLIProxyAPI 为 API 提供商
8. 从可用模型里选一个作为默认
9. 询问是否跳转到机器人对接

装完即可用，不需要再手动改配置文件。

### OAuth 登录说明

#### Windows / macOS
有本地浏览器，直接运行登录命令，浏览器自动打开，授权后回调自动处理，全程无需手动操作。

#### Linux 服务器
服务器没浏览器，登录流程稍微绕一点，但不需要 SSH 端口转发：
1. 脚本在后台启动 `cli-proxy-api --no-browser`，终端里会打印授权 URL
2. 在本地浏览器里打开那个 URL，完成账号授权
3. 授权成功后浏览器会跳转到 `localhost:<port>/oauth2callback?code=...`，页面报连接失败，这是正常的
4. 把地址栏里的完整 URL 复制出来，粘贴到脚本的输入框里
5. 脚本用 curl 把这个回调 URL 发给服务器本地正在监听的进程，完成握手

### CLIProxyAPI 管理

| 操作 | 说明 |
|------|------|
| 启动 / 停止 / 重启 | Windows 用后台进程，macOS 用 brew services，Linux 优先 systemd |
| 查看日志 | Windows 读日志文件，macOS 读 brew 日志，Linux 用 journalctl |
| 账号授权登录 | 五个提供商都支持 |
| 生成并添加 API Key | 生成 sk- 格式的 key，自动写入 config.yaml |
| 查看 API Keys | 列出当前配置的全部 key |
| 编辑配置文件 | Windows 用 notepad，macOS/Linux 用 nano |
| 更新 | Windows 重新下载二进制，macOS 用 brew upgrade，Linux 拉最新版本 |
| 卸载 | 停服务，删目录 |

### 注意事项

**模型切换会重启网关。** 切完之后 OpenClaw gateway 会自动重启，Telegram 机器人有几秒不可用。

**onboard 时随便选的模型不用管。** 安装完成后脚本会让你重新选一个实际可用的模型覆盖掉，不会用 onboard 时选的那个。

**只显示可用模型。** 模型选择界面只列出状态是 `configured` 的，没配好的不会出现。

---

## 👤 项目致谢
- **原始作者**: [Joey](https://github.com/byJoey)
- **YouTube**: [@joeyblog](https://youtube.com/@joeyblog)
- **核心逻辑致谢**: 原始项目由 [byJoey/openclawctl](https://github.com/byJoey/openclawctl) 提供。
- **致谢**: 感谢 kejilion (@kejilion) 及 cliproxyapi-installer。

---
*注：本项目作为学习与自动化部署工具，请在遵守相关法律法规的前提下使用。*
