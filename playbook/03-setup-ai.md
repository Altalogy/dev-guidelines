# 3. Set up AI

**Goal:** make Claude Code productive in the new repo, **and compile the relevant guidelines into the project** so we can stop looking back at the dev-guidelines repo for day-to-day work.

## Ask the user

- Do you have an `AGENTS.md` from a previous project to start from?
- Will designers also run Claude Code locally? (affects setup notes you'll add)
- Anything project-specific Claude should know (animations, design system, content rules)?

## Decide together

- What goes in `AGENTS.md` vs `guidelines.md`?
  - **`AGENTS.md`** — concise (~1 page): stack, structure, conventions, project rules.
  - **`guidelines.md`** *(optional)* — longer-form material (animation conventions, design system token table, content authoring rules). Linked from `AGENTS.md` via `@guidelines.md` so Claude picks it up.

## Actions

**Dev:**

1. WebFetch the AGENTS template (`templates/AGENTS.md` in the guidelines repo — use the URL pattern from the kickoff prompt) and save it to the new project's root as `AGENTS.md`.
2. Adapt it: stack versions, project structure, design tokens, conventions. Strip sections that don't apply.
3. If the project has substantial extra rules, create `guidelines.md` at root and reference it from `AGENTS.md` via `@guidelines.md`.
4. Create `CLAUDE.md` at root with a single line: `@AGENTS.md`.
5. Add a `## Stack` section to the new project's `README.md` (using the choice from step 1).
6. Verify: ask Claude *"what stack does this project use?"* — it should answer from `AGENTS.md`.

**Designer:** ask Claude to do all of the above. Then read the resulting `AGENTS.md` — make sure it describes the project in plain English. If anything is wrong or confusing, ask Claude to fix it.

## External actions

None at this step.

## Output

In the new project's root:

- `AGENTS.md` — project-specific Claude rules
- `CLAUDE.md` — one line pointing at `AGENTS.md`
- `README.md` with a `## Stack` section
- *(optional)* `guidelines.md` — longer-form rules linked from `AGENTS.md`

## Compile into the project

This step **is** the main compile step. After it, Claude should be able to work on the project without fetching from the guidelines repo again.

Pull from the guidelines into the new project as you go:

- Stack notes (step 1)
- `/review` checklist (already inside the AGENTS template — keep it, adapt the framework-specific rows)
- Any cross-project rules you want enforced (designer-collab notes, animation conventions, content authoring rules)

Next: [04-design-handoff.md](04-design-handoff.md).
