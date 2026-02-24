# Claude Qwen3 Implementation Repository

This repository documents the implementation of Claude Code CLI integrated with Qwen3 coder model, including MCP server functionality and custom skills.

## Contents

- `README.md` - Main documentation
- `OLLAMA_BRIDGE.md` - Details about the Ollama bridge
- `MCP_INTEGRATION.md` - Information about MCP server integration
- `skills/intelligent-expert/` - Implementation of the intelligent expert skill
  - `index.js` - Skill implementation
  - `skill.json` - Skill metadata

## Usage

This repository is meant to document your local Claude/Qwen3 implementation. To use these components:

1. Ensure Claude Code CLI is installed
2. Install and run Ollama with qwen3-coder model
3. Configure the Ollama bridge to translate API calls
4. Register the intelligent-expert skill with Claude Code
5. Use MCP tools through Claude's tool interface

## Local Implementation Locations

The actual implementation is located at:
- Claude Code configuration: `~/.claude/`
- Qwen configuration: `~/.qwen/`
- Ollama bridge: `~/.claude/ollama-bridge.js`
- Skills: `~/.claude/skills/`

This repository serves as documentation and reference for that local implementation.