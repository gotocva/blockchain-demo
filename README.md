# Blockchain Demo

An interactive walkthrough of how a blockchain works, built as a single-page React app and inspired by [Anders Brownworth's blockchain demo](https://andersbrownworth.com/blockchain/).

🌐 **Live demo:** <https://gotocva.github.io/blockchain-demo/>

This repository contains the **production build** (static `dist/` output) ready to be served by any static host (GitHub Pages, Netlify, Vercel, S3, Nginx, etc.).

## Live Demo Sections

| Page | What it shows |
|---|---|
| **Hash** | Real-time SHA-256 hashing of any input. Includes a **Find Nonce** button that searches for the smallest integer `nonce` such that `sha256(nonce + data)` starts with `0000`, and reports nonce, attempts, and search time. |
| **Block** | A single mineable block with `index`, `nonce`, `data`, `prev`, and `hash`. The card turns **green** when the hash satisfies the difficulty target (`0000…`) and **red** when tampered. |
| **Blockchain** | Five linked blocks where each block's `prev` is the previous block's hash. Tampering with any block cascades — every block downstream becomes invalid until re-mined. |
| **Distributed** | Three peers (A, B, C) each holding an independent copy of the chain. Mutate one peer to see it diverge from the network. |
| **Tokens** | Coinbase + transfer transactions per block, editable across the same three peers. Demonstrates how transaction history is anchored to the chain. |

## Tech Stack

- **React 18** + **TypeScript** + **Vite 6**
- **Tailwind CSS** + **shadcn/ui** (Radix primitives)
- **React Router v6** for tabbed navigation
- **js-sha256** for hashing
- Mining searches for a hash with the leading prefix `0000`.

## Running Locally

This repo is the built output. Drop the contents into any static file server:

```bash
# Quick preview with Python
python3 -m http.server 8080

# Or with Node
npx serve .
```

Then open <http://localhost:8080>.

## GitHub Pages Notes

This build is configured for the project page at `/blockchain-demo/`:

- Vite `base` is set to `/blockchain-demo/` so all asset URLs are prefixed correctly.
- `.nojekyll` is present so GitHub Pages serves files in `assets/` (Jekyll skips folders starting with `_`, but `.nojekyll` disables Jekyll altogether).
- `404.html` is a copy of `index.html` so client-side routes (`/hash`, `/block`, etc.) survive a hard refresh — GitHub Pages serves `404.html` and React Router takes over.

## Layout

```
.
├── index.html         # SPA entry (base = /blockchain-demo/)
├── 404.html           # SPA fallback for client-side routing on GitHub Pages
├── .nojekyll          # Disable Jekyll processing
├── favicon.ico
├── robots.txt
└── assets/            # Hashed JS + CSS bundles
    ├── index-*.js     # Main bundle
    ├── index-*.css    # Tailwind + shadcn styles
    ├── HashPage-*.js  # Lazy-loaded route chunks
    ├── BlockPage-*.js
    ├── BlockchainPage-*.js
    ├── DistributedPage-*.js
    └── TokensPage-*.js
```

## Credits

Conceptually based on Anders Brownworth's classic educational demo at <https://andersbrownworth.com/blockchain/>. UI rebuilt with shadcn/ui components and a responsive light/dark theme.
