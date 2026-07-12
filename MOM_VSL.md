# MOM_VSL.md — Project State (read this + CLAUDE.md, nothing else needed)

## Site type
Single-scroll VSL landing page — **no header/nav**, pure top-to-bottom scroll (explicit user requirement, do not re-add a nav bar). Single file: `index.html`. Dev server: `node serve.mjs` → `http://localhost:3000`.

## Design reference
`brand_assets/diseno2.png` is the **current layout source of truth** (a full mobile-mockup screenshot, 724×2172). The site was rebuilt to match it structurally (cards, icons, illustrations), while keeping these real assets/behaviors unchanged: `VSL.mp4` (file + mute/unmute behavior), `foto_alpha.png`, `kit.jpg`, and the CTA button text/gradient/shine+pulse animation (a heart-outline icon was added inside the buttons per the reference, but text/color/animation are untouched).

## Current page structure (top → bottom)
1. **Opening**: small filled heart icon (`#ic-heart`) + `brand_assets/Logo.png` + H1 "Guía emocional para el duelo de mamá" (color `text-plum`) + subtitle paragraph. Corner `blossom-branch` illustration top-left.
2. **Video**: `brand_assets/VSL.mp4`, wrapped in a white rounded card (`rounded-[28px] shadow-float p-2/p-3`) — no longer full-bleed/black background. Autoplay **muted** + centered pulsing "🔊 Toca para activar el sonido" button (`unmuteVSL()` JS unmutes to full volume on click, then hides itself).
3. **CTA button** (class `shine-btn`): heart-outline icon + text "Quiero el kit de acompañamiento para el duelo de mamá", pink gradient. Two combined loop animations: diagonal shine sweep (`shine-sweep`, 4s cycle) + scale pulse (`pulse-grow`, 1.8s cycle, scale 1→1.045→1).
4. **Kit info** (`#kit`): `brand_assets/kit.jpg` (all "Incluye" iconography is baked into this image, not HTML) → "Este acompañamiento incluye:" heading (flanked by horizontal rules) → **one** rounded card containing all 3 items (Guía emocional / Cuaderno de ejercicios / Grupo privado WhatsApp), each with a large circular icon badge (`ic-book`/`ic-notebook`/`ic-whatsapp`) + `lavender-sprig` accent, separated by dashed rules → pricing card (heart-in-ring badge overlapping the left edge, $30 tachado → $9 USD) → two-line closing quote (bold plum line + italic rose line, heart bullet + lavender sprig accent) → second CTA button, identical to the first.
5. **Bio**: single white rounded card — `brand_assets/foto_alpha.png` in an arch-top frame (left, or stacked on mobile) + Gabriela Haro bio paragraphs (right), heart-divider at the card's bottom edge.

## Typography & color system
- Body font: **Quicksand** (not Poppins — swapped because the reference's rounded letterforms don't match Poppins). Headings stay **Playfair Display**.
- New color token `plum` (`#22072B`, deep aubergine) used for H1, the "incluye" H3s, H2, and the first line of the closing quote — distinct from the existing `wine` family (still used for bold intro labels like "En ella encontrarás:", via `wine-darker`, and for strong-emphasis text in the bio).
- List bullets are heart-outline icons (`#ic-heart-o`, `text-rose`), not check-circles.
- Icon badges use `bg-rose-pale` circles (already-matching existing token) — no new color needed there.

## Decorative illustration system
- `#blossom-branch` — cherry-blossom line-art branch (thin stem + clustered small circle "petals"), used at page corners (opening + video section).
- `#lavender-sprig` — small stem with clustered purple oval buds, used beside each icon badge in the kit card and beside the closing quote.
- The old `#sprig` symbol (dusty-rose vine with oval leaves) was **removed** — it didn't match `diseno2.png` and is no longer referenced anywhere.

## Key decisions to preserve
- No nav/header — do not add one back.
- Both CTA buttons must stay **identical** to each other (text, pink gradient, shine + pulse animation, heart icon).
- True unmuted autoplay is blocked by all browsers — keep the muted-autoplay + manual unmute-button pattern, don't try to force unmuted autoplay again.
- Brand color for CTAs is **pink** (custom Tailwind color `pink`, ~#E14C7C family) — not wine/burgundy, not orange.
- Animation timings are deliberate: shine sweep = 4s loop, pulse = 1.8s loop. Both animate only `transform`/`opacity` per CLAUDE.md guardrails.
- Video is now boxed in a padded white card (supersedes the older "full-bleed edge-to-edge black section" decision — changed deliberately per `diseno2.png`, confirmed with user).

## Files reference
- `brand_assets/Logo.png`, `foto_alpha.png`, `kit.jpg`, `VSL.mp4` — all actively used, real brand assets (not placeholders).
- `brand_assets/diseno2.png` — **current** design reference (see above).
- `brand_assets/disenoguia.png` — an earlier, different design reference briefly used before the user corrected course to `diseno2.png`. Superseded; kept for history only.
- `brand_assets/VSL_design1.png` — historical mockup from an earlier design phase, superseded. Kept for history only.
- `brand_assets/button_ref.mov` — reference video used once to reverse-engineer the CTA shine animation; already implemented in CSS, file not otherwise needed.
- `vid.mp4` (project root) — unused leftover, not referenced anywhere in `index.html`. Leave in place unless user asks to remove it.

## Pending
- Nothing currently requested/outstanding.

## Do not touch without asking
- Don't delete any file in `brand_assets/` or root `vid.mp4` — ownership/purpose of unreferenced files should be confirmed with user first.
- Don't reintroduce the header/nav, the wine-colored CTA buttons, unmuted autoplay, or the full-bleed black video section — all were explicitly changed away from by user request.
