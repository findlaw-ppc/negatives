# Law Firm Negative Keyword Generator (Google Ads)

A single-file, client-side web app for PPC teams at law firms. Paste your Search Term Report, analyze intent, and export a clean, deduped list of phrase-match negatives:
- Competitors (brands, directories, aggregators)
- Low-value administrative queries (phone, address, hours, forms, payments, jobs, court/DMV/jail lookups, etc.)
- Non–practice-area queries (based on include/exclude practice keywords)

All processing is done in your browser—no servers, no data leaves your machine.

Demo: open `index.html` locally or deploy to GitHub Pages (instructions below).

---

## Features

- Deterministic rules engine (no ML): transparent regex + curated dictionaries
- Input-friendly: paste lines or CSV/TSV; auto-detects separators; auto-selects “Search term” column if present
- Brand protection: “Never negate my brand” toggle
- Practice templates: Personal Injury, Family, Criminal, Immigration, Employment, Estate, Bankruptcy, Business
- Strict mode: if a term matches neither include nor exclude, negate the full query as a phrase (optional)
- One-click copy + file download for:
  - Competitors
  - Administrative
  - Non–practice-area
  - Master (deduped union)

---

## How it works (the brain)

- Competitors: detects legal directories/aggregators (Avvo, Justia, FindLaw, Martindale, Nolo, Super Lawyers, Lawyers.com, LegalZoom, Rocket Lawyer, Yelp, Thumbtack, Angi, etc.) and brand-like firm patterns (e.g., “law offices of X,” “X law,” “X & Y,” “X LLP/PLLC/PC/PA,” “X legal group”). Extracts the brand token as the negative (not the full query). Excludes your firm’s brand if brand-protection is enabled.
- Administrative: curated phrase list for address, directions/map/hours, phone/email/login/portal, billing/payments, careers/jobs, forms/PDF/templates, court/clerk/DMV/jail/inmate/jury, legal aid/pro bono/free/cheap, etc. Normalizes common combos like “phone + number.”
- Practice classification:
  - Include keywords → in-scope (don’t negate)
  - Exclude keywords → out-of-scope (negatives use those phrases)
  - Strict mode → if neither include nor exclude match, negate the full term as a phrase (unless your brand is present)
- Output: everything quoted as phrase-match, case-insensitive dedupe, stable category ordering

---

## Quick start

1) Download the code
- Save the provided HTML file as `index.html` in your repo root.

2) Run locally
- Double-click `index.html` to open in your default browser (no build or server required).

3) Test
- Click “Load Sample,” then “Analyze & Generate Negatives.”
- Try toggles for “Never negate my brand” and “Strict non-PA.”

---

## Deploy to GitHub Pages

1) Create a new repo (public or private)
- Name it something like `law-firm-negative-keyword-generator`.

2) Add files
- Commit `index.html` to the repository root.
- Optionally add `README.md` (this file) and `LICENSE`.

3) Enable Pages
- Go to Settings → Pages.
- Build and deployment: “Deploy from a branch.”
- Branch: `main` (or `master`), Folder: `/root`.
- Save; your site will be live at:
  - `https://<your-username>.github.io/<repo-name>/`

---

## Using the app

1) Context
- Enter law firm name variants (e.g., “Smith & Jones, Smith Law, The Smith Law Firm”) to protect brand queries.
- Optional: Enter office locations to guide your tuning.
- Select a practice template (optional) to preload include/exclude keywords.

2) Paste your Search Term Report
- Works with plain text (one term per line) or CSV/TSV (Google Ads export).
- The app auto-detects the separator and uses the “Search term” column if present.

3) Analyze
- Click “Analyze & Generate Negatives.”
- Copy “Master negative list” or download individual category lists.

4) Import to Google Ads
- Add as phrase-match negatives at the campaign or shared list level.
- Always review before publishing.

---

## Customization

- Include keywords (in-scope): add synonyms you want to keep (e.g., “car crash,” “auto wreck”).
- Exclude keywords (out-of-scope): add practice areas you don’t serve (e.g., “immigration,” “bankruptcy” if you’re PI-only).
- Competitors: extend the aggregator/brand list or add firm-name regexes.
- Administrative: add/remove phrases for your internal filters.
- Strict mode: turn on for aggressive cleanup when discovery terms are broad.

Tip: Keep your lists lean at first. Over time, expand as real search term data reveals patterns.

---

## Data privacy

- 100% client-side. No tracking, no network calls, no persistence by default.
- Paste data stays in the page until you close or clear.

---

## Limitations and notes

- Deterministic rules mean you’ll get high precision but may miss edge-cases or creative misspellings.
- Brand detection uses common patterns; add your market’s known competitors for better recall.
- Google Ads matching changes over time—regularly review your negative lists for impact on volume and intent.
- This tool assists PPC workflows; it does not provide legal advice.

---

## Roadmap (ideas)

- Fuzzy/typo-tolerant matching for competitor brands
- Location-aware filtering (protect in-market geo intent)
- Confidence scoring per category
- Optional LLM/ML second opinion with the rules engine as a guardrail
- Export as CSV for shared negative lists
- Multi-language support (ES, FR)

---

## Contributing

Issues and PRs welcome. Please:
- Open an Issue describing the change and rationale
- Keep the app single-file where possible (easy for non-dev PPC teams)
- Add/adjust tests (manual steps in PR) describing sample inputs and expected outputs
- Follow semantic commit messages (feat:, fix:, docs:, refactor:, chore:)

---

## License

MIT License

Copyright (c) 2026 [Your Name or Organization]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in  
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN  
THE SOFTWARE.

---

## Repository suggestions

- `index.html` — the entire app (HTML/CSS/JS in one file)
- `README.md` — this file
- `LICENSE` — MIT (optional separate file)
- `.gitignore` — optional, e.g., macOS `.DS_Store`

---

## Credits

Built with vanilla JavaScript and CSS. Designed for PPC strategists who want fast, explainable negative keyword workflows.
