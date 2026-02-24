# Automatic MCP Tool and Skill Activation

To ensure that MCP tools and skills are always active with Claude CLI, we've implemented automatic tool activation.

## Implementation Files

1. **Tool Activation Script**: `~/.claude/activate-tools.sh`
   - Automatically enables essential system tools on startup
   - Ensures custom skills are available

2. **Shell Profile Integration**: Added to `~/.zshrc`
   - Runs tool activation script on shell initialization
   - Ensures tools are always ready when Claude CLI is used

## Enabled Tools

The following tools are automatically enabled:
- `Bash`: Execute shell commands
- `Read`: Read files from filesystem
- `Write`: Write files to filesystem
- `Edit`: Edit existing files
- `Glob`: Find files using patterns
- `Grep`: Search within files
- `WebSearch`: Search the web
- `WebFetch`: Fetch content from URLs

## Skills

Custom skills (like intelligent-expert) are automatically discovered and registered from:
`~/.claude/skills/`

## Verification

To verify tools are active:
```bash
claude config get allowedTools
```

This should show all enabled tools.