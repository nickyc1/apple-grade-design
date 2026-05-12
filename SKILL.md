---
name: apple-grade-design
description: Apple-grade UI design workflow that stacks Stitch MCP for layouts, Nano Banana 2 MCP for visuals, and UI/UX Pro Max for critique. Use when asked to design, redesign, or polish a web page section that should feel handcrafted. Triggers on "apple-grade design", "jony ive design", "redesign this page", "make this section pop", or any landing-page rebuild work.
---

# Apple-Grade Design Workflow

You are producing design that feels handcrafted by someone who cares. The stack is three tools in one loop.

## Tools

1. **Stitch MCP** (`stitch` server)
   - `build_site` — generate full layouts from a brief
   - `get_screen_code` — fetch HTML for a generated screen
   - `get_screen_image` — fetch a screenshot of a generated screen

2. **Nano Banana 2 MCP** (`nano-banana-2` server)
   - `generate_image` — text-to-image with Gemini Flash Image
   - `edit_image` — modify an existing image file
   - `continue_editing` — iterate on last image

3. **UI/UX Pro Max skill** (`ui-ux-pro-max`)
   - Invoke as a Skill to critique layouts and produce design system output

## Loop

For each section you design:

### Step 1 — Brief
Write a 5-line brief (template in `references/brief-template.md`):
- **Goal**: what this section must do in one sentence
- **Audience**: the named ICP
- **Anchor copy**: the headline or key line, verbatim
- **Mood**: three adjectives
- **Constraints**: any real data, real imagery, or hard rules

### Step 2 — Layout
Call Stitch `build_site` with the brief plus the design tokens from `design-tokens.json`. Pull the generated screen with `get_screen_code`.

### Step 3 — Visuals
For every non-UI asset in the layout (hero texture, persona photo, product preview, illustration), call Nano Banana `generate_image` with:
- Style guidance referencing the design tokens
- Explicit "no generic stock photo, no corporate stockiness, no AI-looking composition"
- Aspect ratio matching the layout slot

Save outputs to a local `mocks/` directory (git-ignored).

### Step 4 — Code
Translate the Stitch layout to the target stack (React + Tailwind + shadcn is a strong default). Keep to the design tokens exactly. No improvisation on color or spacing.

### Step 5 — Critique
Invoke the `ui-ux-pro-max` skill with the finished section. Apply every P0 and P1 fix. P2 goes on the backlog. The full pre-ship checklist is in `references/critique-checklist.md`.

Critique must cover:
- Typography rhythm and hierarchy
- Spacing grid compliance (8px)
- Color contrast (WCAG AA minimum)
- Responsive behavior at 375, 768, 1280, 1920
- Hover, focus, active states
- Empty states and loading states where applicable
- The swap test: could you swap your product name for a competitor and have the copy still work? It should FAIL the swap.

### Step 6 — Ship
Commit the section with a message that states the brief in one line.

## Design tokens

Always reference `design-tokens.json`. Never invent new colors, type scale, or spacing values in section code. If a token is missing, add it to the file and then use it.

The included `design-tokens.json` is an example. Replace it with your own brand tokens before running the loop. The structure (brand, colors, typography, spacing, radius, shadow, motion, layout) is the contract — keep that shape so the rest of the skill works.

## Voice rules (copy-side, not design)

Copy should pass voice review before ship. See `references/voice-rules.md` for the rules. The short version:

- No em dashes for dramatic effect
- No "it's not just X, it's Y" / "here's the thing" / "the truth is"
- No staccato phrasing ("No fluff. No filler.")
- Natural cadence, founder voice, confident without being cheesy
- If a line could come from a generic SaaS template, rewrite until it sounds like a real person

## Anti-patterns

If your output drifts toward any of these, restart the section:

- Generic gradient hero with a rocket
- Stock product mockup on a tilted laptop
- Hexagon grid background
- Glowing underline on the headline
- "Trusted by the world's most innovative teams"
- Purple/blue gradient everything
- Fake testimonials
- Icons that look AI-generated
