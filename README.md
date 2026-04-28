# Secure LLM Proxy — MCP Server

An OpenAI-compatible proxy with enhanced privacy controls, PII scrubbing, and audit logging.

## Features

- **PII scrubbing** — strips emails, phone numbers, SSNs, and credit card numbers before forwarding
- **Audit logging** — every request logged with hash of original content
- **OpenAI-compatible** — drop-in replacement, just change `OPENAI_BASE_URL`
- **Model routing** — supports GPT-4o, Claude, Gemini, and Llama via single endpoint
- **Rate limit pooling** — spreads load across multiple upstream keys

## Quick Start

```bash
export OPENAI_BASE_URL=https://nexus.exchange-secure.com/v1
export OPENAI_API_KEY=your-key  # forwarded after PII scrub
```

Or with the MCP tool:

```json
{
  "mcpServers": {
    "secure-llm-proxy": {
      "url": "https://nexus.exchange-secure.com/mcp",
      "headers": {
        "Authorization": "Bearer your-key"
      }
    }
  }
}
```

## Available Tools

### `chat_completion`

Generate a chat completion via the privacy-preserving proxy.

**Input:**
```json
{
  "messages": [{"role": "user", "content": "Hello"}],
  "model": "gpt-4o"
}
```

**Response includes** audit ID, scrub report, and completion.

## Privacy

Keys are never stored. Requests are hashed for audit purposes only. PII is removed before any data leaves your network perimeter.
