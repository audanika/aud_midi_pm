<!--
@license
Copyright (c) audanika

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Project management repo guide

## Know what a PM repo is

- A project management (PM) repo holds the goals, concepts, plans,
  decisions and blog posts of a project — no code
- Every ticket belongs to exactly one PM repo. Add it to the ticket before
  any code repo (see the `gg` development guide)
- A ticket that is only planned ends with the PM repo alone

## Structure the repo like this

```text
root
|-doc
| |-2026-Q3
| | |-goals
| | |-concepts
| | | |-topics
| | | |-decisions
| | | | |-000-index.md
| | | |-ux
| | |-architecture
| | | |-architecture.md
| | | |-img
| | |    |-diagram.mmd
| | |-tickets
| | | |-2026-09-10-cdm-1317-infrastructure-discovery-server.md
| | |-bugs
| |-blog
| | |-2026
| | | |-2026-09-10-blogpost-1.md
|-README.md
```

- `README.md` names the project and links to the current quarter
- `doc/<yyyy>-Q<n>` holds one folder per quarter; start a new one at the
  start of a quarter, do not move old files
- `goals` — what the quarter is meant to achieve; one file per goal
- `concepts` — what the product is and why, see below
- `architecture` — the target picture of the system: `architecture.md`
  plus diagrams in `img` as mermaid `.mmd` files
- `tickets` — one plan file per ticket
- `bugs` — one file per bug; a bug turns into a ticket once it is planned
- `blog` — one post per finished ticket; exists only if the repo has the
  `dna_blog` layer, see below

## Fill the concepts folder

- `topics` — one file per product topic: evidence, use cases, requirements,
  what was tried and what holds; the place for problem-space knowledge
- `decisions` — one file per decision, `<area>-<nnn>.md`, e.g.
  `design-001.md`; `000-index.md` lists all decisions with ID, status,
  date, one line and open work
- `ux` — accepted statements about the product's surface and flows: which
  objects, places and words the user meets, and why
- Write a decision file with: title, status (proposed / accepted /
  superseded), date, canonical source, open work, the decision in one
  paragraph
- Never rewrite a decision; supersede it with a new one and link both ways

## Write blog posts

- Write a post only if the repo has the `dna_blog` layer; follow its blog
  guide for content and template
- Put the post into `doc/blog/<yyyy>` of the PM repo, one folder per year
- Name it `<yyyy>-<mm>-<dd>-<title>.md`, title in English kebab case

## Name the files

- Prefix ticket and bug files with the date: `<yyyy>-<mm>-<dd>-`
- Add the ticket ID in lower case: `cdm-1317`
- Finish with the title in English kebab case:
  `2026-09-10-cdm-1317-infrastructure-discovery-server.md`
- Name goals, topics, ux files, architecture files and diagrams by their
  topic, in English kebab case

## Use the design layers

- Plan with the seven layers of product design; the `dna_design_layers`
  layer ships the [layers guide](layers-guide.md), one guide per layer and
  the `/layers-*` skills
- Run `/layers-orient` before planning a ticket that changes the product;
  it names the layer that needs attention first
- Write the residue of each layer into the PM repo:

| Layer                                  | Lands in                      |
| -------------------------------------- | ----------------------------- |
| Observed behaviour, domain, user needs | `concepts/topics`             |
| Product strategy                       | `goals`                       |
| Conceptual model, interaction flow     | `concepts/ux`, `architecture` |
| Surface                                | `concepts/ux`                 |
| Every decision made on the way         | `concepts/decisions`          |

- Do not plan a ticket on a layer whose foundations are weak; plan the
  foundation first, or say plainly that the ticket is a bet

## Plan a ticket

Set the goal: one paragraph on what is achieved and for whom, and which
goal of the quarter it serves.

Name the affected repos and what changes in each one.

List the rough steps in order; one line per step.

Collect the open questions; decide them with the user before implementing.

Link the decisions and topics the plan rests on.

Let the user review the plan and revise it until they confirm it.

## Write the ticket file

- Create `doc/<quarter>/tickets/<date>-<id>-<title>.md`
- Use these sections, in this order:

```markdown
# <ID>: <Title>

## Goal

## Affected repos

## Steps

## Open questions
```

- Keep the plan short; write more only for complex tickets
- Wrap lines at 80 characters
- Embed mermaid diagrams when a picture says more than text

## Keep the plan alive

- Update the plan when the implementation deviates from it
- Move answered questions from `Open questions` into the plan or into a
  decision file
- Reference the plan from the blog post that closes the ticket
- Keep the file: the plan documents why things are the way they are

## Plan a quarter

Write the goals of the quarter into `goals`, one file per goal.

Update `architecture/architecture.md` when a goal changes the target
picture.

Derive tickets from the goals; each ticket names the goal it serves.
