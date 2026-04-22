# ARGUS FIELD
### ArgusLand Planning & Engineering — Field Intelligence System
**Version 2.0**

---

## What Is ARGUS FIELD?

ARGUS FIELD is the single operating app for the ArgusLand Planning & Engineering Department. It replaces the Telegram bot + AppScript relay system with a direct, offline-capable PWA that your team installs on their phones like a native app.

**It does five things:**

| Function | What it replaces |
|---|---|
| Daily check-in (3 questions, role-based) | Telegram daily updates |
| CSW prompt generator + archive | Manual CSW drafting + paper filing |
| Team dashboard (transparent, everyone sees) | Coordination meeting verbal updates |
| Weekly health report | Manual weekly summary |
| Manager intelligence (locked, code: 092018) | No existing equivalent |

---

## FILE STRUCTURE — Upload These to GitHub

```
argus-field/                    ← your new GitHub repository
├── index.html                  ← the entire app
├── manifest.json               ← PWA install config
├── sw.js                       ← offline engine
├── README.md                   ← this file
├── icons/
│   ├── icon-192.png            ← app icon
│   └── icon-512.png            ← app icon (large)
├── csw-files/                  ← auto-created when first CSW is uploaded
│   └── (PDF and JPEG files go here automatically)
├── csw-index.json              ← auto-created, do not edit manually
└── .github/
    └── workflows/
        └── notify.yml          ← email alert automation
```

---

## SETUP GUIDE — Do This Once

### Step 1 — Create a New GitHub Repository

1. Go to **github.com** → sign in as `arguslandengineering-cell`
2. Click **+** (top right) → **New repository**
3. Name: `argus-field`
4. Set to **Public**
5. Check **"Add a README file"**
6. Click **Create repository**

### Step 2 — Upload App Files

In your new repo, click **"Add file" → "Upload files"**

Upload these files to the **root folder**:
- `index.html`
- `manifest.json`
- `sw.js`
- `README.md`

### Step 3 — Upload Icons

1. Click **"Add file" → "Create new file"**
2. In the filename box, type: `icons/placeholder.txt`
3. Write anything in the body → click **"Commit changes"**
4. Go back to repo → **"Add file" → "Upload files"**
5. Upload `icon-192.png` and `icon-512.png` — GitHub will put them in `icons/`

### Step 4 — Set Up GitHub Actions (Email Alerts)

1. In your repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **"New repository secret"** — add these two:

| Name | Value |
|---|---|
| `MAIL_USERNAME` | `arguslandengineering@gmail.com` |
| `MAIL_PASSWORD` | Your Gmail App Password (see below) |

**Getting Gmail App Password:**
1. Go to **myaccount.google.com** → Security
2. Enable **2-Step Verification** if not yet active
3. Go to **App passwords** → Select app: Mail → Device: Other → type "GitHub"
4. Copy the 16-character password → use as `MAIL_PASSWORD`

### Step 5 — Upload the Workflow File

The `.github/workflows/` folder needs special handling:

1. In your repo → **"Add file" → "Create new file"**
2. In the filename box, type exactly: `.github/workflows/notify.yml`
3. Copy the entire content of `notify.yml` and paste it into the editor
4. Click **"Commit changes"**

### Step 6 — Enable GitHub Pages

1. In your repo → **Settings** → **Pages**
2. Source: **main** branch → folder: **/ (root)**
3. Click **Save**
4. Wait 2 minutes
5. Your app URL: `https://arguslandengineering-cell.github.io/argus-field`

### Step 7 — Generate Personal Access Token (PAT)

This lets the app upload CSW files directly from phones to GitHub.

1. GitHub → top-right avatar → **Settings**
2. Left sidebar → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. Click **"Generate new token (classic)"**
4. Note: `ARGUS FIELD Upload`
5. Expiration: **No expiration**
6. Check scope: ✅ **repo** (full repo access)
7. Click **Generate token**
8. **Copy the token immediately** — you cannot see it again
9. Format: `ghp_xxxxxxxxxxxxxxxxxxxx`

---

## APP CONFIGURATION — Do This After Setup

### Step 8 — Configure the App (Charles Only)

1. Open the app URL in Chrome on your phone
2. Go to **⚙️ Config tab**
3. Enter your name in **My Profile** → Save
4. Type `092018` in the Manager Code box → tap **Unlock**
5. In **GitHub Settings**, fill in:
   - Username: `arguslandengineering-cell`
   - Repository: `argus-field`
   - Token: paste your PAT from Step 7
   - Email: `arguslandengineering@gmail.com`
