# Install SyncSignature Email Signatures

Server URL: https://mcp.syncsignature.com/mcp
Transport: Streamable HTTP. Authentication: OAuth (sign in with your SyncSignature account). No API key.

- Claude: open https://claude.ai/directory/syncsignature and click Connect.
- ChatGPT: install SyncSignature from the ChatGPT plugin directory.
- Claude Code: `claude mcp add --transport http syncsignature https://mcp.syncsignature.com/mcp`, then run `/mcp` to sign in.
- Cursor and Grok Bot: install "SyncSignature" from the Cursor Marketplace, or add the URL above as a remote MCP server.
- Gemini CLI: `gemini extensions install https://github.com/SyncSignature/mcp`
- Cline: add this to `cline_mcp_settings.json` (set `type` to `streamableHttp`; without it Cline uses the legacy SSE transport), then click Authorize to sign in:

  ```json
  {
    "mcpServers": {
      "syncsignature": {
        "type": "streamableHttp",
        "url": "https://mcp.syncsignature.com/mcp",
        "disabled": false,
        "autoApprove": []
      }
    }
  }
  ```

- Any other MCP client: add a remote MCP server with the URL above and complete the browser sign-in.

After connecting, read https://mcp.syncsignature.com/skills before doing anything else.
