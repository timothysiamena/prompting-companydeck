# MASTER PROMPT — Company Intelligence Slide (Reverse Engineered)
### One-Page Scrollable HTML Intelligence Brief · Consulting Style · 1920px Wide
**Author:** Timothy Isaac Siamena · **Template Version:** 1.1 · **Base Company:** Mola TV (Djarum Group)

---

## HOW TO USE THIS PROMPT

Copy everything between the `---PROMPT START---` and `---PROMPT END---` markers below into a new Claude/GPT/Gemini/Yuanbao/etc. chat. Replace every instance of `[COMPANY_NAME]`, `[PARENT_GROUP]`, `[TICKER_1]`, `[TICKER_2]`, `[INDUSTRY]`, `[STATUS]`, and `[YEAR]` with your target company. Everything else such as layout, design, color system, section order, intelligence framework should stays identical.

---PROMPT START---

# TASK: Build a Company Intelligence HTML Slide

You are a senior investment analyst and intelligence researcher. Build a **single-file, fully self-contained HTML intelligence brief** for the company below. The output must be a professionally designed, consulting-style dense information page that can be used for investment analysis, competitive intelligence, or strategic review.

## TARGET COMPANY
- **Company:** [COMPANY_NAME]
- **Parent / Owner:** [PARENT_GROUP]
- **Primary Listed Entity (IDX ticker 1):** [TICKER_1] (e.g., parent holding company)
- **Secondary Listed Entity (IDX ticker 2):** [TICKER_2] (e.g., operating subsidiary, if any)
- **Industry / Vertical:** [INDUSTRY] (e.g., OTT Streaming, Fintech, E-commerce)
- **Market / Region:** Indonesia (primary), Southeast Asia (secondary)
- **Operational Status:** [STATUS] (Active / Closed / Restructuring)
- **Analysis Year:** [YEAR]

---

## PHASE 1 — RESEARCH (Do this before writing any HTML)

Conduct deep research on [COMPANY_NAME] across the following dimensions. For EVERY fact you include in the HTML, you must have a real source URL ready to embed as a blue hyperlink inline in the text. Do NOT cite a company's main homepage as proof of a data point — find the specific article, report, or announcement page.

### 1A — Company & Product Research
- What products or services does [COMPANY_NAME] offer? List all sub-brands, tiers, platforms
- What are their primary content/service categories (sports rights, original content, licenses)?
- Who are their direct and indirect competitors in Indonesia?
- What is their subscriber/user count, market share, and growth trajectory?
- What key partnerships or distribution deals exist?
- Has the company undergone any closures, restructuring, pivots, or M&A? Note exact dates.

### 1B — Financial Research
Search IDX portal for listed parent entities. Start at:
`https://www.idx.co.id/en/listed-companies/financial-statements-and-annual-report/`
Search by ticker [TICKER_1] and [TICKER_2]. Also check company investor relations pages.

Extract for the most recent full fiscal year (FY 2024 preferred):
- Total Revenue — **convert to USD** (see Currency Rule below)
- COGS / Cost of Revenue — **convert to USD**
- Gross Profit + Gross Margin %
- EBITDA + EBITDA Margin %
- Net Income + Net Margin %
- Any specific segment data for [COMPANY_NAME]'s division (subscription revenue, digital segment, etc.)
- **IT/Technology Spend line item** — search PDF for keywords: "Teknologi Informasi", "Infrastruktur", "Sistem Informasi"
- **If IT spend not found:** Use **8% of COGS** as the industry estimate (Gartner benchmark for media/tech companies)

For PRIVATE companies (no IDX listing): Note as private, use third-party revenue estimates (Owler, Crunchbase, ZoomInfo) and label clearly as estimates.

Save the direct PDF download URL for each annual report.

### 1C — Cloud / Technology Infrastructure Research
For each competitor platform (and [COMPANY_NAME] itself):
- Primary cloud provider (AWS, Google Cloud, Azure, Alibaba Cloud, Tencent Cloud, Local/Telkom)
- CDN provider
- Any confirmed public announcements (press releases, AWS case studies, summit presentations)
- Tencent Cloud specific: What % of this platform's cloud workloads run on Tencent Cloud?

