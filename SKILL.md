---
name: "step-12-kdp-cover-interior-design"
description: "Universal agent skill to capture live Amazon KDP print/ebook technical specifications (trim, bleed, margins, spine width), verify commercial-use licenses for all fonts/images, format front/back matter, and produce cover and interior specs/assets in 09_Cover_and_Interior/."
---

# 

---
name: Step_12_kdp-cover-interior-design
description: Universal agent skill to capture live Amazon KDP print/ebook technical specifications (trim, bleed, margins, spine width), verify commercial-use licenses for all fonts/images, format front/back matter, and produce cover and interior specs/assets in 09_Cover_and_Interior/.
---

# KDP Cover & Interior Design (`Step_12_kdp-cover-interior-design`)

**Role:** Cover & Interior Agent  
**Purpose:** Capture current KDP cover and interior technical specifications from official `kdp.amazon.com` help pages (with URL + capture date), verify commercial-use licenses for every font and visual asset, and prepare print-ready and ebook-ready interior and cover deliverables.

---

## 1. Environment Adaptation & Pre-Flight Gate
- **Required Upstream Inputs:**
  1. `08_Book_Development/MANUSCRIPTS/<shortname>_vNN.md` *(Audited manuscript for exact page count and body text)*
  2. `08_Book_Development/QUALITY_CHECKS/qc_<shortname>_<yyyymmdd>.md` *(Should have a `PASS` verdict)*
  3. `05_Competition_Research/competitors_<niche>_<yyyymmdd>.md` *(Competitor cover style notes so our cover stands out)*
- **Output Delivery:**
  - **Workspace Agents (Manus, Hermes):**
    - Save live KDP spec quotes to `09_Cover_and_Interior/specs_sources_<yyyymmdd>.md`.
    - Save cover deliverables/briefs to `09_Cover_and_Interior/cover_<shortname>/`.
    - Save interior files and the master spec sheet to `09_Cover_and_Interior/interior_<shortname>/spec_<shortname>_<yyyymmdd>.md`.
  - **Web / Chat Agents (Claude Projects, Genspark):**
    - Fetch live KDP specification rules from `kdp.amazon.com`, calculate exact dimensions/spine width, write the complete Front & Back Matter text, and output the complete `specs_sources` and `spec_<shortname>_<yyyymmdd>.md` Markdown documents in the chat.

---

## 2. Step-by-Step Design & Formatting Procedure

### Step 1: Capture Live KDP Specifications First (Never From Memory)
1. Browse official `kdp.amazon.com` help pages for:
   - Paperback trim sizes, bleed settings, and inside (gutter) / outside / top / bottom margin tables by page count.
   - Paperback spine width calculation formula (by paper type: white vs. cream) and full-wrap cover dimensions.
   - Ebook cover ideal pixel dimensions, aspect ratio, and file rules.
2. Save the quoted numbers, **Source URL**, and **Capture Date** to `09_Cover_and_Interior/specs_sources_<yyyymmdd>.md`.
   - *Block Rule:* If `kdp.amazon.com` help pages cannot be reached, stop and log `BLOCKED` (`Error: / Tried: / Next:`) in `09_Cover_and_Interior/BLOCKED.md`. Never guess or use undated spec numbers from memory.

### Step 2: Calculate Exact Paperback Dimensions & Spine Width
Using the dated KDP formula and the formatted page count (`N`):
- **Spine Width:** `Page Count (N) × KDP Paper Factor (in/page)` *(cite exact URL + capture date)*.
- **Full Paperback Cover Width:** `Back Cover Trim Width + Spine Width + Front Cover Trim Width + (2 × Bleed)`.
- **Full Paperback Cover Height:** `Trim Height + (2 × Bleed)`.

### Step 3: Verify Commercial-Use Licenses (Fonts & Images)
- Before using any font or image on the cover or interior, verify its **commercial-use license**.
- Record in the Licence Register: **Asset Name**, **Asset Type (Font/Image)**, **Source URL**, **License Type (Commercial Use Allowed = Yes)**, **License Proof Path**, and **Date**.
- **Strict Ban:** Never use "Personal Use Only" assets, unlicensed stock, or copied competitor cover art.

