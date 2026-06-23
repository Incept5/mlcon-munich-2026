> ⚠️ **TEMPORARY — DELETE AT END OF DAY 2.**
> The addresses below point at the instructor's laptop for today's session only.
> They stop working once the session ends.

# Day 2 Quickstart: Use the Shared Ollama Server

No local model? No problem. Point your tools at the **instructor's Ollama server**
for today. Pick the address that matches your network.

---

## Which address do I use?

| Your situation | Base address |
|---|---|
| On the room Wi‑Fi, **not** on a VPN | `http://172.22.41.204:11434` |
| On a **corporate VPN** | `https://yang-parenting-relates-magnificent.trycloudflare.com` |

> The VPN tunnel URL also works off-VPN — when in doubt, use it. For
> OpenAI-compatible tools, append **`/v1`** to whichever address you use.

## Quick test

Replace `<ADDRESS>` with your address from the table above:

```bash
curl <ADDRESS>/api/tags          # should return JSON listing the available models
```

---

## Codex CLI

```toml
# ~/.codex/config.toml   (Windows: C:\Users\<you>\.codex\config.toml)
model = "qwen2.5-coder:14b"
model_provider = "ollama"

[model_providers.ollama]
name = "Ollama"
base_url = "<ADDRESS>/v1"
```

Then just run `codex` (no flags).

## Claude Code

```bash
export ANTHROPIC_BASE_URL="<ADDRESS>/v1"
claude
```

## Python (OpenAI SDK)

```python
from openai import OpenAI

client = OpenAI(base_url="<ADDRESS>/v1", api_key="ollama")  # key is ignored
resp = client.chat.completions.create(
    model="qwen2.5-coder:14b",
    messages=[{"role": "user", "content": "Say hi in one line."}],
)
print(resp.choices[0].message.content)
```

## Native Ollama client

```bash
export OLLAMA_HOST="<ADDRESS>"
ollama list
```

---

## If something goes wrong

| Problem | Fix |
|---|---|
| `connection refused` / timeout on the IP | You're probably on a VPN — switch to the tunnel URL. |
| Tunnel URL fails | The instructor may have restarted it; ask for the new URL. |
| `model not found` | Run `curl <ADDRESS>/api/tags` to see which models are actually loaded. |
| Slow / queued responses | The whole class shares one server; it serializes per model. Be patient. |
