**[SyncSignature](https://syncsignature.com/mcp/)**: email signature management for teams, from any AI assistant.

[![SyncSignature Email Signatures MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.syncsignature/email-signatures/badges/score.svg)](https://glama.ai/mcp/connectors/com.syncsignature/email-signatures)

# SyncSignature Email Signatures (MCP server)

Manage your company's email signatures from an AI assistant: add teammates, assign templates by group, control banner campaigns and check signature click analytics. Works with Google Workspace and Microsoft 365 workspaces.

SyncSignature does not route or read your email. You can connect with read-only access.

| | |
|---|---|
| Server URL | `https://mcp.syncsignature.com/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth (sign in with your SyncSignature account, no API key) |
| Registry name | `com.syncsignature/email-signatures` |
| Docs | https://syncsignature.com/docs/connect-ai-assistant-mcp/ |

This repository holds the connection manifests and the agent skill. The server itself is hosted by SyncSignature; there is nothing to run locally.

## Install

- **Claude** (web, desktop, mobile, Cowork): open [claude.ai/directory/syncsignature](https://claude.ai/directory/syncsignature) and click Connect.
- **Claude Code**:
  ```
  claude mcp add --transport http syncsignature https://mcp.syncsignature.com/mcp
  ```
  Then run `/mcp` to sign in. Or install the plugin (server plus skill):
  ```
  /plugin marketplace add SyncSignature/mcp
  /plugin install syncsignature@syncsignature
  ```
- **ChatGPT**: install SyncSignature from the ChatGPT plugin directory.
- **Cursor and Grok Bot**: install SyncSignature from the Cursor Marketplace, or add to `.cursor/mcp.json`:
  ```json
  { "mcpServers": { "syncsignature": { "url": "https://mcp.syncsignature.com/mcp" } } }
  ```
- **Gemini CLI**:
  ```
  gemini extensions install https://github.com/SyncSignature/mcp
  ```
- **VS Code (GitHub Copilot)**: add a remote MCP server with type `http` and the URL above.
- **Any other MCP client**: add a remote MCP server with the URL above and complete the browser sign-in.

After connecting, the assistant should read the skill at [skills/syncsignature-admin/SKILL.md](skills/syncsignature-admin/SKILL.md) (also served at https://mcp.syncsignature.com/skills).

## Example requests

- "Add Priya Shah, priya@acme.com, Sales Manager, to the Sales group."
- "Which teammates have no phone number?"
- "Change the phone number on the Sales template. Preview it with Priya's details and tell me who it affects first."
- "Pause our webinar banner for the Sales group."
- "Which teammates got the most signature clicks last month?"
- "Is our Google Workspace sync connected?"

## Tools (30)

Reads change nothing. Every write asks the user to confirm first.

| Tool | Type | What it does |
|---|---|---|
| `get_workspace` | Read | The signed-in workspace: name, domain, seat usage, teammate count |
| `list_teammates` | Read | Teammates with their signature values (paginated) |
| `get_teammate` | Read | One teammate by id, including signature detail values |
| `get_teammate_signature` | Read | A teammate's signature HTML and install record (platform, success, time) |
| `get_teammate_analytics` | Read | Clicks on a teammate's signature links by country, browser, OS and device |
| `list_signature_links` | Read | Tracked links inside a signature and where each points |
| `list_groups` | Read | Groups with teammate counts and the template each carries |
| `list_signature_templates` | Read | The product template catalog with numeric ids |
| `list_workspace_templates` | Read | Templates this workspace has built, with their groups |
| `get_workspace_template` | Read | One template's fields and design |
| `preview_signature` | Read | Render a signature or a proposed template edit without saving |
| `list_campaigns` | Read | Banner campaigns with schedule and active status |
| `list_smart_fields` | Read | The field registry: each field's source and whether it is required |
| `list_integrations` | Read | Connected integrations and whether credentials have expired |
| `create_teammate` | Write | Add a teammate (optionally straight into a group) |
| `update_teammate` | Write | Change a teammate's values |
| `delete_teammate` | Delete | Remove a teammate and their signature |
| `create_group` | Write | Create a group, optionally with a template |
| `update_group` | Write | Rename a group or change its template |
| `delete_group` | Delete | Delete a group and the signatures built from it |
| `add_teammates_to_group` | Write | Assign teammates to a group, building their signatures |
| `remove_teammates_from_group` | Write | Take teammates out of a group |
| `update_workspace_template` | Write | Change a template; goes live for every teammate using it |
| `update_campaign` | Write | Change a campaign's content, schedule or groups |
| `pause_campaign` | Write | Pause a running campaign and pull its banner |
| `resume_campaign` | Write | Resume a paused campaign |
| `delete_campaign` | Delete | Delete a campaign and remove its banner everywhere |
| `create_smart_field` | Write | Add a custom field to the registry |
| `update_smart_field` | Write | Rename, require or rebind a field's source |
| `delete_smart_field` | Delete | Remove an unused custom field |

New banner campaigns are created in the SyncSignature app, because the banner image is uploaded there.

## What is in this repository

| File | Used by |
|---|---|
| `server.json` | Official MCP Registry |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code and Cowork plugin |
| `plugin.json`, `mcp.json` | Cursor Marketplace and Grok Bot (Agent Plugin) |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `skills/syncsignature-admin/SKILL.md` | Agent skill for any client that reads skills |
| `llms-install.md` | Agent-readable install steps (Cline and others) |

## Links

- Product: https://syncsignature.com
- MCP page: https://syncsignature.com/mcp/
- Setup docs: https://syncsignature.com/docs/connect-ai-assistant-mcp/
- Claude directory: https://claude.ai/directory/syncsignature
- Official MCP Registry: `com.syncsignature/email-signatures`

## Privacy and terms

- Privacy: https://syncsignature.com/privacy/
- Terms: https://syncsignature.com/terms/

## Support

Questions or issues: open an issue here or contact support from https://syncsignature.com.

## License

MIT for the manifests and skill in this repository. The SyncSignature service is covered by its own terms at https://syncsignature.com.
