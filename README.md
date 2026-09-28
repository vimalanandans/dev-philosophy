# Product Development Philosophy & Practice

This repository is the evolving handbook for how I think about, design, build,
and improve digital products.

It captures the principles behind the work: how product decisions are made,
how experiences should feel, how software should be structured, how teams and
agents should collaborate, and how ideas become useful, trustworthy products.

The documents here are intentionally practical. They are not a rigid process
or a collection of universal rules. They are reusable guides, contracts,
decision frameworks, and design principles that can be adapted to a product's
context.

## Why this repository exists

Product development becomes more consistent when its assumptions are visible.
This repository makes those assumptions explicit so they can be:

- reused across projects;
- discussed, challenged, and improved;
- translated into product, design, engineering, and AI-agent instructions;
- used as a shared reference during planning and implementation;
- kept separate from the codebase of any single product.

The goal is not to prescribe one visual style or technology stack. The goal is
to preserve the reasoning and standards that should remain true even when the
product, team, platform, or implementation changes.

## What belongs here

This repository may include:

- product development philosophy and principles;
- UX and interaction contracts;
- component and design-system guidance;
- AI-native product and workspace patterns;
- architecture and implementation principles;
- agile product development practices;
- research, discovery, and prioritization methods;
- accessibility, trust, privacy, and resilience standards;
- collaboration practices for people and AI agents;
- quality, review, and release principles;
- templates, checklists, and decision records.

Each document should explain not only *what* to do, but also *why* it matters,
when it applies, and where judgment is required.

## How to use the documents

Use this repository as a living reference:

1. Start with the principle or guide relevant to the product decision.
2. Adapt it to the product's domain, users, constraints, and maturity.
3. Turn applicable principles into concrete requirements, designs, or tests.
4. Record important deviations and the reasoning behind them.
5. Feed lessons from implementation back into the documents.

The documents are inputs to judgment, not substitutes for judgment.

## Initial guides

### [AI-Native Workspace UX Brief](./web-ui-development.md)

An interaction and implementation contract for an AI-native workspace. It
covers a canvas-first application shell, contextual AI, reviewable and undoable
changes, agent runs, approvals, artifacts, multi-agent workflows, automation,
data trust, accessibility, responsive behavior, and modular implementation.

More guides will be added as the product development practice evolves.

## Working principles

The repository is guided by a few broad principles:

- **Clarity over novelty:** new interaction patterns should make the user's
  work easier to understand, not merely look different.
- **Work before machinery:** tools, settings, models, and infrastructure should
  support the user's work rather than become the work.
- **Explicit scope and consent:** people should know what a system is using,
  changing, or sending before consequential actions occur.
- **Reversible by default:** important actions should be reviewable, undoable,
  recoverable, or restorable whenever technically possible.
- **Progressive disclosure:** simple paths should stay calm while advanced
  capabilities remain available to users who need them.
- **Accessible capability:** power and flexibility should not require abandoning
  keyboard access, clear language, responsive layouts, or assistive technology.
- **Trust is a product feature:** saving, syncing, privacy, permissions,
  failures, and recovery must be understandable parts of the experience.
- **Adaptable systems:** product architecture should support changing canvases,
  workflows, agents, and domains without rebuilding the entire foundation.
- **Continuous learning:** practice improves through observation, critique,
  experiments, and honest documentation of what did not work.

## Philosophy, practice, or handbook?

The repository name `dev-philosophy` is a good concise identity. The broader
description is **Product Development Philosophy & Practice**.

“Philosophy” describes the beliefs and principles. “Practice” includes the
guides, contracts, methods, and artifacts that turn those beliefs into daily
product work. Together, they leave room for future material on component
design, agile development, AI collaboration, architecture, and personal ways
of working without making the repository sound like a static manifesto.

## Status

This is an evolving working handbook. Content may be incomplete, opinionated,
or revised as new products and experiments provide better evidence.

When adding a document, prefer:

- a clear purpose and intended audience;
- principles supported by practical guidance;
- explicit trade-offs and boundaries;
- examples where they improve understanding;
- links to related guides;
- a concise record of significant revisions.

## License and reuse

Unless a more specific notice is included in a document, the material in this
repository is intended as reusable guidance. Preserve attribution and the
context of the original principle when adapting it for another project.
