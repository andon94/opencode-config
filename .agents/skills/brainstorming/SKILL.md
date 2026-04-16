---
name: brainstorming
description: "Use before implementing new features, significant behavior changes, or ambiguous work with meaningful product or technical trade-offs. Clarifies requirements, explores alternatives, and gets design approval before implementation. Skip for clearly-scoped small fixes, routine refactors, targeted config edits, and other low-risk changes."
---

# Brainstorming Ideas Into Designs

Help turn ideas into fully formed designs and specs through natural collaborative dialogue when the work actually benefits from upfront design.

Start by understanding the current project context, then ask questions one at a time to refine the idea when requirements or trade-offs are still unclear. Once you understand what you're building, present the design and get user approval before implementation.

<HARD-GATE>
Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until you have presented a design and the user has approved it when the request is a new feature, a significant behavior change, or otherwise ambiguous/high-impact. For clearly-scoped small fixes, routine refactors, targeted config edits, and similar low-risk changes, a brief confirmation is enough and a full brainstorming flow is unnecessary.
</HARD-GATE>

## Anti-Pattern: "Everything Needs Full Brainstorming"

Do not force a heavyweight design ritual onto tiny, well-scoped tasks. The point of this skill is to reduce wasted work on ambiguous or high-impact changes, not to add ceremony to obvious ones. Scale the process to the task: sometimes that means a real spec, sometimes it means a short design summary, and sometimes it means skipping this skill entirely.

## Checklist

Use the lightest path that fits the task:

1. **Explore project context** — check files, docs, recent commits
2. **Offer visual companion** (if topic will involve visual questions) — this is its own message, not combined with a clarifying question. See the Visual Companion section below.
3. **Ask clarifying questions** — one at a time, only as needed to understand purpose, constraints, and success criteria
4. **Propose 2-3 approaches** — when there are meaningful trade-offs
5. **Present design** — scale it to the complexity of the task and get approval before implementation when this skill is in use
6. **Write design doc** — only for large or long-running work, or when the user asks for a written spec
7. **Spec self-review** — only if you created a written spec
8. **User reviews written spec** — only if you created a written spec
9. **Transition to implementation** — invoke writing-plans only when a detailed execution plan is actually warranted

## Process Flow

- **Light path:** explore context -> ask only the necessary clarifying question(s) -> present a concise design -> get approval -> implement
- **Full path:** explore context -> clarify requirements -> compare approaches -> present design -> optional written spec -> optional writing-plans -> implement

**The terminal state is not automatically invoking writing-plans.** Only invoke it when the user explicitly wants a detailed plan or the task is large enough to benefit from one.

## The Process

**Understanding the idea:**

- Check out the current project state first (files, docs, recent commits)
- Before asking detailed questions, assess scope: if the request describes multiple independent subsystems (e.g., "build a platform with chat, file storage, billing, and analytics"), flag this immediately. Don't spend questions refining details of a project that needs to be decomposed first.
- If the project is too large for a single spec, help the user decompose into sub-projects: what are the independent pieces, how do they relate, what order should they be built? Then brainstorm the first sub-project through the normal design flow. Each sub-project gets its own spec → plan → implementation cycle.
- For appropriately-scoped projects, ask questions one at a time to refine the idea
- Prefer multiple choice questions when possible, but open-ended is fine too
- Only one question per message - if a topic needs more exploration, break it into multiple questions
- Focus on understanding: purpose, constraints, success criteria

**Exploring approaches:**

- Propose 2-3 different approaches with trade-offs
- Present options conversationally with your recommendation and reasoning
- Lead with your recommended option and explain why

**Presenting the design:**

- Once you believe you understand what you're building, present the design
- Scale each section to its complexity: a few sentences if straightforward, up to 200-300 words if nuanced
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something doesn't make sense

**Design for isolation and clarity:**

