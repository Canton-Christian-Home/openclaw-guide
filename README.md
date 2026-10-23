# OpenClaw Workspace Generator & Best Practices

A single-page static site that lets you configure your OpenClaw agent workspace
with a simple form, then download the generated files:

- `workspace/AGENTS.md` — operating instructions (formatting rules, hard rules)
- `workspace/SOUL.md` — tone, personality, hard constraints
- `workspace/USER.md` — who you are, environment, preferences
- `workspace/ACTIVE-TASK.md` — current objective / focus lock
- `openclaw.json` — master config with the self-improvement hooks section

Plus the five community best practices as an on-page guide.

## How it works

- 100% client-side. No backend, no framework, no dependencies — one `index.html`.
- Fill in the form; the live preview regenerates the selected file as you type.
- **Download workspace (.zip)** builds a real zip in the browser (stored entries,
  CRC-32 computed in vanilla JS) containing `workspace/*.md` and `openclaw.json`.
- Your settings are saved to browser `localStorage` automatically, so you can
  come back and tweak. "Reset all settings" clears them.
- Below the generator, the full best-practices guide (workspace structure,
  recursive improvement, multi-agent hierarchy, learning hooks, crons).

## Run locally

```bash
python -m http.server 8000
# open http://localhost:8000
```

(Opening index.html directly via file:// also works — there are no fetches.)

## Deploy to GitHub Pages

1. Create a new public repository (e.g., `openclaw-generator`).
2. Upload `index.html` (and this README) to the default branch (`main`).
   - Web UI: repo → "Add file" → "Upload files"
   - Or via CLI:
     ```bash
     git init
     git add index.html README.md
     git commit -m "Add workspace generator site"
     git branch -M main
     git remote add origin https://github.com/<you>/openclaw-generator.git
     git push -u origin main
     ```
3. Go to **Settings → Pages** in the repo.
4. Set **Source** to *Deploy from a branch*, branch `main`, folder `/ (root)`, click **Save**.
5. Open `https://<you>.github.io/openclaw-generator/` after ~1–2 minutes.

## Customizing

- Form fields and file templates live in the `<script>` block at the bottom of
  `index.html` — the `genAgents`, `genSoul`, `genUser`, `genTask`, and `genConfig`
  functions. Edit the template strings to change what gets generated.
- Theme colors are CSS variables at the top of the `<style>` block.
- To add more form fields: add the input HTML, add its id to the `IDS` array,
  use it in a generator, and it will persist automatically.