6. Tap **Save GitHub Config**
7. In **Team Roster**, verify the team list is correct
8. Assign each person their role and site

### Step 9 — Set Up Team Members (Each Person Does This)

Each team member does this once on their own phone:

1. Open the app URL in Chrome
2. Go to **⚙️ Config tab**
3. Type their name in **My Profile** → tap **Save My Profile**
4. Done — their role and site are set by Charles in the roster

---

## INSTALL ON PHONE

### Android (Chrome)
1. Open the app URL
2. Tap **⋮** (3-dot menu, top right)
3. Tap **"Add to Home screen"**
4. App installs with the ARGUS icon — no browser bar when opened from home screen

### iPhone (Safari)
1. Open the app URL in Safari
2. Tap the **Share** button (box with arrow)
3. Tap **"Add to Home Screen"**

### Convert to APK (for sharing via WhatsApp/USB)
1. Go to **pwabuilder.com**
2. Paste the app URL
3. Click **Package for stores → Android**
4. Download the `.apk` file
5. Share the APK — recipients install via Settings → Allow unknown sources

---

## HOW TO USE — Daily Operations

### Daily Check-in (Every Core Team Member, Every Day)

1. Open ARGUS FIELD → tap **✏️ UPDATE** (home screen button) or go to **📰 Daily tab**
2. Answer your 3 role-based questions (takes under 1 minute)
3. Pick your site status: 🟢 On Track / 🟡 Needs Attention / 🔴 Problem
4. Tap **✅ Submit Check-in**
5. Done — visible to the whole team immediately

**If you miss a day:** Your name appears with ⚫ on the dashboard — Charles will see it.

**Questions by role:**

| Role | Q1 | Q2 | Q3 |
|---|---|---|---|
| QA/Inspection | Inspections done today? | Pag-IBIG or doc issues? | What to check tomorrow? |
| QA/QC Head | Quality issues flagged? | BT or finishing progress? | System or procedure concerns? |
| BOM/Costing | BOM items processed? | Cost changes to flag? | Reports up to date? |
| Structural Eng | Design work done today? | Technical blocker? | Priority tomorrow? |
| Technical Head | Team status today? | Biggest bottleneck? | What needs decision today? |
| Site Engineer | What was done on site? | Delays or site problems? | Focus tomorrow? |

### Daily Digest (Charles Publishes After Check-ins)

1. Go to **📰 Daily tab → Team**
2. Tap **✨ Build Digest Prompt**
3. Tap **📋 Copy Digest Prompt**
4. Open Claude or any AI → paste prompt → copy the AI output
5. Go back to **📰 Daily tab → Digest**
6. Paste AI output into the publish box → tap **📢 Publish to All**
7. Everyone sees the digest on their Home screen

### Creating a New CSW

1. Tap **📋 CSW** (home screen button) or go to **📋 CSW tab → New**
2. Select type (Field Issue / Policy/System / Inter-Department)
3. Type the title — app checks for duplicates automatically
4. App shows detected owner (Angely / Ana / Gio / Oliver / Charles / Site-in-Charge)
5. Fill in Situation, Impact (optional), Recommendation (optional)
6. Tap **✨ Generate AI Prompt**
7. Tap **📋 Copy Prompt** → paste into Claude or any AI
8. Review the AI draft → print → route for signatures
9. Tap **💾 Save Draft** to track it while pending

### Uploading an Approved CSW

1. Get the signed CSW scanned as PDF or JPEG
2. Go to **📋 CSW tab → Upload**
3. Type the CSW number (or tap Auto)
4. Select status (Approved / Submitted / Rejected)
5. Tap **📄 Tap to choose PDF or photo** → select your file
6. Tap **📤 Upload to Archive**
7. Done — file stored in GitHub, Charles gets an email alert

### Updating CSW Status

1. Go to **📋 CSW tab → List**
2. Find the CSW → tap **✏️ Edit Status**
3. Select new status from dropdown
4. If Rejected: fill in the reason
5. If Revised: describe what changed
6. If Approved: set date + check if already implemented
7. Tap **✅ Save Status**

### Searching the Archive

1. Go to **📋 CSW tab → Search**
2. Type any keyword — title, site, owner, CSW number
3. Filter by status or type
4. Tap any result to see full details
5. Tap **📄 Open / Reprint Signed CSW** to open the file

---

## MANAGER FUNCTIONS (Code: 092018)

