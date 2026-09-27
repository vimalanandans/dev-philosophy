# AI-Native Workspace UX Brief

Build an original, English-first AI-native web workspace. Use the interaction principles below as inspiration only; do not copy AGPL code, assets, labels, screens, schemas, or exact visual styling from a reference product.

The product should feel calm, capable, and trustworthy: users navigate on the left, do focused work in the center, and open contextual tools on the right.

```txt
Application Shell
├── Navigation rail / sidebar
├── Primary canvas
│   ├── Optional Professional Editor
│   ├── Dashboard
│   ├── Record/detail page
│   ├── Table/spreadsheet
│   ├── Builder/canvas
│   └── Inbox or conversation
├── Context drawer
│   ├── AI Assistant
│   ├── Inspector
│   ├── Comments
│   ├── Activity
│   └── Version history
└── Optional bottom command / voice surface
```

## Core principles

- **Work first:** the center canvas owns the screen. Do not make chat, settings, or model selection the primary experience.
- **Stable spatial memory:** navigation stays left, current work stays center, contextual tools stay right.
- **Progressive disclosure:** advanced AI details, token usage, traces, costs, raw requests, and diagnostics remain available but hidden by default.
- **AI as a layer:** AI acts on the user’s selected object or current context; it is not a separate, disconnected chat product.
- **User control:** AI never silently changes content. Every proposed change can be previewed, accepted, revised, rejected, and undone.
- **Trust by default:** local save is immediate; sync, privacy, data sharing, and recovery are clear and understandable.
- **Keyboard-first, mouse-friendly:** every core action is accessible by keyboard without making the UI feel developer-only.

## Layout and panels

### Left navigation

Use a persistent sidebar on desktop with:

- Workspace switcher
- Projects, recent items, favorites, and search
- Domain-specific item tree or list
- Create button
- Settings/help at the bottom

The sidebar should be collapsible. Its collapsed state preserves recognizable icons with tooltips. Do not hide the current item or key status merely because the sidebar is compact.

### Primary canvas

The center view is a pluggable canvas. Each canvas type should expose:

- Current item identity and breadcrumbs
- Selection state
- Context available to AI
- Undo/redo capability
- Optional export and versioning capability
- Optional inspector fields

A document editor is only one implementation. Do not force pagination, formatting toolbars, or document-specific controls into dashboards, records, or other canvas types.

### Right context drawer

The right drawer hosts context-sensitive tools:

- Assistant
- Inspector
- Comments
- Activity
- Versions

It should remember the last useful tab per workspace or item. It must be collapsible, resizable, and able to operate either as:

- **Overlay mode:** floats over the canvas; best for focused work and smaller screens.
- **Docked mode:** pushes the canvas inward; best for large desktop displays.

Persist this preference per user. On mobile, always use an overlay/sheet rather than showing three columns.

### Bottom command and voice surface

Keep this optional and unobtrusive.

It can host:

- Global command palette entry point
- AI input for the current context
- Voice dictation and TTS controls
- Connection/offline status
- A compact save/sync indicator

Voice is an enhancement, never the only way to complete an action.

## Panel behavior and motion

Use motion to clarify spatial relationships, not to decorate.

- Standard interaction duration: 120–200 ms.
- Larger panel transitions: 180–260 ms.
- Use a restrained ease-out curve; avoid bouncy spring motion for persistent panels.
- Respect `prefers-reduced-motion`: remove sliding, scale, shimmer, and streaming cursor animation; preserve only instant state changes.

Panel rules:

- Opening a sidebar or drawer slides it from its owning edge and fades its contents in slightly.
- Closing reverses that motion; do not abruptly remove focus.
- In docked mode, animate the layout width smoothly; in overlay mode, animate with transforms for performance.
- A drawer resize handle appears on hover/focus, supports pointer and keyboard resizing, has sensible minimum widths, and persists its width.
- Double-clicking a resize handle restores the default width.
- Pressing `Escape` closes the most recently opened transient UI first: menu → popover → dialog → drawer.
- Clicking the backdrop closes temporary overlays, but never discards unsaved work.
- Menus, popovers, and dialogs must trap focus only when they block a decision. Sidebars and drawers should not trap focus.

Use clear but quiet feedback:

- Button press: brief opacity/color response.
- Save success: no toast unless the user explicitly saved/exported.
- Error: keep the error near the action, explain the next recovery step, and preserve the user’s input.
- Long-running work: show progress or meaningful phase text, not an indefinite spinner alone.

## AI interaction model

### Context and scope

Every AI interaction must state its scope in plain language:

- “Use selected text”
- “Ask about this record”
- “Use this project’s approved references”
- “No project references attached”

The AI composer shows context as removable chips. Users can inspect exactly what will be sent before running an action.

### Selection actions

When the user selects meaningful content, show a compact contextual action bar after a brief delay. Offer only relevant actions:

- Ask
- Rewrite
- Improve
- Summarize
- Extract
- Compare
- Generate
- Convert
- Fix

Do not show every action for every object.

### Streaming and ghost text

For generative edits:

1. User invokes an action.
2. Show a concise request state with Cancel.
3. Stream output as a clearly distinct proposal, not committed content.
4. Keep the original content intact.
5. Let users Accept, Reject, Edit Instruction, or open a Diff.
6. On accept, turn it into one undoable user-visible operation.
7. On reject/cancel, restore the exact prior selection and viewport.

