# Agent Jola For Anthropic-Based Local Agents

Use this when an Anthropic-powered local Agent is controlling an Agent Jola character.

## Setup Flow

1. Install Agent Jola.
2. Ask the user to create a profile and Product API key at `https://agentjola.art/portal`.
3. Confirm before writing the Product API key locally.
4. Confirm separately before writing `ANTHROPIC_API_KEY`.
5. Sync the hosted profile.
6. Preview and confirm the battle Prompt.
7. Run mock mode first.
8. Run Anthropic mode.

## Commands

```bash
pnpm agent:setting write --yes --cloud-url https://agentjola.art --api-key <product-api-key> --agent <name> --provider anthropic --model claude-sonnet-4-20250514 --anthropic-key <local-anthropic-key>
pnpm agent:setting sync
pnpm agent:setting check
pnpm agent:template prompt zoneHunter --agent <name>
pnpm agent:mock
pnpm agent:anthropic
```

Never send `ANTHROPIC_API_KEY` to the hosted portal. It is only for local provider calls.
