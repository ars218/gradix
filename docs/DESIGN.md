# Design Reference — Gradix

## Philosophy

Gradix is built for students who deserve tools that feel as serious as their work. The design language borrows from fintech dashboards — precise, premium, and uncluttered — rather than the bright, toy-like aesthetics that dominate student apps.

The goal: open the app and immediately feel like your results matter.

---

## Visual Language

### Color

| Role | Token | Value |
|---|---|---|
| Page background | `--bg-deep` | `#040810` |
| Background mid | `--bg-navy` | `#070d1c` |
| Background surface | `--bg-mid` | `#0b1428` |
| Glass card background | `--glass-bg` | `rgba(255,255,255,0.04)` |
| Glass border | `--glass-border` | `rgba(255,255,255,0.08)` |
| Accent (electric blue) | `--accent` | `#4f9eff` |
| Accent bright | `--accent-bright` | `#70b4ff` |
| Accent glow | `--accent-glow` | `rgba(79,158,255,0.25)` |
| Primary text | `--text-primary` | `#e8f0fe` |
| Secondary text | `--text-secondary` | `rgba(200,215,245,0.65)` |
| Muted text | `--text-muted` | `rgba(150,175,220,0.4)` |
| Red / fail | `--red` | `#ff5a7e` |
| Green / pass | `--green` | `#3dffa0` |
| Yellow | `--yellow` | `#ffd060` |
| Orange | `--orange` | `#ff9a45` |
| Purple | `--purple` | `#b87fff` |

### Typography

| Role | Font | Weight |
|---|---|---|
| Headings / display | Sora | 700, 800 |
| UI labels, body | Outfit | 400, 500, 600 |

Both fonts are loaded from Google Fonts. They are geometric and clean — chosen to convey clarity and modernity without feeling sterile.

### Depth & Texture

The background uses a layered radial gradient mesh to create a sense of depth — a faint blue-purple glow in the top-left and bottom-right corners against near-black. A noise texture overlay (SVG fractalNoise filter at 4% opacity) adds subtle grain to prevent the dark background from feeling flat.

Cards use `backdrop-filter: blur(12px)` with a semi-transparent background and a subtle border to achieve the glassmorphism effect.

---

## Motion

- **Page / card entry**: `cardIn` keyframe — `opacity: 0 → 1` with a `translateY(16px → 0)` over `0.35s`. Staggered on dashboard grid with `animation-delay`.
- **Modal entry**: `slideUp` — `opacity + translateY + scale(0.98 → 1)` over `0.3s cubic-bezier(0.4,0,0.2,1)`.
- **Hover states**: Cards lift `translateY(-3px)` with a stronger glow on the border. Buttons shift up `1px` on `.btn-primary`.
- **Progress bars**: Width animates from `0` to the target percentage over `0.6s ease` — visible on result detail load.
- **Step indicator dots**: Width transitions from `8px` circle to `24px` pill for the active step.

All transitions use `0.25s cubic-bezier(0.4,0,0.2,1)` as the base easing.

---

## Grade Badge Colors

Each letter grade maps to a distinct color to make scanning a results table instant:

| Grade | Color |
|---|---|
| A+ | Green (`#3dffa0`) |
| A | Electric blue (`#70b4ff`) |
| B | Purple (`#b87fff`) |
| C | Yellow (`#ffd060`) |
| D | Orange (`#ff9a45`) |
| E | Soft red (`#ff8fa7`) |
| F | Red (`#ff5a7e`) |

---

## Layout

- Max content width: `960px`, centered.
- Dashboard uses CSS Grid with `auto-fill, minmax(280px, 1fr)` — naturally responsive.
- New Result flow is constrained to `560px` max-width for a focused, form-like feel.
- The sticky header uses `backdrop-filter: blur(20px)` with a dark semi-transparent background to stay readable over scrolling content.

---

## Mobile

- Subject entry rows reflow to tighter column widths on `max-width: 480px`.
- The detail percentage display shrinks from `72px` to `52px`.
- The grid collapses to a single column.
- Touch targets are a minimum of `42px` tall on all interactive elements.