### Step 4: Format the Interior & Front/Back Matter (Free Tools First)
Use free tools first: **KDP Word/Interior Templates, Kindle Create, LibreOffice, or Google Docs** *(Paid tools like Vellum may only be listed as options, never used without Samir's written approval)*.
1. **Typography:** Set body font to **Georgia, Garamond, or Times New Roman at 11pt or 12pt** `[COURSE]`.
2. **Required Front & Back Matter Sequence `[COURSE]`:**
   - **Front Matter:** Title Page → Copyright + Disclaimer Page → Table of Contents (TOC) → *"Your Free Gift"* Page (if applicable) → Introduction.
   - **Body:** Chapters `1..N` → Conclusion.
   - **Back Matter:** **"Thank You" Page (MUST be 100% rewritten in original words—never copy the course template verbatim, as copied Thank You pages trigger KDP plagiarism warnings)** → Resources / References (APA) Page.
3. **Export Settings:** Export to print-ready PDF with **all fonts embedded**, **300 DPI** resolution, and exact KDP trim, bleed, and gutter margins.

### Step 5: Plan & Produce the Cover (Ebook + Paperback Wrap)
Use free tools first: **Canva (Free Tier), KDP Cover Calculator & Templates, GIMP, or Inkscape**.
1. **Ebook Cover:** Front cover (`WxH px` per KDP spec, 300 DPI).
2. **Paperback Full Wrap:** Front + Spine + Back + Barcode clear zone + Bleed, matching the KDP Cover Calculator template.
3. **Positioning & Compliance:** Ensure high-contrast, readable thumbnail typography that stands out against the Page-1 competitor covers analyzed in `Step_06`. Confirm zero trademark violations per `00B_kdp-policy-verification`.

### Step 6: Verify Final Files (Strict `FAIL-INCOMPLETE` Rule)
- Inspect the exported PDFs (via browser PDF properties or local check) to confirm:
  1. File opens cleanly without corruption.
  2. Exact trim/page dimensions match the spec.
  3. All fonts are embedded.
- **Honesty Rule:** If any verification check (such as embedded font inspection) cannot be performed in your current environment, mark that row **`FAIL-INCOMPLETE`** and ask Samir to verify it on his PC. **Never mark an unverified check as `PASS`.**

---

## 3. Required Output Formats

### File 1: Live Spec Capture (`09_Cover_and_Interior/specs_sources_<yyyymmdd>.md`)
```markdown
# KDP Live Technical Specifications Capture
Capture date: <YYYY-MM-DD>

- **Paperback Trim & Margin Rules:** "<Verbatim quoted dimensions/margins for page count>" [VERIFIED: <kdp_url>, <YYYY-MM-DD>]
- **Paperback Spine Width Formula:** "<Verbatim quoted spine multiplier by paper type>" [VERIFIED: <kdp_url>, <YYYY-MM-DD>]
- **Ebook Cover Requirements:** "<Verbatim quoted pixel dimensions & file rules>" [VERIFIED: <kdp_url>, <YYYY-MM-DD>]

# Cover & Interior Spec — <Book Title>
<!-- skill: Step_12_kdp-cover-interior-design -->
Shortname: <shortname>
Trim size: <W x H in> — source: <URL> captured <YYYY-MM-DD>
Bleed: <in> · Margins (inside/outside/top/bottom): <in> — source: <URL> <YYYY-MM-DD>
Spine width: <in> (page count <N> x <paper factor>) — formula source: <URL> <YYYY-MM-DD>
Full wrap dimensions (W x H in): <W x H in> — source: <URL> <YYYY-MM-DD>
Interior font: <Georgia|Garamond|Times New Roman>, <11|12>pt — licence: <path_or_url>
Cover font(s): <name(s)> — licence: <path_or_url>
Image licences: <path(s) or "Text-only / No external images used">
Ebook cover: <path>, <WxH px>
PDF settings: <embedded fonts, 300 DPI, KDP preset>
Created: <YYYY-MM-DD>

## 1. Front & Back Matter Checklist
- [x] Title Page
- [x] Copyright & Disclaimer Page
- [x] Table of Contents
- [x] "Your Free Gift" Page (or N/A)
- [x] Introduction, Body Chapters, Conclusion
- [x] "Thank You" Page (100% rewritten in original words)
- [x] Resources & References (APA) Page

## 2. Licence Register (100% Commercial-Use Verified)
| Asset Name | Type (Font / Image) | Source URL | Commercial Licence Allowed? | Licence Proof Path | Captured Date |
|---|---|---|---|---|---|
| <Font/Asset> | Font | <URL> | Yes [VERIFIED] | `09_Cover_and_Interior/...` | <YYYY-MM-DD> |

## 3. File Verification Table
| Deliverable File | Opens Cleanly? | Matches KDP Spec (Trim / Bleed / Embedded Fonts)? | Verdict (`PASS` / `FAIL` / `FAIL-INCOMPLETE`) | Evidence / Action Needed |
|---|---|---|---|---|
| Interior PDF (`<path>`) | <Yes/No> | <Details> | <Verdict> | <Browser check or "Needs Samir PC font-embed check"> |
| Paperback Wrap PDF (`<path>`) | <Yes/No> | <Details> | <Verdict> | <Evidence> |
| Ebook Cover (`<path>`) | <Yes/No> | <Details> | <Verdict> | <Evidence> |
