# 权限控制技能

**[English](./README.md) | [中文](./README.zh-CN.md)**

执行 sudo/root 命令前强制要求用户明确授权。仅 VPN 相关命令自动放行。

## 规则

- **白名单（自动放行）**：`ipsec start/stop/up/down/status/restart`
- **其他所有命令**：必须获得用户明确确认（说"执行"、"允许"、"确认"）

## 授权关键词

有效：执行、允许、确认、"use sudo"

无效：嗯、哦、随便、沉默

## License

MIT
