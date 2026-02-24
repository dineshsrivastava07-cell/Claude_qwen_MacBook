# Claude Qwen3 Integration with MCP Server and Skills

This repository contains the implementation of Claude Code CLI integrated with Qwen3 coder model, including MCP server functionality and custom skills.

## Overview

This project demonstrates a complete integration of:
- Claude Code CLI as the primary interface
- Qwen3 coder model (480B parameters) as the backend LLM
- MCP (Model Coordination Protocol) server for tool coordination
- Custom skills for specialized functionalities

## Architecture

```
┌─────────────────┐    ┌──────────────────────┐    ┌─────────────────────┐
│   Claude Code   │◄──►│   Ollama Bridge      │◄──►│   Qwen3 Coder       │
│      CLI        │    │ (http://127.0.0.1:8082)   │ (qwen3-coder:480b-cloud)│
└─────────────────┘    └──────────────────────┘    └─────────────────────┘
         │                           │
         ▼                           ▼
┌─────────────────┐    ┌──────────────────────┐
│   MCP Server    │    │   Custom Skills      │
│  Integration    │    │  (intelligent-expert)│
└─────────────────┘    └──────────────────────┘
```

## Components

### 1. Claude Code CLI Configuration
Located at: `~/.claude/`

Main configuration file: `~/.claude.json`

Key features:
- Uses Qwen3 coder as primary model via Ollama bridge
- Custom skills implementation
- Plugin and marketplace support

### 2. Ollama Bridge
File: `ollama-bridge.js`

Functionality:
- Translates Anthropic Messages API to Ollama OpenAI-compatible API
- Routes all Claude CLI requests to Qwen3 model
- Runs on http://127.0.0.1:8082

### 3. Qwen3 Integration
Model: `qwen3-coder:480b-cloud`
Access: http://127.0.0.1:11434 (standard Ollama endpoint)

### 4. MCP Server Implementation

MCP (Model Coordination Protocol) enables coordinated access to a variety of tools. The implementation includes:

#### Features:
- Tool coordination between Claude Code and various system tools
- Standard tool interfaces for file operations, web search, etc.
- Extensible architecture for custom tools

#### Configuration:
MCP servers are configured in `~/.claude/config.json` (if it exists) or through project-specific settings.

#### Standard MCP Tools:
- File reading and writing
- Web search and fetching
- Command execution
- Database access

### 5. Custom Skills

#### Intelligent Expert Skill
Location: `~/.claude/skills/intelligent-expert/`

Commands:
- `architecture` - Design software architectures
- `cybersecurity` - Perform cybersecurity assessments
- `best-practices` - Review codebases for best practices
- `optimize` - Optimize system performance

##### Architecture Command
```
/intelligent-expert architecture --requirements "[requirements]" --constraints "[constraints]"
```

##### Cybersecurity Command
```
/intelligent-expert cybersecurity --scope "[scope]" --type "[assessment-type]"
```

##### Best Practices Command
```
/intelligent-expert best-practices --target "[path]" --review-type "[type]"
```

##### Optimization Command
```
/intelligent-expert optimize --metrics "[metrics]" --goals "[goals]"
```

## Setup Instructions

### Prerequisites
- Claude Code CLI installed
- Ollama installed and running
- Qwen3 coder model pulled (`ollama pull qwen3-coder:480b-cloud`)

### Installation Steps

1. Clone this repository:
```bash
git clone [repository-url]
```

2. Ensure Ollama is running:
```bash
ollama serve
```

3. Pull the Qwen3 model:
```bash
ollama pull qwen3-coder:480b-cloud
```

4. Copy skill to Claude Code directory:
```bash
cp -r ./skills/intelligent-expert ~/.claude/skills/
```

5. Start using the integration with Claude Code CLI

## Usage Examples

### Using the Intelligent Expert Skill
```
/intelligent-expert architecture --requirements "e-commerce platform" --constraints "budget: $50k"
```

### Accessing via Ollama API
```bash
curl http://127.0.0.1:11434/api/generate -d '{
  "model": "qwen3-coder:480b-cloud",
  "prompt": "Explain how this Claude-Qwen integration works",
  "stream": false
}'
```

## Configuration Files

### Main Configuration
- File: `~/.claude.json`
- Purpose: Global Claude Code settings

### Ollama Bridge
- File: `~/.claude/ollama-bridge.js`
- Purpose: API translation layer

### Skill Definition
- File: `~/.claude/skills/intelligent-expert/skill.json`
- Purpose: Skill metadata and permissions

## Directory Structure

```
~/.claude/
├── skills/
│   └── intelligent-expert/
│       ├── index.js          # Skill implementation
│       └── skill.json       # Skill metadata
├── ollama-bridge.js         # API translation layer
├── CLAUDE.md                # User instructions
└── config.json              # Configuration (if exists)

~/.qwen/
├── skills/                  # Qwen-specific skills
└── debug/                   # Debug information
```

## Troubleshooting

### Common Issues

1. **Ollama not running**: Ensure `ollama serve` is running
2. **Model not found**: Pull the qwen3-coder model with `ollama pull qwen3-coder:480b-cloud`
3. **Bridge connection failed**: Check if the bridge is running on port 8082

### Logs
Check `~/.claude/ollama-bridge.log` for bridge-related issues.