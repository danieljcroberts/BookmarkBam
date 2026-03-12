# BookmarkBam 🔖

A fast, personal bookmark manager that runs entirely on **Cloudflare Workers** — no server, no database, no subscription. Your bookmarks live in Cloudflare's global KV store, accessible from anywhere.

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/danieljcroberts/BookmarkBam)

---

## Features

- 📁 **Category organisation** — group bookmarks your way, rename or delete categories anytime
- 🔍 **Instant search** — filter bookmarks or launch a web search from the same box
- 🌤️ **Live weather** — shows current conditions for your location
- 🎨 **Theming** — choose from built-in themes or customise every colour
- 🔗 **Dual links** — store both an external and internal URL per bookmark (great for self-hosted services)
- ⌨️ **Keyboard navigation** — arrow keys, Enter to open, Escape to clear
- 📱 **Mobile friendly** — works on any screen size

---

## Prerequisites

You'll need a **Cloudflare account** — [sign up free at cloudflare.com](https://dash.cloudflare.com/sign-up). No credit card is required, and BookmarkBam runs entirely within Cloudflare's free tier:

- ✅ **Workers** — free tier includes 100,000 requests/day
- ✅ **KV storage** — free tier includes 100,000 reads/day and 1,000 writes/day

For a personal bookmark manager this is more than enough — you'd have to click a bookmark 100,000 times in a single day to get anywhere near the limits.

---

## Deploy

### Option 1 — One Click (No coding required)

1. Click the **Deploy** button above
2. Connect your GitHub account and Cloudflare account when prompted
3. Follow the setup wizard — it will fork the repo and deploy the worker automatically

> **One manual step required after deployment:**
> Go to **Cloudflare Dashboard → Workers & Pages → KV**, create a namespace called `bookmarks`, copy the ID, and paste it into `wrangler.toml` under `id = "..."`. Then redeploy.

---

### Option 2 — Wrangler CLI

```bash
# 1. Install Wrangler
npm install -g wrangler

# 2. Log in to Cloudflare
wrangler login

# 3. Create the KV namespace
wrangler kv namespace create bookmarks
# → Copy the ID from the output

# 4. Paste the ID into wrangler.toml
#    Find: id = "REPLACE_WITH_YOUR_KV_ID"
#    Replace with your actual ID

# 5. Deploy
wrangler deploy
```

---

## Configuration

All settings are configured on first launch via the setup screen — no file editing needed. Once deployed, visit your worker URL and you'll be walked through entering your name, location coordinates, and WeatherAPI key.

You can update any of these anytime from the padlock menu once the app is running.

To get a free weather API key, sign up at [weatherapi.com](https://www.weatherapi.com) — no credit card required.

---

## Project Structure

```
BookmarkBam/
├── bookmarkbam.js   # The entire worker — all logic and UI in one file
├── wrangler.toml    # Cloudflare Workers config
├── package.json     # Node dependencies (just Wrangler)
└── README.md
```

---

## How It Works

BookmarkBam is a single Cloudflare Worker that:
- Serves a full HTML page with embedded CSS and JavaScript
- Stores all bookmark, category, and theme data in **Cloudflare KV**
- Fetches live weather from WeatherAPI on each page load
- Requires no backend framework, no build step, and no database

---

## License

MIT — do whatever you like with it.
