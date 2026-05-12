# Pre-ship critique checklist

Run every section through this before commit. Invoke `ui-ux-pro-max` skill for the deeper audit. P0 must pass. P1 must pass unless there's a stated reason. P2 goes to the backlog.

## P0 — ship blockers

- [ ] Section passes the **swap test**: swap your product name for a competitor or adjacent tool. Does the copy still make sense? It should FAIL the swap. If it passes, the section is too generic — rewrite.
- [ ] Copy reads in founder voice (no "here's the thing", no "it's not just X, it's Y", no em dashes for effect, no staccato "No fluff. No filler.")
- [ ] No placeholder testimonials, no fake quotes, no "trusted by world-class teams"
- [ ] Colors come from `design-tokens.json` only. No improvised hex codes.
- [ ] Spacing is 8px grid-compliant
- [ ] No copy that's trying too hard (military / spy / Bond clichés: CLEARANCE, WAR ROOM, INITIALIZE, INTEL briefing). Unless the brand is genuinely in that space, cut it.
- [ ] Real data where stated. If the section shows numbers or quotes, those numbers and quotes are real and sourced — or the section is clearly labeled as illustrative.

## P1 — should pass

- [ ] Typography rhythm is deliberate (no more than 4 sizes in one section)
- [ ] Hierarchy scans in 3 seconds at full-width desktop
- [ ] WCAG AA contrast on all text pairs
- [ ] Hover + focus + active states on every interactive element
- [ ] Responsive at 375 / 768 / 1280 / 1920 without horizontal scroll
- [ ] Cards stack cleanly on mobile without information loss
- [ ] Animations respect `prefers-reduced-motion`
- [ ] Images have alt text; decorative images have `alt=""`
- [ ] Headlines read aloud without making the reader wince

## P2 — polish backlog

- [ ] Entrance animations tuned to feel deliberate, not flashy
- [ ] Type pairing tested at body-sm on low-DPI displays
- [ ] Empty states designed if the section is interactive
- [ ] Performance: LCP < 2.5s, CLS < 0.1
- [ ] SEO: one h1 per page, meta description matches hero subhead

## 5-second test (run on every section)

Show the section to someone cold. Ask:

1. What does this product do?
2. Who is it for?
3. Why would I care?

They should answer all three in 5 seconds. If not, rewrite.

## Founder voice test

Read every line out loud. Any line that sounds like marketing copy instead of a real person talking? Cut or rewrite.
