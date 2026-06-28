# Magento 2 Lead Engineer — Agent Skill

A free, open-source **Agent Skill** that turns Claude Code, Codex, Cursor, and other
SKILL.md-compatible AI agents into a senior Magento 2 / Adobe Commerce engineer.

It enforces **production-safe, upgrade-safe engineering**: every change is environment-aware,
weighed against alternatives, and implemented through Magento's intended extension points —
never core hacks, never `ObjectManager`, never edits to `vendor/`.

> Built and maintained by [Growsera](https://growsera.com) — eCommerce support &
> maintenance for Magento, WooCommerce, Shopify, Salla, and Zid stores.

---

## Why this skill

Most AI coding agents will happily generate Magento code that *works in a demo* and
*breaks on the next upgrade* — editing core files, overriding classes with `preference`,
calling `ObjectManager` directly, or ignoring whether you're on Luma, Hyva, Docker, or
production mode.

This skill makes the agent behave like a lead engineer doing a code review *before* it
writes a line:

- **Confirms the environment first** — Magento version, dev vs production mode, Docker vs host,
  and frontend stack — instead of assuming and breaking things.
- **Lists viable approaches with trade-offs** — plugin, observer, layout XML, ViewModel,
  JS mixin, DI virtual type — then picks the safest maintainable one.
- **Respects architectural boundaries** — module vs theme vs framework, DI principles, PSR-12.
- **Closes the loop** — tells you the exact CLI commands, affected caches, upgrade risks,
  and how to validate the change.

The result is code you can actually ship and maintain, not just paste.

---

## What's inside

```
magento2-lead-engineer/
├── SKILL.md                  # Core workflow + safety rules (always loaded)
├── references/
│   ├── approaches.md         # Override approaches & trade-offs (plugin/observer/preference/…)
│   ├── commands.md           # Environment-aware CLI patterns (Docker, markshust, host)
│   ├── debugging.md          # 500-error & developer-mode debugging playbook
│   └── frontend.md           # Luma / Blank / Hyva stack-specific guidance
```

The skill uses **progressive disclosure**: the lean `SKILL.md` loads up front, and the agent
pulls in the relevant `references/*.md` file only when the task needs it — keeping context
small while still covering deep ground.

---

## Compatibility

| Tool | Supported | Install location |
| --- | :---: | --- |
| **Claude Code** | ✅ | `~/.claude/skills/` (personal) or `.claude/skills/` (project) |
| **Claude.ai** (Pro/Team/Enterprise) | ✅ | Upload the zip via **Settings → Capabilities/Features** |
| **OpenAI Codex** | ✅ | `~/.codex/skills/` |
| **Cursor** | ✅ | `.cursor/skills/` (project) |
| Other SKILL.md agents (Gemini CLI, Windsurf, Aider, etc.) | ✅ | Their respective `skills/` directory |

The skill is a standard `SKILL.md` package, so it works with any agent that follows the
Agent Skills format. Only the install directory differs per tool.

---

## Installation

### Claude Code

**Personal (available in every project):**

```bash
git clone https://github.com/growsera/magento2-lead-engineer.git
cp -r magento2-lead-engineer ~/.claude/skills/magento2-lead-engineer
```

**Project-scoped (committed with a specific repo):**

```bash
mkdir -p .claude/skills
cp -r magento2-lead-engineer .claude/skills/magento2-lead-engineer
```

Start a new session and confirm it loaded:

```bash
# Ask the agent: "what skills do you have available?"
# or list the folder:
ls ~/.claude/skills/
```

### OpenAI Codex

```bash
cp -r magento2-lead-engineer ~/.codex/skills/magento2-lead-engineer
```

### Cursor

```bash
mkdir -p .cursor/skills
cp -r magento2-lead-engineer .cursor/skills/magento2-lead-engineer
```

### Claude.ai

Download `magento2-lead-engineer.zip` from the
[Releases](https://github.com/growsera/magento2-lead-engineer/releases) page and upload it
under **Settings → Capabilities** (custom skills, available on paid plans).

> ⚠️ **Most common install mistake:** the `SKILL.md` file must sit **directly** inside the
> skill folder — i.e. `~/.claude/skills/magento2-lead-engineer/SKILL.md`, **not**
> `~/.claude/skills/magento2-lead-engineer/magento2-lead-engineer/SKILL.md`. If your agent
> doesn't see the skill, you probably have one folder too many. Unzipping a GitHub download
> often creates that extra nesting — move the inner folder up one level.

---

## Usage

The skill triggers automatically when you ask about Magento 2 architecture, module work,
overrides, frontend features, or debugging. You can also invoke it explicitly.

**Example prompts:**

```text
Use the Magento 2 Lead Engineer skill: I need to add a custom field to the
checkout shipping step on a Hyva theme. What's the safest approach?
```

```text
A product attribute's value needs to be transformed before it's saved.
Should I use a plugin, an observer, or a preference? I'm on 2.4.7, production mode, Docker.
```

```text
Getting a 500 on the category page in developer mode. Walk me through debugging it.
```

The agent will confirm any missing environment details, lay out the options with their
risks, implement the safest one as a proper custom module with exact file paths, and finish
with the CLI commands and cache types you need to run.

---

## Design principles enforced

- ✅ Custom module by default — no edits to core or `vendor/`
- ✅ Plugin / observer / layout / ViewModel **before** `preference` (last resort only)
- ✅ No direct `ObjectManager` usage
- ✅ Dependency Injection + PSR-12
- ✅ Stack-aware: Luma/Blank (RequireJS, Knockout, UI Components) vs Hyva (Alpine.js, Tailwind, ViewModels)
- ✅ Environment-aware commands labelled **"inside container"** vs **"on host"**
- ✅ Magento CLI over direct DB changes
- ✅ Explicit upgrade & backward-compatibility risk callouts

---

## Contributing

Contributions are welcome — better trade-off notes, more debugging recipes, additional
frontend patterns, or fixes for newer Magento releases.

1. Fork the repo
2. Create a branch (`git checkout -b improve-debugging-ref`)
3. Keep `SKILL.md` lean; put depth in `references/`
4. Open a pull request describing the change and the Magento version(s) it targets

Please keep all guidance **upgrade-safe** — the whole point of this skill is to stop agents
from generating code that breaks on the next Magento update.

---

## License

Released under the **MIT License** — free to use, modify, and distribute. See [`LICENSE`](LICENSE).

---

## About Growsera

[Growsera](https://growsera.com) provides ongoing support and maintenance for online stores
on Magento, WooCommerce, Shopify, Salla, and Zid. We build skills like this one to share the
production-safe practices we apply to client stores every day.

If this skill saved you from a risky override, a ⭐ on the repo helps other Magento devs find it.
