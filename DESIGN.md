# Fuji-Mayon Landing Page — Design Decisions

## Goal
Increase **trust** and **application conversion** from Filipino caregivers who want to work in Japan.

---

## 1. Mobile-first layout
- **Base styles target small screens** (single column, touch-friendly targets). Breakpoints at 640px and 900px add columns and spacing.
- **Why:** Many applicants will first see the site on a phone. Mobile-first avoids cramped, unreadable layouts and ensures CTAs are easy to tap (min 48px height).
- **Implementation:** All section and grid rules are written for one column first; `@media (min-width: 640px)` and `900px` then add multi-column grids and wider containers.

---

## 2. Clean, modern UI
- **Limited palette:** Primary blue (`#1a6fb4`), dark blue for contrast, muted grays for text hierarchy, light gray backgrounds for section alternation. No decorative gradients or heavy shadows.
- **Consistent radius (8px)** and 1px borders. Trust is conveyed by clarity and consistency, not visual flair.
- **Why:** A clean UI reads as professional and legitimate—important for an audience wary of scams. “Modern” here means readable, spacious, and current (e.g. 2020s conventions) without trend-heavy effects.

---

## 3. Clear hierarchy
- **One H1 per page** in the hero: “Work in Japan as a caregiver. Safe, legal, no placement fee.” It states audience, benefit, and key differentiator.
- **Sections use H2** for the main heading; subsections use H3. No skipped levels.
- **Visual hierarchy:** Section titles use larger size and weight; leads use muted color; body text and notes are smaller/lighter. Cards use a clear label → value → note pattern.
- **Why:** Clear hierarchy lets users scan quickly (especially on mobile) and understand what each block is for, which supports both trust and conversion.

---

## 4. Strong CTA
- **Primary CTA:** “Apply free — we’ll contact you” in the hero. Repeated as “Open application form” before the form and as “Start application — free” after the process section.
- **Secondary CTA:** “Check eligibility” / “Check if I qualify” for users who aren’t ready to apply. “I qualify — apply free” and “Apply free” appear mid-page.
- **Placement:** Hero (above fold), after Eligibility, after Salary & life, after Process, and a final CTA section dedicated to the form.
- **Buttons:** Primary = solid blue; secondary = outline/ghost. Large tap targets (48px min, 56px for hero). `btn--block` used for one full-width CTA on small screens.
- **Why:** Multiple, clear CTAs reduce friction for different mindsets (ready vs. still checking) and give a clear next step at every stage of the scroll.

---

## 5. Large spacing
- **Design tokens:** `--space-xs` (8px) through `--space-3xl` (80px). Sections use `--space-2xl` or `--space-3xl` vertical padding; blocks inside sections use `--space-lg` / `--space-xl` for breathing room.
- **Containers:** Horizontal padding via `.container`; narrow content (e.g. FAQ) uses `container--narrow` so line length stays readable.
- **Why:** Large spacing improves readability and reduces cognitive load. It also makes the page feel serious and uncluttered, which supports trust.

---

## 6. Accessible typography
- **Font stack:** System fonts (e.g. -apple-system, Segoe UI, Roboto) plus Japanese fallbacks (Hiragino, Yu Gothic, Meiryo) for any mixed content.
- **Scale:** `--text-xs` (13px) for labels/hints, `--text-sm` (14px) for secondary text, `--text-base` (16px) for body, `--text-lg` to `--text-3xl` for headings.
- **Line height:** `--line-tight` (1.3) for headings, `--line-normal` (1.5) and `--line-relaxed` (1.65) for body/leads.
- **Contrast:** Text and muted text use colors that meet WCAG AA on white/light gray.
- **Why:** Readable, scalable type and contrast help all users, including those on small screens or with slight visual impairment, and support longer reading without fatigue.

---

## 7. Section-by-section rationale

| Section | Role |
|--------|------|
| **Hero** | Identify audience (Filipino caregivers), state value (safe, legal, no fee), and offer the main CTA plus “Check eligibility”. |
| **Trust indicators** | Reinforce no fee, legal process, registered org, and post-arrival support in a scannable 4-item block. |
| **Eligibility** | Let users quickly see if they qualify (NC II, N4, passport, etc.) and CTA “I qualify — apply free”. |
| **Salary and life** | Answer “what will I earn and pay?” with concrete numbers and benefits (legal protection, insurance, environment). |
| **Application process** | Explain the 8 steps and “who does what” (Fuji-Mayon, Association, Employer) to reduce uncertainty and build confidence. |
| **Support before/after** | Show that support is continuous (before departure and after arrival), not only at application time. |
| **Why Fuji-Mayon** | Differentiate (no fee, legal only, clear roles, post-arrival support) and explain the company’s role. |
| **FAQ** | Address common objections and practical questions (salary, dorm, family, interview, timing, fee, Japanese level, contract issues). |
| **Final CTA** | Dedicated block with “What happens next”, one clear button to the form, then the embedded form and a short privacy note. |

---

## 8. Semantic HTML
- **Landmarks:** `<header>`, `<main>`, `<section>`, `<footer>`. Each section has an `aria-labelledby` or appropriate heading for screen readers.
- **Headings:** Single H1, then H2 per section, H3 for subsections. FAQ uses `<dl>` with `<dt>` (question) and `<dd>` (answer).
- **Lists:** `<ul>` / `<ol>` with `role="list"` where needed for Safari. Navigation and trust grid are lists.
- **Buttons vs links:** `<button>` for toggle and language; `<a>` for navigation and CTAs that change location (including in-page `#apply`).
- **Why:** Semantic structure improves accessibility and SEO and keeps the document logical for future changes.

---

## 9. Modular CSS
- **Naming:** BEM-like blocks (e.g. `.hero`, `.trust`, `.section`, `.card`) with modifiers (e.g. `--alt`, `--primary`, `--lg`) and elements (e.g. `__title`, `__lead`). No dependency on HTML structure depth.
- **Tokens:** Colors, spacing, font sizes, and line heights in `:root`. Layout (e.g. `.container`, `.cards--2`) is separate from components.
- **Sections:** Each major block has its own comment and a limited set of classes so styles can be updated or reused without side effects.
- **Why:** Modular CSS keeps the stylesheet maintainable and makes it easy to adjust one section (e.g. Trust or CTA) without breaking others.

---

## 10. Minimal JavaScript
- **Behavior:** (1) Toggle mobile nav open/close and `aria-expanded` / `aria-label`. (2) Toggle language dropdown and `aria-expanded`. (3) Smooth scroll for in-page links and close nav after click.
- **No frameworks:** Vanilla JS, wrapped in an IIFE. Runs after DOM is available (script at end of body).
- **Why:** Keeps the page fast and reliable; works without JS for static content (only interactivity is nav, lang, and smooth scroll). Inlined in `index.html` so the site works with only `index.html` + `style.css`.

---

## Files delivered
- **index.html** — Single page with all 9 sections, semantic markup, and inlined minimal script.
- **style.css** — Mobile-first, token-based, modular styles; no framework or preprocessor.

Assets (images, flags, form iframe) assume the same folder as the original site (e.g. `Top_image2.png`, `flag-en.png`, Google Form embed). Place `index.html` and `style.css` in that folder (or adjust paths) for a working deployment.
