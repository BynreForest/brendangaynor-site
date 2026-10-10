# brendangaynor.com

Personal portfolio for Brendan Gaynor — iOS/Swift developer and founder of BBG Studios LLC, an AI development consultancy. The site showcases the apps he has built. Hosted on Cloudflare as static assets, deployed from GitHub.

## Tech constraints (do not break these)

- Plain HTML, CSS, and minimal vanilla JS. **No frameworks, no build step, no npm.**
- Every page must work when opened directly from disk (`file://`). Use **relative paths** for links, styles, and images (`apps/thinktrace.html`, `../assets/...`). Never root-absolute paths (`/assets/...`) — the one exception is `404.html` (see below).
- Mobile-first and responsive. Must look great on iPhone (safe-area insets, tap targets ≥ 44px).
- Dark and light mode via `prefers-color-scheme`. **Dark is the primary design**; light is the override.
- Accessible: semantic HTML (`header`/`main`/`section`/`footer`, one `h1` per page), alt text, visible `:focus-visible` states, WCAG AA contrast, respect `prefers-reduced-motion`.
- Fast: no heavy libraries, no web fonts (system font stack). **One shared stylesheet**: `assets/css/styles.css`. No per-page `<style>` blocks; per-app accent color is set with an inline `style="--accent: …"` custom property only.

## Structure

```
/index.html              homepage (hero, app grid, footer)
/apps/<slug>.html        one detail page per app, all from the same template
/assets/css/styles.css   shared styles
/assets/icons/<slug>.png app icons (1024×1024 source PNGs, provided)
/assets/screens/<slug>/  screenshots (may be empty)
/404.html
```

`404.html` links the stylesheet twice — `/assets/css/styles.css` (works when Cloudflare serves it at any depth) and `assets/css/styles.css` (works from disk). Keep both.

## Apps — in this exact order

| # | Name | Slug | Status | Accent |
|---|------|------|--------|--------|
| 1 | Thinktrace | `thinktrace` | In development | Purple (from icon) |
| 2 | iDetail | `idetail` | [TODO] | [TODO] |
| 3 | Cue | `cue` | [TODO] | [TODO] |
| 4 | BeatingU: Vision Challenge | `beatingu-vision` | On the App Store | Blue |
| 5 | BeatingU: Running Challenge | `beatingu-running` | In development | Orange |
| 6 | Fit Tunes | `fittunes` | [TODO] | [TODO] |

### Source content (only facts we have — do not embellish)

- **Thinktrace** — iOS voice-notes app: record voice memos, then ask questions about their content. Stack: SwiftUI, MVVM, Apple SpeechAnalyzer (on-device transcription), Python/FastAPI, LangGraph agents (router, retriever, answer composer), PostgreSQL + pgvector, AWS (RDS, ECS), Amazon Bedrock Titan Text Embeddings V2, eval suite with golden Q&A set, Swift Testing. Status: in development.
- **iDetail** — iOS and web sales-enablement app for pharma sales reps. Website: https://idetailapp.com. Stack: [TODO].
- **Cue** — AI voice agent platform; deployed as a conversational AI kiosk at pharma conferences (directional cardioid mic + push-to-talk). Stack: ElevenLabs Conversational AI, Bland.ai, WKWebView with a bidirectional JS bridge, [TODO: rest]. Website: https://hellocue.app.
- **BeatingU: Vision Challenge** — visual-skills game: a "20/20 Sprint" of shrinking Landolt C rings; tap the direction of the gap; compete via Game Center leaderboards and challenges. Stack: SwiftUI, GameKit/Game Center. Status: on the App Store [TODO: App Store link]. Blue accent.
- **BeatingU: Running Challenge** — timed runs (0.5–10 mi) with Game Center leaderboards and real-time head-to-head racing. Stack: SwiftUI, MVVM, Core Location (background), GameKit/Game Center. Status: in development. Orange accent.
- **Fit Tunes** — [TODO: description, stack, status].

## Content rules

- **Never invent** features, metrics, users, awards, or claims. Where information is missing, write a visible placeholder like `[TODO: description]` wrapped in `<span class="todo">…</span>` so it stands out on the page.
- Contact email is a placeholder (`you@example.com`) until Brendan provides the real one.
- Footer: contact link + `© BBG Studios LLC`.

## Detail page template

`apps/thinktrace.html` is the reference template. Every detail page has, in order:

1. Back link to `../index.html`
2. Hero: large icon, app name (`h1`), tagline, status badge (`badge--live` for "On the App Store", `badge--dev` for "In development")
3. Optional App Store / website button(s) (`.btn`) — omit if none
4. About: 2–3 short paragraphs
5. Tech stack: chips (`.chips`), optionally grouped
6. Screenshots (`.screens`): list `<img>` tags for files in `assets/screens/<slug>/`. The section hides itself via CSS `:has()` when it contains no images, and each `<img>` removes itself on load error — so an empty or missing folder never shows a broken section.

## Missing assets (as of first commit)

- `assets/icons/idetail.png` is not present yet — the homepage tile shows a lettered fallback until it's added.
- `assets/icons/cue.png` is currently a byte-identical copy of `thinktrace.png` — needs the real Cue icon.

## Workflow

- Preview: `python3 -m http.server 8000` from the repo root, then http://localhost:8000 — or just open `index.html`. (In the Claude desktop app, `.claude/launch.json` attaches the Browser pane to that server; start the server from a shell first, since the launcher lacks Desktop folder access.)
- Don't add tooling, package.json, or a build step.
