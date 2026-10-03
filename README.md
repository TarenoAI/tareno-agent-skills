# Tareno agent skills

Official workflow skills for Tareno social operations, backed by the OAuth MCP endpoint https://tareno.co/api/mcp.

- `skills/tareno-social-ops`: OpenClaw connection and social workflows.
- `skills/tareno-hermes-social-ops`: Hermes connection and social workflows.

Each skill includes 30 example requests. Installing a skill does not authorize an account or publish content. Service limits and approval flows apply. The instruction files under `skills/` are licensed under MIT-0; this package contains no Tareno application source code, credentials or private account data.

## Install the Hermes skill

With Hermes already installed, choose one method:

```bash
# Skills CLI: install only the Hermes variant to the Hermes user directory
npx skills add TarenoAI/tareno-agent-skills --skill tareno-hermes-social-ops --agent hermes-agent --global --copy --yes

# Or use Hermes's own GitHub skill installer
hermes skills install TarenoAI/tareno-agent-skills/skills/tareno-hermes-social-ops

hermes skills list
```

The Skills CLI's project installation has been checked in an isolated temporary directory. A live authenticated Hermes/Tareno session has not yet been tested.

## Connect Tareno over MCP

Add this server to your existing `~/.hermes/config.yaml`, preserving other settings. No API key or client secret belongs in this configuration:

```yaml
mcp_servers:
  tareno:
    url: https://tareno.co/api/mcp
    auth: oauth
    tools:
      include:
        - list_workspaces
        - list_accounts
        - list_posts
        - get_platform_schema
        - get_analytics_overview
```

Complete browser OAuth with `hermes mcp login tareno`, then start a new session or use `/reload-mcp`. Verify the connection by asking for your Tareno workspaces and connected accounts. The initial tool list is read-only. Use `hermes mcp configure tareno` to opt into drafting, media, scheduling, publishing and Get Viral tools as needed. Consequential actions still require Tareno approval; quoted AI-credit costs apply to paid analyses.

Hermes manages OAuth credentials locally. Never put tokens, passwords or reviewer credentials into this repository, prompts or public configuration.

## Catalog status

The separate official Hermes MCP catalog request is [PR #132278](https://github.com/NousResearch/hermes-agent/pull/132278). Until NousResearch merges it and users receive an updated catalog, configure the URL directly as above. The skill's ClawHub listing is an external distribution source, not an official Hermes catalog approval.

Documentation: https://tareno.co/docs/mcp
