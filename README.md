# apple-grade-design

A [Claude Code](https://claude.com/claude-code) skill that stacks three design tools into one Apple-grade design workflow.

You design page sections like a small in-house team would: a brief, a layout, real visuals, code, critique, ship. The three tools handle the parts a model does well, and the skill is the loop that keeps them coherent.

## The stack

1. **[Stitch MCP](https://github.com/_davideast/stitch-mcp)** — generates full-screen mockups from natural language. Use for section layouts before JSX.
2. **[Nano Banana 2 MCP](https://www.npmjs.com/package/nano-banana-2-mcp)** — generates real product visuals from text or reference images. Use for hero textures, persona photos, product previews, illustrations.
3. **[UI/UX Pro Max](https://github.com/Skyless-Network/ui-ux-pro-max)** skill — design critique and design-system output. 67 UI styles, 161 palettes, 57 font pairings, 99 UX guidelines. Use as the pre-ship quality gate.

The skill ties them together with three things they don't share by default:

- A **shared design-tokens.json** so all three tools produce coherent output
- A **5-line brief template** so each section starts with the same shape of intent
- A **pre-ship critique checklist** so output passes the same bar every time

## Why this exists

Most AI-design output is either too generic to ship (rocket-gradient hero, "trusted by the world's most innovative teams") or too unstructured to scale (every section a one-off, no design system, no design tokens). This skill produces sections that pass the swap test — swap your product name for a competitor's and the copy should NOT still work. If it does, the section isn't real yet.

The output looks handcrafted because it is. The skill just compresses the loop.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- Three MCP servers / skills configured (see Install below)
- API keys for Stitch and Nano Banana (Gemini)

## Install

```bash
# Clone the skill
git clone https://github.com/nickyc1/apple-grade-design.git ~/.claude/skills/apple-grade-design

# Add the two MCP servers
claude mcp add-json nano-banana-2 '{
  "command": "npx",
  "args": ["-y", "nano-banana-2-mcp"],
  "env": {"GEMINI_API_KEY": "your_key_here"}
}'

claude mcp add-json stitch '{
  "command": "npx",
  "args": ["@_davideast/stitch-mcp", "proxy"],
  "env": {"STITCH_API_KEY": "your_key_here"}
}'

# Install the UI/UX Pro Max skill
git clone https://github.com/Skyless-Network/ui-ux-pro-max.git ~/.claude/skills/ui-ux-pro-max
```

Restart Claude Code. The skill is available.

## Usage

In Claude Code:

```
Use apple-grade-design to redesign the hero section for [product].
Brief:
  Goal: [one sentence]
  Audience: [named ICP]
  Anchor copy: [verbatim headline]
  Mood: [three adjectives]
  Constraints: [hard rules]
```

The skill will:

1. Use your brief plus `design-tokens.json` as the input to Stitch
2. Generate the layout, fetch the HTML
3. Generate any required visuals via Nano Banana
4. Translate to your target stack (React + Tailwind + shadcn is a good default)
5. Invoke UI/UX Pro Max as the critique gate
6. Apply P0/P1 fixes, ship the section

## Design tokens

The included `design-tokens.json` is an example. Replace it with your own brand tokens before running the workflow. Keep the structure (brand, colors, typography, spacing, radius, shadow, motion, layout) so the rest of the skill works.

## Repo structure

```
apple-grade-design/
├── SKILL.md                         # the skill prompt Claude Code reads
├── design-tokens.json               # example tokens — replace with your brand
├── references/
│   ├── brief-template.md           # the 5-line brief format
│   ├── critique-checklist.md       # pre-ship quality gate
│   └── voice-rules.md              # copy voice rules
└── README.md
```

## Why three tools, not one

Each tool does one thing well:

- **Stitch** ships strong layouts when you give it a clear brief. Bad at on-brand specificity.
- **Nano Banana** generates real-looking product/persona imagery. Bad at layout.
- **UI/UX Pro Max** has the world's most opinionated design critique catalog. Bad at production.

The skill stops you from asking any one tool to do the others' job. That's where the AI-design output usually breaks.

## License

MIT — see [LICENSE](LICENSE).

Built by [Nick Christensen](https://github.com/nickyc1).
