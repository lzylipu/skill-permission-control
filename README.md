# Permission Control Skill

**[English](./README.md) | [中文](./README.zh-CN.md)**

Enforce explicit user authorization before executing sudo/root commands. Only VPN-related commands are auto-allowed.

## Rules

- **Whitelist (auto-allow)**: `ipsec start/stop/up/down/status/restart`
- **Everything else**: Must get explicit user confirmation (say "execute", "allow", "confirm")

## Authorization Keywords

Valid: execute, allow, confirm, "use sudo"

Invalid: hmm, oh, whatever, silence

## License

MIT
