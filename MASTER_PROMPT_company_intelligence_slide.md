# MASTER PROMPT — Company Intelligence Slide (Reverse Engineered)
### One-Page Scrollable HTML Intelligence Brief · Consulting Style · 1920px Wide
**Author:** Timothy Isaac Siamena · **Template Version:** 1.2 · **Base Company:** GoTo Group (PT GoTo Gojek Tokopedia Tbk)

---

## COPY FROM THIS SECTION

Do this prompt but for [Name of the company]

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
- **Second Language:** [LANG2] (e.g., 中文, Bahasa Indonesia, 日本語 — for the bilingual toggle)

---

## PHASE 1 — RESEARCH (Do this before writing any HTML)

Conduct deep research on [COMPANY_NAME] across the following dimensions. For EVERY fact you include in the HTML, you must have a real source URL ready to embed as a blue hyperlink inline in the text. Do NOT cite a company's main homepage as proof of a data point — find the specific article, report, or announcement page.

### 1A — Company & Product Research
- What products or services does [COMPANY_NAME] offer? List all sub-brands, tiers, platforms
- What are their primary content/service categories?
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
- Any specific segment data
- **IT/Technology Spend line item** — search PDF for keywords: "Teknologi Informasi", "Infrastruktur", "Sistem Informasi"
- **If IT spend not found:** Use **8% of COGS** as the industry estimate (Gartner benchmark for media/tech companies)

For PRIVATE companies (no IDX listing): Note as private, use third-party revenue estimates (Owler, Crunchbase, ZoomInfo) and label clearly as estimates.

### 1C — Cloud / Technology Infrastructure Research
For each competitor platform and [COMPANY_NAME] itself:
- Primary cloud provider (AWS, Google Cloud, Azure, Alibaba Cloud, Tencent Cloud, Local/Telkom)
- CDN provider
- Any confirmed public announcements
- Tencent Cloud specific: What % of this platform's cloud workloads run on Tencent Cloud?

