# Agents

<!-- agent: claude — whole file, created 2026-08-07 when the repository was
     created. It is a sibling of the AGENTS.md files in s7r and zocam; see
     "Paired agent files". -->

These instructions are for AI agents that work in this repository. They use
ASD-STE100 (Simplified Technical English). Keep that style when you edit this
file.

This repository holds a library that describes processes: what the steps of a
process are, what must happen before what, and what tells you a step is done. It
describes a process. It does not run one, and it does not schedule one.

**This is a public library.** It must stand on its own, and it must teach
through its reference pages. The rule in "Examples and recipes" is strongest
here, exactly as it is in zocam.

**The repository is empty.** No code, no stack, no decisions recorded. Read
"First questions" below before you write anything.

## First questions

Nothing here is decided. Ask me about each of these before you start:

1. **How much of this already exists in s7r?** `S7r.Activity`, `S7r.Task`, and
   `S7r.Dependency` already describe steps and prerequisites. This library may
   be an extraction of those, or a more general thing that s7r comes to depend
   on. This is the first question.
2. **What is the stack?** The rest of the platform is Elixir, and zocam is a Hex
   package. That is a strong default and not a decision.
3. **Where is the line against s7r?** A process says "step B needs step A". A
   schedule says "step B is on Tuesday at 10". The line sounds clear and it is
   not: a prerequisite with a lead time ("call at least one hour before") lives
   on both sides of it.

## Because it is public

- The library is released to Hex, and its reference goes to hexdocs.pm. A
  release is a tag `vX.Y.Z` that equals the `version` in `mix.exs`, and GitHub
  Actions does the publishing. Do not publish from a local console.
- Write every docstring example as a doctest (`iex>` lines), so the test suite
  proves that each example stays true.
- Publication does not create users. The "No users" rule still holds: make the
  breaking change when it gives a better design.

## Where this sits in the platform