- Break the system into smaller units that each have one clear purpose, communicate through well-defined interfaces, and can be understood and tested independently
- For each unit, you should be able to answer: what does it do, how do you use it, and what does it depend on?
- Can someone understand what a unit does without reading its internals? Can you change the internals without breaking consumers? If not, the boundaries need work.
- Smaller, well-bounded units are also easier for you to work with - you reason better about code you can hold in context at once, and your edits are more reliable when files are focused. When a file grows large, that's often a signal that it's doing too much.

**Working in existing codebases:**

- Explore the current structure before proposing changes. Follow existing patterns.
- Where existing code has problems that affect the work (e.g., a file that's grown too large, unclear boundaries, tangled responsibilities), include targeted improvements as part of the design - the way a good developer improves code they're working in.
- Don't propose unrelated refactoring. Stay focused on what serves the current goal.

## After the Design

**Documentation:**

- Write the validated design (spec) to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md` only for large or long-running work, or when the user asks for a written spec
  - (User preferences for spec location override this default)
- Use elements-of-style:writing-clearly-and-concisely skill if available
- Do not commit the design document unless the user explicitly asks for a commit

**Spec Self-Review:**
After writing the spec document, look at it with fresh eyes:

1. **Placeholder scan:** Any "TBD", "TODO", incomplete sections, or vague requirements? Fix them.
2. **Internal consistency:** Do any sections contradict each other? Does the architecture match the feature descriptions?
3. **Scope check:** Is this focused enough for a single implementation plan, or does it need decomposition?
4. **Ambiguity check:** Could any requirement be interpreted two different ways? If so, pick one and make it explicit.

Fix any issues inline. No need to re-review — just fix and move on.

**User Review Gate:**
If you wrote a spec, ask the user to review the written spec before proceeding:

> "Spec written to `<path>`. Please review it and let me know if you want any changes before we continue."

Wait for the user's response. If they request changes, make them and re-run the spec review loop. Only proceed once the user approves.

**Implementation:**

- Invoke the writing-plans skill only when the user asks for a detailed implementation plan or the task is large enough to benefit from one
- Otherwise, proceed directly to implementation after design approval

## Key Principles

- **One question at a time** - Don't overwhelm with multiple questions
- **Scale the process to complexity** - Full specs are for ambiguous, high-impact, or long-running work
- **Multiple choice preferred** - Easier to answer than open-ended when possible
- **YAGNI ruthlessly** - Remove unnecessary features from all designs
- **Explore alternatives** - Always propose 2-3 approaches before settling
- **Incremental validation** - Present design, get approval before moving on
- **Be flexible** - Go back and clarify when something doesn't make sense

## Visual Companion

A browser-based companion for showing mockups, diagrams, and visual options during brainstorming. Available as a tool — not a mode. Accepting the companion means it's available for questions that benefit from visual treatment; it does NOT mean every question goes through the browser.

**Offering the companion:** When you anticipate that upcoming questions will involve visual content (mockups, layouts, diagrams), offer it once for consent:
> "Some of what we're working on might be easier to explain if I can show it to you in a web browser. I can put together mockups, diagrams, comparisons, and other visuals as we go. This feature is still new and can be token-intensive. Want to try it? (Requires opening a local URL)"

**This offer MUST be its own message.** Do not combine it with clarifying questions, context summaries, or any other content. The message should contain ONLY the offer above and nothing else. Wait for the user's response before continuing. If they decline, proceed with text-only brainstorming.

**Per-question decision:** Even after the user accepts, decide FOR EACH QUESTION whether to use the browser or the terminal. The test: **would the user understand this better by seeing it than reading it?**

- **Use the browser** for content that IS visual — mockups, wireframes, layout comparisons, architecture diagrams, side-by-side visual designs
- **Use the terminal** for content that is text — requirements questions, conceptual choices, tradeoff lists, A/B/C/D text options, scope decisions

A question about a UI topic is not automatically a visual question. "What does personality mean in this context?" is a conceptual question — use the terminal. "Which wizard layout works better?" is a visual question — use the browser.

If they agree to the companion, read the detailed guide before proceeding:
`skills/brainstorming/visual-companion.md`