For editor canvases, ghost text can appear inline with a visually distinct but readable treatment. It must never be confused with saved content. `Tab` may accept and `Escape` may reject, but visible buttons must always be present.

### Assistant drawer

The assistant supports free-form chat, but it should remain grounded in the active workspace.

Include:

- Conversation history
- Context/reference selector
- Model selector in advanced settings or a compact dropdown
- Stop/cancel generation
- Attachments
- Expandable run details: provider, model, sources, duration, tokens, estimated cost, errors, trace ID

Do not permanently display token counts, provider logos, or debug information in the normal working view.

## Optional Professional Editor

Implement this as `ProfessionalEditorCanvas`, not as the application’s mandatory center view.

Capabilities:

- Tiptap-based rich text: headings, bold, italic, links, lists, block quotes, code blocks, tables where appropriate, and keyboard shortcuts.
- Optional paginated print layout for document workflows only.
- Inline comments/remarks anchored to exact content.
- KaTeX math support.
- Font family, size, line-height, color, and focus-mode controls.
- Current paragraph focus highlight, without harming text selection or accessibility.
- Live word, character, and paragraph counts.
- Text-to-speech and dictation where supported.
- DOCX/PDF/EPUB export through explicit export adapters, each with stated fidelity limits.

## Data, sync, and privacy behavior

Treat this as a visible product surface called **Data & Trust**.

- Save locally first, immediately and optimistically.
- Display “Saved” quietly; only call attention to Offline, Syncing, Conflict, or Backup Failed.
- Queue sync while offline and retry when connectivity returns.
- Never overwrite a remote/local conflict silently. Present a comparison, a merge option where possible, and a restore point.
- Support version history, named restore points, deletion recovery, portable project export/import, and per-item export.
- Show a simple answer to: “Where is this saved?”, “Is it synced?”, “What did AI receive?”, and “Can I recover it?”
- Never use customer content for model training by default.
- Explain provider-specific data handling before a user connects a provider.
- In managed web deployments, use encrypted server-side credential storage or authorized provider connections; do not retain long-lived API keys in browser storage.
- Diagnostics must be exportable and redact credentials, authorization headers, private text where possible, and personally identifying metadata.

## Settings architecture

Organize settings around user intent:

- General: appearance, theme, language, accessibility, keyboard shortcuts
- Workspace: profile, organization, roles, sharing
- AI: providers, default model, custom instructions, context policy, usage limits
- Data & Trust: local cache, cloud sync, retention, backups, export/import, privacy
- Voice: microphone permissions, dictation, TTS voice and rate
- Integrations: Google, Microsoft, Apple, Dropbox, Slack, GitHub, enterprise SSO
- Advanced: traces, diagnostics, experiments, developer controls

Default to English (US), US dates/numbers, familiar US integrations, and provider-neutral choices such as OpenAI, Anthropic, Google, and compatible custom endpoints. Do not include China-specific providers, login methods, storage, sync, payments, or non-English-first UI unless explicitly requested.

## Visual direction

Create an original visual system based on clarity and low cognitive load:

- Neutral light and dark palettes; one restrained accent color.
- Generous canvas space; compact but readable sidebars.
- Clear typography hierarchy; use system or licensed fonts selected for English readability.
- Subtle borders and surfaces rather than heavy shadows or glass effects.
- Design tokens for color, spacing, radius, elevation, type scale, panel width, and motion.
- Avoid copying reference branding, iconography, wording, color values, or exact geometry.

## Implementation requirements

Use a modular architecture:

- `AppShell`
- `NavigationSidebar`
- `PrimaryCanvas`
- `CanvasAdapter`
- `ContextDrawer`
- `CommandPalette`
- `AIComposer`
- `AIChangeSet`
- `SyncStatus`
- `VersionHistory`
- `Diagnostics`
- `Settings`

Recommended stack:

- Next.js, React, TypeScript
- Tailwind with CSS design tokens
- Radix UI or Base UI
- TanStack Query plus Zustand/Jotai
- `react-resizable-panels`
- `cmdk`
- Tiptap only for the optional editor adapter
- IndexedDB for offline cache
- Postgres/object storage for managed sync
- Streaming via SSE or WebSockets
- Server-side provider adapters and structured AI actions
- Sentry/OpenTelemetry for operational observability

## Coding-agent instruction

```txt
Build an original AI-native workspace from this UX brief.

Do not access, copy, adapt, or recreate code, assets, labels, screenshots,
storage keys, schemas, visual styling, or exact layouts from AGPL references.

Implement a stable left navigation area, a dominant interchangeable central
canvas, a resizable/collapsible contextual right drawer, and an optional bottom
command/voice surface. Make the professional rich-text editor an optional
CanvasAdapter rather than the product foundation.

AI must always operate on explicit user context and create reviewable,
undoable ChangeSets. Stream proposed output without silently mutating user
content. Include accept, reject, revise, cancel, and undo behaviors.

Persist panel state, current context, drafts, layout mode, and drawer width.
Save locally first, synchronize in the background, handle offline queues, and
show conflicts/recovery without data loss.

Use English (US) defaults and a provider-neutral configuration focused on
OpenAI, Anthropic, Google, and compatible custom endpoints. Build a visible
Data & Trust center for storage, sync, privacy, backups, export, recovery, and
AI data-sharing controls.

Use original design tokens and copy. Prioritize calm density, clear hierarchy,
accessible keyboard behavior, progressive disclosure, and restrained motion.
```
