# 4Lines for Claude

Draw architectural floor plans with Claude: lay out a home, furnish its rooms, remodel a plan someone gives you and review a plan the way an architect would. The plugin bundles the 4Lines connector with four skills that carry the order of work, the defaults and the design rules the 4Lines server applies.

The design rules in this package were calibrated with the help and collaboration of Sergi Pujadó Soler, Architect.

## Install

In Claude Code:

```
/plugin install 4lines --marketplace 4lines-ai/4lines-claude
```

Or in two steps: `/plugin marketplace add 4lines-ai/4lines-claude`, then `/plugin install 4lines@4lines`. Once it is listed in the Claude directory, it is added on claude.ai and in Cowork from there.

## Skills

| Skill | Use it when |
|---|---|
| `design-a-home` | The user wants a new flat or house: a room program, a total area, a footprint. |
| `furnish-a-room` | A room or a whole plan needs its kitchen, bathroom, bedroom or living room laid out. |
| `remodel-a-plan` | The user describes or sends an existing plan and wants it changed. |
| `review-a-plan` | The user asks whether a plan works, or wants its problems found and fixed. |

Each skill keeps the design rules in `references/`, word for word as the server states them. The same rules come back from the server with `get_capabilities` and a `topic` (`dwelling`, `kitchen`, `bathroom`, `bedroom`, `living`, `doors`, `furniture`).

These are design criteria for drawing with 4Lines. They do not replace the project of a qualified professional or the building regulations of each place.

## Use it

Ask Claude for a plan in your own words: "a 90 m2 flat with three bedrooms and two bathrooms", "furnish this bedroom", "move the kitchen to the living room", "is this plan any good?". Claude draws on a 4Lines draft, checks the result with the server's own measurements, shows you the drawing and gives you a link to open the plan in the 4Lines editor, where you can keep editing it, save it to your account and render it.

## Connector

`.mcp.json` points at `https://mcp.4lines.ai/mcp/drafts`, the drafting tools of the 4Lines MCP server. It needs no account: each plan is an anonymous draft. Documentation: https://4lines.ai/mcp/claude/

## Data

What Claude sends to mcp.4lines.ai is the plan itself: walls, doors, windows, room names, furniture and cameras, plus the room program when the layout engine is used. An unclaimed draft lives on 4Lines servers for seven days, renewed every time a tool touches it; opening the link and saving the plan to a 4Lines account is what keeps it. The plugin runs nothing on your computer and stores nothing itself. Privacy policy: https://4lines.ai/legal/mcp-privacy

## Help and license

Questions and help: hello@4lines.ai. Released under the MIT License (see `LICENSE`).
