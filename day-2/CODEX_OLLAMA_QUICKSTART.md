# Quickstart: Codex CLI on a Local Model (Ollama)

Run an AI coding agent on your own laptop — **no API key, no cloud, no cost.**

You'll point OpenAI's **Codex CLI** at a model running in **Ollama**. This is the
easy one: it just works, no proxy needed.

⏱️ ~10 minutes (plus model download time).

---

## 1. Install the two tools

```bash
# Ollama — the local model server (https://ollama.com)
# install it from the website, then check it's running:
ollama --version

# Codex CLI
npm install -g @openai/codex
codex --version
```

## 2. Download a coding model

```bash
ollama pull qwen2.5-coder:14b
```

> Use a **coding** model — `qwen2.5-coder` is a safe choice. Codex needs a model
> that can call tools; a random chat model won't work. On a smaller machine try
> `qwen2.5-coder:7b`.

## 3. Launch Codex on the local model

```bash
codex --oss -m qwen2.5-coder:14b
```

The `--oss` flag tells Codex to use your local Ollama server. ✅ You should land
at a Codex prompt. Try:

```
write a Python script that prints the first 20 Fibonacci numbers, then run it
```

That's it — you're vibe coding locally. 🎉

---

## Make it one short command

Add this to your shell profile (`~/.zshrc` or `~/.bashrc`) so you don't retype it:

```bash
alias ox='codex --oss -m qwen2.5-coder:14b'
```

Open a new terminal and just run `ox`.

---

## Try it on today's exercise

Feed it the vibe‑coding brief from this folder:

```bash
codex exec --oss -m qwen2.5-coder:14b "$(cat vibe/instruct.txt)"
```

`exec` runs one task start‑to‑finish without the interactive prompt.

---

## If something goes wrong

| Problem | Fix |
|---|---|
| `connection refused` | Ollama isn't running. Run `ollama serve` (or open the Ollama app). |
| `model not found` | Run `ollama pull qwen2.5-coder:14b`. Check names with `ollama list`. |
| It loops or ignores your request | Your model can't use tools — switch to `qwen2.5-coder` or `gpt-oss`. |
| Answers get cut off | Restart Ollama with more context: `OLLAMA_CONTEXT_LENGTH=32768 ollama serve` |
| Too slow | Use a smaller model, e.g. `qwen2.5-coder:7b`. |
| A flag isn't recognised | Run `codex --help` — the CLI changes often. |

Want Claude Code instead of Codex? See
**[CLAUDE_CODE_OLLAMA_QUICKSTART.md](CLAUDE_CODE_OLLAMA_QUICKSTART.md)** (one extra step).
