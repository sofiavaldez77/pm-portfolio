# Handoff: Building Case Study 2 (Sofia Valdez UX Portfolio)

This continues a portfolio of standalone, single-file HTML case studies. Case Study 1 (Panda Mobile, `case-study-1-panda-mobile-v2.html`) is done. Read that file end to end before writing anything, it's the canonical style reference, copy its CSS and interactive patterns wholesale rather than rebuilding from scratch.

## Case Study 2 topic

The audience research pivot into international Chinese students at Panda Mobile / Moxee Technologies, which led to pricing and referral strategy work, the "Bye Bye Family Plans" marketing positioning, and broader brand positioning. Case Study 1's closing section ("Other Work") ends by teeing this up directly, so Case 2 should pick up from exactly that point rather than re-introducing the company from scratch.

## Design system (locked, don't redesign)

- Single HTML file: all CSS in one `<style>` block in `<head>`, all JS in one `<script>` block at the end of `<body>`, no external frameworks.
- Fonts: Inter only.
- Colors: `--cream:#faf9f7`, `--cream-2:#f2efe9` (deeper cream, used to tint every other section for separation, and as card/box backgrounds), `--ink:#26221f`, `--ink-soft:#5c554e`, `--rose:#B8737E`, `--rose-deep:#8f4f5a`, `--rose-pale:#f1e2e4`, `--line:#e4ddd3`.
- No em dashes, en dashes, or hyphen-as-punctuation anywhere in copy (compound words like "single-page" are fine).
- Section labels (eyebrows) render larger than the h2 headline beneath them.
- Headlines are literal and plain, understandable with zero context.
- Quotes use a quiet left rose border, never a dark boxed background.
- Big stat callouts get their own visual moment (large number, small label beneath).
- Numbered 01/02/03 sub-blocks break a section into steps, with generous whitespace between them.
- Progressive disclosure: a `<details>` element with a bold pink "+" icon for optional or supporting detail (participant lists, examples, secondary decks), rather than showing everything at once. This was the single most effective tool for controlling density.
- Don't use pink pill/chip styling for anything that isn't actually clickable, it reads as a button and misleads. Reserve pills for real interactive elements (tabs, filters).

## Structural pattern from Case 1

Masthead → opening quote → The Ask → Background Research → Approach → Customer Interviews → Customer Needs Analysis → Competitive Benchmarking → Design Requirements → Results → Other Work.

Every major section is a `<div class="section-label">` + `<h2>` + one or more `<div class="num-block">` beats. A sticky top nav bar (`.toc-topbar`) lists every section as arrow-separated links and highlights (and auto-centers) whichever section is in view via IntersectionObserver. Reuse this nav, just swap the section list.

## Interactive components already built, reuse these

- `.funnel-box` / `.funnel-box.is-scroll` — a fixed 16:9 box that's either a click-through image gallery (click the image or use the arrows) or an internally scrollable tall image with a fading "Scroll ↓" cue. Use for anything document-shaped: flows, landing pages, multi-page decks.
- Lightbox (`#lightbox-overlay`) — the zoom button opens any image full-size; clicking the enlarged image again toggles a true pixel-zoom (scrollable, pannable). Earlier versions just closed on click, that's a regression, don't reintroduce it.
- Tabs + detail explorer pattern (`.theme-tab` / `.decision-tab` / `.lp-tab` + a fixed-height scrollable detail box) — for any set of 3 to 5 categorized options where a reader picks one to see supporting quotes. Used three times in Case 1. Bold only the single most load-bearing phrase per quote, and treat the exact bolded phrase as an editorial judgment call unless you can zoom into the actual source slide image to confirm it.
- Region-highlight overlay (`.decision-hl`) — a tab click can outline a percentage-based region of an adjacent image. Coordinates come from overlaying a pixel grid on the source image (PIL) and reading off approximate percentages, they're estimates, flag them as such.
- Alternating section background bands (`section:nth-of-type(even)::before`, full-bleed via `left:50%; transform:translateX(-50%); width:100vw`) — this is what fixed "it feels like one long wall of text," worth keeping from the first draft rather than waiting for the same complaint again.

## Content principles (hard-won through iteration)

- A recruiter reads top to bottom in 3 to 5 minutes. Every section leads with plain fact, then interpretation.
- Cut ruthlessly, and do a dedicated concision pass after each section is drafted, not just while writing it. Look specifically for: a body sentence that just restates its own heading in different words, a caption that repeats a sentence already stated nearby, and the same stat or fact restated three-plus times without adding anything new each time. These three patterns accounted for nearly all remaining wordiness once the obvious fat was gone.
- Preserve real quotes verbatim. If a quote contains profanity, ask before softening it rather than deciding unilaterally.
- This case study still needs a Reflection section, that was never built for Case 1 either. Worth asking Sofia if she wants it in Case 2, Case 1, or both.

## How Sofia likes to work

- Iterative, section by section. Show one section, wait for feedback, then move to the next, don't dump the whole thing at once.
- Never silently overwrite a big chunk. If a change is significant and wasn't explicitly requested, ask first.
- Validate every edit: extract the `<script>` block and run `node --check` on it, and check every image `src=` actually exists on disk, every single round. Skipping this risks shipping broken JS or a 404'd image silently.
- She edits copy word by word across many turns and often already has the exact replacement phrasing in mind, apply it as given rather than pushing back on small stylistic calls.
- After a batch of edits, present the file once and stop. Don't recap what changed at length, she can see it herself.

## Image sourcing constraint

Canva's MCP tools can read slide text, quotes, and thumbnails directly, and can even generate an export download URL, but that URL can't actually be fetched from this environment (blocked as too-long or 403). The only pipeline that works: Sofia exports the image herself from Canva and drops it into the case study's folder, then tells you it's there. Don't burn turns trying to work around the fetch block.

## Before starting Case 2

1. Ask for the Canva deck (or wherever the Case 2 source material lives) and confirm the folder it should be built in.
2. Skim `case-study-1-panda-mobile-v2.html` in full, rendered structure and CSS/JS, before writing anything.
3. Confirm the section outline with Sofia before building. The likely shape, based on Case 1's closing bridge: what the interviews with international Chinese students found → how that reshaped pricing and referral strategy → the "Bye Bye Family Plans" positioning → the broader brand positioning outcome.
