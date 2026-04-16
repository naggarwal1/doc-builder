---
name: doc-builder
description: Turn rough content into a clean, branded, responsive interactive HTML document. Trigger on "interactive doc", "HTML doc", "turn this into a doc", "make this look good", "style this", or when the user wants a document output instead of a PDF. Covers pitch decks, investor updates, sales proposals, one-pagers, articles, memos, strategy docs. Output is a single self-contained HTML file with TOC, collapsibles, slide nav for decks, and paged layouts for proposals. Works on mobile and prints cleanly.
---

# Doc Builder

Turn unstructured content into a clean, branded, responsive **interactive HTML document**.

## When to use this skill

The user has something to say (a rough draft, an outline, bullet points, a memo-in-their-head) and wants a finished document. They may mention "interactive doc," "interactive HTML doc," "HTML doc," or no format at all. Common triggers:

- "Turn this into an interactive doc"
- "Make this an interactive HTML doc"
- "Turn this into an investor update"
- "Write me a board memo based on these notes"
- "Make this pitch proposal look good"
- "I need a one-pager for [thing]"
- "Here's my draft, can you style it"
- "Produce an HTML doc for this"

Use Doc Builder instead of writing a Word doc, Markdown file, or static HTML page when the user wants something that actually *responds* to the reader: a doc with a table of contents that jumps to sections, collapsibles for detail, slide-by-slide navigation for decks, paged layouts for proposals. The output is called an **interactive HTML doc** because the distinction matters. A static PDF is a sheet of paper in digital form. An interactive HTML doc adapts to the device, lets the reader navigate, and carries structure the reader can act on.

## What the output looks like

A single self-contained HTML file. One file, no dependencies (fonts pulled from Google Fonts CDN, everything else inlined). Opens in any modern browser. Renders well from 320px phones to large desktops. Prints cleanly on paper via an included print stylesheet.

The file has a sensible filename based on the doc title or doc type.

## Process

### 0. Quick intake (before generating)

Before you generate anything, do a quick intake so the output matches what the user actually wants. This is the difference between "one-shot guess" and "informed generation". It makes the skill feel like a partner, not a generator.

**Skip the intake entirely if the user's opening message already contains:**
- A clear doc type (named explicitly, or unambiguous from context)
- A brand config, OR an explicit statement that defaults are fine
- Enough content to generate confidently

**Otherwise, ask ONE message with up to three bundled questions**. Only for what's actually missing. Infer everything else you can from the input. Phrase the questions briefly and in plain language. Do not drip-feed questions one at a time.

