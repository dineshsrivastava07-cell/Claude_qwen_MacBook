# Claude-Qwen3 Ollama Bridge

This bridge translates Anthropic Messages API requests from Claude Code CLI to Ollama's OpenAI-compatible API, enabling the use of Qwen3 models with Claude Code.

## Configuration

Host: 127.0.0.1
Ollama Port: 11434
Bridge Port: 8082
Default Model: qwen3-coder:480b-cloud

## Functionality

- Translates Claude tool calls to Ollama-compatible function calls
- Handles message format conversion between Anthropic and OpenAI formats
- Manages streaming responses from Qwen3 model
- Provides error handling and logging

For the full implementation, refer to the local installation at:
`~/.claude/ollama-bridge.js`