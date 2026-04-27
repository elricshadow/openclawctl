# OpenClaw CTL / MoltBot 管理脚本 (Zevon 特供版)

---

### 👤 项目信息
- **原始作者**: [by Joey](https://github.com/byJoey)
- **当前维护**: **Zevon** (elricshadow)
- **致谢**: 原始脚本基础来自 kejilion (@kejilion) 及 cliproxyapi-installer。

---

### 🚀 Zevon 版新增/修改功能
本版本在原始版本基础上，由 Zevon 的 Agent 进行了深度定制与安全加固：

1.  **私有化适配**：全库 URL 已重定向至 Zevon 的私有 GitHub 仓库，确保 `oc` 快捷指令及脚本更新完全处于私有受控环境。
2.  **多 Profile 环境兼容**：修正了原始脚本中硬编码的 `.openclaw` 路径，增加了对多 Agent 实例（如 `--profile test_lobster`）的潜在支持。
3.  **安全性加固**：清理了可能导致敏感信息泄露的硬编码逻辑，优化了部分命令的执行权限校验。

---

### 📥 快速安装
```bash
curl -fsSL https://raw.githubusercontent.com/elricshadow/openclawctl/main/openclaw.sh -o openclaw.sh && chmod +x openclaw.sh && ./openclaw.sh
```

---
*注：本仓库仅供内部及授权用户使用。*
