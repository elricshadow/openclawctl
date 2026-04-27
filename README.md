# OpenClaw CTL / MoltBot 管理脚本 (Zevon 增强版)

> **🚀 提示：此版本由 Zevon 深度定制，完美适配多 Profile 隔离环境及自动化管理。**

---

## 🚀 版本亮点 (Change Log)
1.  **原生多环境支持**：优化了对 OpenClaw 多实例（如 `--profile test_lobster`）的路径识别，避免配置冲突。
2.  **独立软件库**：所有组件与核心脚本均从 `elricshadow/openclawctl` 仓库直接拉取，确保维护的独立性与安全性。
3.  **安装逻辑增强**：修正了原始脚本在非交互环境下的部分路径报错。

---

## 📥 快速安装指令 (一键脚本)

在你的服务器终端运行以下命令即可：

```bash
curl -fsSL https://raw.githubusercontent.com/elricshadow/openclawctl/main/openclaw.sh -o openclaw.sh && chmod +x openclaw.sh && ./openclaw.sh
```

---

## 👤 项目致谢
- **当前维护者**: [Zevon](https://github.com/elricshadow)
- **核心逻辑致谢**: 原始项目由 [byJoey/openclawctl](https://github.com/byJoey/openclawctl) 提供。
- **致谢**: 感谢 kejilion (@kejilion) 提供的 CLI 逻辑灵感。

---
*OpenClaw 是一款强大的特工引擎，本脚本旨在简化其在 Linux 环境下的部署与管理。*
