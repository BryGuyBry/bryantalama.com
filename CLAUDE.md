# CLAUDE.md — bryantalama.com

Personal portfolio site for Bryant Alama. A static HTML/CSS/JS site with a retro CRT/VHS aesthetic, deployed via GitHub Pages at bryantalama.com.

## Repository Structure

```
bryantalama.com/
├── index.html        # Home page — animated portal navigation hub
├── music.html        # Music section — releases, catalog, influences
├── writing.html      # Writing section — blog, fiction, obsessions
├── technology.html   # Technology section — homelab posts, skills, stack
└── CNAME             # GitHub Pages custom domain (bryantalama.com)
```

No build tools, frameworks, or package managers. All pages are self-contained HTML files with embedded CSS and JavaScript.

## Design System

All pages share a consistent visual language. Use these values when adding or modifying any HTML/CSS:

### CSS Custom Properties (defined in `:root` on every page)
```css
--amber:     #ffb347   /* Primary text and headings */
--orange:    #ff6b00   /* Accents, borders, section headings */
--red-neon:  #ff2200   /* Hot accents, error states */
--darker:    #080300   /* Page background (index) */
--dark:      #0d0500   /* Card backgrounds */
--dim:       #1a0a00   /* Subtle fills */
--text-dim:  #a05a20   /* Body copy, dimmed text */
--glow-amber: 0 0 10px #ffb347, 0 0 30px #ff6b00, 0 0 60px #ff2200
--glow-soft:  0 0 8px #ffb34788, 0 0 20px #ff6b0055
```

### Typography
- **Headings / labels:** `Orbitron` (Google Fonts) — weights 400, 700, 900; `letter-spacing: 0.3em`
- **Body / mono text:** `Share Tech Mono` (Google Fonts)
- Fluid sizing via `clamp()` for page titles

### Background Layers (z-index stack, present on every page)
| Layer | Element | z-index |
|---|---|---|
| Starfield canvas | `#starfield` (index only) | 0 |
| Grid overlay | `.grid-overlay` | 1 |
| Scanlines | `.scanlines` | 2 |
| Vignette | `.vignette` | 3 |
| Content | `.site-wrapper` | 10 |

### Animation Conventions
- Entry animations: `fadeDown` (header) and `fadeUp` (content/footer) keyframes
- Staggered delays on `.content-section:nth-child(n)` — 0.6s, 0.8s, 1.0s
- Elements start `opacity: 0`, animate to final state on load
- Hover transitions: `0.3s–0.5s ease`

## Page Patterns

### Index (`index.html`)
- Full-viewport layout with flexbox centering (`justify-content: space-between`)
- Three `.portal` `<a>` elements linking to the section pages
- Each portal has inline SVG art with CSS hover animations (reel spin, VU meters, book opening, screen flicker, etc.)
- Glitch transition on portal click: JS animates `#glitch-overlay` before navigating
- Animated canvas starfield in the background (220 stars, amber color, twinkling)
- VHS glitch effect on `window.load`

### Section Pages (`music.html`, `writing.html`, `technology.html`)
- Shared layout: `max-width: 900px; margin: 0 auto; padding: 3rem 2rem 4rem`
- Top nav: `← Home` back link + `//` divider + current page name
- Header: large glowing page title + subtitle + `.section-line` gradient divider
- Content in `.content-section` divs containing `.placeholder-card` elements
- Each card: `border: 1px solid rgba(255,107,0,0.2)`, semi-transparent dark background, hover brightens border
- Tags: `.tag` — small uppercase bordered labels

### Footer (all pages)
- Gradient divider line
- Social links: Spotify, YouTube, Instagram, GitHub (BryGuyBry)
- Copyright line

## Development Workflow

No build step required. Edit HTML files directly and open in a browser.

```bash
# Preview locally (any static server works)
python3 -m http.server 8080
# or
npx serve .
```

### Deployment
- Hosted on **GitHub Pages** from the `main` branch
- Custom domain configured via `CNAME` file (`bryantalama.com`)
- Push to `main` → site updates automatically

### Git Branching
- `main` — production branch (GitHub Pages serves from here)
- `master` — mirrors main; legacy ref
- Feature branches: `claude/<description>-<id>` for AI-assisted changes

## Key Conventions

1. **No external dependencies** — no npm, no bundler, no frameworks. Keep it that way unless there is a strong reason to change.
2. **CSS lives in `<style>` tags** — each page is self-contained. There is no shared stylesheet. Duplicate common styles across pages intentionally.
3. **Consistent CSS variable usage** — always reference `--amber`, `--orange`, etc. rather than hardcoding hex values in new rules.
4. **SVG art is inline** — the portal illustrations in `index.html` are inline SVG. CSS classes on SVG elements drive hover animations.
5. **Placeholder content is intentional** — section pages use `.placeholder-card` with `// Loading` / `// Incoming` headings. This is the current state of the site. Replace with real content when it exists; don't remove structural elements.
6. **Social links are `href="#"`** — Spotify, YouTube, Instagram links are not yet filled in. GitHub points to `https://github.com/BryGuyBry`. Update social hrefs when real URLs are available.
7. **Responsive breakpoints** — `@media (max-width: 768px)` on index (stack portals vertically), `@media (max-width: 600px)` on section pages (reduce padding).

## Content Sections Reference

| Section | Current Content |
|---|---|
| Music — Transmitting | New material in progress; post-punk/synth direction |
| Music — Catalog | Existing singer-songwriter releases on streaming platforms |
| Music — Influences | MGMT, Joy Division, LCD Soundsystem, Depeche Mode, Bowie, Eno, The Cure, Pink Floyd, The Clash, Mac DeMarco, Geese, MJ Lenderman, Silver Jews |
| Writing — Transmissions | Personal essays placeholder, no posts yet |
| Writing — Fiction | Short stories in progress; themes: technology, isolation, time |
| Writing — Obsessions | Linux, self-hosted infra, analog synthesis, post-punk, vintage sci-fi, home recording |
| Technology — Posts | Linux on 2012 MacBook Pro (Linux Mint 22.3), Pi-hole setup, Jellyfin media server |
| Technology — Stack | Linux Mint, Ubuntu, Bash, Git, Networking, DNS, HTML/CSS, Pi-hole, Jellyfin, Tailscale, NAS |