**IMPORTANT RULES FOR CLOUD MARKET SHARE:**
- Do NOT assign a specific percentage to any provider unless you can derive it via bottoms-up calculation OR find a published source
- Bottoms-up method: (Platform's estimated % of total cloud spend) × (% of that platform on each provider) = weighted contribution
- Show ranges (e.g., ~18–24%) not point estimates when uncertain
- Clearly label all figures as "Bottoms-up estimate — no public IDC/Canalys report covers this breakdown"

### 1D — News Intelligence Research (Last 3–6 months minimum, expand to 2 years for context)
Search across Indonesian and English-language business news, industry publications, and official announcements. Extract: Strategic signals, financial signals, competitive signals, reputation risks, market opportunities. Rank from highest to lowest strategic impact.

### 1E — Source Validation Rules
- Every number must have a clickable blue hyperlink embedded inline
- Do NOT create a separate "Sources" section — embed links directly in the sentence where the data appears
- If a number is unverifiable, either remove it or clearly label it as an estimate with methodology explained
- Never cite a company's main homepage as proof of a specific data point

---

## PHASE 2 — HTML CONSTRUCTION

Build ONE fully self-contained HTML file. No external CSS files, no external JS (except Google Fonts). Inline everything.

### CRITICAL ARCHITECTURE — FIXED VIEWPORT + CUSTOM SCROLLBARS

> ⚠️ **This is the most important architectural decision in the entire build.** Do NOT use `document.body.style.transform` for zoom and do NOT use `window.scrollBy` for scrolling. The entire scroll/zoom system described below MUST be implemented exactly as specified.

**The Problem with the naive approach:** Using `transform: scale()` on `<body>` breaks `position:fixed` elements — the footer, topbar, and UI overlay move with the zoom instead of staying fixed. Using `window.scrollBy` doesn't work when the page is inside a fixed viewport div.

**The Solution — Fixed Viewport Shell Architecture:**

The page has three fixed-position layers that never zoom, plus one inner zoomable content layer:

```
<body>                          ← overflow:hidden, height:100%
  #topbar-shell (fixed)        ← always at top, contains #topbar-inner which scales
  .bottombar (fixed)           ← always at bottom, never scales
  #vscroll (fixed)             ← custom vertical scrollbar track + thumb
  #hscroll (fixed)             ← custom horizontal scrollbar track + thumb
  #ui-overlay (fixed)          ← language toggle + zoom controls, top-right
  #viewport (fixed)            ← clips the scrollable area, overflow:hidden
    #page-wrap                 ← ONLY this element gets transform:scale()
      [all page content]
```

**Key measurements:**
- `#topbar-shell`: `position:fixed; top:0; height:66px; z-index:500`
- `#viewport`: `position:fixed; top:66px; bottom:72px; left:0; right:0; overflow:hidden`
- `.bottombar`: `position:fixed; bottom:0; height:64px; z-index:9000`
- `#page-wrap`: `width:1920px; transform-origin:top left`
- `#topbar-inner`: `width:1920px; transform-origin:top left` ← scales WITH page, lives inside #topbar-shell
- `#vscroll`: `position:fixed; right:4px; top:74px; bottom:80px; width:7px; z-index:8000`
- `#hscroll`: `position:fixed; left:0; right:14px; bottom:72px; height:7px; z-index:8000`
- `#ui-overlay`: `position:fixed; top:14px; right:20px; z-index:9999`

**Zoom behavior:** `applyZoom()` calls `transform:scale(currentZoom)` on BOTH `#page-wrap` AND `#topbar-inner` simultaneously. It also adjusts `#topbar-shell` height and `#viewport` top offset to match the scaled topbar height: `Math.round(66 * currentZoom) + 'px'`.

**Scroll behavior:** `#viewport` scrolls via `vp.scrollTop` and `vp.scrollLeft` (not `window.scroll`). The wheel event listener is on `#viewport`, not `window`. Trackpad horizontal swipe uses `e.deltaX`; vertical uses `e.deltaY`; `shiftKey` + mouse wheel forces horizontal.

**Custom scrollbar logic:** Thumb size = `trackSize * Math.min(1, viewportSize / contentSize)`. Thumb position = `scrollRatio * (trackSize - thumbSize)`. Draggable via mousedown/mousemove/mouseup. Click-on-track jumps to position.

### FILE STRUCTURE

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=1920">
  <title>[COMPANY_NAME] — [PARENT_GROUP] Analysis [YEAR]</title>
  <style>[ALL CSS — see Design System]</style>
</head>
<body>
  <!-- STATIC CHROME (never zooms) -->
  [1] #topbar-shell → contains #topbar-inner (scales with zoom)
      Inside topbar-inner: #topbar-en (default visible) + #topbar-zh (hidden)
  [2] .bottombar (fixed footer)
      Inside: #footer-en (default visible) + #footer-zh (hidden)
  [3] #vscroll + #hscroll (custom scrollbar elements)
  [4] #ui-overlay (language toggle + zoom controls)

  <!-- ZOOMABLE CONTENT -->
  [5] #viewport
        #page-wrap
          <!-- ENGLISH SECTION -->
          <div id="section-en">
            <div class="main-body"> ← 4-col CSS grid
              [2a] .sidebar (grid-col 1, row 1/3)
              [2b] Panel A: Products & Services (col 2, row 1)
              [2c] Panel B: Key Assets & Strategic Moves (col 3, row 1)
              [2d] Panel C: Corporate Timeline (col 4, row 1)
              [2e] Panel D: Market Analysis (col 2, row 2)
              [2f] Panel E: Competitor Landscape (col 3, row 2)
              [2g] Panel F: Strategic Outlook (col 4, row 2)
              [2h] Cloud Infrastructure Section (full-width, col 1/-1)
              [2i] Platform Financials & IT Spend (full-width, col 1/-1)
              [2j] News Key Findings (full-width, col 1/-1)
            </div>
          </div>

          <!-- CHINESE SECTION (hidden by default) -->
          <div id="section-zh" style="display:none">
            [identical structure, fully translated content]
          </div>

  [6] <script> ← ONE script block only, at end of body
</body>
</html>
```

---

## DESIGN SYSTEM — COPY THESE EXACTLY

### Typography
```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');
*,*::before,*::after { box-sizing:border-box; margin:0; padding:0 }
html { overflow:hidden; height:100%; width:100% }
body { width:100%; height:100%; overflow:hidden; background:#ffffff; color:#1a2035; font-family:'Inter',sans-serif; font-size:13px; margin:0 }
```

### Color Tokens
```
Background (page):          #ffffff
Background (sidebar):       #fafbfe
Text primary:               #0a1020
Text secondary:             #1a2a44
Text muted:                 #5a6a88 / #8a9ab8 / #9aaabb
Border default:             rgba(0,20,80,0.07)
Sidebar border:             1.5px solid rgba(0,20,80,0.08)
Accent blue:                #0044cc / #0055cc
Warning orange:             #dd6600
Danger red:                 #cc2222
Success green:              #006633 / #44aa77
Purple:                     #6622aa / #9922bb
Yellow:                     #7a5500
```

### Custom Scrollbar CSS
```css
#vscroll { position:fixed; right:4px; top:74px; bottom:80px; width:7px; z-index:8000; }
#vscroll-track { position:absolute; inset:0; background:rgba(0,20,80,0.06); border-radius:6px; }
#vscroll-thumb { position:absolute; left:0; right:0; background:rgba(0,60,180,0.22); border-radius:6px; min-height:28px; cursor:grab; transition:background 0.15s; }
#vscroll-thumb:hover, #vscroll-thumb.dragging { background:rgba(0,60,180,0.42); cursor:grabbing; }
#hscroll { position:fixed; left:0; right:14px; bottom:72px; height:7px; z-index:8000; }
#hscroll-track { position:absolute; inset:0; background:rgba(0,20,80,0.06); border-radius:6px; }
#hscroll-thumb { position:absolute; top:0; bottom:0; background:rgba(0,60,180,0.22); border-radius:6px; min-width:28px; cursor:grab; transition:background 0.15s; }
#hscroll-thumb:hover, #hscroll-thumb.dragging { background:rgba(0,60,180,0.42); cursor:grabbing; }
```

### Tag System (topbar category pills)
```css
.tag { padding:3px 11px; border-radius:20px; font-size:10px; font-weight:700; letter-spacing:0.4px; text-transform:uppercase; white-space:nowrap }
.tag-blue   { background:rgba(0,100,220,0.09);  color:#0055bb; border:1px solid rgba(0,100,220,0.18) }
.tag-orange { background:rgba(210,90,0,0.09);   color:#aa4400; border:1px solid rgba(210,90,0,0.18) }
.tag-green  { background:rgba(0,160,80,0.09);   color:#006633; border:1px solid rgba(0,160,80,0.18) }
.tag-red    { background:rgba(200,30,30,0.09);  color:#aa1111; border:1px solid rgba(200,30,30,0.18) }
.tag-purple { background:rgba(110,50,200,0.09); color:#6622aa; border:1px solid rgba(110,50,200,0.18) }
.tag-yellow { background:rgba(180,130,0,0.09);  color:#7a5500; border:1px solid rgba(180,130,0,0.18) }
.tag-gray   { background:rgba(0,20,60,0.06);    color:#5a6a88; border:1px solid rgba(0,20,60,0.11) }
```

### Status Badge
- **ACTIVE:** `background:rgba(0,160,80,0.08); border:1px solid rgba(0,160,80,0.2); color:#006633` — text: "ACTIVE"
- **CLOSED:** `background:rgba(200,30,30,0.08); border:1px solid rgba(200,30,30,0.25); color:#bb1111` — text: "CLOSED [MONTH YEAR]"
- **RESTRUCTURING:** orange/yellow scheme

---

## BILINGUAL ARCHITECTURE — EN / [LANG2] TOGGLE

> ⚠️ **Critical rule:** Do NOT use Google Translate API. Do NOT use JS `innerHTML` swapping with template strings. Do NOT use `data-zh` attribute replacement. These all cause `Unexpected token '<'` syntax errors or incomplete translations.

**The ONLY correct approach is two complete, pre-written HTML sections:**

1. Write the full English content in `<div id="section-en">...</div>`
2. Translate ALL text content (every label, description, data point, panel title, button, badge, category tag, sidebar row, timeline entry, signal card, synthesis paragraph, footer label) into [LANG2]
3. Write the complete translated content in `<div id="section-zh" style="display:none">...</div>`
4. The topbar has TWO versions inside `#topbar-inner`: `#topbar-en` and `#topbar-zh`
5. The footer has TWO versions inside `.bottombar`: `#footer-en` and `#footer-zh`
6. The `setLang()` JS function simply toggles `display:none` / `display:block` on these pairs

**Translation scope — translate EVERYTHING:**
- All panel titles and section labels
- All product names, descriptions, and type tags
- All sidebar labels, values, and info-block rows
- All timeline year titles and detail text
- All market bar labels and footnotes
- All competitor card names, descriptions, and badge text (High → 高威胁, etc.)
- All outlook card titles and body text
- All cloud section headers, methodology box, bar labels, and reference footnotes
- All financial card headers, metric labels, notes, and access instructions
- All news signal titles, body text, and impact lines
- All synthesis panel category names and body paragraphs
- All footer metric labels
- All topbar tags and status badge
- Threat levels: High → 高威胁 · Medium → 中等威胁 · Low → 低威胁

**What NOT to translate:**
- URLs inside `href=""` attributes
- Numeric values ($1.15B, 61.1M, IDR 386B, etc.)
- Company proper nouns (GoTo, Gojek, GoPay, Tokopedia, Grab, etc.)
- Ticker symbols (GOTO, GRAB, SE)
- Technical strings (CSS class names, IDs, JS variable names)

**Preventing `</script>` termination errors:**
The translated HTML sections are plain HTML in the document body — NOT inside JavaScript strings, template literals, or `<script>` tags. There is exactly ONE `<script>` block in the entire file, placed immediately before `</body>`, containing only JavaScript. Zero HTML inside the script block. Zero `<script>` tags inside the content sections.

```
✓ CORRECT structure:
  <div id="section-zh">... all Chinese HTML here ...</div>
  <script>
    // ONLY pure JavaScript here — no HTML, no template literals containing HTML
    function setLang(lang) { ... }
  </script>
  </body>

✗ WRONG — never do this:
  <script>
    var ZH_PAGE = `<div>中文内容</div>`; // </div> inside template literal = parser confusion
  </script>
```

---

## UI OVERLAY — Language Toggle + Zoom Controls

Place immediately after `#hscroll`, before `#viewport`:

```html
<div id="ui-overlay" style="position:fixed;top:14px;right:20px;z-index:9999;display:flex;align-items:center;gap:8px;">

  <!-- Language toggle -->
  <div style="display:flex;align-items:center;gap:3px;background:#fff;border:1px solid rgba(0,20,80,0.15);border-radius:22px;padding:4px 10px;box-shadow:0 2px 8px rgba(0,20,80,0.1)">
    <span style="font-size:10px;margin-right:3px">🌐</span>
    <button id="btn-en" onclick="setLang('en')" style="font-size:10px;font-weight:700;padding:3px 9px;border-radius:14px;border:none;cursor:pointer;background:rgba(0,80,220,0.12);color:#0044cc">EN</button>
    <button id="btn-zh" onclick="setLang('zh')" style="font-size:10px;font-weight:700;padding:3px 9px;border-radius:14px;border:none;cursor:pointer;background:transparent;color:#8a9ab8">[LANG2_LABEL]</button>
  </div>

  <div style="width:1px;height:22px;background:rgba(0,20,80,0.1)"></div>

  <!-- Zoom controls -->
  <div style="display:flex;align-items:center;gap:4px;background:#fff;border:1px solid rgba(0,20,80,0.15);border-radius:22px;padding:4px 8px;box-shadow:0 2px 8px rgba(0,20,80,0.1)">
    <button onclick="adjustZoom(-0.1)" style="font-size:14px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">−</button>
    <span id="zoom-label" style="font-size:9px;font-weight:700;color:#4a5a78;min-width:34px;text-align:center">100%</span>
    <button onclick="adjustZoom(+0.1)" style="font-size:14px;font-weight:900;padding:2px 7px;border-radius:12px;border:none;cursor:pointer;background:transparent;color:#4a5a78;line-height:1">+</button>
    <button onclick="resetZoom()" style="font-size:9px;font-weight:700;padding:2px 8px;border-radius:12px;border:none;cursor:pointer;background:rgba(0,20,80,0.06);color:#8a9ab8">↺</button>
  </div>

</div>
```

Replace `[LANG2_LABEL]` with the display label for the second language (e.g., `中文`, `ID`, `日本語`).

> **Note:** No scroll ‹ › buttons needed. The custom scrollbar + trackpad wheel handler covers all scroll interactions.

---

## JAVASCRIPT — ONE BLOCK, PLACED BEFORE `</body>`

```javascript
<script>
var currentLang = 'en';
var currentZoom = 1.0;
var vp = document.getElementById('viewport');

// ── LANG TOGGLE ──────────────────────────────────────────────────
function setLang(lang) {
  currentLang = lang;
  var isZH = (lang === 'zh');
  document.getElementById('section-en').style.display = isZH ? 'none' : 'block';
  document.getElementById('section-zh').style.display = isZH ? 'block' : 'none';
  document.getElementById('topbar-en').style.display  = isZH ? 'none' : 'block';
  document.getElementById('topbar-zh').style.display  = isZH ? 'block' : 'none';
  document.getElementById('footer-en').style.display  = isZH ? 'none' : 'flex';
  document.getElementById('footer-zh').style.display  = isZH ? 'flex' : 'none';
  document.getElementById('btn-en').style.background = isZH ? 'transparent' : 'rgba(0,80,220,0.12)';
  document.getElementById('btn-en').style.color      = isZH ? '#8a9ab8' : '#0044cc';
  document.getElementById('btn-zh').style.background = isZH ? 'rgba(0,80,220,0.12)' : 'transparent';
  document.getElementById('btn-zh').style.color      = isZH ? '#0044cc' : '#8a9ab8';
  vp.scrollTop = 0; vp.scrollLeft = 0;
  applyZoom();
  setTimeout(updateScrollbars, 100);
}

// ── ZOOM ──────────────────────────────────────────────────────────
function applyZoom() {
  var pw = document.getElementById('page-wrap');
  var ti = document.getElementById('topbar-inner');
  var s  = 'scale(' + currentZoom + ')';
  pw.style.transform = s; pw.style.transformOrigin = 'top left';
  ti.style.transform = s; ti.style.transformOrigin = 'top left';
  document.getElementById('topbar-shell').style.height = Math.round(66 * currentZoom) + 'px';
  vp.style.top = Math.round(66 * currentZoom) + 'px';
  document.getElementById('vscroll').style.top = (Math.round(66 * currentZoom) + 8) + 'px';
  document.getElementById('zoom-label').textContent = Math.round(currentZoom * 100) + '%';
  setTimeout(updateScrollbars, 50);
}
function adjustZoom(d) {
  currentZoom = Math.min(2.5, Math.max(0.3, +(currentZoom + d).toFixed(2)));
  applyZoom();
}
function resetZoom() { currentZoom = 1.0; applyZoom(); }

// ── SCROLLBAR UPDATE ──────────────────────────────────────────────
function updateScrollbars() {
  var pw = document.getElementById('page-wrap');
  var vpH = vp.clientHeight, vpW = vp.clientWidth;
  var contentH = pw.scrollHeight * currentZoom;
  var contentW = pw.scrollWidth  * currentZoom;
  // Vertical
  var vEl = document.getElementById('vscroll');
  var vThumb = document.getElementById('vscroll-thumb');
  var trkH = vEl.clientHeight;
  var tH = Math.max(28, trkH * Math.min(1, vpH / Math.max(contentH, 1)));
  vThumb.style.height = tH + 'px';
  var rV = vp.scrollTop / Math.max(1, contentH - vpH);
  vThumb.style.top = Math.min(trkH - tH, rV * (trkH - tH)) + 'px';
  vEl.style.display = contentH > vpH ? 'block' : 'none';
  // Horizontal
  var hEl = document.getElementById('hscroll');
  var hThumb = document.getElementById('hscroll-thumb');
  var trkW = hEl.clientWidth;
  var tW = Math.max(28, trkW * Math.min(1, vpW / Math.max(contentW, 1)));
  hThumb.style.width = tW + 'px';
  var rH = vp.scrollLeft / Math.max(1, contentW - vpW);
  hThumb.style.left = Math.min(trkW - tW, rH * (trkW - tW)) + 'px';
  hEl.style.display = contentW > vpW ? 'block' : 'none';
}
vp.addEventListener('scroll', updateScrollbars);
window.addEventListener('resize', updateScrollbars);

// ── DRAG — VERTICAL SCROLLBAR ─────────────────────────────────────
(function(){
  var thumb=document.getElementById('vscroll-thumb'),
      track=document.getElementById('vscroll-track'),
      drag=false, sy, ss;
  thumb.addEventListener('mousedown',function(e){
    drag=true; sy=e.clientY; ss=vp.scrollTop;
    thumb.classList.add('dragging'); e.preventDefault(); e.stopPropagation();
  });
  document.addEventListener('mousemove',function(e){
    if(!drag) return;
    var pw=document.getElementById('page-wrap');
    var tH=parseFloat(thumb.style.height)||28;
    var trkH=document.getElementById('vscroll').clientHeight;
    var ratio=(e.clientY-sy)/(trkH-tH);
    vp.scrollTop=ss+ratio*(pw.scrollHeight*currentZoom-vp.clientHeight);
  });
  document.addEventListener('mouseup',function(){ drag=false; thumb.classList.remove('dragging'); });
  track.addEventListener('click',function(e){
    var r=document.getElementById('vscroll').getBoundingClientRect();
    var pw=document.getElementById('page-wrap');
    vp.scrollTop=(e.clientY-r.top)/r.height*(pw.scrollHeight*currentZoom-vp.clientHeight);
  });
})();

// ── DRAG — HORIZONTAL SCROLLBAR ───────────────────────────────────
(function(){
  var thumb=document.getElementById('hscroll-thumb'),
      track=document.getElementById('hscroll-track'),
      drag=false, sx, ss;
  thumb.addEventListener('mousedown',function(e){
    drag=true; sx=e.clientX; ss=vp.scrollLeft;
    thumb.classList.add('dragging'); e.preventDefault(); e.stopPropagation();
  });
  document.addEventListener('mousemove',function(e){
    if(!drag) return;
    var pw=document.getElementById('page-wrap');
    var tW=parseFloat(thumb.style.width)||28;
    var trkW=document.getElementById('hscroll').clientWidth;
    var ratio=(e.clientX-sx)/(trkW-tW);
    vp.scrollLeft=ss+ratio*(pw.scrollWidth*currentZoom-vp.clientWidth);
  });
  document.addEventListener('mouseup',function(){ drag=false; thumb.classList.remove('dragging'); });
  track.addEventListener('click',function(e){
    var r=document.getElementById('hscroll').getBoundingClientRect();
    var pw=document.getElementById('page-wrap');
    vp.scrollLeft=(e.clientX-r.left)/r.width*(pw.scrollWidth*currentZoom-vp.clientWidth);
  });
})();

// ── WHEEL + TRACKPAD ──────────────────────────────────────────────
vp.addEventListener('wheel', function(e){
  e.preventDefault();
  if (e.deltaX !== 0) vp.scrollLeft += e.deltaX;          // trackpad horizontal swipe
  if (e.deltaY !== 0) {
    if (e.shiftKey) { vp.scrollLeft += e.deltaY; }        // shift+wheel = horizontal
    else            { vp.scrollTop  += e.deltaY; }        // normal = vertical
  }
  updateScrollbars();
}, { passive: false });

// ── INIT ──────────────────────────────────────────────────────────
window.addEventListener('load', function(){ setTimeout(updateScrollbars, 200); });
setTimeout(updateScrollbars, 400);
</script>
```

---

## SECTION-BY-SECTION SPECIFICATIONS

### [1] TOPBAR SHELL

```html
<div id="topbar-shell">      <!-- fixed, height adjusts with zoom -->
  <div id="topbar-inner">   <!-- scales via transform:scale() with page -->

    <div id="topbar-en">    <!-- English version, visible by default -->
      <div class="topbar"> ... </div>
    </div>

    <div id="topbar-zh" style="display:none">  <!-- [LANG2] version, hidden by default -->
      <div class="topbar"> ... </div>
    </div>

  </div>
</div>
```

Topbar CSS:
```css
#topbar-shell { position:fixed; top:0; left:0; right:0; height:66px; z-index:500; background:#fff; border-bottom:1.5px solid rgba(0,20,80,0.1); }
#topbar-inner { width:1920px; height:66px; transform-origin:top left; }
.topbar { height:66px; padding:0 36px; display:flex; align-items:center; gap:12px; width:1920px; }
```

**Contents (left to right):**
1. Logo block: 30×30px rounded square, gradient, company initial, 14px weight 900 white
2. Company name (18px, weight 800) + sub-label (11px, muted)
3. Vertical divider
4. Category `.tag` pills
5. Right side (`margin-left:auto`): subtitle text + status badge

> Leave ~280px right clearance for the fixed UI overlay.

---

### [2] FOOTER

```html
<div class="bottombar">
  <div id="footer-en" class="key-metrics"> ... 7 metric items ... </div>
  <div id="footer-zh" class="key-metrics" style="display:none"> ... 7 translated metric items ... </div>
</div>
```

Footer CSS:
```css
.bottombar { position:fixed; bottom:0; left:0; width:100vw; height:64px; background:#fff; border-top:1.5px solid rgba(0,20,80,0.09); display:flex; align-items:center; padding:0 36px; z-index:9000; box-shadow:0 -2px 12px rgba(0,20,80,0.05); }
.key-metrics { display:flex; gap:0; flex:1; }
.metric-item { flex:1; text-align:center; padding:8px 12px; border-right:1px solid rgba(0,20,80,0.07); }
.metric-item:last-child { border-right:none; }
.metric-val { font-size:18px; font-weight:900; color:#0a1020; }
.metric-lbl { font-size:9px; color:#9aaabb; font-weight:600; letter-spacing:0.3px; margin-top:2px; }
```

Include 7 metrics, all values in USD.

---

### [3] MAIN BODY GRID

```css
.main-body {
  display: grid;
  grid-template-columns: 320px 1fr 1fr 1fr;
  grid-template-rows: auto auto;
  padding-bottom: 20px;
  min-height: calc(100vh - 66px);
}
```

**Panel base class:**
```css
.panel { padding:20px 22px; border-right:1px solid rgba(0,20,80,0.07); border-bottom:1px solid rgba(0,20,80,0.07); display:flex; flex-direction:column; gap:10px; overflow:visible; }
.panel-title { font-size:9px; font-weight:700; letter-spacing:1.3px; text-transform:uppercase; color:#8a9ab8; display:flex; align-items:center; gap:6px; margin-bottom:2px; }
.panel-title::after { content:''; flex:1; height:1px; background:rgba(0,20,80,0.08); }
```

---

### [2a] SIDEBAR — grid-column:1, grid-row:1/3

```css
.sidebar { grid-column:1; grid-row:1/3; background:#fafbfe; padding:24px 20px; border-right:1.5px solid rgba(0,20,80,0.08); display:flex; flex-direction:column; gap:14px; }
```

Contents: logo box → stat rows → company profile info-block → investors info-block → milestone/alert box

---

### [2b] PANEL A — Products & Services (col 2, row 1)

Product cards in 2-column CSS grid. Each card has: colored top border, icon, product name, type tag, description with inline source links.

---

### [2c] PANEL B — Key Assets & Strategic Moves (col 3, row 1)

Vertical flex of asset/partnership cards. Each: colored icon, asset name, status badge (Active/Expired/Lost), description. This replaces the original "Content Rights / IP Portfolio" spec — adapt to the company's key strategic moves.

---

### [2d] PANEL C — Corporate Timeline (col 4, row 1)

> ⚠️ **ORDERING RULE — Latest → Oldest (ALWAYS):** Render timeline entries with the most recent year at TOP, oldest at BOTTOM. Add a small "Latest → Oldest" label (8px, #c0cce0) directly above the first entry. Never render oldest-first.

```css
.tl-list { display:flex; flex-direction:column; gap:0; }
.tl-item { display:flex; gap:10px; padding-bottom:10px; border-left:1.5px solid rgba(0,20,80,0.1); padding-left:14px; position:relative; }
.tl-item:last-child { border-left-color:transparent; }
.tl-dot { position:absolute; left:-5px; top:3px; width:9px; height:9px; border-radius:50%; border:1.5px solid #fff; }
.tl-year { font-size:10px; font-weight:800; color:#0a1020; }
.tl-title { font-size:10.5px; font-weight:700; color:#1a2a44; line-height:1.3; }
.tl-detail { font-size:9px; color:#9aaabb; line-height:1.45; margin-top:2px; }
.tl-order-label { font-size:8px; color:#c0cce0; margin-bottom:6px; font-weight:500; }
```

---

### [2e] PANEL D — Market Position (col 2, row 2)

Highlight box (big GTV/share number) + horizontal bar charts for market share. Include two bar chart groups: primary market (e.g. ride-hailing) and secondary market (e.g. payments). Add a context box at bottom.

---

### [2f] PANEL E — Competitor Landscape (col 3, row 2)

Competitor cards with: icon, name, description, threat badge (High/Medium/Low → translate in ZH version), type tag, cloud provider tag.

---

### [2g] PANEL F — Strategic Outlook (col 4, row 2)

Outlook cards with colored left borders: green=opportunity, orange=risk, red=threat, gray=neutral. Include 5–7 cards covering profitability, growth, competitive risks, macro/geopolitical factors.

---

### [2h] CLOUD INFRASTRUCTURE SECTION — Full-width (col 1/-1)

Three-column inner grid: `grid-template-columns: 400px 1fr 520px`

- **Col 1:** Platform cloud map table (platform → primary/secondary cloud → Tencent %)
- **Col 2:** Cloud market share bars with methodology box above, references box below
- **Col 3:** Tencent Cloud opportunity analysis (current wins + growth opportunities + footprint stats)

All cloud percentages must be ranges derived from bottoms-up calculation, not point estimates.

---

### [2i] PLATFORM FINANCIALS & IT SPEND — Full-width (col 1/-1)

Three financial cards side-by-side: main listed entity + segment breakdown + peer comparison. All figures in USD. IT spend = 8% of COGS if not disclosed. Include annual report access links and PDF keyword guide.

Horizontal IT spend comparison bar at bottom of section.

---

### [2j] NEWS KEY FINDINGS — Full-width (col 1/-1)

Dark-header section (`background:linear-gradient(135deg,#0a1020,#0f1a30)`). Dark keyword strip. Two-column inner: ranked signal cards (left) + five-dimension synthesis panel (right, 420px).

Signal priority colors: #1–2=red, #3–4=orange, #5–6=blue, #7–8=gray, #9–10=green. Every signal has inline blue hyperlinks.

Synthesis categories: Strategy & Direction → Financial & Operational Health → Reputation & Risk → Product & UX → Market Perception & Narrative.

---

## CONTENT RULES

### Source Links
Every number has an inline blue hyperlink: `<a href="URL" target="_blank" style="color:#0055cc;">source ↗</a>`

### Currency Rule — All Figures in USD
Convert all currencies to USD using fiscal year average exchange rate. Show local currency in muted small text below:
```html
<strong>$148M</strong>
<span style="font-size:8px;color:#9aaabb;display:block">(IDR 2.34T · IDR 15,800/$)</span>
```

### Cloud Market Share
Always label as "Bottoms-up estimate — no public IDC/Canalys report covers this breakdown". Show ranges, never point estimates.

### IT Spend
Use 8% of COGS if not disclosed in filings. Label clearly as "(est. · 8% of COGS)".

### Timeline
Always Latest → Oldest. Add "Latest → Oldest" label above first entry.

### Never include
- Generic homepage URLs as proof of specific data points
- Point estimates for cloud market share
- Separate "Sources" or "References" section
- HTML inside `<script>` blocks
- More than one `<script>` tag in the entire file

---

## SELF-CHECK BEFORE OUTPUTTING

- [ ] All sections present: topbar → sidebar → 6 panels → cloud → financials → news → footer → UI overlay
- [ ] Fixed viewport architecture: `#topbar-shell` + `#viewport` + `.bottombar` all position:fixed
- [ ] `transform:scale()` applied to BOTH `#page-wrap` AND `#topbar-inner` on zoom
- [ ] `vp.scrollTop` / `vp.scrollLeft` used for scrolling (NOT `window.scroll`)
- [ ] Wheel listener on `#viewport` (NOT `window`), handles `deltaX` + `deltaY` + `shiftKey`
- [ ] Custom scrollbar drag handlers for both axes
- [ ] Exactly ONE `<script>` block in the file, immediately before `</body>`
- [ ] Zero HTML inside the `<script>` block
- [ ] Bilingual: `#section-en` + `#section-zh` both present, ZH hidden by default
- [ ] Bilingual: `#topbar-en` + `#topbar-zh` both present inside `#topbar-inner`
- [ ] Bilingual: `#footer-en` + `#footer-zh` both present inside `.bottombar`
- [ ] `setLang()` toggles display on all 6 paired elements
- [ ] `applyZoom()` adjusts `#topbar-shell` height AND `#viewport` top to match `66 * currentZoom`
- [ ] All cloud percentages are ranges with methodology box
- [ ] All financial figures labeled: "(confirmed)", "(derived)", or "(estimated)"
- [ ] All monetary figures in USD with local currency in muted secondary text
- [ ] Timeline (Panel C) ordered LATEST → OLDEST
- [ ] Footer has exactly 7 metric items
- [ ] ALL claims have blue inline hyperlinks — no separate sources section
- [ ] Status badge matches company operational status
- [ ] No external file dependencies — single self-contained HTML file

---PROMPT END---

---

## ADAPTATION GUIDE — Changing the Company

| Variable | GoTo Group Example | Replace With |
|---|---|---|
| `[COMPANY_NAME]` | GoTo Group | Target company name |
| `[PARENT_GROUP]` | PT GoTo Gojek Tokopedia Tbk | Parent conglomerate |
| `[TICKER_1]` | GOTO | Primary IDX-listed ticker |
| `[TICKER_2]` | — (single entity) | Secondary listed entity if any |
| `[INDUSTRY]` | On-Demand · Fintech · E-Commerce | Target industry verticals |
| `[STATUS]` | Active | Active / Closed / Restructuring |
| `[YEAR]` | 2024 | Analysis fiscal year |
| `[LANG2]` | 中文 | Second language for bilingual toggle |
| `[LANG2_LABEL]` | 中文 | Button label (e.g. ID, TH, 日本語) |
| Logo gradient | `#00cc88 → #007755` (GoTo green) | Brand color of target company |
| Category tags | Ride-Hailing · Fintech · Food Delivery · On-Demand · Logistics · E-Commerce | Relevant industry tags |
| Panel C title | "Corporate Timeline" | "Rights Timeline" / "Key Milestones" |
| Footer metrics | GTV, ATU, EBITDA, cloud contract | Company-specific KPIs |
| Cloud focus | Tencent Cloud | Relevant cloud provider to analyze |
| Sidebar milestone box | Green (positive EBITDA milestone) | Red (failure signal) if company is distressed |

---

## PROMPT EVOLUTION LOG

**v1.0 (Mola TV base):** Initial build. 1920px dense layout, 4-column grid, sidebar, 6 panels, cloud section, financials, news. Dark → white theme. Fixed footer. Cloud provider analysis section. Methodology box for market share. IT spend 8% COGS rule. USD currency rule. Timeline latest→oldest ordering rule. Google Translate API integration.

**v1.1 (Mola TV refined):** Fixed UI overlay with EN/TH/ID language buttons (Google Translate API), ‹ › scroll buttons (500px per press), − + ↺ zoom via `transform:scale()` on `<body>`. Scroll buttons for horizontal navigation.

**v1.2 (GoTo Group rebuild — current):** Major architectural overhaul. All changes below supersede v1.1:

1. **Fixed viewport shell architecture** replaces `transform:scale()` on `<body>`. The old approach broke `position:fixed` elements (footer, topbar, UI overlay all moved with zoom). New architecture: `#topbar-shell` + `#viewport` (overflow:hidden) + `.bottombar` are all `position:fixed` and never scale. Only `#page-wrap` (content) and `#topbar-inner` (topbar content) get `transform:scale()`. `applyZoom()` adjusts `#topbar-shell` height and `#viewport` top offset dynamically to match `66 * currentZoom`.

2. **Custom pill scrollbars** replace browser native scrollbars and the old ‹ › scroll buttons. Two 7px pill-style draggable scrollbars: `#vscroll` (vertical, right edge) and `#hscroll` (horizontal, bottom edge). Both are `position:fixed`, live outside the zoom transform, and update via `updateScrollbars()`. Thumb size and position calculated from scroll ratio. Draggable via mousedown/mousemove. Click-on-track jumps to position. Wheel/trackpad handler on `#viewport` handles `deltaX` (trackpad horizontal), `deltaY` (vertical), `shiftKey+deltaY` (forced horizontal). **The ‹ › scroll buttons are removed entirely.**

3. **Bilingual toggle replaces Google Translate API.** Google Translate API caused visual glitches, missed content, and toolbar banners. New approach: two complete HTML sections pre-written in full — `#section-en` (English) and `#section-zh` (fully translated [LANG2]). Language button toggles `display:none/block` on 6 paired elements: `#section-en/zh`, `#topbar-en/zh`, `#footer-en/zh`. `setLang()` also resets `vp.scrollTop/Left` to 0 and re-calls `applyZoom()`. **The Google Translate script tag is removed entirely.**

4. **Translation completeness rule.** All UI text must be translated — not just panel titles. This includes every product description, timeline entry, competitor card, signal body, synthesis paragraph, footer label, and status badge. Threat levels: High → 高威胁, Medium → 中等威胁, Low → 低威胁. Any untranslated English text in the ZH section counts as a bug.

5. **Single script block rule.** There is exactly one `<script>` block in the file, placed immediately before `</body>`. Zero HTML inside the script. Any attempt to store translated HTML as JavaScript template literals will cause `Unexpected token '<'` parser errors because browsers terminate `<script>` blocks at the literal string `</script>` regardless of JS string context.

6. **Zoom range expanded** from 40%–200% (v1.1) to 30%–250% (v1.2).

7. **GoTo Group** replaces Mola TV as the base company reference. GoTo is an active company (EBITDA milestone achieved FY2024), whereas Mola TV was closed. The sidebar milestone box is green (positive signal) instead of red (failure signal).

---

*Template by Timothy Isaac Siamena · Built with Claude · Version 1.2 · March 2026*
