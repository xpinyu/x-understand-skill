# x-understand

A reusable agent skill for turning complex ideas and source material into grounded, transferable understanding.

`x-understand` helps an AI agent explain concepts, systems, trade-offs, source material, and reasoning chains in a way the user can actually reuse. It emphasizes causal models, cognitive-gap teaching, concrete cases, practical heuristics, boundaries, and transfer checks.

## Install

```bash
npx skills add xpinyu/x-understand-skill
```

Install globally:

```bash
npx skills add -g xpinyu/x-understand-skill
```

Install only this skill from the repository:

```bash
npx skills add xpinyu/x-understand-skill --skill x-understand
```

## What It Does

This skill guides the agent to:

- Identify what the user is trying to understand and why
- Build the smallest useful causal model
- Use a gap -> fill -> next gap -> fill teaching rhythm
- Extract the core logic chain from source material
- Ground abstract ideas in a real case or concrete scenario
- Turn understanding into a practical rule or next step
- Mark boundaries and failure modes
- End with a transfer question that tests whether the model can be reused

## When To Use It

Use `x-understand` when the user asks to:

- Understand a concept, system, field, or method
- Build intuition
- Explain why something works
- Compare trade-offs
- Extract the core logic of an article, paper, transcript, or argument
- Turn dense material into a reusable mental model
- Learn how to apply an idea in practice

Example prompts:

```text
Help me understand how vector databases work.
```

```text
Extract the core logic chain from this essay.
```

```text
Give me a practical mental model for product positioning.
```

```text
Explain this trade-off with one real case and one boundary.
```

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

## Philosophy

Do not try to cover the whole topic.

Build the smallest grounded model that is useful for the user's current goal.

A good explanation should leave the user with something they can picture, explain, and use.

## Author

Created by [pinyu](https://pinyu.ai/).

## License

MIT
