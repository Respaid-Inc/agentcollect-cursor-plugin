# AgentCollect: Cursor Plugin

Minimal shared marketplace plugin for **Cursor** and **Grok Bot** that exposes
read-only accounts receivable intelligence from AgentCollect over the Model
Context Protocol (MCP).

- Publisher: Respaid Inc. (dba AgentCollect)
- Contact: support@agentcollect.com
- Docs: https://agentcollect.com/docs/mcp

## Status

- Marketplace submission: **not yet submitted**
- End-to-end Grok Bot runtime test: **pending**

This repository only contains the plugin manifest and MCP server pointer. No
license is granted and no repository URL is implied.

## What it does

Connects your IDE/agent to the hosted AgentCollect MCP endpoint:

```
https://mcp.agentcollect.com/public-mcp
```

Authentication uses **OAuth 2.1 with PKCE**. After sign-in, every call is
scoped to the authenticated AgentCollect account, so the agent can only see
data belonging to that tenant.

### Capability

- `ask-ar-analyst`: a single read-only tool that answers natural-language
  questions about your accounts receivable. It cannot create, modify, or
  delete any data.

### Sample AR questions

- "Where should I focus this week?"
- "What is my engagement rate?"
- "Show my top 5 active accounts by amount."
- "How much have we recovered, and what is still in motion?"

## Install (Cursor marketplace)

Once approved, install **AgentCollect** from the Cursor plugin marketplace and
sign in when prompted. The OAuth 2.1 PKCE flow completes in your browser.

## Manual fallback: `mcp.json`

If you prefer not to use the marketplace, add this to your Cursor MCP config
(`~/.cursor/mcp.json` or project-level `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "agentcollect": {
      "url": "https://mcp.agentcollect.com/public-mcp"
    }
  }
}
```

Restart Cursor and sign in through the OAuth prompt.

## Files

- `.cursor-plugin/plugin.json`: Cursor plugin manifest
- `mcp.json`: MCP server pointer (same shape used by the manual fallback)
- `README.md`: this document

## Notes

- No secrets, scripts, or lifecycle hooks are shipped with this plugin.
- The server URL is the only runtime surface; everything else is handled by
  the hosted MCP service.
