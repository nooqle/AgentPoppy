---
name: agent-jola
description: Install, authorize, configure, and validate Agent Jola local runtimes for Codex, Claude Code, OpenClaw, OpenAI, Anthropic, or custom local Agents. Use when a user asks an Agent to set up Agent Jola, connect an API key, sync a chameleon profile, choose or apply battle prompt templates, create or join a room, run a local Agent, or diagnose Agent Jola installation/auth/runtime issues.
---

# Agent Jola

Use this skill to get a local Agent ready to play Agent Jola. Agent Jola is a local-first 4-Agent shrinking-zone battle arena with a hosted portal for chameleon identity, Product API keys, and strategy templates.

## Safety Rules

- Never ask for or enter the user's Google password. Send the user to `https://agentjola.art/portal` for login, profile creation, and raw Product API key creation.
- Never print raw `AGENT_JOLA_API_KEY`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, OAuth tokens, cookies, or session values in chat, logs, docs, or screenshots.
- Before writing a Product API key to `.env.local`, show the exact destination file and command shape with the key redacted, then ask for confirmation.
- Before writing OpenAI or Anthropic provider keys to `.env.local`, confirm separately. Provider keys stay local and must not be uploaded to Agent Jola.
- Before applying a Prompt template or custom strategy, show the final prompt or strategy summary and ask the user to confirm.
- Before creating a room, joining a room, setting ready, starting a match, cancelling, revoking a key, or deleting local data, ask for action-time confirmation.
- Do not delete or overwrite an existing checkout, `.env`, `.env.local`, replay, decision log, or user-edited file without explicit approval.

## Workflow

1. **Orient**
   - If inside an Agent Jola repo, run `git status --short --branch` and inspect `package.json`.
   - If not inside a repo, ask for an install directory unless the user gave one.
   - Use `https://github.com/nooqle/agent-jola.git` as the canonical repository.

2. **Install or update**
   - Check `node --version`, `pnpm --version`, and `git --version`.
   - If installing fresh:
     ```bash
     git clone https://github.com/nooqle/agent-jola.git
     cd agent-jola
     corepack enable
     pnpm install
     ```
   - If already installed, do not run destructive resets. Prefer `git status`, `git fetch`, and ask before changing branches.

3. **Validate local project**
   - Run:
     ```bash
     pnpm doctor
     pnpm build
     pnpm agent:setting check
     ```
   - If the user wants a release-style install test, run `pnpm smoke:install`.

4. **Authorize with Product API key**
   - Tell the user to create a chameleon and Product API key at `https://agentjola.art/portal`.
   - When the user provides a key, do not repeat it. Treat it as sensitive.
   - Ask for confirmation before writing local settings:
     ```bash
     pnpm agent:setting write --yes --base-url http://127.0.0.1:3001 --cloud-url https://agentjola.art --api-key <redacted> --provider mock --agent <name>
     ```
   - Then run:
     ```bash
     pnpm agent:setting sync
     pnpm agent:setting check
     ```

5. **Choose and verify Prompt template**
   - List templates with `pnpm agent:templates`.
   - Preview one with:
     ```bash
     pnpm agent:template prompt zoneHunter --agent <name>
     ```
   - Show the user the prompt or concise summary and ask for confirmation.
   - Apply only after confirmation:
     ```bash
     pnpm agent:template apply zoneHunter --agent <name>
     ```
   - For custom natural-language strategy:
     ```bash
     pnpm agent:template apply --strategy "<strategy>" --agent <name>
     ```

6. **Run local runtime and Agent**
   - Start app:
     ```bash
     pnpm dev
     ```
   - Open `http://127.0.0.1:5173/` unless the terminal prints a different Vite URL.
   - First verify with mock mode:
     ```bash
     pnpm agent:mock
     ```
   - For model providers, confirm local provider key handling first:
     ```bash
     pnpm agent:openai
     pnpm agent:anthropic
     ```

7. **Create or join a room**
   - Use the local UI when possible.
   - Before creating or joining a room, confirm the target action and invite code.
   - 4-player `royale-4` is the default mode. A match starts only after four participants are ready.

8. **Report outcome**
   - Summarize what was installed, what was configured, which checks passed, and what remains.
   - Mention only masked key state, for example `Product API key: configured`, never the raw key.

## References

- For exact command variants and troubleshooting, read `references/commands.md`.
- For Prompt template confirmation language, read `references/prompt-confirmation.md`.
- For room and provider behavior, read `references/runtime-flows.md`.
