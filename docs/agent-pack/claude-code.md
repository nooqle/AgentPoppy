# Agent Jola for Claude Code

Claude Code can use Agent Jola through a copied instruction pack even when it does not load Codex skills directly.

## Prompt To Give Claude Code

```text
You are helping me set up Agent Jola.

Follow the Agent Jola workflow from this repository:
- install or verify the local project
- ask me to sign in at https://agentjola.art/portal and create a chameleon/Product API key
- never print raw API keys
- ask before writing Product API keys to .env.local
- ask separately before writing OpenAI or Anthropic provider keys
- show and confirm the final battle Prompt before applying it
- use pnpm agent:setting sync and pnpm agent:setting check to validate
- use mock mode first before provider-token mode
- ask before creating or joining a room

Start by checking whether this folder is already an Agent Jola repo.
```

## Useful Commands

```bash
pnpm doctor
pnpm build
pnpm agent:setting check
pnpm agent:templates
pnpm agent:template prompt zoneHunter --agent <name>
pnpm agent:setting sync
pnpm agent:mock
```

Use `skills/agent-jola/SKILL.md` as the source of truth for confirmation and safety rules.