**IMPORTANT RULES FOR CLOUD MARKET SHARE:**
- Do NOT assign a specific percentage to any provider unless you can derive it via bottoms-up calculation OR find a published source
- Bottoms-up method: (Platform's estimated % of total OTT cloud spend) × (% of that platform on each provider) = weighted contribution. Calculation comes from how big the clients are in each market/
- Show ranges (e.g., ~55–62%) not point estimates when uncertain
- Clearly label all figures as "Bottoms-up estimate — no public IDC/Canalys report covers this breakdown"
- The 8% COGS rule applies to IT spend only, not to market share

### 1D — News Intelligence Research (Last 3–6 months minimum, expand to 2 years for context)
Search across:
- **Indonesian news:** Kompas Tekno, CNN Indonesia, Detik.com, ANTARA News, VOI.id, Bisnis Indonesia
- **English business news:** DealStreet Asia, Nikkei Asia, Reuters, Bloomberg, TechNode Global
- **Industry publications:** Media Partners Asia (MPA), SportBusiness, Sportcal, Variety, Deadline
- **Social signals:** LinkedIn (leadership posts, hiring), Reddit/Kaskus (user sentiment), Twitter/X
- **Official announcements:** Company press releases, investor relations pages

Extract: Strategic signals, financial signals, competitive signals, reputation risks, market opportunities. Rank from highest to lowest strategic impact.

### 1E — Source Validation Rules
- Every number must have a clickable blue hyperlink `<a href="URL" target="_blank" style="color:#0055cc;">source ↗</a>` embedded inline
- Do NOT create a separate "Sources" section — embed links directly in the sentence where the data appears
- If a number is unverifiable, either remove it or clearly label it as an estimate with methodology explained
- Never cite a company's main homepage (e.g., company.com) as proof of a specific data point

---

## PHASE 2 — HTML CONSTRUCTION

Build ONE fully self-contained HTML file. No external CSS files, no external JS. Inline everything.

### FILE STRUCTURE
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=1920">
  <title>[COMPANY_NAME] — [PARENT_GROUP] Analysis</title>
  <style>
    [ALL CSS HERE — see Design System below]
  </style>
</head>
<body>
  [1] STICKY TOPBAR
  [2] MAIN BODY (CSS Grid)
      [2a] LEFT SIDEBAR
      [2b–2g] SIX PANELS (3 cols × 2 rows)
      [2h] CLOUD INFRASTRUCTURE SECTION (full-width)
      [2i] PLATFORM FINANCIALS & IT SPEND (full-width)
      [2j] NEWS KEY FINDINGS — INTELLIGENCE BRIEF (full-width)
  [3] FIXED FOOTER
  [UI] FIXED UI OVERLAY — zoom · scroll · translate (top-right, always on top)
</body>
</html>
```

---

## DESIGN SYSTEM — COPY THESE EXACTLY

### Typography
```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');
font-family: 'Inter', sans-serif;
```

### Page Dimensions
```css
html, body {
  width: 1920px;
  overflow-x: hidden;
  overflow-y: auto;
  background: #ffffff;
  color: #1a2035;
}
```

### Color Tokens
```
Background (page):          #ffffff
Background (sidebar):       #fafbfe
Background (panel alt):     #f4f6fb
Background (section header alt): #fafbfe

Text primary:               #0a1020
Text secondary:             #1a2a44
Text muted:                 #5a6a88 / #8a9ab8
Text placeholder:           #9aaabb / #c0cce0

Border default:             rgba(0,20,80,0.07)
Border medium:              rgba(0,20,80,0.08)
Border heavy:               rgba(0,20,80,0.1) / rgba(0,20,80,0.12)
Sidebar border:             1.5px solid rgba(0,20,80,0.08)

Accent blue (primary):      #0044cc / #0055cc / #1a6aff
Accent blue (light):        #0088ff
Accent text:                #0033cc / #003388
Accent background:          rgba(0,80,220,0.04–0.09)
Accent border:              rgba(0,80,220,0.14–0.2)

Warning orange:             #aa4400 / #dd6600
Warning background:         rgba(200,80,0,0.06–0.09)

Danger red:                 #bb1111 / #aa1111 / #cc2222
Danger background:          rgba(200,30,30,0.08–0.1)

Success green:              #006633 / #005522 / #44aa77
Success background:         rgba(0,160,80,0.08–0.09)

Purple:                     #6622aa / #9922bb
Yellow:                     #7a5500 / #aa6600
Gray:                       #5a6a88
```

### Tag System (topbar category pills)
```css
.tag {
  padding: 3px 11px;
  border-radius: 20px;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.4px;
  text-transform: uppercase;
  white-space: nowrap;
}
.tag-blue   { background: rgba(0,100,220,0.09);  color: #0055bb; border: 1px solid rgba(0,100,220,0.18); }
.tag-orange { background: rgba(210,90,0,0.09);   color: #aa4400; border: 1px solid rgba(210,90,0,0.18); }
.tag-green  { background: rgba(0,160,80,0.09);   color: #006633; border: 1px solid rgba(0,160,80,0.18); }
.tag-red    { background: rgba(200,30,30,0.09);  color: #aa1111; border: 1px solid rgba(200,30,30,0.18); }
.tag-purple { background: rgba(110,50,200,0.09); color: #6622aa; border: 1px solid rgba(110,50,200,0.18); }
.tag-yellow { background: rgba(180,130,0,0.09);  color: #7a5500; border: 1px solid rgba(180,130,0,0.18); }
.tag-gray   { background: rgba(0,20,60,0.06);    color: #5a6a88; border: 1px solid rgba(0,20,60,0.11); }
```

### Status Badge (top-right of topbar)
- If company is **CLOSED:** `background: rgba(200,30,30,0.08); border: 1px solid rgba(200,30,30,0.25); color: #bb1111;` — text: "CLOSED [MONTH YEAR]"
- If company is **ACTIVE:** `background: rgba(0,160,80,0.08); border: 1px solid rgba(0,160,80,0.2); color: #006633;` — text: "ACTIVE"
- If company is **RESTRUCTURING:** use yellow/orange

---

## SECTION-BY-SECTION SPECIFICATIONS

### [1] STICKY TOPBAR
```
Height: 66px
Position: sticky, top: 0, z-index: 100
Background: #ffffff
Border-bottom: 1.5px solid rgba(0,20,80,0.1)
Padding: 0 36px
Layout: flex, align-items center, gap 12px
```

**Contents (left to right):**
1. Logo block: 30×30px rounded square with gradient `linear-gradient(135deg, #0088ff, #0055cc)`, letter initial of company, font-size 14px weight 900 white. Beside it: company name (18px, weight 800, #0a1020, letter-spacing -0.5px) and sub-label (11px, #7a90b0, weight 500)
2. Vertical divider: 1px × 28px, rgba(0,20,80,0.12)
3. Category tags: Use `.tag` classes. Choose relevant categories for [COMPANY_NAME]. Typical: Sports · OTT · Streaming · Media · Fintech · E-Commerce · Telecom · etc.
4. Right side (`margin-left: auto`): Brief subtitle text (11px, #9aaac0) then status badge

> **Note:** Leave enough right-side clearance (~340px) for the fixed UI overlay (zoom/scroll/translate controls) which sits at `position:fixed; top:12px; right:20px` above the topbar visually.

---

### [2] MAIN BODY — CSS GRID
```css
.main-body {
  display: grid;
  grid-template-columns: 320px 1fr 1fr 1fr;
  grid-template-rows: auto auto;
  padding-bottom: 80px;
  min-height: calc(100vh - 66px - 64px);
}
```

**Panel base class:**
```css
.panel {
  padding: 20px 22px;
  border-right: 1px solid rgba(0,20,80,0.07);
  border-bottom: 1px solid rgba(0,20,80,0.07);
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow: visible;
}
```

**Panel title (section label above each panel):**
```css
.panel-title {
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 1.3px;
  text-transform: uppercase;
  color: #8a9ab8;
  display: flex;
  align-items: center;
  gap: 6px;
  margin-bottom: 2px;
}
/* Horizontal rule that auto-extends to fill remaining width */
.panel-title::after {
  content: '';
  flex: 1;
  height: 1px;
  background: rgba(0,20,80,0.08);
}
```

---

### [2a] LEFT SIDEBAR — grid-column:1, grid-row: 1/3
```css
.sidebar {
  grid-column: 1;
  grid-row: 1 / 3;
  background: #fafbfe;
  padding: 24px 20px;
  border-right: 1.5px solid rgba(0,20,80,0.08);
  display: flex;
  flex-direction: column;
  gap: 14px;
}
```

**Sidebar contents (top to bottom):**

**A) Logo box:**
```css
background: linear-gradient(135deg, #e8f2ff 0%, #d4e8ff 100%);
border: 1px solid rgba(0,100,220,0.18);
border-radius: 12px;
padding: 18px;
```
Contains: 56×56px circle logo (`border-radius:50%`, gradient `#0055cc→#0088ff`, box-shadow), company name (19px, weight 900, #0a1020, letter-spacing -0.5px), sub-description (10px, #3366aa, text-align center)

**B) Stat row:** Two or three side-by-side `.stat-box` cards
```css
.stat-box { flex:1; background:#fff; border:1px solid rgba(0,20,80,0.09); border-radius:8px; padding:9px 6px; text-align:center; }
.stat-val  { font-size:15px; font-weight:800; color:#0a1020; }
.stat-lbl  { font-size:8.5px; color:#9aaabb; font-weight:600; letter-spacing:0.3px; margin-top:2px; }
```
Put: Subscriber count / market share / key metric

**C) Info block (key-value table):**
```css
background: #fff; border-radius: 8px; border: 1px solid rgba(0,20,80,0.08); padding: 11px 13px;
```
Rows: `.info-row` with `.info-key` (8a9ab8, weight 600) and `.info-val` (1a2a44, weight 500, text-align right).
Include: Founded, Owner/Parent, HQ, Industry, Status, Ticker(s), Listed Exchange

**D) Failure Signal / Risk Alert box** (if company is closed or distressed):
```css
background: rgba(200,30,30,0.05);
border: 1px solid rgba(200,30,30,0.18);
border-radius: 8px;
padding: 11px 13px;
border-left: 3px solid #cc2222;
```
Title: "⚠ Failure Signal" (9px, weight 700, uppercase, #bb2222)
Body: Key reason for closure or distress in 2–3 bullet points (8.5px, #883333)

---

### [2b] PANEL A — Products & Services
```
grid-column: 2; grid-row: 1
```
Panel title: "Products & Channels" or "Services & Platforms"

**Product grid:** CSS Grid, `grid-template-columns: repeat(2, 1fr)` or repeat(3,1fr), gap 8px.
Each product card:
```css
background: #f8faff;
border: 1px solid rgba(0,20,80,0.07);
border-radius: 8px;
padding: 10px 11px;
border-top: 2px solid [accent color per product];
```
Card contains: product icon/initial in colored square (18×18px, border-radius 5px), product name (10.5px, weight 700, #1a2a44), type tag (8px, weight 600, rounded), description (9.5px, #8a9ab8, line-height 1.4).

---

### [2c] PANEL B — Content Rights / IP Portfolio
```
grid-column: 3; grid-row: 1
```
Panel title: "Sports Rights Portfolio" / "Content Rights" / "IP Assets"

**Rights list:** Vertical flex, gap 6px.
Each right item:
```css
background: #f8faff;
border: 1px solid rgba(0,20,80,0.07);
border-radius: 7px;
padding: 8px 11px;
display: flex; align-items: flex-start; gap: 10px;
```
Left: colored icon square (20×20px). Right: right name (10.5px, weight 700), detail line (8.5px, #8a9ab8), status badge (8px pill: green=Active, yellow=Expired, red=Lost, gray=Never).

**Status badge colors:**
```css
.s-active  { background:rgba(0,160,80,0.09); color:#006633; border:1px solid rgba(0,160,80,0.18); }
.s-expired { background:rgba(180,130,0,0.09); color:#7a5500; border:1px solid rgba(180,130,0,0.2); }
.s-lost    { background:rgba(200,30,30,0.09); color:#aa1111; border:1px solid rgba(200,30,30,0.18); }
.s-never   { background:rgba(0,20,60,0.06);  color:#9aaabb; border:1px solid rgba(0,20,60,0.11); }
```

---

### [2d] PANEL C — Timeline / History
```
grid-column: 4; grid-row: 1
```
Panel title: "Rights Timeline" / "Company Timeline" / "Key Milestones"

> **⚠ ORDERING RULE — Latest → Oldest:** Always render timeline entries with the **most recent year at the TOP** and the oldest year at the **BOTTOM** (reverse chronological order). Never render oldest-to-newest. Add a small `"Latest → Oldest"` label in 8px #c0cce0 muted text directly above the first entry.

**Timeline:** Vertical flex. Each entry:
```css
display: flex; gap: 10px; padding-bottom: 8px;
border-left: 1.5px solid rgba(0,20,80,0.1); /* continuous left line */
padding-left: 14px;
position: relative;
```
Dot marker (position absolute, left -5px):
```css
width:9px; height:9px; border-radius:50%; background:[color by status]; border:1.5px solid #fff;
```
Year label (10px, weight 800, #0a1020), title (10.5px, weight 700, #1a2a44), detail text (9.5px, #9aaabb, line-height 1.45).

Color-code dot by significance: blue=major win, green=launch, red=loss/closure, gray=neutral.

---

### [2e] PANEL D — Market Analysis
```
grid-column: 2; grid-row: 2
```
Panel title: "Indonesia Market" / "Market Position"

**Highlight box** (key market stat):
```css
background: linear-gradient(135deg, rgba(0,100,220,0.06), rgba(0,60,180,0.03));
border: 1px solid rgba(0,100,220,0.12);
border-radius: 8px;
padding: 10px 12px;
```
Big number (20px, weight 900, #0044cc), label below (9px, #4477aa).

**Market share bars:** Horizontal bar charts for each competitor.
```
.bar-row: display flex, align-items center, gap 8px, margin-bottom 6px
.bar-track: flex 1, height 6px, background #f0f2f8, border-radius 3px
.bar-fill: height 100%, border-radius 3px, background gradient
.bar-label: 10px, weight 600, #4a5a78, width 120px
.bar-val: 10px, weight 600, #4a5a78, width 38px, text-align right
```

---

### [2f] PANEL E — Competitor Landscape
```
grid-column: 3; grid-row: 2
```
Panel title: "Competitor Landscape"

**Competitor cards:** Vertical flex, gap 8px.
Each card:
```css
background: #f8faff;
border: 1px solid rgba(0,20,80,0.07);
border-radius: 8px;
padding: 9px 11px;
```
Layout: flex row. Left icon (24×24px colored square, border-radius 7px, 2-letter abbrev, weight 900). Right: name (10.5px, weight 700) + description line (9px, #8a9ab8) + badge row.

**Badge types per competitor:**
- Type tag: "OTT", "FTA TV", "Pay TV", "OTT+PayTV" — use `.tag` colors
- Main interests: 8px gray pills
- Cloud provider: 8px blue pill
- Threat level: "High" (red), "Medium" (orange), "Low" (green) — positioned right

---

### [2g] PANEL F — Forward Outlook / Strategic Analysis
```
grid-column: 4; grid-row: 2
```
Panel title: "2026 Outlook" / "Strategic Outlook" / "Forward View"

**Outlook cards:** Vertical flex, gap 8px.
Each card:
```css
background: #f8faff;
border: 1px solid rgba(0,20,80,0.07);
border-radius: 8px;
padding: 10px 12px;
border-left: 3px solid [color];
```
Title (11px, weight 700), description (9px, #5a6a88, line-height 1.45). Left border color:
- Opportunity = #44aa77 (green)
- Risk = #dd6600 (orange)
- Threat = #cc2222 (red)
- Neutral = #9aaabb (gray)

---

### [2h] CLOUD INFRASTRUCTURE SECTION — Full-width
```css
grid-column: 1 / -1;
width: 100%;
border-top: 2px solid rgba(0,20,80,0.08);
background: #fff;
```

**Section header:**
```css
display: flex; align-items: center; gap: 14px;
padding: 18px 36px 14px;
border-bottom: 1px solid rgba(0,20,80,0.07);
background: #fafbfe;
```
Left: 34×34px icon box (gradient blue, border-radius 9px, ☁️ emoji). Title (15px, weight 900, #0a1020, letter-spacing -0.3px). Subtitle (10.5px, #9aaabb). Right: pill badges (status, market share estimate).

**Three-column inner grid:**
```css
display: grid;
grid-template-columns: 400px 1fr 520px;
min-height: 480px;
```

**COL 1 — Platform Cloud Map table (400px)**
Padding: 20px 22px. Section label (9px, uppercase, 1.3px tracking, #8a9ab8).

Table header row: `grid-template-columns: 150px 1fr 80px`, 3 columns: Platform | Primary / Secondary Cloud | TCloud %

Table rows: `grid-template-columns: 150px 1fr 80px`
- Col 1: icon (20×20px colored square, 5px radius) + name (10px, weight 700) + type subtitle (8px, #9aaabb)
- Col 2: primary cloud name + secondary cloud name
- Col 3: Tencent Cloud % in highlighted background

Row colors:
- Normal: `background: #f8faff; border: 1px solid rgba(0,20,80,0.08);`
- Mola/Closed company: `background: rgba(200,30,30,0.03); border: 1px solid rgba(200,30,30,0.1);`

**COL 2 — Cloud Market Share Bars (1fr)**
Padding: 20px 28px. Section label.

**Methodology box (place ABOVE bars):**
```css
background: #fffbf0;
border: 1px solid rgba(200,140,0,0.25);
border-radius: 8px;
padding: 9px 12px;
margin-bottom: 12px;
```
Title: "📐 Methodology — How These Ranges Were Derived" (8.5px, weight 700, #996600, uppercase).
Body: Explain the 3-step bottoms-up process: (1) Platform→cloud mapping from public announcements, (2) workload weight estimation from subscriber counts & traffic type, (3) cross-multiply to derive provider share ranges. End with warning that these are estimates.

**Bar entries (for each cloud provider):**
```
flex column, gap 10px
each entry: flex row, justify-content space-between, margin-bottom 4px
icon: 10×10px square, border-radius 3px, provider color
provider name: 11px, weight 700, #1a2a44
clients list: 9px, #9aaabb
range: 12px, weight 900, provider color
bar track: height 8px, background #f0f2f8, border-radius 4px
bar fill: width = midpoint %, gradient using provider color
description: 8px, #c0cce0, margin-top 3px
```

Highlight the FOCUS provider (e.g., Tencent Cloud) with:
```css
background: rgba(0,80,220,0.04);
border: 1.5px solid rgba(0,80,220,0.2);
border-radius: 9px;
padding: 10px 12px;
```

**References box (below bars):**
```css
background: #f8faff; border: 1px solid rgba(0,20,80,0.07); border-radius: 7px; padding: 10px 12px;
```
Title: "References & Sources" (8px, weight 700, uppercase, #8a9ab8).
Body: Numbered `[¹]` through `[N]` footnotes. Each = claim description + blue hyperlink to source. Font: 7.8px, #9aaabb, line-height 1.65.

**COL 3 — Cloud Opportunity Analysis (520px)**
Background: #fafbff. Section label.

Sections:
1. "✓ Current Wins" (9px, weight 700, #0044cc, uppercase) — cards with blue left border
2. "↗ Growth Opportunities" (9px, weight 700, #aa6600, uppercase) — cards with orange left border
3. "🇮🇩 [Country] Cloud Footprint" — 2×2 stat grid
   ```css
   background: rgba(0,60,200,0.05); border: 1px solid rgba(0,60,200,0.15); border-radius: 8px; padding: 10px 12px;
   ```

Cards:
```css
background: #fff;
border: 1px solid rgba(0,80,220,0.14);
border-radius: 7px;
padding: 9px 11px;
border-left: 3px solid [blue or orange];
```
Title: 10.5px, weight 700, #0033cc. Body: 9px, #5577aa, line-height 1.4.

---

### [2i] PLATFORM FINANCIALS & IT SPEND — Full-width
```css
grid-column: 1 / -1;
width: 100%;
border-top: 2px solid rgba(0,20,80,0.08);
background: #fff;
```

**Section header:**
```css
background: #fafbfe; padding: 18px 36px 14px; border-bottom: 1px solid rgba(0,20,80,0.07);
```
Icon: 💰 on green gradient. Title: "Platform Financials & Estimated IT Spend". Subtitle: mention IDX annual reports, 8% COGS rule, FY year. **Note in subtitle: "All figures in USD."**

**Three-column cards grid:**
```css
padding: 20px 36px;
display: grid;
grid-template-columns: repeat(3, 1fr);
gap: 16px;
```

**Card type 1 — IDX Listed Company (main subject / [TICKER_1])**
```css
background: #f8faff;
border: 1.5px solid rgba(0,80,200,0.15);
border-radius: 10px;
overflow: hidden;
```
Header: blue gradient bg, ticker badge (bg: rgba(0,168,224,0.12), color: #0077bb), company name (12px, weight 800), parent/subsidiary note.

Four 2×2 metric boxes inside:
```css
display: grid; grid-template-columns: 1fr 1fr; gap: 8px;
```
Metrics: Est. Revenue | Net Income (confirmed) | COGS (derived) | **Est. IT Spend** (highlighted in blue).
All values in USD — show local currency in small muted text below each figure.

IT Spend box style (highlighted):
```css
background: rgba(0,80,200,0.06);
border: 1.5px solid rgba(0,80,200,0.2);
border-radius: 7px;
padding: 8px 10px;
```

Margin badges row: Gross Margin %, EBITDA Margin %, Net Margin % — green pills.

Report access box (bottom of card):
```css
background: #f0f4ff; border: 1px solid rgba(0,60,200,0.1); border-radius: 7px; padding: 8px 10px;
```
Content: IDX portal link → "search ticker: [TICKER]" → "Annual Report [YEAR]" + direct investor relations URL + PDF keyword guide ("In PDF: Search 'Pendapatan' (Revenue) · 'Beban Pokok' (COGS) · 'Teknologi Informasi' (IT)")

**Card type 2 — IDX Listed Company ([TICKER_2] / operating subsidiary)**
Same structure but with orange/amber color scheme (`rgba(200,90,0,...)`). Include any segment-specific revenue line (e.g., Subscription Revenue, Digital Segment).

**Card type 3 — Private / Foreign Companies**
Red/dark color scheme. Show multiple sub-sections for beIN Sports (private), WeTV/Tencent (HKEX), Netflix (NASDAQ). For each: global revenue in USD, IT spend estimate (global only, note Indonesia not disclosed), links to HKEX or SEC filings where available.

**IT Spend Summary Bar (bottom, full-width within section):**
```css
background: #f4f6fb;
border: 1px solid rgba(0,20,80,0.08);
border-radius: 8px;
padding: 12px 18px;
```
Horizontal bar per company: name (120px fixed) + bar track (flex:1) + value in USD (180px fixed) + note.
Footer note: Explain 8% COGS benchmark and how to find actual IT spend in annual report PDFs.

---

### [2j] NEWS KEY FINDINGS — Full-width
```css
grid-column: 1 / -1;
width: 100%;
border-top: 2px solid rgba(0,20,80,0.08);
background: #fafbfe;
```

**Section header — DARK BACKGROUND (contrasting from rest of page):**
```css
background: linear-gradient(135deg, #0a1020, #0f1a30);
padding: 18px 36px 14px;
border-bottom: 1px solid rgba(0,20,80,0.07);
```
Icon: 📡 on red gradient. Title (15px, weight 900, **#fff**). Subtitle (10.5px, **#7a9acc**). Right: "Closed [DATE]" red pill + "N Signals Extracted" blue pill.

**Keyword clusters strip — DARK BACKGROUND:**
```css
background: #0e1628;
padding: 10px 36px;
border-bottom: 1px solid rgba(255,255,255,0.06);
display: flex; align-items: center; gap: 10px; flex-wrap: wrap;
```
Label: "Keyword Clusters Scanned →" (8px, weight 700, #4a6a99, uppercase).
Pills (3 color groups):
- Core brand terms: `background:rgba(0,80,200,0.2); color:#88aaee; border:1px solid rgba(0,80,200,0.25);`
- Risk/closure terms: `background:rgba(200,60,0,0.2); color:#ff9966; border:1px solid rgba(200,60,0,0.25);`
- Market/competitor terms: `background:rgba(0,160,80,0.18); color:#66dd99; border:1px solid rgba(0,160,80,0.25);`

**Main intelligence grid:**
```css
display: grid;
grid-template-columns: 1fr 420px;
min-height: 560px;
```

**LEFT — Ranked Signal List:**
Padding: 20px 30px. Section label.
9 signal cards minimum, ordered by strategic impact.

Each signal card:
```css
background: #fff;
border: 1px solid rgba(0,20,80,0.08);
border-radius: 9px;
padding: 11px 14px;
border-left: 4px solid [priority color];
```

Priority color system for left border + rank badge background:
- #1–2: `#cc2222` (critical/red) — strategic collapse, existential risks
- #3–4: `#dd6600` (orange) — competitive dynamics, significant market changes
- #5–6: `#0066cc` (blue) — strategic opportunities, market structure
- #7–8: `#999999` (gray) — weak signals, reputation, watch items
- #9: `#44aa77` (green) — opportunity / positive signal

Rank badge (inside card):
```css
background: [priority color]; color: #fff; border-radius: 5px;
padding: 2px 7px; font-size: 8px; font-weight: 900; flex-shrink: 0;
```

Category tag (pill beside title):
```css
border-radius: 8px; padding: 1px 7px; font-size: 7.5px; font-weight: 700;
```
Tag colors: STRATEGY=red, COMPETITION=orange, MARKET=green, REPUTATION RISK=red, WEAK SIGNAL=gray, OPPORTUNITY=green

Card body: 9px, #3a4a64, line-height 1.5. Bold key data points.
Impact line (below body): 8px, weight 600, muted version of priority color. Blue hyperlinks `[Source name ↗]` inline.

**RIGHT — Synthesis Panel (420px):**
Background: #fafbfe. Padding: 20px 22px. Section label.

Five synthesis categories (in this order):
1. Strategy & Direction — red header (`#cc2222`)
2. Financial & Operational Health — orange header (`#dd6600`)
3. Reputation & Risk — purple header (`#9922bb`)
4. Product & User Experience — blue header (`#0066cc`)
5. Market Perception & Narrative — green header (`#44aa77`)

Each category block:
```css
margin-bottom: 12px;
```
Header: 8.5px, weight 700, uppercase, letter-spacing 0.8px, with 8×8px colored square dot.
Body card:
```css
background: #fff;
border: 1px solid rgba([category color rgb], 0.1);
border-radius: 7px;
padding: 9px 11px;
font-size: 8.5px; color: #3a4a64; line-height: 1.55;
```
Inline hyperlinks where relevant.

---

### [3] FIXED FOOTER
```css
.bottombar {
  position: fixed;
  bottom: 0;
  width: 1920px;
  height: 64px;
  background: #ffffff;
  border-top: 1.5px solid rgba(0,20,80,0.09);
  display: flex;
  align-items: center;
  padding: 0 36px;
  gap: 0;
  z-index: 90;
  box-shadow: 0 -2px 12px rgba(0,20,80,0.05);
}
.key-metrics { display: flex; gap: 0; flex: 1; }
.metric-item {
  flex: 1; text-align: center;
  padding: 8px 12px;
  border-right: 1px solid rgba(0,20,80,0.07);
}
.metric-item:last-child { border-right: none; }
.metric-val { font-size: 18px; font-weight: 900; color: #0a1020; }
.metric-lbl { font-size: 9px; color: #9aaabb; font-weight: 600; letter-spacing: 0.3px; margin-top: 2px; }
```

**Include 7 key metrics** relevant to [COMPANY_NAME]. Examples:
- Revenue in USD / "Closed" (red #cc2222 if applicable)
- Total subscriber count
- Primary market share metric
- Key rights or assets
- A competitive market metric
- A financial metric
- Year of analysis or key date

---

### [UI] FIXED UI OVERLAY — Top-Right Corner, Always Visible

Add this block **immediately before the closing `</body>` tag**. It is `position: fixed` and never scrolls. Sits at `top: 12px; right: 20px; z-index: 9999` — always above the topbar and all content.

**Three pill groups in a flex row:** Translate → Scroll → Zoom

```html
<!-- ═══ FIXED UI CONTROLS (top-right, static) ═══ -->
<div id="ui-overlay" style="position:fixed;top:12px;right:20px;z-index:9999;display:flex;align-items:center;gap:8px;">

  <!-- TRANSLATE: 2 language buttons + EN restore -->
  <div style="display:flex;align-items:center;gap:4px;background:#fff;border:1px solid rgba(0,20,80,0.15);border-radius:22px;padding:4px 10px;box-shadow:0 2px 8px rgba(0,20,80,0.1)">
    <span style="font-size:9px;font-weight:700;color:#8a9ab8;letter-spacing:0.5px;margin-right:4px">🌐</span>
    <button onclick="setLang('en')" id="btn-en" style="font-size:10px;font-weight:700;padding:3px 9px;border-radius:14px;border:none;cursor:pointer;background:rgba(0,80,220,0.12);color:#0044cc">EN</button>
    <button onclick="setLang('th')" id="btn-th" style="font-size:10px;font-weight:700;padding:3px 9px;border-radius:14px;border:none;cursor:pointer;background:transparent;color:#8a9ab8">TH</button>
    <button onclick="setLang('id')" id="btn-id" style="font-size:10px;font-weight:700;padding:3px 9px;border-radius:14px;border:none;cursor:pointer;background:transparent;color:#8a9ab8">ID</button>
  </div>

  <div style="width:1px;height:22px;background:rgba(0,20,80,0.1)"></div>

  <!-- SCROLL LEFT / RIGHT -->
  <div style="display:flex;align-items:center;gap:4px;background:#fff;border:1px solid rgba(0,20,80,0.15);border-radius:22px;padding:4px 8px;box-shadow:0 2px 8px rgba(0,20,80,0.1)">
    <button onclick="window.scrollBy({left:-500,behavior:'smooth'})" title="Scroll Left" style="font-size:13px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">‹</button>
    <span style="font-size:9px;color:#c0cce0;font-weight:600">scroll</span>
    <button onclick="window.scrollBy({left:500,behavior:'smooth'})" title="Scroll Right" style="font-size:13px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">›</button>
  </div>

  <div style="width:1px;height:22px;background:rgba(0,20,80,0.1)"></div>

  <!-- ZOOM IN / OUT / RESET -->
  <div style="display:flex;align-items:center;gap:4px;background:#fff;border:1px solid rgba(0,20,80,0.15);border-radius:22px;padding:4px 8px;box-shadow:0 2px 8px rgba(0,20,80,0.1)">
    <button onclick="adjustZoom(-0.1)" title="Zoom Out" style="font-size:14px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">−</button>
    <span id="zoom-label" style="font-size:9px;font-weight:700;color:#4a5a78;min-width:34px;text-align:center">100%</span>
    <button onclick="adjustZoom(+0.1)" title="Zoom In" style="font-size:14px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">+</button>
    <button onclick="resetZoom()" title="Reset" style="font-size:9px;font-weight:700;padding:2px 8px;border-radius:12px;border:none;cursor:pointer;background:rgba(0,20,80,0.06);color:#8a9ab8">↺</button>
  </div>

</div>

<!-- Google Translate hook (hidden) -->
<div id="google_translate_element" style="display:none"></div>

<script>
// ── ZOOM ────────────────────────────────────────────────
var currentZoom = 1.0;
function adjustZoom(delta) {
  currentZoom = Math.min(2.0, Math.max(0.4, currentZoom + delta));
  document.body.style.transform = 'scale(' + currentZoom + ')';
  document.body.style.transformOrigin = 'top left';
  document.getElementById('zoom-label').textContent = Math.round(currentZoom * 100) + '%';
}
function resetZoom() {
  currentZoom = 1.0;
  document.body.style.transform = 'scale(1)';
  document.body.style.transformOrigin = 'top left';
  document.getElementById('zoom-label').textContent = '100%';
}

// ── TRANSLATE ────────────────────────────────────────────
function googleTranslateElementInit() {
  new google.translate.TranslateElement({
    pageLanguage: 'en',
    includedLanguages: 'th,id',   // Thai + Bahasa Indonesia — change to e.g. 'zh-CN,ms' for other regions
    autoDisplay: false
  }, 'google_translate_element');
}
function setLang(lang) {
  ['en','th','id'].forEach(function(l) {
    var b = document.getElementById('btn-' + l);
    b.style.background = (l === lang) ? 'rgba(0,80,220,0.12)' : 'transparent';
    b.style.color = (l === lang) ? '#0044cc' : '#8a9ab8';
  });
  if (lang === 'en') {
    var frame = document.querySelector('.goog-te-banner-frame');
    if (frame) {
      var doc = frame.contentDocument || frame.contentWindow.document;
      var btn = doc.querySelector('.goog-te-button button');
      if (btn) btn.click();
    }
  } else {
    var sel = document.querySelector('.goog-te-combo');
    if (sel) { sel.value = lang; sel.dispatchEvent(new Event('change')); }
  }
}
</script>
<script src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
```

> **Language defaults:** TH = Thai · ID = Bahasa Indonesia. To target other regions change `includedLanguages` to any ISO 639-1 pair, e.g. `'zh-CN,ms'` (Mandarin + Malay) or `'ko,ja'` (Korean + Japanese).

> **Zoom range:** 40%–200%, default 100%. Uses `transform: scale()` on `<body>` with `transformOrigin: top left` — preserves 1920px layout without reflow.

> **Scroll buttons:** Each press scrolls 500px horizontally with smooth animation, useful when page overflows viewport width.

---

## CONTENT GENERATION RULES

### What to ALWAYS include
- Every number has an inline blue hyperlink: `<a href="URL" target="_blank" style="color:#0055cc;">source ↗</a>`
- Cloud market share = always labeled as bottoms-up estimate
- IT spend = 8% of COGS if not disclosed, labeled as estimate
- If a company is closed: red closed badge in topbar, strike-through product section, red failure signal in sidebar
- Financial data labeled: "(confirmed from annual report)", "(derived)", "(estimated)"
- GoTo-style timeline corrections: cite both the partnership announcement date AND the execution date

### Currency Rule — All Figures in USD
> **ALL monetary values must be expressed in USD regardless of the company's home market or listing currency.**

- Convert IDR, SGD, HKD, JPY, CNY, MYR, THB, or any other currency → USD
- Use the **fiscal year average exchange rate** for historical figures (not spot rate)
- State the rate used inline: e.g., `"$148M (IDR 2.34T · avg IDR 15,800/$, FY2024)"`
- **HTML format:** USD amount bold/primary → local currency in small muted span below:
  ```html
  <strong>$148M</strong>
  <span style="font-size:8px;color:#9aaabb;display:block">(IDR 2.34T · IDR 15,800/$)</span>
  ```
- **Exchange rate sources to cite inline:** [Wise Historical Rates](https://wise.com/tools/exchange-rate-history/) · [Bank Indonesia](https://www.bi.go.id/en/statistik/informasi-kurs/) · [xe.com](https://www.xe.com/currencytables/)
- **Exception:** Stock tickers, per-share prices, and exchange-specific data may remain in native currency for accuracy (e.g., "EMTK · IDR 0.XX/share")

### What to NEVER include
- Generic homepage URLs as proof of specific data points
- Specific exact percentages for cloud market share without source or bottoms-up calculation
- A separate "Sources" or "References" section — all links go inline
- "No corrections needed" or "removed from slide" meta-commentary
- Any emoji unless specifically in section headers for visual anchoring
- The phrase "consulting-style dense page" in the output HTML

### Typography scale
```
Section header titles:   15px, weight 900, letter-spacing -0.3px
Section subtitles:       10.5px, color #9aaabb
Panel titles (labels):   9px, weight 700, uppercase, letter-spacing 1.3px
Product/right names:     10.5px, weight 700, #1a2a44
Body text (dense):       9px–9.5px, color #3a4a64–#5a6a88, line-height 1.4–1.5
Fine print / footnotes:  7.5px–8px, color #9aaabb–#c0cce0
Stats (big numbers):     12px–20px, weight 900, #0a1020 or accent color
Footer metrics:          18px, weight 900
```

---

## ADAPTATION GUIDE — Changing the Company

| Variable | Mola TV Example | Replace With |
|---|---|---|
| `[COMPANY_NAME]` | Mola TV | Target company name |
| `[PARENT_GROUP]` | Djarum Group | Parent conglomerate |
| `[TICKER_1]` | EMTK | Primary IDX-listed parent ticker |
| `[TICKER_2]` | MNCN | Secondary listed entity ticker |
| `[INDUSTRY]` | OTT Streaming | Target industry |
| `[STATUS]` | Closed Dec 2025 | Active / Closed / Restructuring |
| `[YEAR]` | 2024 | Analysis fiscal year |
| Logo gradient | `#0055cc → #0088ff` | Brand color of target company |
| Category tags | Sports · OTT · Streaming | Relevant industry tags |
| Panel C title | "FIFA Timeline" | Relevant milestone/rights type |
| Footer metrics | Subscriber count, FIFA count | Company-specific KPIs |
| Cloud section focus | Tencent Cloud | Relevant cloud provider to analyze |
| News sources | Kompas Tekno, CNN Indonesia | Relevant local + regional news sources |
| Translate languages | `'th,id'` | Any 2 ISO 639-1 language codes |

---

## SELF-CHECK BEFORE OUTPUTTING

Before finalizing the HTML, verify:
- [ ] All sections present: topbar → sidebar → 6 panels → cloud → financials → news → footer → UI overlay
- [ ] ALL cloud percentages are ranges with methodology box, not point estimates
- [ ] ALL financial figures have "(confirmed)", "(derived)", or "(estimated)" labels
- [ ] ALL claims have blue hyperlinks inline — no separate sources section
- [ ] Status badge in topbar matches company status
- [ ] Sidebar failure signal box present if company is closed/distressed
- [ ] Footer has exactly 7 metric items, all values in USD
- [ ] `grid-column: 1 / -1` applied to ALL full-width sections
- [ ] `position: sticky` on topbar, `position: fixed` on footer
- [ ] No external file dependencies — single self-contained HTML file
- [ ] **[NEW] Timeline (Panel C) ordered LATEST → OLDEST** — newest entry at top, "Latest → Oldest" label above
- [ ] **[NEW] Fixed UI overlay present** at `top:12px; right:20px; z-index:9999` with EN/TH/ID translate buttons, ‹ › scroll buttons, and − + ↺ zoom controls
- [ ] **[NEW] ALL monetary figures in USD** — local currency shown in muted secondary text with exchange rate cited and linked
- [ ] **[NEW] Google Translate script** loaded before `</body>` with `includedLanguages` set to correct 2-language pair

---PROMPT END---

---

## PROMPT EVOLUTION LOG

The following iterative refinements were made to arrive at this final version. Include these as context if you need the model to understand why certain decisions were made.

**R1:** Initial request — research Mola TV, FIFA rights, competitors, Indonesia market. Output: multi-section research plan.

**R2:** "Make it packed like a consulting type of page, all in one page" — Established 1920×1080px dense layout, 4-column grid, sidebar, 6-panel structure.

**R3:** "Make the color whiteish instead of dark color" — Full CSS rewrite from `#0b0f1a` dark theme to `#ffffff` white theme. Changed all text from light-on-dark to dark-on-white.

**R4:** "Make the footer fixed where I can scroll up and down" — Changed footer from static to `position:fixed; bottom:0`. Added `padding-bottom:80px` to main body.

**R5:** "Make the background all white, no square background grid" — Removed CSS pseudo-element grid pattern. Set pure `background:#ffffff`.

**R6:** "Make another section for cloud provider for our Tencent cloud analysis" — Added Cloud Infrastructure Section (full-width, 3-column inner grid: Platform Cloud Map + Market Share Bars + Tencent Opportunity).

**R7:** "Feels like the layout can be widen horizontally" — Fixed `grid-column: 1 / -1` on cloud section wrapper. Changed inner grid from `320px 1fr 340px` to `400px 1fr 520px`.

**R8:** "How did you calculate the market share, give me the very detailed number and explanation" — Added methodology box above bar chart. Changed all single-value percentages to ranges. Added numbered `[¹]` footnotes with source links. AWS corrected from 44% → 55–62%. Alibaba corrected from 18% (with wrong GoTo attribution) → 5–8% declining. Removed unverified 7.67% APAC Tencent stat.

**R9:** "For each figure, get the references for the number... add a download/see link... get their EST IT spend" — Added Platform Financials & IT Spend section. Used IDX reports for EMTK and MNCN. Derived EMTK revenue from Net Income ÷ Net Margin. Applied 8% COGS for IT spend estimate. Added PDF keyword guides.

**R10:** "For each figure... prove it by hyperlink... no need for separate source validation section" — Removed standalone Source Validation section. Embedded all hyperlinks inline in blue directly in sentences.

**R11:** Added News Key Findings section with: keyword clusters strip, 9 ranked signals, synthesis-by-category panel. Dark header to visually anchor the intelligence section.

**R12:** Four structural upgrades applied to user's modified version:
1. **Timeline ordering** — Panel C now requires latest → oldest (reverse chronological). "Latest → Oldest" label added above first entry. Ordering rule block added to spec.
2. **Fixed UI overlay** — New `position:fixed; top:12px; right:20px; z-index:9999` pill bar with: 🌐 EN/TH/ID language toggle (Google Translate API, active state highlights in blue), ‹ › horizontal scroll buttons (500px per press, smooth), − + zoom controls (40%–200% via `transform:scale()` on body), ↺ zoom reset to 100%.
3. **USD currency rule** — All monetary figures must be in USD first; local currency shown as small muted secondary text below each figure with exchange rate cited and linked. Exchange rate source must be hyperlinked (Wise, BI, xe.com). Exception for per-share/ticker data.
4. **Translate button** — Defaults to Thai (TH) + Bahasa Indonesia (ID). Configurable via `includedLanguages` in Google Translate init. Language toggle highlights active button. EN button triggers Google Translate's built-in restore.

---

*Template by Timothy Isaac Siamena · Built with Claude · Version 1.1 · March 2026*
