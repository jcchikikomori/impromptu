
# MCP Setup Instructions

## For VS Code

1. **Open Settings** (`Ctrl+,` or `Cmd+,`)
2. **Search** for "MCP" in settings
3. **Locate** `modelContextProtocol.servers` (or similar MCP config)
4. **Add** your MCP server configuration:
    ```json
    {
      "mcpServers": {
         "your-server-name": {
            "command": "node",
            "args": ["path/to/server.js"]
         }
      }
    }
    ```
5. **Restart** VS Code
6. **Verify** in the "MCP" panel or terminal output

## For Open Code / Generic Setup

1. **Locate** your IDE's config folder (usually `.config/` or settings directory)
2. **Create/edit** the MCP configuration file
3. **Add** server details with command and arguments
4. **Save** and reload your IDE
5. **Check** logs for connection status

---

*Need specific setup steps for your particular MCP server or IDE?*
