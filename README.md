# Tuition Tracker Validator

Monthly data quality validator for the tuition payment tracker spreadsheet. Upload the `.xlsx` file and it runs three checks instantly in the browser — no data is sent to any server.

## Checks

1. **Tab ↔ Summary name matching** — flags any name in Summary row 1 without a matching tab, any tab without a matching row 1 entry, and near-matches with spacing/casing differences
2. **Month column coverage** — finds any row with data in columns A–D but a blank Month cell, across every individual family tab
3. **Summary formula consistency** — verifies rows 7–22 have the correct SUMIF, SUM, and balance formulas for each family column

## Local development

```bash
npm install
npm start
```

Then open [http://localhost:3000](http://localhost:3000).

## Deploy to Railway

### Option A — Railway dashboard (recommended)

1. Push this repo to GitHub
2. Go to [railway.app](https://railway.app) → New Project → Deploy from GitHub repo
3. Select this repo — Railway will auto-detect Node.js and deploy
4. Your app will be live at the generated Railway URL within ~60 seconds

### Option B — Railway CLI

```bash
npm install -g @railway/cli
railway login
railway init
railway up
```

## Project structure

```
tuition-validator/
├── public/
│   └── index.html      # Full app (single HTML file, all logic client-side)
├── server.js           # Minimal Express static file server
├── package.json
├── .gitignore
└── README.md
```

## Notes

- All validation runs entirely in the browser via [SheetJS](https://sheetjs.com/) — the spreadsheet is never uploaded anywhere
- No database, no auth, no environment variables needed
- The server is a single-file static Express server; the only dependency is `express`
