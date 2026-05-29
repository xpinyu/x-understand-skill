# x-understand

`x-understand` helps AI agents turn long source material, complex ideas, and trade-offs into grounded, transferable understanding.

Instead of producing broad summaries or textbook-style explanations, the skill guides the agent to extract the source material's core logic and build the smallest useful mental model for the user's current goal. It emphasizes causal models, cognitive-gap teaching, concrete cases, practical heuristics, boundaries, and transfer checks.

## Why This Skill Exists

Many explanations sound clear while the user is reading them, but fail when the user tries to apply the idea later. `x-understand` is designed for that application gap.

It asks the agent to explain the mechanism behind an idea, show where it works, mark where it breaks, and leave the user with a reusable way to think.

## Installation

Install the skill from this repository:

```bash
npx skills add xpinyu/x-understand-skill --skill x-understand
```

Install it globally for Cursor:

```bash
npx skills add xpinyu/x-understand-skill --skill x-understand -g -a cursor
```

List the skills available in this repository:

```bash
npx skills add xpinyu/x-understand-skill --list
```

Project-level installs are best when a team wants the skill tracked with a repository. Global installs are best when you want the skill available across Cursor workspaces.

## Usage

Cursor discovers installed skills from their `SKILL.md` metadata and can apply them automatically when the request matches the skill description.

You can also invoke the skill explicitly in Agent chat:

```text
/x-understand
```

Example prompts:

```text
Here is a long article/transcript/paper. Extract the core logic chain and help me understand what I can reuse from it.
```

```text
Extract the core logic chain from this essay.
```

```text
Help me understand how vector databases work.
```

```text
Explain this trade-off with one real case and one boundary.
```

## What It Does

`x-understand` guides the agent to:

- Identify what the user is trying to understand and why
- Extract the claim -> premise -> mechanism -> implication chain from source material
- Build the smallest useful causal model
- Use a gap -> fill -> next gap -> fill teaching rhythm
- Ground abstract ideas in a real case or clearly labeled concrete scenario
- Turn understanding into a practical rule, decision path, or next step
- Mark boundaries, failure modes, and uncertainty
- End with a transfer question that tests whether the model can be reused

## When To Use

Use this skill when the user wants to:

- Understand a concept, system, field, method, or trade-off
- Make sense of a long article, transcript, paper, note, or argument
- Build intuition without losing practical accuracy
- Explain why something works, not only what it is
- Extract the core logic of an article, paper, transcript, or argument
- Convert dense material into a reusable mental model
- Learn how to apply an idea in practice

## When Not To Use

This skill is usually not necessary for:

- Pure factual lookup
- One-step mechanical tasks
- Narrow bug diagnosis with no learning goal
- Requests where the user explicitly wants only a short direct answer

## Output Shape

A strong `x-understand` answer usually includes:

- A concise frame for what the explanation is trying to enable
- The source material's core logic chain when material is provided
- A causal model that shows what drives what
- A concrete case or scenario that makes the mechanism visible
- A practical rule of thumb or next move
- A non-obvious point when the topic genuinely has one
- A clear boundary where the model stops working
- A short transfer check

See [`skills/x-understand/examples.md`](skills/x-understand/examples.md) for representative answer shapes.

## Repository Structure

```text
x-understand-skill/
├── README.md
├── LICENSE
└── skills/
    └── x-understand/
        ├── SKILL.md
        └── examples.md
```

The skill itself lives in [`skills/x-understand/SKILL.md`](skills/x-understand/SKILL.md). That file contains the metadata and operating instructions the agent reads when the skill is invoked.

## Trust And Review

This repository is intentionally small and auditable:

- The skill is plain Markdown.
- It does not include executable scripts.
- It does not declare external runtime dependencies.
- The behavior is defined in `SKILL.md` and illustrated in `examples.md`.

As with any skill, review the contents before installing it in a sensitive workspace.

## Compatibility

The skill follows the common Agent Skill pattern: a directory containing a `SKILL.md` file with YAML frontmatter and Markdown instructions. It is intended for Cursor workflows and may also be useful in other agents that support compatible skill directories.

## Contributing

Issues and pull requests are welcome. Good contributions usually improve one of three things:

- Clearer trigger conditions in `SKILL.md`
- Better examples in `examples.md`
- Tighter wording that improves agent behavior without adding unnecessary context

Please keep changes focused and easy to audit.

## Author

Created by [pinyu](https://pinyu.ai/).

## License

[MIT](LICENSE)
