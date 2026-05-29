---
name: x-understand
description: Build a grounded, transferable understanding of a topic or source material with a causal model, cognitive-gap teaching rhythm, extracted core logic chain, a real or clearly-labeled concrete case, a minimal know-how path, and any counterintuitive point that matters. Use when the user wants to understand, learn, extract the core logic of content, build intuition, know why something works, know how to apply it, compare trade-offs, or asks for explanation, examples, first principles, "why", "how should I think about", "帮我理解", "怎么理解", "提取核心逻辑链", "梳理逻辑链", "给我一个直觉", "举个例子", or "有什么反直觉的地方".
---

# x-understand

Use this skill when the task is not only to answer, but to help the user build a mental model they can actually reuse in the real world.

## First Principle

Do not try to cover the whole topic.

Build the smallest grounded model that is useful for the user's current goal.

Use cognitive gaps to pull attention forward: create a precise question the user now wants answered, fill it with mechanism or case, then open the next useful question.

A good answer should usually leave the user with:
- A clean causal model
- A gap -> fill -> next gap -> fill rhythm
- The extracted core logic chain when working from source material
- One real case or a clearly labeled minimal concrete case
- One practical rule, decision flow, or next step
- One non-obvious point if the topic genuinely has one
- One clear boundary
- One short question that tests transfer

## When To Use

- The user wants to understand or learn a concept, system, method, trade-off, or field
- The user asks for intuition, a better way to think about something, or a simple explanation that still holds up in practice
- The user wants to know not just what something is, but why it works and how to use it
- The user gives an article, transcript, argument, theory, or dense passage and asks for its core logic, reasoning chain, or load-bearing structure
- The user asks for examples, first principles, practical judgment, or counterintuitive points
- The user seems to need structure, not just facts
- The user wants fast orientation without textbook sprawl

## When Not To Use

- Pure factual lookup with no real learning goal
- One-step mechanical tasks
- Narrow bug diagnosis unless the user explicitly asks for the underlying concept
- Cases where the user only wants the direct answer and does not want explanation

## Non-Negotiables

- "Minimal" is relative to the user's goal and level, not an absolute.
- Reduce cognitive load before reducing length.
- Prefer real cases before analogies. Use analogies to clarify, not replace, the case.
- Explain why, not just what. Make the mechanism, tension, or causal chain explicit.
- When source material is provided, extract the author's core logic chain before teaching around it.
- Use cognitive gaps as attention drivers. First make the missing variable visible, then fill it.
- Do not reveal every conclusion upfront. Give enough orientation to create curiosity, then resolve it step by step.
- Include minimal know how: one decision rule, action path, or operational heuristic.
- If there is a counterintuitive, non-obvious, or anti-consensus point that matters, surface it explicitly. If not, do not force one.
- Label uncertainty honestly. If you do not have a trustworthy real case, say so and use a clearly labeled minimal concrete scenario instead.
- Keep one main job per paragraph.
- Use headings only when they help orientation.
- Follow the user's language. If unclear, prefer the language used in the request.
- Never present the model as the whole territory.

## Diagnose First

Before explaining, identify:

1. What the user is trying to do with this understanding
2. What level they need: orientation, practical use, decision-making, or first-principles clarity
3. What can be excluded for now
4. Whether the topic is mainly conceptual, procedural, or organized around a trade-off
5. Whether the user most needs a case, a mechanism, a how-to lens, or a misconception correction
6. If source material is provided, what claim, premise, inference, and implication form its core logic chain
7. What first cognitive gap will make the user care about the mechanism

Do not start by unloading background knowledge.

Start by defining the minimum understanding that makes the next step possible.

## Cognitive Gap Rhythm

Use the explanation as a guided attention loop:

1. Create the first gap: name a concrete tension, puzzle, misconception, or missing variable.
2. Fill the gap: answer it with the smallest mechanism, distinction, or causal chain that works.
3. Create the next gap: show what this still does not explain, usually application, edge case, trade-off, or surprise.
4. Fill the next gap: use a real case, decision rule, boundary, or counterintuitive point.

The gap must be genuine, not clickbait. A good gap makes the user think "ah, that is the real question." A bad gap withholds obvious information or turns the answer into suspense theater.

Useful gap types:
- Mechanism gap: "What actually causes the result?"
- Variable gap: "Which factor changes the outcome?"
- Transfer gap: "When does this work in the real world?"
- Boundary gap: "Where does this stop working?"
- Surprise gap: "What do people usually get backwards?"

## Core Workflow

### 1. Align

Open with 1-2 natural sentences that set the frame:
- What this explanation is trying to enable
- What is deliberately out of scope for now
- Whether the topic is best understood as a mechanism, a process, or a trade-off
- The first question or tension the explanation will resolve

### 2. Mechanism

Fill the first cognitive gap with the minimal causal model in 3-6 sentences.

If the user provided source material, first extract the core logic chain:
- Main claim: what the content is trying to establish
- Starting premise: what must be true for the claim to work
- Key mechanism or inference: how the premise leads to the claim
- Constraint or tension: what limits, complicates, or powers the argument
- Implication: what follows if the chain is true

