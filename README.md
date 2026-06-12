<div align="center">

<img src="https://img.shields.io/badge/DevLens-v1.0.0-6C63FF?style=for-the-badge&labelColor=0D0F12" />
<img src="https://img.shields.io/badge/License-MIT-00D4FF?style=for-the-badge&labelColor=0D0F12" />
<img src="https://img.shields.io/badge/Made%20with-Vanilla%20JS-F7DF1E?style=for-the-badge&labelColor=0D0F12" />
<img src="https://img.shields.io/badge/Deployed%20on-Vercel-ffffff?style=for-the-badge&labelColor=0D0F12" />

<br/><br/>

```
</> DevLens •
```

# See every PR clearly. Ship with confidence.

**DevLens transforms any GitHub Pull Request into a visual dashboard —
diff explorer, risk score, commit timeline, and language breakdown. Instant. No login. No install.**

[**→ Live Demo**](https://your-demo-link.vercel.app) · [**Report a Bug**](https://github.com/yourusername/devlens/issues) · [**Request a Feature**](https://github.com/yourusername/devlens/issues)

<br/>

![DevLens Dashboard Preview](screenshots/dashboard-preview.png)

</div>

---

## What is DevLens?

Most developers review PRs by scrolling through raw diffs on GitHub. DevLens gives you the full picture at a glance — file-by-file diffs with syntax highlighting, an algorithmic risk score, a visual commit timeline, and a language breakdown chart — all from a single URL paste, running entirely in your browser.

No sign-up. No API key required. No server. Just open the page and paste a PR.

---

## Features

| Feature | Description |
|---|---|
| **Diff Viewer** | Color-coded additions and deletions, collapsible file blocks, line numbers, file tree sidebar |
| **Risk Score** | Algorithmic 0–100 complexity rating based on churn, file spread, config changes, and test coverage |
| **Commit Timeline** | Full commit history with author avatars, messages, SHAs, and relative timestamps |
| **Language Breakdown** | Live donut chart showing file type distribution across all changed files |
| **Keyboard Shortcuts** | `⌘K` to focus input · `J`/`K` to navigate files · `Esc` to collapse all |
| **Shareable URLs** | Every analysis generates a `?pr=` URL you can bookmark and share |
| **Token Support** | Optional GitHub token via settings — raises rate limit from 60 to 5,000 req/hr |
| **Dark Mode** | Premium dark theme built-in, saved to localStorage |

---

## Demo

> Paste any of these into DevLens and hit Analyse:

```
https://github.com/facebook/react/pull/28768
https://github.com/vercel/next.js/pull/62001
https://github.com/tailwindlabs/tailwindcss/pull/13500
```

---

## Screenshots

<table>
  <tr>
    <td align="center"><b>Landing Page</b></td>
    <td align="center"><b>PR Analysis Dashboard</b></td>
  </tr>
  <tr>
    <td><img src="screenshots/landing.png" alt="Landing page" /></td>
    <td><img src="screenshots/dashboard.png" alt="Dashboard" /></td>
  </tr>
  <tr>
    <td align="center"><b>Diff Viewer</b></td>
    <td align="center"><b>Risk Score</b></td>
  </tr>
  <tr>
    <td><img src="screenshots/diff-viewer.png" alt="Diff viewer" /></td>
    <td><img src="screenshots/risk-score.png" alt="Risk score" /></td>
  </tr>
</table>

---

## How It Works

```
┌─────────────────────────────────────────────────────────┐
│  1. Paste a GitHub PR URL into the input bar            │
│  2. DevLens parses owner / repo / PR number             │
│  3. GitHub REST API returns files, commits, metadata    │
│  4. Patch strings are parsed line-by-line               │
│  5. Risk algorithm scores complexity (0–100)            │
│  6. Results render in an interactive dashboard          │
└─────────────────────────────────────────────────────────┘
```

**Risk Score Algorithm**

```
score = 0
score += (filesChanged  / 20)  * 25   // file spread      → max 25
score += (linesAdded    / 500) * 20   // additions        → max 20
score += (linesDeleted  / 200) * 15   // deletions        → max 15
score += (commitCount   / 15)  * 15   // commit count     → max 15
score += hasConfigFiles ? 15 : 0      // .json/.yml/.env  → +15
score += lacksTestFiles ? 10 : 0      // no tests in PR   → +10
score  = Math.min(100, Math.round(score))

0–33  → Low     (green)
34–66 → Medium  (amber)
67–100→ High    (red)
```

---

## Tech Stack

**No frameworks. No build step. No dependencies.**

| Layer | Technology |
|---|---|
| Structure | HTML5 (single file) |
| Styling | CSS3 — custom properties, grid, animations |
| Logic | Vanilla JavaScript (ES2022, async/await) |
| Icons | [Lucide Icons](https://lucide.dev) via CDN |
| Data | GitHub REST API v3 (public, unauthenticated) |
| Fonts | Inter + JetBrains Mono via Google Fonts |
| Hosting | Vercel (free tier) |

---

## Project Structure

```
devlens/
├── index.html          # Entire app — markup, styles, and logic
├── screenshots/        # README screenshots
│   ├── landing.png
│   ├── dashboard.png
│   ├── diff-viewer.png
│   └── risk-score.png
├── README.md
└── LICENSE
```

---

## Running Locally

No install needed. Seriously.

```bash
# Clone the repo
git clone https://github.com/yourusername/devlens.git

# Open in browser — that's it
open devlens/index.html
```

Or with a local server (optional, for clean URLs):

```bash
npx serve .
# → http://localhost:3000
```

---

## GitHub API Rate Limits

DevLens works without any token — but the GitHub API allows **60 requests/hour** for anonymous use. For heavy usage, add a free personal access token:

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Generate a token with `public_repo` scope (read-only)
3. Click the ⚙️ gear icon in DevLens → paste your token
4. Rate limit increases to **5,000 requests/hour**

Your token is stored only in your browser's `localStorage`. It is never sent anywhere except directly to `api.github.com`.

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `⌘K` / `Ctrl+K` | Focus the PR input |
| `J` | Jump to next file |
| `K` | Jump to previous file |
| `Esc` | Collapse all files |

---

## Deployment

**Deploy to Vercel in 60 seconds:**

```bash
# Install Vercel CLI (one-time)
npm i -g vercel

# Deploy
vercel
```

Or connect your GitHub repo at [vercel.com](https://vercel.com) and every push auto-deploys.

---

## What I Learned Building This

- Parsing raw Git patch strings manually (the `@@` hunk format is non-trivial)
- Designing a risk scoring algorithm that produces meaningful, non-arbitrary results
- Building accessible, keyboard-navigable UIs without a framework
- Rate-limit handling and graceful degradation with public APIs
- Rendering animated SVG gauge arcs and CSS conic-gradient donut charts from scratch
- `IntersectionObserver` for performant scroll-based animations
- Canvas API for the animated dot-grid hero background

---

## Roadmap

- [ ] Side-by-side diff view
- [ ] GitLab PR support
- [ ] Export analysis as PDF
- [ ] PR comparison (compare two PRs)
- [ ] Comment thread viewer

---

## License

MIT © [Parthi Rohi](https://github.com/yourusername)

---

<div align="center">
  <b>If DevLens helped you, consider giving it a ⭐ on GitHub.</b><br/>
  <sub>Built with focus and zero dependencies · Deployed on Vercel</sub>
</div>
