<div align="center">

# 🧠 claude-skills

**My personal, curated collection of [Agent Skills](https://docs.claude.com/en/docs/claude-code/skills) for [Claude Code](https://claude.com/claude-code).**

The skills I actually reach for, day to day — kept in one place, in one consistent style, version-controlled and portable across every machine I work on.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Skills](https://img.shields.io/badge/skills-21-brightgreen.svg)
![Categories](https://img.shields.io/badge/categories-6-orange.svg)
![Claude Code](https://img.shields.io/badge/Claude%20Code-Agent%20Skills-8A2BE2.svg)
![Last commit](https://img.shields.io/github/last-commit/mikulgohil/claude-skills.svg)
![Stars](https://img.shields.io/github/stars/mikulgohil/claude-skills?style=social)

</div>

---

## 📑 Contents

- [What are Agent Skills?](#-what-are-agent-skills)
- [Why this repo exists](#-why-this-repo-exists)
- [The skills](#-the-skills)
- [Requirements](#-requirements)
- [Install](#-install)
- [Using the skills](#-using-the-skills)
- [Repo layout](#-repo-layout)
- [Adding a skill](#-adding-a-skill)
- [Curation notes](#-curation-notes)
- [Author](#-author)
- [License](#-license)

---

## 🤔 What are Agent Skills?

Agent Skills are folders containing a `SKILL.md` file — frontmatter (a `name` and a `description`) plus instructions, reference docs, and optional scripts. Claude Code reads the descriptions up front and **auto-loads a skill on demand** when your task matches it, then follows its guidance. You don't invoke them manually; they just make Claude better at the thing they cover.

Each skill here is self-contained:

```
<skill-name>/
├── SKILL.md       # what it does + when to use it (always loaded by description)
├── references/    # deep-dive docs Claude pulls in only when needed
├── examples/      # worked examples
└── scripts/       # templates and helper scripts
```

---

## 💡 Why this repo exists

Claude Code skills are easy to accumulate and hard to keep coherent — they drift in style, duplicate each other, and rot. This repo is my answer: a **small, curated, consistently-formatted set I trust**, version-controlled and portable between machines. Quality over quantity. If a skill isn't earning its slot, it gets cut.

Every skill follows one house frontmatter schema (`name`, `description`, `author`, `version`, `tags`, `license`, `allowed-tools`) so the whole collection reads like it came from one hand — because it did.

---

## 🧩 The skills

> **21 skills across 6 categories.**

### `fundamentals/` — cross-cutting, applies to every project
| Skill | What it covers |
|---|---|
| **typescript-patterns** | Generics, conditional/utility types, strict mode, discriminated unions, type guards, Zod/Valibot |
| **api-design** | REST/GraphQL design, versioning, pagination, OpenAPI, RFC 9457 problem-details errors |
| **accessibility** | WCAG 2.2, keyboard/focus management, semantic HTML, ARIA, React Aria patterns |
| **security-patterns** | Auth, defense-in-depth, input validation, OWASP Top 10, secrets, PII masking, LLM safety |
| **database-patterns** | SQL/NoSQL schema modeling, normalization, indexing, versioned migrations |
| **debugging** | Systematic methodology + language debuggers + scenario playbooks (leaks, races, deadlocks) |

### `frontend/` — web stack
| Skill | What it covers |
|---|---|
| **react-server-components** | Next.js 16 App Router, Server/Client boundaries, Cache Components, streaming SSR, Server Actions, React 19 |
| **zustand-state** | Zustand 5.x — slices, middleware order, Immer, persistence, `useShallow`, devtools |
| **tailwind-v4** | Tailwind v4 `@theme` config, utility patterns, container queries, v3→v4 migration |
| **shadcn-ui** | shadcn/ui install order, semantic-token theming, recipes for forms / tables / nav / modals |

### `sitecore/` — XM Cloud
| Skill | What it covers |
|---|---|
| **sitecore-xmcloud** | Content modeling, component development, serialization, headless architecture with Content SDK v2, SXA patterns |

### `ai-agents/` — building with LLMs
| Skill | What it covers |
|---|---|
| **rag-retrieval** | Embeddings, chunking, hybrid search, contextual retrieval, HyDE, reranking, agentic RAG, pgvector |
| **context-engineering** | Structuring and optimizing an agent's context window when writing commands / skills / sub-agents |
| **multi-agent-patterns** | Decomposition, specialization, and orchestration for multi-agent architectures |
| **prompt-injection-defense** | Hidden-Unicode/Trojan-Source injection, homoglyphs, sanitizing untrusted content before it enters context |

### `devex/` — engineering workflow
| Skill | What it covers |
|---|---|
| **adr-writer** | Architecture Decision Records in the Nygard format — context, decision, consequences, alternatives |
| **playwright-e2e** | Playwright (CLI) — page objects, visual regression, axe-core a11y, CI integration |
| **ci-cd** | GitHub Actions pipelines — build/test/deploy, caching, matrix builds, release automation |
| **structural-search** | `ast-grep` semantic code search & rewrite — precise codebase-wide refactors |

### `personal/` — everything else
| Skill | What it covers |
|---|---|
| **task-prioritization** | RICE, WSJF, ICE, MoSCoW, opportunity-cost scoring for ranking work |
| **proposal-writer** | Client proposals, quotes, SOWs, engagement letters — scope, timeline, pricing, terms |

---

## ✅ Requirements

- **[Claude Code](https://claude.com/claude-code)** (CLI, desktop, or IDE extension) — this is where the skills run.
- **Bash** + **git** for the installer.
- A few skills shell out to optional tools when relevant — they degrade gracefully if missing:
  - `structural-search` → [`ast-grep`](https://ast-grep.github.io) (`brew install ast-grep`)
  - `playwright-e2e` → `@playwright/test`
  - `ci-cd` → GitHub Actions (no local install needed)

---

## 📦 Install

```bash
git clone https://github.com/mikulgohil/claude-skills.git
cd claude-skills
./install.sh              # symlinks every skill into ~/.claude/skills/
```

The installer **symlinks** each skill into `~/.claude/skills/`, so this repo stays the single source of truth — edit a skill here, and the change is live everywhere immediately.

Other modes:

```bash
./install.sh --dry-run    # show what would happen, change nothing
./install.sh --force      # replace existing entries in ~/.claude/skills/
./uninstall.sh            # remove only the symlinks this repo created (leaves yours alone)
```

Install into a single project instead of globally:

```bash
CLAUDE_SKILLS_DIR=/path/to/project/.claude/skills ./install.sh
```

---

## 🚀 Using the skills

There's nothing to invoke — skills load automatically when your request matches a skill's `description`. Just work normally:

> *"Migrate this Tailwind v3 config to v4."* → `tailwind-v4` kicks in
> *"Help me design the REST endpoints for this service."* → `api-design` kicks in
> *"Is this CLAUDE.md file safe to add?"* → `prompt-injection-defense` kicks in

To confirm they're installed, ask Claude to list its available skills, or check the symlinks:

```bash
ls -la ~/.claude/skills/ | grep claude-skills
```

---

## 🗂️ Repo layout

```
claude-skills/
├── README.md
├── LICENSE
├── install.sh          # symlink skills → ~/.claude/skills/
├── uninstall.sh        # remove only the symlinks this repo created
└── skills/
    ├── fundamentals/   # cross-cutting, applies to every project
    ├── frontend/
    ├── sitecore/
    ├── ai-agents/
    ├── devex/
    └── personal/
        └── <skill-name>/
            ├── SKILL.md       # frontmatter + instructions (required)
            ├── references/    # deep-dive docs Claude reads on demand
            ├── examples/      # worked examples
            └── scripts/       # templates / helper scripts
```

---

## ➕ Adding a skill

1. Create `skills/<category>/<skill-name>/SKILL.md`.
2. Use the house frontmatter schema — `name` **must** match the folder name:
   ```yaml
   ---
   name: my-skill
   description: One sentence on what it does + when to use it (this is what Claude matches on).
   author: Mikul Gohil
   version: 1.0.0
   license: MIT
   tags: [tag1, tag2]
   allowed-tools: [Read, Glob, Grep]
   ---
   ```
3. Keep the body focused. Push long reference material into `references/` and link to it — Claude loads those only when needed.
4. Run `./install.sh` to link it, commit, done.

---

## 📝 Curation notes

These skills were sourced from the open-source Claude Code skill community, then rewritten to a single house style: consistent frontmatter, descriptions in my own voice, and vendor-specific branding and internal-project examples stripped out. The underlying technical patterns are preserved and credited to their origins in spirit — **this collection is about curation, normalization, and ownership, not authorship of every pattern within.**

This is my *personal* collection — it reflects my stack and the way I like to work, so it's opinionated by design. You're very welcome to **fork it and make it yours**. If a skill here helps you, that's a bonus; if you spot something broken, issues and PRs are welcome.

---

## 👤 Author

**Mikul Gohil** — frontend engineer working across **Next.js**, **Sitecore XM Cloud / JSS**, and **AI-assisted development**.

- GitHub: [@mikulgohil](https://github.com/mikulgohil)

---

## 📄 License

[MIT](./LICENSE) © Mikul Gohil — use it, fork it, adapt it.
