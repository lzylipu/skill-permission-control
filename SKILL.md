---
name: permission-control
description: "Permission control - block sudo/root without explicit user authorization, VPN commands whitelisted"
version: 1.0.0
author: lzylipu
license: MIT
platforms: [linux]
metadata:
  hermes:
    tags: [permission, sudo, security, vpn, 权限, 安全]
    related_skills: [vpn-connect, openwrt-redial, wake-pc]
    homepage: https://github.com/lzylipu/skill-permission-control
    category: personal
    skill_type: constraint
---

# 权限控制规范

## 核心规则

⚠️ **未经用户明确授权，禁止执行任何需要 root/sudo 权限的操作**

---

## 白名单命令（可自动执行）

以下命令**无需用户确认**，可自动使用 sudo：

| 命令 | 用途 | 说明 |
|------|------|------|
| `ipsec start` | 启动 VPN 服务 | 内网访问必需 |
| `ipsec stop` | 停止 VPN 服务 | |
| `ipsec up <conn>` | 连接 VPN | |
| `ipsec down <conn>` | 断开 VPN | |
| `ipsec status` | 查看 VPN 状态 | 只读操作 |
| `ipsec restart` | 重启 VPN 服务 | |

**白名单理由**：VPN 是访问内网服务的前置依赖，用户发起的唤醒/重拨等操作隐含授权 VPN 连接。

---

## 需要确认的命令

以下操作**必须等待用户明确授权**：

| 类别 | 命令示例 | 需要确认 |
|------|----------|----------|
| 系统软件包 | `apt install/remove/upgrade` | ✅ |
| 系统服务 | `systemctl start/stop/enable/disable` | ✅ |
| 系统配置 | 修改 `/etc/` 下文件 | ✅ |
| 用户权限 | `useradd/usermod/userdel` | ✅ |
| 网络配置 | `ip route/iptables/ifconfig`（非 VPN） | ✅ |
| 文件权限 | `chmod/chown` 系统文件 | ✅ |
| 进程管理 | `kill/killall` 系统进程 | ✅ |
| 磁盘操作 | `mount/umount/fdisk` | ✅ |
| 其他 root 命令 | 任何未在白名单的 sudo 命令 | ✅ |

---

## 授权词

用户必须说以下之一才算授权：

- "执行" / "执行吧"
- "可以" / "可以执行"
- "允许" / "允许执行"
- "确认" / "确认执行"
- "用 sudo 执行"
- "用 root 执行"

**模糊回复不算授权**：
- ❌ "嗯" / "哦" / "好"
- ❌ "随便" / "都行"
- ❌ 沉默或无回复

---

## 执行流程

### 白名单命令（VPN）

```
用户: 开电脑
助手: [自动执行] sudo ipsec status
      [自动执行] sudo ipsec up <vpn-connection>（如未连接）
      [执行唤醒]
      ✅ 完成
```

### 需确认命令

```
用户: 安装 nginx

助手: ⚠️ 此操作需要 root 权限：
      sudo apt install nginx
      
      确认执行请回复「允许执行」

用户: 允许执行
助手: [执行] sudo apt install nginx
      ✅ 安装完成
```

---

## 禁止行为

| 禁止 | 说明 |
|-----|------|
| ❌ 诱导用户提权 | 不得主动请求 sudo 权限 |
| ❌ 绕过确认流程 | 未授权直接执行非白名单命令 |
| ❌ 模糊授权判定 | 非明确授权词视为拒绝 |
| ❌ 批量授权 | 一次授权不能覆盖多个无关操作 |

---

## 特殊情况

| 情况 | 处理 |
|-----|------|
| 用户直接给密码 | 可以使用，但仅限当前操作 |
| 用户说"随便用 sudo" | 视为全局授权，但仍需逐次告知 |
| 紧急安全操作 | 如防火墙规则阻止攻击，可先执行后报告 |

---

**版本**: 2.0  
**更新**: 2026-04-03  
**优先级**: 最高（覆盖其他技能的权限请求）