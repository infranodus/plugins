# InfraNodus plugins

The marketplace for InfraNodus plugins for Claude Code, Codex (OpenAI) and
Grok Build (xAI). This repository holds no plugin code: each plugin lives in
its own repository, and the two catalogs here point at them. The memory plugin's id is `infranodus-memory`; its name is InfraNodus Graph Memory. The InfraNodus
skills have their own marketplace, [infranodus/skills](https://github.com/infranodus/skills).

## Install

Claude Code (Grok Build takes the same lines):

```
/plugin marketplace add infranodus/plugins
/plugin install infranodus-memory@infranodus-plugins
/plugin install infranodus@infranodus-plugins
```

Codex:

```
codex plugin marketplace add infranodus/plugins
```

then install from the marketplace in the Codex app or the `/plugins` screen of
the CLI.

## Plugins

| Plugin | What it does | Repository | Clients |
|---|---|---|---|
| `infranodus-memory` | InfraNodus Graph Memory: automatic memory for coding agents, stored as a knowledge graph in your InfraNodus account. Saves what a session learned about the project when it ends, recalls it at the first prompt of the next one with GraphRAG retrieval along the graph's links, and names a gap the memory does not cover yet. [Docs](https://infranodus.com/docs/claude-code-memory-plugin) | [infranodus/infranodus-memory-plugin](https://github.com/infranodus/infranodus-memory-plugin) | Claude Code, Codex, Grok Build |
| `infranodus` | The core InfraNodus plugin: the `/infranodus` skill and the InfraNodus MCP server. Knowledge graphs, topic clusters, content gaps, research questions, GraphRAG retrieval, SEO/GEO. Listed here for convenience; it is the same plugin as `infranodus@infranodus-skills`, so install one or the other, not both. | [infranodus/skills](https://github.com/infranodus/skills) (folder `infranodus`) | Claude Code, Grok Build |

Both plugins register the InfraNodus MCP server at the same address. Claude
Code keeps one connection per address, so installing both, or adding them next
to a server you already configured, does not create a second connection.

## Adding a plugin

One entry per plugin in `.claude-plugin/marketplace.json` (Claude Code and Grok
Build) and, when the plugin ships a `.codex-plugin/plugin.json`, one in
`.agents/plugins/marketplace.json` (Codex). Entries carry no version: a plugin's
version is the one in its own `plugin.json`, so a release in the plugin's
repository needs no change here.

Marketplace names are keys in each user's client settings, one source per name,
so every InfraNodus repository that ships a marketplace file uses a different
name: `infranodus-plugins` here, `infranodus-skills` for the skills,
`infranodus-memory` for the memory plugin's own repository.
