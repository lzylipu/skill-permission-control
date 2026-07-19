# 🛡️ Permission Control Skill / 安全权限拦截控制器

> 🌐 English | [简体中文](./README.md)
> Enforce explicit user authorization before executing sudo/root commands. Only VPN-related commands are auto-allowed.
> 强制在执行含有 sudo/root 权限的敏感命令前获取用户明确授权。仅 VPN 管理命令默认放行。

## 📋 Rules / 规则

| 类别 / Category | 策略 / Policy |
|---|---|
| ✅ **Whitelist (auto-allow) / 白名单（自动放行）** | `ipsec start/stop/up/down/status/restart` |
| ❌ **Everything else / 其他命令** | Must get explicit user confirmation / 需用户明确授权 |

## 💬 Authorization Keywords / 授权词汇

| 状态 / Status | 词汇 / Keywords |
|---|---|
| **Valid / 放行** | `execute`, `allow`, `confirm`, `use sudo`, `允许`, `放行`, `确认` |
| **Invalid / 拒绝** | `hmm`, `oh`, `whatever`, `silence`, `拒绝`, `不行` |

## 📄 License / 许可证

MIT. See [LICENSE](./LICENSE).
