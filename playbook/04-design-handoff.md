# 4. Design handoff

**Goal:** turn Figma designs into specs Claude Code can implement reliably.

## To be filled in

Topics to cover:

- **Figma → spec workflow** — what to extract before coding (tokens, components, layouts)
- **Writing specs AI can execute** — SDD tiers (1 = tight spec, 2 = loose spec, 3 = chat-and-iterate)
- **Figma MCP** — using `get_design_context` and friends directly from Claude Code
- **Naming consistency** — components and sections that match Figma frames
- **Responsive breakpoints** — how to express them in a spec
- **Asset export** — SVGs, raster, video conventions

## Open questions

- Do we standardize on a single Figma → code workflow, or document multiple per project type?
- Where do specs live in the repo? (`docs/specs/<feature>.md` like the AGENTS template suggests?)

Next: [05-build-feature.md](05-build-feature.md).
