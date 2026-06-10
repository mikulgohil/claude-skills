# claude-skills

My personal collection of [Agent Skills](https://docs.claude.com/en/docs/claude-code/skills) for Claude Code — the ones I actually reach for across day-to-day work and side projects. Each skill is a self-contained `SKILL.md` (plus references, examples, and scripts) that Claude loads on demand when the task matches.

This repo is the single source of truth. The skills are symlinked into `~/.claude/skills/`, so I edit them here, commit, and the changes are live everywhere immediately.

---

## Why this exists

Claude Code skills are easy to accumulate and hard to keep coherent — they drift in style, duplicate each other, and rot. This repo is my answer: a small, curated, consistently-formatted set I trust, version-controlled and portable between machines. Quality over quantity. If a skill isn't earning its slot, it gets cut.

Every skill follows one house frontmatter schema (`name`, `description`, `author`, `version`, `tags`, `license`, `allowed-tools`) so the whole set reads like it came from one hand — because it did.

---

## Skills

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

## Install

```bash
git clone <this-repo> ~/Developer/personal/tools/claude-skills
cd ~/Developer/personal/tools/claude-skills
./install.sh              # symlinks every skill into ~/.claude/skills/
```

Other modes:

```bash
./install.sh --dry-run    # show what would happen, change nothing
./install.sh --force      # replace existing entries in ~/.claude/skills/
./uninstall.sh            # remove only the symlinks this repo created
```

Override the target with `CLAUDE_SKILLS_DIR=/some/path ./install.sh` (e.g. to install into a single project's `.claude/skills/` instead of the global one).

Verify Claude picked them up by asking it to list available skills, or check `~/.claude/skills/` for the symlinks.

---

## Repo layout

```
claude-skills/
├── README.md
├── LICENSE
├── install.sh          # symlink skills → ~/.claude/skills/
├── uninstall.sh
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

## Adding a skill

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

## Curation notes

These skills were sourced from the open-source Claude Code skill community, then rewritten to a single house style: consistent frontmatter, descriptions in my own voice, vendor-specific branding and internal-project examples stripped out. The underlying technical patterns are preserved and credited to their origins in spirit — this collection is about curation, normalization, and ownership, not authorship of every pattern within.