| Repository | What it holds |
| --- | --- |
| [hicha-aggregate](https://github.com/yuri4n/hicha-aggregate) | The centre: reads every source, answers combined questions |
| [hicha-graph](https://github.com/yuri4n/hicha-graph) | Resources, topics, roadmaps |
| [hicha-process](https://github.com/yuri4n/hicha-process) | The library that describes processes |
| [s7r](https://github.com/yuri4n/s7r) | The scheduler: activities, goals, the planner |
| [zocam](https://github.com/yuri4n/zocam) | The time library s7r stands on |

Work for this repository is tracked in The **hicha — process description library** project on the Linear board.

## Origin

The vision for this project is mine. I designed it with concepts that I learned
while I explored ideas together with an AI agent. I set the direction; the agent
helps me to build and to learn.

## Communication

- My requests are often not precise. When I say "I would like to make X", read
  it as the start of a discussion. First, help me make the goal clear. Then show
  the possible implementations and their caveats.
- Write all prose in simple ASD-STE100: reports, code comments, docstrings, and
  documentation pages. Write to teach, because my goal is to learn as much as
  possible.
- I understand visual explanations better than text. Use diagrams when they show
  a flow or a structure better than words (see "Diagrams").

## Examples and recipes

The docs teach through examples and through process, not through description
alone.

- **Start with the "why".** Each page and each docstring first tells what the
  thing tries to do, and how it connects with the rest of the system. Give the
  reader the purpose before the mechanics.
- **Write recipes.** Build the docs around common scenarios: "You want to get X
  done. Do these steps." A recipe shows the process, step by step, not only the
  final call.
- Use many examples in the docs and in the docstrings. Show each concept with at
  least one example that the reader can run.
- Cover four kinds of cases:
  - The common use case — the call that most readers come for.
  - The pitfall — the call that looks correct and is not.
  - The edge — the surprising case at the boundary.
  - The integrated use — one concept inside another.
- **Tests follow the same principle.** Shape a test as a recipe for a real
  scenario. Stop where the recipe form makes a test more complicated or more
  costly than necessary; a plain test is then better.

## No users

The project has no users. No other person and no other code depends on it.

- Make a breaking change when it gives a better design. Do not add a deprecation
  path, a compatibility shim, or a migration guide unless I ask.
- Rename, move, and delete freely. A better name is worth the diff.
- Delete an ADR when its decision is dead. Do not keep a dead ADR "for the
  history".
- **An ADR is mutable here.** The usual rule says a record is immutable, and
  that a new decision must supersede an old one. That rule protects a team that
  reads the old record. This project has one developer and is at an early stage,
  thus the rule costs more than it gives. Edit an ADR in place, renumber it,
  split it, or delete it. Do not add a "Superseded by" chain.

## Separate repositories

Each part of the hicha platform is its own repository. Keep them apart.

- Two repositories touch at one point only: a declared dependency. Nothing else
  crosses the boundary.
- No script, build step, or page in one repository can read a file in another.
  If a tool needs a path that starts with `../`, the design is wrong.
- Each repository documents itself. Do not copy a page from one site to another.
  Link to it.
- Each repository numbers its ADRs from 001. The series are independent. Write
  "s7r ADR-003" with a link, never a bare number.
- A decision that touches two projects becomes two ADRs, one in each repository.
  Each ADR records its own side only.
- If two repositories need the same machinery, make it a package that both
  depend on. Do not copy the file, and do not read it across the boundary.

### Paired agent files

Each repository keeps its own AGENTS.md, and the files are a set:

- When one repository learns a rule that also applies to another, update both
  files in the same session. Write each side in its own file, in its own words.
- Facts that belong to one repository only stay in that repository's file.
- Each file stays complete on its own. A reader of one repository must not need
  another file.

## Ask me first

Ask me before you:

- Redesign the API, the code structure, or the overall plan for the code.
- Commit to a distributed-system design.
- Create integration tests.
- Apply changes to the README or to other documentation pages. Propose the
  changes first, at the end of your other work.

## Workflow

- Write code test-first (TDD).
- Shape the tests as recipes for real scenarios.
- Do not run tests while design questions are open. Ask the questions first. A
  test run that comes before a decision can be wasted work.
- Update AGENTS with relevant info (and tag your changes as always).

## Where work is tracked

Open work lives in two places, and the split is by scope. Put each item in one
place only.

- **Linear** holds the project management: everything that a person plans,
  prioritises, or schedules. Epics, decisions that wait on the user, work that
  crosses more than one file, and anything another session must find without
  reading this repository.
- **`docs/TODO.md`** holds the localised, scoped items: a note that belongs to
  one file or one component, small enough that the person who opens that file is
  the person who does it. Keep the list short. Delete an entry when it ships or
  when it dies.

Two rules follow:

- **Keep both current as you work.** Work that exists only in a chat report is
  work that is lost, because the next session starts with an empty context.
- **Promote an item when it outgrows its home.** A `docs/TODO.md` entry that
  turns out to need an ADR, or to touch several files, becomes a Linear issue
  and leaves the file.

## Reports

When you finish code work, give me a report. The report must contain:

- A summary of the changes.
- Mermaid diagrams, if the code is more complex than usual.
- The next steps.
- Important remarks, trade-offs, and todos.

Keep the report compact. A full read must take 5 to 10 minutes. I will ask
questions about the parts that are not clear.

## Code style

- Tag the code that you write. Use a comment.
  - Tag each function or each comparable unit.
  - Tag a whole module only if I will use it as a black box and will not modify
    it myself.
  - If you change code that I wrote, mark that you made a change.
- Add comments and docstrings to all code that is not fully obvious. Explain the
  code as a teacher does.
- Use abstractions and patterns, not ad-hoc designs. Do not write two
  definitions for things that are semantically the same. Name the pattern that
  you use (for example: "This is a proxy").
- Model data as a graph when a graph represents the data better than other
  structures.

## Diagrams

- In Markdown files, use Mermaid diagrams. Always set the `mermaid` language on
  the code block.
- In docstrings, use ASCII diagrams for complex or important flows.
- In chat replies, create a `.mmd` file (only in your memory), so I can see them
  in VSCode.
- On a public page, give a caption to each diagram (see "Attribution").

## Documentation

- Document each choice between two or more implementations or designs. Record
  the choice in the code and in the docs. For a design choice, write an ADR.
- If you change the code structure, the functionality, or the commands that run
  the code, propose the matching README changes. Ask me before you apply them
  (see "Ask me first").
- Put dedicated documentation pages in `docs/content/`. An ADR goes in
  `docs/content/2.design/adrs/NNN-slug.md`. The number is the sort key. **The
  files are the pages**: no script generates an ADR page, and no script copies
  one.
- Each public page must show who made it (see "Attribution").

## Attribution

These rules apply to text that other persons will read: the README, the pages in
`docs/content`, and any website that comes from them. They do not apply to chat
replies or to code comments (for code, see "Code style").

- Tell the reader that an AI agent made the content. Use the words "AI SLOP".
  This is on purpose. An honest joke is better than a notice that hides the
  truth.
- Tell the reader that a senior engineer gave the direction and did the review.
  Say also that the review is human. A human review has normal limits, thus
  errors can stay. Do not claim full verification.
- Show my GitHub profile: `https://github.com/yuri4n`. Keep it small and calm.
  One link on each page is sufficient. Do not put my name in the title, in a
  heading, or in more than one position on the same page. The page is about the
  work, not about me.

Use this notice, or a text with the same meaning:

```markdown
> **AI SLOP** — an AI agent wrote this page. [yuri4n](https://github.com/yuri4n), a senior
> engineer, gave the direction and did the review. The review is human, thus errors can stay.
```

### Level of the tag

- Put the notice at the highest level that is still true, and no lower. One
  notice for each page is usually correct.
- Use a lower level (a section) only if that part is different from the
  remainder of the page.
- Do not put a tag on each bullet, on each paragraph, or on each list item.
- Keep the notice in the same position on all pages: immediately after the page
  title.

### Figures

A figure is a Mermaid diagram, an image, a chart, or a table that the text
refers to as a unit.

- Give a caption to each figure on a public page. Put the caption immediately
  below the figure.
- The caption must have three parts: the number or the name of the figure, one
  line that tells what the figure shows, and the note that AI made it.
- Example:

```markdown
_Figure 3 — How the planner makes a schedule from the constraints. AI generated, human reviewed._
```