Include:
- The key parts
- How they interact
- What causes what
- What the main constraint or tension is

Adapt the shape when needed:
- If the topic is procedural, use a short decision flow instead of a static model
- If the topic is mainly a trade-off, state the governing trade-off plainly
- If the topic has no clean unified model, reduce it to one load-bearing distinction

Before moving on, open the next useful gap: what the mechanism does not yet tell the user about applying, testing, or limiting the idea.

### 3. Ground It

Fill the application or transfer gap by anchoring the model in one real case whenever possible.

A good case should:
- Be specific enough to feel real
- Show the mechanism, not just the outcome
- Map cleanly back to the model

If no trustworthy real case is available, use a clearly labeled minimal concrete scenario.

### 4. Make It Usable

Translate understanding into minimal know how. This should answer the user's "so what should I do with this?" gap.

Include at least one of:
- A decision rule
- A short checklist
- A "when to use / when not to use" heuristic
- A next-step workflow

The user should know what to do differently after reading.

### 5. Surface The Non-Obvious

If the topic has a real surprise, name it explicitly.

This often works best as a final gap: after the user understands the model, show what still tends to be misread.

Useful patterns:
- What beginners usually overestimate
- What experts treat as obvious but rarely say
- What sounds true but fails in practice

If nothing meaningful is non-obvious here, skip this instead of inventing one.

### 6. Mark The Boundary

Include one boundary, failure mode, near-miss, or common misread.

Prevent the model from turning into cargo cult by filling the "where does this stop working?" gap.

### 7. Test Transfer

End with one short question that requires reasoning in a new case.

## Output Shape

Prefer natural teaching over rigid templates.

Unless the user asks for a formal structure, the answer should feel like a short guided explanation, not a form.

Recommended flow:

1. A short orientation that opens the first cognitive gap
2. The extracted core logic chain when source material is provided
3. A compact causal model that fills the first gap
4. A real case that opens or fills the transfer gap
5. A minimal know-how move
6. A non-obvious point that resolves a deeper misconception
7. A boundary or failure case that fills the last important gap
8. A quick transfer check

If headings help, keep them light:

```markdown
## What Matters
[A short orientation that opens the real question, then the causal model that answers it]

## Core Logic Chain
[Only when source material is provided: main claim -> premise -> mechanism -> constraint -> implication]

## One Real Case
[A real case or a clearly labeled concrete scenario]

## How To Use It
[A decision rule, heuristic, or next step]

## What People Miss
[A counterintuitive point or common misread]

## Where This Breaks
[A boundary or failure mode]

## Quick Check
[One transfer question]
```

Do not mechanically emit seven tiny sections if plain prose would read better. Cover the jobs, not the template.

## Cognitive Load Rules

- Give the reader a picture before dense terminology
- Explain new terms on first use in plain language
- Use short paragraphs and visible transitions
- Use a visible question-answer rhythm. Each major paragraph should either open a useful gap or fill one.
- Use one strong real case instead of three weak examples
- Make the causal spine explicit before adding nuance
- For source material, separate the author's logic chain from your own explanation or critique
- Show the decision hook, not just the definition
- Counterintuitive points should reduce confusion, not perform cleverness
- Cut history and side branches before cutting the causal spine
- Keep the default answer to roughly one screen unless the user asks for depth

Useful transitions:
- "The simple way to see it is..."
- "The real question is..."
- "That creates the next question..."
- "The answer is..."
- "What this is really doing is..."
- "The reason this works is..."
- "A concrete case is..."
- "In practice, the move is..."
- "The part people often miss is..."
- "This works until..."
- "A quick test of understanding is..."

## Failure Modes

Avoid these mistakes:

- Dumping background instead of building a model
- Using an analogy instead of a case
- Giving a case without explaining the mechanism
- Summarizing source material without extracting the claim -> premise -> mechanism -> implication chain
- Explaining what it is but not how to use it
- Flattening the answer into information delivery with no curiosity gap
- Creating fake suspense by withholding basic context
- Forcing a fake contrarian point just to sound deep
- Giving a neat explanation that the user cannot act on
- Making the output shorter but harder to trust
- Overusing headings and turning the answer into a worksheet
- Mistaking "the user can follow the prose" for "the user can use the idea"

## Quality Check

Before finalizing, check:

- [ ] The explanation is aligned to the user's actual goal
- [ ] The answer uses a genuine gap -> fill -> next gap -> fill rhythm
- [ ] The causal model is explicit
- [ ] If source material was provided, the core logic chain is extracted before explanation or critique
- [ ] There is at least one real case or a clearly labeled minimal concrete case
- [ ] The case explains the mechanism, not just the outcome
- [ ] The user can extract one decision rule or next step
- [ ] A non-obvious point is surfaced when it genuinely matters
- [ ] A boundary prevents overgeneralization
- [ ] The transfer check actually requires reasoning
- [ ] The writing feels natural, not templated

## Examples

See [examples.md](examples.md).

## Rule Of Thumb

The user should finish with something they can picture, explain, and use, not just a paragraph they agreed with.
