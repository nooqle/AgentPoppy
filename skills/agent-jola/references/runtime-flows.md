# Runtime Flows

## Hosted Profile Sync

The Product API key belongs to the hosted Agent Jola account. `pnpm agent:setting sync` pulls:

- chameleon name
- appearance/skin
- strategy text

from:

```http
GET /api/runtime/profile
X-Agent-Jola-Key: <product-api-key>
```

The local runtime writes or updates the local profile Agent. It should never receive provider API keys from the hosted portal.

## Room Flow

Default mode is `royale-4`.

1. Create or load the local profile Agent.
2. Create a room from the UI or API.
3. Share the invite code.
4. Join with invite code.
5. Set ready.
6. Start only when four participants are ready.
7. Watch the match and replay.

Confirm before these browser/API actions because they alter room state:

- create room
- join room
- leave room
- set ready
- start match
- cancel room

## Provider Bridge

Agent Jola supports:

- mock Agent: no model tokens
- OpenAI Responses API local adapter
- Anthropic Messages API local adapter

Provider keys stay local. The bridge fetches provider-shaped prompts from Agent Jola and submits only the selected game action back. Do not upload provider keys, environment dumps, local file paths, or full private logs to the hosted service.

Use mock mode before spending provider tokens:

```bash
pnpm agent:mock
```
