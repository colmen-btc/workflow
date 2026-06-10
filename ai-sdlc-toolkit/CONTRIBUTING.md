# Contributing to the AI-SDLC Toolkit

This toolkit is maintained as part of the [AI-Native Development](../initiatives/ai-native-development/initiative.md) initiative. Contributions from any team member are welcome.

## What You Can Contribute

| Type | Examples |
|------|---------|
| Template improvements | Better structure, missing fields, clearer placeholders |
| New samples | Filled-in examples from real initiatives |
| Checklist updates | New gate criteria based on lessons learned |
| Agent rule refinements | Better prompts, new rules for common patterns |
| IDE support | New IDE distributions, updated install instructions |
| Standard clarifications | Wording fixes, ambiguity resolution, new glossary terms |
| Bug fixes | Broken links, incorrect paths, inconsistencies |

## How to Contribute

1. **Create a branch** from `main`
2. **Make your changes** — follow the derivation chain below
3. **Open a PR** — link it to the AI-Native Development initiative
4. **Get a review** — at least one team member must approve

## Derivation Chain

Changes must stay consistent across the chain. If you change the standard, update the templates and samples to match.

```
standard/    → defines what each artifact IS
templates/   → enforces the structure
samples/     → demonstrates the template with real content
```

| If you change... | Also update... |
|-----------------|---------------|
| A term in `glossary.md` | Every file that uses that term |
| A stage in `ai-sdlc-standard.md` | `guide.md`, `onboarding.md`, agent rules |
| A template | The corresponding sample (omit `<!-- AGENT: ... -->` blocks from samples — filled content only) |
| Agent rules in `agent-rules/` | All IDE distributions in `ide/` |

## Agent Rules: Author Once, Distribute Per IDE

Agent rules are authored in `agent-rules/` (IDE-agnostic markdown). They are then distributed to each supported IDE:

| Source | Cursor | Claude Code | Copilot |
|--------|--------|-------------|---------|
| `agent-rules/*.md` | `ide/cursor/cursor-rules/*.mdc` | `ide/claude-code/CLAUDE.md` | `ide/copilot/copilot-instructions.md` |

If you change a rule in `agent-rules/`, update all three IDE distributions. If you only change one IDE's version, it will drift from the others.

## Suggest Ideas or Ask Questions

- **Have an idea?** Post in [GitHub Discussions → Ideas](https://github.com/47lining/product-workspace/discussions/categories/ideas)
- **Have a question?** Post in [GitHub Discussions → Q&A](https://github.com/47lining/product-workspace/discussions/categories/q-a)
- **Found a bug?** File a [GitHub Issue](https://github.com/47lining/product-workspace/issues/new)

Ideas that gain traction get promoted to Issues. Issues get assigned and built.

## Style Guidelines

- Use the locked vocabulary from [glossary.md](standard/glossary.md)
- Keep templates minimal — only include fields that every instance needs
- Samples should be realistic, not hypothetical
- Templates in **`templates/`** may include a concise **`<!-- AGENT: ... -->`** HTML comment with fill instructions for agents **while scaffolding**. **Do not keep that block** in generated artifacts under **`initiatives/`**, **`docs/`**, or anywhere outside the toolkit — remove it after generation so only product content ships (same idea as **samples**: filled content, no agent preamble). Update the matching **sample** when template structure changes.
- Links between toolkit files should be relative and clickable
