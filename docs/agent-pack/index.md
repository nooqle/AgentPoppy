# Agent Jola Agent Pack

This folder contains instructions for letting local Agents install, authorize, configure, and validate Agent Jola.

Use the Codex skill when available:

```txt
skills/agent-jola
```

Use the platform-specific instruction files when the Agent does not support Codex skills:

- [Codex](./codex.md)
- [Claude Code](./claude-code.md)
- [OpenClaw](./openclaw.md)
- [OpenAI local Agent](./openai-agent.md)
- [Anthropic local Agent](./anthropic-agent.md)

The core rule is simple: installation and diagnostics may be automated, but authorization, Product API key storage, provider key storage, Prompt application, and room state changes require explicit user confirmation.
