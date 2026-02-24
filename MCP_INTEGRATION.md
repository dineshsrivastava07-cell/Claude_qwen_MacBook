# MCP (Model Coordination Protocol) Integration

## Overview

The Model Coordination Protocol (MCP) enables Claude Code CLI to coordinate with various tools and services. This integration allows for seamless interaction between Claude and the system environment.

## MCP Features in Claude Code

- Tool discovery and registration
- Permission management for tool usage
- Standardized tool interfaces
- Session context management

## Tool Categories

### System Tools
These are automatically available in Claude Code:
- `Bash`: Execute shell commands
- `Read`: Read files from the filesystem
- `Write`: Write files to the filesystem
- `Edit`: Edit existing files
- `Glob`: Find files using patterns
- `Grep`: Search within files
- `WebSearch`: Search the web
- `WebFetch`: Fetch content from URLs

### Custom Tools
Additional tools can be registered through plugins and skills.

## Configuration

MCP servers are configured in project settings and can be enabled/disabled per project. The configuration is stored in:
`~/.claude/projects/[project-id]/`

## Permissions

Each tool requires explicit user permission before it can be used. The permission system ensures that Claude Code can only access resources that the user has granted access to.

## Integration with Qwen3

When using Qwen3 through the Ollama bridge, MCP tools function identically to how they would with Claude models, providing consistent access to system capabilities regardless of the underlying LLM.

## Standard MCP Tool Interfaces

### File Operations
```javascript
{
  "name": "read_file",
  "description": "Read a file from the filesystem",
  "input_schema": {
    "type": "object",
    "properties": {
      "path": {"type": "string", "description": "Path to the file to read"}
    },
    "required": ["path"]
  }
}
```

### Web Search
```javascript
{
  "name": "web_search",
  "description": "Search the web for information",
  "input_schema": {
    "type": "object",
    "properties": {
      "query": {"type": "string", "description": "Search query"}
    },
    "required": ["query"]
  }
}
```

### Command Execution
```javascript
{
  "name": "bash",
  "description": "Execute a bash command",
  "input_schema": {
    "type": "object",
    "properties": {
      "command": {"type": "string", "description": "Command to execute"}
    },
    "required": ["command"]
  }
}
```

## Extensibility

New MCP tools can be added through:
1. Plugins in `~/.claude/plugins/`
2. Custom skills with appropriate permissions
3. Direct tool registration in project configurations

For more information about MCP implementation, visit the official MCP documentation or check plugin examples in:
`~/.claude/plugins/marketplaces/claude-plugins-official/plugins/plugin-dev/skills/mcp-integration/`