**Before asking anything else, do a platform-intent check.** If the user mentions posting to a platform that has its own native editor (LinkedIn articles, Twitter/X, Medium, Substack's web editor), an HTML file is usually the wrong deliverable. Those platforms re-render content in their own format, so you'd just be producing a file the user will paste away from. When you see this signal, surface the mismatch directly:

Example: "Heads up. If this is going into LinkedIn's article editor or Medium's editor, you don't really need an HTML file. Want me to give you the formatted text to paste in instead? Or is the HTML for something else (like hosting on your own site and linking to it from LinkedIn)?"

Only proceed to generate HTML if the user confirms a self-hosted destination (their own site, a shareable link, a Substack custom domain, etc.). If they really just want LinkedIn-ready text, hand them that instead. Structured prose with the formatting LinkedIn supports (bolds, line breaks, lists, no inline styles). No template needed.

The three questions, in priority order:

**1. Doc type (ask if ambiguous)**
Example: "Quick check. Is this meant to be an investor update, a board memo, a general strategy doc, or something else?"
If you can reasonably infer from content (e.g., traction metrics → investor update; scope + pricing → sales proposal), propose the inference instead: "Looks like a board memo to me. Is that right?"

**2. Brand (ask if no config provided)**
Example: "Any brand colors / fonts to use? Or neutral defaults (warm off-white background, near-black ink, orange accent)?"
If the user said "use our brand" without specifying, ask for the actual config values.

**3. Content scope (ask if the input is sparse or overly dense)**
Example: "The notes are brief. Should I expand each section, or keep the doc tight and literal to what you wrote?"
Or if too dense: "This is ~3000 words. Should I keep everything, or edit down to the essentials?"

**Always offer an escape hatch.** End the intake message with something like: "Or say 'just go' and I'll use sensible defaults."

**Once you have the answers (or an escape hatch), proceed to Step 0.5 for any type-specific questions, then to Step 1.**

### 0.5. Type-specific intake (after doc type is locked in)

Each doc type has its own required info. Specifics that are mandatory to produce a credible output. Once you know which template you're using, scan the user's input for the type's required fields. Ask for anything missing, bundled into ONE message. Skip this step entirely if the input already has everything.

Same rules as Step 0: one bundled message, plain language, escape hatch ("or say 'just go' and I'll use defaults / placeholders where needed"). Never loop.

**Field requirements by template:**

| Template | Required (ask if missing) | Optional (default or leave blank) |
| --- | --- | --- |
| **investor-update** | Period covered (Q1 2026, March 2026, etc.), company name, at least 3 key metrics with values | Distribution list, specific asks to investors, logo |
| **sales-proposal** | Client name, firm/proposer name, at least one scope phase with deliverables, at least one pricing line, date | Proposal ID / reference number, payment terms (default: 50% upfront, net 30 on milestones), signatory name, validity window (default: 30 days) |
| **pitch-deck** | Company name, one-line tagline, target audience (seed / Series A / late-stage / partners / customers), fundraise amount (if fundraising deck) | Team bios, traction metrics, competitor context, contact info |
| **one-pager** | Product/subject name, audience (internal / customer-facing / partner / investor), CTA text and destination | Deadline, contact name, hero facts beyond the three in the template |
| **article** | Category tag (e.g. "Essay", "Founder Journal"), byline name, self-hosted destination confirmed | Read time estimate (can auto-compute from word count), cover image reference |
| **generic** | Title, author name | Audience tag, eyebrow text, kicker content |

**Examples:**

Input (after universal intake): "Make this a sales proposal for a 3-month engagement, $75K."
Type-specific intake runs: "Before I write it. Who's the client, who's it from (firm name), and what should I use as the date? Or say 'just go' and I'll use placeholders you can fill in."

Input: "Make this a Q2 investor update for Northbeam. Metrics: ARR $920K, 47 customers, 124% NRR. Brand defaults."
Type-specific intake skips entirely. Period, company, and metrics are all present.

Input: "Make this a pitch deck for Series A."
Type-specific intake runs: "Quick. What's the company name, the one-line tagline, and the fundraise amount? Or 'just go' for placeholders."

**When to skip this step even if fields are missing:**
- User says "just go" or equivalent at any point
- User explicitly asks for a template/placeholder version ("give me the structure, I'll fill it in")
- The doc type is `generic` and the input has enough content to infer a title

**Handling "just go" / placeholder requests:**
Insert clearly-marked placeholders for required fields (e.g., `[CLIENT NAME]`, `[COMPANY NAME]`, `[FUNDRAISE AMOUNT]`). Use bracketed caps so the user can find and replace them easily. Note which placeholders you inserted in your response.

Do not loop back for more clarifying questions. Generate the doc with what you have.

**Examples of when to skip intake:**

Input: "Turn this into a Q1 investor update using our brand (primary #0a2540, accent #00d4aa, Inter + Georgia). [notes]"
→ Skip intake. Everything needed is present.

Input: "Make this a sales proposal for Acme Corp. $50K engagement, 3 phases, terms attached."
→ Skip intake for doc type and content scope. Ask only about brand: "Brand colors / fonts, or neutral defaults?"

Input: "Here's my draft, can you style it? [paste]"
→ Run full intake. Nothing is specified. Ask all three.

Input: "Turn this into a doc, just go."
→ Skip intake entirely. Infer doc type from content, use defaults for everything else.

### 1. Read the content and classify it

Look at what the user gave you. Identify:
- **Doc type**. Investor update, board memo, strategy doc, sales proposal, product brief, one-pager, or generic. If the user told you the doc type, use that. Otherwise infer from the content itself (an "investor update" has traction metrics and quarterly themes; a "sales proposal" has a client name and a scope; a "board memo" has an agenda and recommendations). When uncertain, default to `generic`.
- **Approximate length**. Short (under 400 words), medium (400-1500), or long (1500+). This affects whether you include a TOC or add collapsibles.
- **Natural structure**. Headings, lists, quotes, tables, sections already in the content. Preserve what's there, add structure where it's missing.

### 2. Pick the matching template

Templates live in `templates/`:
- `templates/generic.html`. Use this as default. Works for strategy docs, memos, essays, any document where no specific template applies.
- `templates/investor-update.html`. Traction-forward layout with metrics block near top.
- `templates/one-pager.html`. Tight, single-scroll layout with strong hero and CTA block. Good for product briefs, partnership overviews, role briefs.
- `templates/pitch-deck.html`. Scrollable vertical deck. Each slide is a full-viewport section with big type and slide numbers. Use for generating a pitch deck from text (not for converting an existing .pptx. That's the Deck Converter skill).

  **Critical preservation rules for pitch-deck output:**
  The pitch-deck template has four MANDATORY HTML chrome blocks in the `<body>` BEFORE the `<!-- SLIDES -->` placeholder: (1) the hamburger menu toggle button, (2) the slide navigation sidebar + backdrop, (3) the left/right arrow navigation buttons, (4) the deck header with the slide counter span. These are marked "MANDATORY 1/4", "MANDATORY 2/4", etc. in the template. **Copy all four verbatim into every generated deck.** They are not decoration. Together with the `<script>` block at the bottom, they power the hamburger menu, keyboard navigation, arrow buttons, and slide counter. If you generate the deck without these HTML elements, the deck loses all interactivity even though the CSS and JS are still intact.

  **Slide structure for pitch decks:** Typically generate 8-10 slides in this order: hero, problem, solution, how it works, why now (optional), traction, team, ask, contact. The contact slide should be a SEPARATE, distinct slide (a final `<section class="slide cta">` with a "Let's talk." type headline and contact info). Do NOT fold contact into the ask slide.

  **Metric class rule for pitch decks:** Any number you want to animate on scroll-in must be wrapped in a `<div class="deck-metric-value">` element. This includes team size, growth multiples, ARR, churn rate, percentages, any numeric highlight on any slide. Use the `.deck-metrics` grid pattern for grouped metrics. For a standalone emphasized number on a non-metrics slide, you can still use a plain `.deck-metric-value` wrapper. The animation JS only targets this class. Plain text numbers will not animate.
- `templates/sales-proposal.html`. Client-facing proposal with scope / pricing / timeline / signature sections. **Signature column convention (always follow, do not flip):** client goes on the LEFT with a blank signature line for them to sign; proposer goes on the RIGHT pre-filled with the signatory's printed name, and a caption of the form `[Title], [Firm] · [Date of proposal]`.
- `templates/article.html`. Long-form reading-optimized layout. Drop cap, generous line-height, pull quotes, no TOC or metrics. **For self-hosted content only**. Content that will live at a URL the user controls (personal site, Substack, company blog, shareable link). Not for content that will be pasted into a platform's native editor (LinkedIn articles, Twitter, Medium's default editor). Those platforms re-render content in their own format, so an HTML file is the wrong deliverable.

Each template is an HTML skeleton with placeholder zones marked by HTML comments like `<!-- TITLE -->`, `<!-- DECK -->`, `<!-- CONTENT -->`, `<!-- KICKER -->`.

Read the template that matches the doc type. If no specific template matches, use `generic.html`.

### Paged vs. Pageless layouts

Not every doc should read as one long scroll. Templates fall into two layout modes:

**Pageless (continuous scroll):**
- `generic`, `article`, `investor-update`, `one-pager`
- Designed to be read top-to-bottom in one flow
- No hard page breaks in the UI
- Reader scrolls naturally through the content

**Paged (distinct page/slide feel):**
- `sales-proposal`. Cover page + distinct section pages, each section feels like its own page
- `pitch-deck`. Slide-by-slide with keyboard navigation, slide counter, scroll-snap
- Each "page" is ≥100vh and has its own visual identity
- Print stylesheet uses real `page-break-after` so the doc prints as multiple pages, not one wall of text

This distinction matters because traditional proposals and decks are paged in people's mental model. A sales proposal that reads like a long scroll feels informal or incomplete; a pitch deck that reads like a blog post doesn't feel like a deck. The paged templates reinforce the reader's expectation of the format.

If a user asks for a paged feel on a typically-pageless doc (e.g., "I want the strategy doc to feel paged, with a cover"), you can apply the same `.page` / `.page-num` / page-break pattern from the `sales-proposal` template to the `generic` template. Note this is an explicit user request, not the default.

### How to decide between templates

- User asks for investor/board update with traction numbers → `investor-update`
- User asks for a one-pager, product brief, partnership overview → `one-pager`
- User asks for a pitch deck, slide deck, presentation (from text input, not a file) → `pitch-deck`
- User asks for a proposal, SOW, consulting proposal, engagement brief → `sales-proposal`
- User asks for a blog post, essay, article, longform, or is writing something editorial and reading-optimized → `article`
- Anything else (strategy doc, memo, white paper, general-purpose) → `generic`

### 3. Apply brand configuration

If the user provided a brand config (either inline as description or as JSON), merge it into the template's `:root` CSS variables block. Look for this block at the top of the template's style section:

```css
:root {
  --ink: #1a1a1a;
  --bg: #faf8f3;
  --accent: #ff5722;
  --heading-font: 'Inter', sans-serif;
  --body-font: 'Source Serif 4', Georgia, serif;
}
```

Replace the values with the user's brand config. If the config specifies Google Fonts that aren't already loaded in the template, add them to the `@import` statement at the top of the `<style>` block.

If no brand config is provided, the template's built-in defaults are already sensible. Leave them.

### 4. Fill the content

Replace placeholder zones in the template with the user's content, structured as semantic HTML:
- Top-level title goes in `<!-- TITLE -->`
- Deck/subtitle (one sentence summary) goes in `<!-- DECK -->`
- Section headings become `<h2>` with an optional number prefix
- Body paragraphs become `<p>`
- Bulleted lists become `<ul>` / `<li>`
- Numbered lists become `<ol>` / `<li>`
- Pull quotes or emphasized claims become `<blockquote>`
- Strong claims can be wrapped in `<strong>`
- Data points or metrics should use the `.metrics` block pattern if the template has one

For unstructured prose, decide on section breaks yourself. Use the doc type to guide this. An investor update typically has sections like Highlights / Metrics / Product / Team / Ask; a board memo typically has Summary / Context / Recommendation / Next Steps.

**Aim for 4-6 sections, not 8+.** More sections feels over-structured and fragments the reader's attention. When in doubt, merge adjacent thoughts into one longer section rather than splitting them into separate ones. A 1500-word strategy memo reads better with 5 substantial sections than with 8 thin ones.

### 5. Add interactivity based on length

Use the length classification from step 1:
- **Short (under 400 words)**. **No TOC even if there are multiple sections.** No collapsibles. Keep it flat. The reader can scan the whole doc in one scroll — a TOC is visual noise at this length, not a navigation aid.
- **Medium (400-1500 words)**. Add TOC only if there are 3+ `<h2>` sections AND the doc is over 400 words. No collapsibles.
- **Long (1500+ words)**. Add TOC. Wrap sub-sections in `<details>` / `<summary>` if any section runs long. Add a "back to top" link after major sections.

**Word count comes first.** Before applying the "3+ sections" rule, verify the doc is actually long enough to benefit from navigation. A 200-word memo with four crisp sections does not need a TOC — the whole thing fits in one viewport.

The TOC markup is a `<nav class="toc">` containing an `<ol>` of links to each `<h2>` id. See `styles/components.css` for the styling.

Collapsibles use plain `<details>` / `<summary>`. No JavaScript needed.

### 6. Finalize metadata and output

Set the `<title>` tag in `<head>` to the doc's title. Update the `<meta>` description if the user gave you a summary. Save the file with a sensible name based on the title (kebab-case, no spaces).

Present the final HTML file to the user with its location.

## Interactive features baked into templates

Every template (except pitch-deck, which has its own slide nav chrome) includes a small set of interactive behaviors via inlined JS. These are client-side only, no backend, no tracking, no external calls. Preserve them verbatim in outputs. The top of each template has a "DO NOT REMOVE" comment on the `<script>` block.

**Reading progress bar.** A 3px strip fixed to the top of the viewport that fills with the accent color as the reader scrolls. Works across all scrolling templates. Hidden in print.

**Active table-of-contents highlighting.** If the output has a TOC (`<nav class="toc">`), the TOC link for the section currently on screen gets a `.active` class (accent color, small arrow indicator). Uses IntersectionObserver. Makes the TOC feel responsive rather than static.

**Animated metric counters.** Any element with `.metric-value` (investor-update) or `.deck-metric-value` (pitch-deck) animates from zero to the final value when it scrolls into view. Preserves the original string exactly, so formatted values like `$340K`, `124%`, `3.7x`, `$48M`, `78,432` all work. Uses ease-out cubic over ~900ms.

These three features are the skill's answer to "interactive HTML doc" — navigation that responds, TOCs that track the reader, metrics that come alive. They do NOT include tracking, analytics, Q&A, live updates, or reader-adaptive content (those belong to a platform product, not a free skill). Do not add those.

## Quality bar

The output should meet these standards:

- **Valid HTML5.** Proper doctype, charset, viewport meta tag. No unclosed tags, no broken attributes.
- **Semantic.** Use `<article>`, `<section>`, `<nav>` where appropriate. Not every container is a `<div>`.
- **Responsive.** Renders well from 320px up. The CSS uses relative units for font sizes and includes a mobile breakpoint.
- **Accessible.** Proper heading hierarchy (one `<h1>`, then `<h2>`s, then `<h3>`s. Don't skip levels). Contrast ratios at or above 4.5:1 for body text. Focus states on interactive elements.
- **Print-friendly.** The included `@media print` block adjusts fonts, hides navigation, and prevents awkward page breaks.
- **Looks professional.** Typography, spacing, and color work together. A reader should think "this came from a company that knows what it's doing," not "this came from a quick AI tool."

## Brand config format

Users can specify brand config in two ways:

**Inline description:**
> "Use primary color #0066ff, accent color #ff9900, heading font Inter, body font Georgia."

**JSON:**
```json
{
  "primary": "#0066ff",
  "accent": "#ff9900",
  "headingFont": "Inter",
  "bodyFont": "Georgia",
  "logoUrl": "https://example.com/logo.png"
}
```

Accept both. If JSON is provided, parse it. If inline description, extract the values.

## Files in this skill

- `SKILL.md`. This file
- `templates/generic.html`. Default fallback template
- `templates/investor-update.html`. Investor update layout with metrics block
- `templates/one-pager.html`. Tight single-scroll layout with hero + CTA
- `templates/pitch-deck.html`. Scrollable vertical deck with slide counter and keyboard navigation (paged)
- `templates/sales-proposal.html`. Multi-page proposal with cover + distinct section pages (paged)
- `templates/article.html`. Reading-optimized longform layout
- `styles/base.css`. Typography, spacing, color foundation
- `styles/brand-defaults.css`. Default CSS variables (ink, bg, accent, fonts)
- `styles/components.css`. TOC, collapsibles, pull quotes, metrics blocks
- `styles/print.css`. `@media print` rules
- `examples/example-pitch-deck.html`. Rendered reference output (9-slide Series A deck)
- `examples/example-investor-update.html`. Rendered reference output (Q1 SaaS update with metrics)
- `examples/example-one-pager.html`. Rendered reference output (founding-engineer role brief)
- `examples/example-sales-proposal.html`. Rendered reference output (multi-page proposal)
- `README.md`. User-facing documentation

The styles are designed to be embedded directly into templates' `<style>` blocks rather than linked as separate files. This keeps the output a single self-contained file. Templates already have inlined style blocks. Use the separate `styles/*.css` files as reference when you need to extend or tweak them, not as runtime dependencies.

## What this skill does not do

- Does not generate images, charts, or diagrams. If the content references these, leave placeholders and note them.
- Does not replicate PDF's pixel-perfect rendering. That is not the goal. Paged templates (sales-proposal, pitch-deck) give a paged feel but HTML is fundamentally responsive, not fixed-layout.
- Does not hit external APIs. Everything is local generation.
- Does not produce LinkedIn articles, Medium posts, or other content meant for a platform's native editor. See the platform-intent check in Step 0 intake.

If a user needs something outside this scope, note the limitation and suggest the appropriate alternative tool.

## Example invocation

**User input:**
> "Here are my Q1 notes, can you turn this into an investor update? Keep our brand: primary #2d3436, accent #00b894, heading Inter, body Georgia."
>
> [paste of rough notes]

**Skill behavior:**
1. Classify as `investor-update`.
2. Load `templates/investor-update.html`.
3. Apply brand config to `:root` CSS variables.
4. Structure the notes into standard sections (Highlights, Metrics, Product, Team, Ask).
5. Medium length → add TOC for navigation.
6. Output: `q1-2026-investor-update.html`.
