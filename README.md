# AgentsBoard

**Agent-native home-screen intelligence for people who run complex systems.**

AgentsBoard turns AI agents into an always-on, glanceable surface: widgets that update themselves, explain what matters, and make the next action obvious — without opening another app.

<p align="center">
  <a href="https://wedi-dev.github.io/agents-board-demo/">
    <img src="assets/showcase-en-v2/contact-sheet.png?v=2" alt="AgentsBoard widget showcase" width="920">
  </a>
</p>

<p align="center">
  <a href="https://wedi-dev.github.io/agents-board-demo/"><strong>View the interactive concept site →</strong></a>
</p>

---

## The idea

Most dashboards assume a human will keep checking them. AgentsBoard flips that model:

- **Agents decide what deserves a slot.** They can publish, rotate, and retire widgets.
- **Widgets are intentionally tiny.** One signal, one interpretation, one next move.
- **The surface is personal and operational.** Todoist, deploys, calendar, cash, home ops, decision queues — curated into a phone-sized command board.
- **The system has guardrails.** Layout validation, safe-area rules, readable typography, TTLs, provenance, and audit metadata prevent agent-generated UI from becoming chaotic.

This repository is a **public demo / concept deck**, not the production codebase yet. The goal is to communicate the product direction clearly while the implementation is still being prepared for open-source release.

---

## Why it matters

AI agents are becoming good at doing work in the background, but humans still need a calm way to supervise them.

AgentsBoard is designed as that supervision layer:

| Problem | AgentsBoard answer |
|---|---|
| Agents produce too much text | Convert output into one glanceable widget |
| Dashboards get stale | Let agents refresh slots on schedule |
| Everything looks equally important | Put the strongest signal in the main area |
| Generated UI can break | Validate layout, font sizes, safe areas, and provenance |
| Context lives in many tools | Let agents summarize Todoist, ops, calendar, finance, code, home |

---

## What the demo shows

The current showcase includes 15 generated slots exploring different information shapes:

- decision inbox
- ops pulse
- cash focus
- deep-work timer
- meeting brief
- habit stack
- learning card
- delivery pipeline
- risk radar
- energy/status card
- travel checklist
- home ops
- launch gate
- code health
- style/mood card

Each slot is rendered by the actual widget server and validated before publishing.

---

## Design principles

### 1. Glanceable first

A widget should be readable in under two seconds:

- one dominant headline/value
- one short explanation
- optional metadata
- no microtext for primary content

### 2. Agent-native, not dashboard-native

The best slot is not “a chart”. It is an agent’s opinionated interpretation:

> “9 overdue. First: Google Workspace CLI.”

That is more useful than a passive list of tasks.

### 3. Safe by construction

AgentsBoard uses a constrained HTML/CSS primitive:

```html
<section class="widget-grid">
  <div class="top-l">LABEL</div>
  <div class="top-c">TITLE</div>
  <div class="top-r">META</div>
  <div class="main">Primary content</div>
  <div class="bottom-l">Status</div>
  <div class="bottom-r">Source</div>
</section>
```

Validation catches common problems before publishing:

- forbidden tags and event handlers
- unsupported layout areas
- duplicate grid areas
- absolute/fixed positioning
- tiny font sizes
- unsafe bottom-center placement assumptions

### 4. Provenance is part of the UI system

Slots carry metadata such as:

- `updated_by`
- `ttl_seconds`
- live/demo/playground mode
- source system
- owner
- audit status

This matters because agent-generated surfaces need trust boundaries.

---

## Architecture concept

```text
+------------------+        +---------------------+        +-------------------+
| External systems |        | AI / automation jobs |        | AgentsBoard       |
| Todoist, GitHub, | -----> | curator, watchdogs,  | -----> | widget slots,     |
| calendar, ops... |        | codex/hermes agents  |        | renderer, audit   |
+------------------+        +---------------------+        +-------------------+
                                                                  |
                                                                  v
                                                         phone / widget surface
```

The public demo intentionally avoids shipping the full server implementation for now. The production direction includes:

- Django/DRF API for boards and slots
- constrained widget layout primitive
- PNG renderer for phone widgets
- validation/audit layer
- MCP interface for agents
- scheduled autonomous updates
- provenance manifest

---

## Why Codex is relevant

AgentsBoard is the kind of project where coding agents are not just a productivity tool — they are part of the product model.

Codex-style agents can help with:

- generating widget variants from design constraints
- writing validators for agent-authored UI
- evolving the server safely
- creating tests for layout regressions
- turning product feedback into working prototypes
- maintaining documentation as the architecture changes

The project is moving toward an open-source release, and the demo repo is the first public artifact for that path.

---

## Current status

- **Public:** concept demo, screenshots, GitHub Pages site
- **Private for now:** production server code and operational integrations
- **Next:** extract a clean OSS core with examples, validation tests, and agent authoring docs

---

## Preview

- Website: https://wedi-dev.github.io/agents-board-demo/
- Repository: https://github.com/wedi-dev/agents-board-demo

---

## License

Demo content © Bartosz Wiśniewski / wedi-dev. License will be finalized before code release.