Enter `092018` in the Config tab → Manager Code box.

### Team Roster Management
- Add, edit, or remove team members
- Change roles — next check-in automatically shows new role's questions
- Generate **Team Composition Prompt** → AI suggests workload adjustments

### Ownership Keywords
- Edit keyword lists for each owner
- Generate **Discover New Keywords Prompt** → AI finds new terms from recent CSW data
- Paste AI output back → app updates keyword lists automatically

### Bottleneck Analysis (Charles Domain)
- See all items owned by Charles or unassigned
- Generate **Bottleneck Analysis Prompt** → AI writes a 2-paragraph analysis
- Paste AI output back → app applies tone/urgency adjustment to flag language

### Weekly Report
- Go to **📊 Report tab** (unlocked after entering manager code)
- Tap **✨ Build Weekly Prompt** → copy → paste into AI → get weekly narrative
- Paste result back for archive

### CSW Metadata Editing
- In **List tab**, tap **✏️ Edit Status** on any CSW
- Manager can override any field: status, rejection reason, revision notes, dates

---

## OWNERSHIP MATRIX

| Owner | Domain | Keywords (sample) |
|---|---|---|
| **Angely** | BOM, Cost, Materials | bom, cost, material, price, budget, estimate, payment, quote |
| **Ana** | QA/QC, Land Dev, Planning Systems | qa, quality, land development, drainage, survey, lot, policy, lgu, permit |
| **Gio** | Plan Details, Finishing Quality | ft, finishing, inspection, pag-ibig, coc, punch list, tile, paint, door, window |
| **Oliver** | Structural, Box Type Quality | bt, box type, structural, footing, beam, column, slab, rebar, concrete, retaining wall |
| **Site-in-Charge** | Site Implementation, Delays | manpower, equipment, weather, delay, excavation, contractor, delivery |
| **Charles** | Process, Efficiency, Escalations | process, efficiency, production, bottleneck, team, performance, management |

**Note:** Ownership tags are internal only — they never appear on printed CSW documents.

---

## CSW TYPE GUIDE

| Type | Use When | What AI Produces |
|---|---|---|
| **Field Issue** | One-time problem at a specific site | Corrective action memo with responsible party |
| **Policy/System** | New standing rule for all future occurrences | Policy document — once approved, cite CSW number for all future cases |
| **Inter-Department** | Action required from Finance, Admin, Sales, Legal, HR | Formal request with deadline and expected output |

**Key rule:** A Policy/System CSW approved by the President is a **permanent ruling**. For the same situation next time, staff cite the CSW number — no new CSW needed.

---

## SIGNATORY CHAIN (Locked — Same for All CSW)

| Role | Name |
|---|---|
| Prepared By | Staff member who created the CSW |
| Reviewed By | Reviewing Engineer |
| Noted By | Engr. Charles Rey B. Casiño — Technical Head |
| Approved By | Jose Edison O. Argayoso III / Edward V. Argayoso — President |

---

## LANGUAGE STANDARD

All app text and AI-generated CSW content uses **Grade 10 reading level**:
- Short sentences (max 20 words)
- No unexplained jargon
- Direct and clear — say what you mean
- Active voice where possible

---

## TROUBLESHOOTING

| Problem | Fix |
|---|---|
| Upload fails | Check Config → GitHub settings. Token, username, and repo must be exact |
| Sync failed | Check internet. Repo must be Public. Run sync again |
| No email on upload | Check GitHub Actions tab for errors. Verify MAIL_PASSWORD secret |
| Check-in not showing | Check if profile name is set in Config |
| Manager code not working | Use `092018` — no spaces, no quotes |
| App not working offline | Open once on WiFi first to cache. Then works offline |
| Wrong questions showing | Charles updates your role in Config → Team Roster |
| Duplicate warning on every CSW | Expected behavior — it's a warning, not a block. Proceed if it's truly different |

---

## SUSTAINABILITY

| Item | Status |
|---|---|
| GitHub storage | Free — unlimited for documents this size |
| GitHub Pages (app hosting) | Free |
| GitHub Actions (email alerts) | Free — 2,000 minutes/month |
| Offline support | Built-in — no internet needed to draft or search cached data |
| APK distribution | Free via pwabuilder.com |
| API calls | None — no recurring costs |
| Token refresh | Every 12 months recommended — 5 minutes to update |

---

*ArgusLand Planning & Engineering Department*
*ARGUS FIELD v2.0 · Built for field-first, offline-capable operations*
