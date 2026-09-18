# Project Analysis Report — `woodex-int/surahyaseen`

**Date:** 18 September 2026
**Scope:** Complete analysis of the repository (all 72 tracked files, ~249 MB), including unpacked inspection of the PPTX and the gallery website ZIP.
**Method:** Git forensics, OOXML (PPTX) structure extraction and text mining, ZIP inventory, image-header inspection, and visual verification of sample frames.

---

## 1. Executive Summary

This repository is **not a software project** — it is an **art-sales asset repository** for **Biya Gallery Art & Craft (Lahore)** and its founder/artist **Biya Jee** (Naghmana Khursheed/Khurshid). It holds three distinct components:

| # | Component | What it is | Size |
|---|-----------|------------|------|
| A | `1.png … 71.png` (69 files present) | Photographs of framed, hand-painted Quranic art folios (1613×1314 px, ~3.3 MB each) | 220 MB |
| B | `Surah Yaseen - The Heart of the Quran (28 Slides) - FIXED.pptx` | A 28-slide, 16:9 sales/acquisition deck marketing a 70-folio Surah Yaseen collection to museums and collectors; machine-generated with python-pptx | 22 MB |
| C | `biyas-art-gallery.zip` | A complete static marketing-website project for the gallery (15 HTML pages, CSS/JS, 36 images) plus ~27 planning/audit docs, 3 agent prompts, and a WordPress Stage-2 template package | 8.6 MB |

**Headline findings**

1. 🔴 **Critical content mismatch:** The Yaseen deck uses frames `1.png`, `35.png`, `70.png` as the visual evidence for "Folio 01 / 35 / 70" of the *Surah Yaseen* collection — but visual inspection shows those frames depict verses from **other surahs** (Ar-Rahman, Al-Insan, and non-Yaseen verses; `71.png` is Al-Waqi'ah 76:26). **No genuine Yaseen folio images exist anywhere in this repository.** If the deck is sent to prospects as-is, it risks misrepresenting the collection.
2. 🟠 **Incomplete frame set:** `4.png` and `46.png` are missing — 69 of 71 frames (98.6%) are present.
3. 🟡 **The repo conflates two different folio series:** the gallery's own docs reference a separate "70 Surah Rehman folios" archive (its images are exactly the kind of Quranic-verse folios present here), while the Yaseen series being sold in the deck has no imagery.
4. 🟡 **Repo hygiene:** a single 249 MB commit ("Add files via upload", GitHub web UI), no README substance, no `.gitignore`, no per-frame metadata, opaque filenames, and the website project committed as a compressed snapshot rather than browsable files.
5. 🟢 **No code, no build, no secrets** — this is a pure content/art-asset repo, so there is no security surface beyond distribution etiquette.

---

## 2. Repository Composition

```
surahyaseen/                                   (72 files tracked, single commit f534636)
├── README.md                                  22 bytes — "# surahyaseen / project" (no substance)
├── 1.png … 71.png                             69 × framed-folio photographs, all 1613×1314 px, 220 MB total
│                                              (4.png and 46.png MISSING)
├── Surah Yaseen - The Heart of the Quran
│   (28 Slides) - FIXED.pptx                   22 MB, 28 slides, 7 embedded images
└── biyas-art-gallery.zip                      82 files when extracted, 8.8 MB
    ├── 15 × HTML pages (index, founder, services, collections, portfolio,
    │   gallery, visit, faq, events, journal, poetry, product, b2b,
    │   custom-studio, third-art)
    ├── style.css (95 KB) · app.js (7 KB) · collections.js (1.6 KB)
    ├── portfolio/                             36 images (jpg/jpeg/png/webp)
    ├── ~23 planning & audit .md documents
    ├── agents/ 01-brand-content-archive, 02-frontend-wordpress-system, 03-qa-seo-launch
    ├── templates/stage2-template-package.json (WordPress Stage 2 plan, "planning_only")
    └── GALLERY_CONTENT_AGENT_SYSTEM_PROMPT.txt (chat-agent spec, BiyaArtGallery.pk)
```

**Git forensics**

- One commit: `f534636 "Add files via upload"` by `woodex-int`, 2026-09-18 21:36 UTC (Lahore time) — a GitHub web-UI upload, not a developer workflow.
- Working tree and `.git` are each ~249 MB (large binaries stored inline; no Git LFS).
- No `.gitignore`, no branches of interest, no CI, no hooks.
- No credentials, keys, or sensitive data found anywhere (content-only repo).

---

## 3. Component A — The 69 Folio Photographs

**Facts**

- All 69 images are identical in format: PNG, 1613×1314 px (4:3), ~2.4–4.1 MB each (avg 3.33 MB).
- Each photograph shows a **framed, hand-painted work**: Arabic calligraphic verse at top, hand-illustrated scene in the center, red artist signature ("Biyas"), a gold frame, cream matting, and a caption strip with **Urdu + English translation** of the verse.
- Visual quality is high and consistent — clearly photographs of finished physical artworks (not renders).

**Verified content (sample of 4 frames inspected visually)**

| Frame | Deck label | Actual verse content on the panel | Match? |
|-------|-----------|-----------------------------------|--------|
| `1.png` | "FOLIO 01 — YA-SIN OPENING: *Ya-Sin, by the wise Quran*" | Basmala + **"Al-Rahman 'allama l-Qur'an"** (Surah **Ar-Rahman** 55:1–2); caption: "(Allah) Most Gracious! It is He Who has taught the Qur'an" | ❌ |
| `35.png` | "FOLIO 35 — HEART OF THE COLLECTION: *the story of the messengers*" | A non-Yaseen verse about the Day of resurrection ("In the Day we convene…"), storm/palm illustration | ❌ |
| `70.png` | "FOLIO 70 — CLOSING DETAIL: *'Be, and it is'"* (Yaseen 36:82) | **"Fi-hima 'aynani nadi'htani"** — Surah **Al-Insan** 76:15–16 ("In them will be two springs…"), waterfall illustration | ❌ |
| `71.png` | "additional detail" (per deck's frame count) | **"Lam yattarr 'alayhi insun qablahum wa la jann"** — Surah **Al-Waqi'ah** 76:26 ("Whom no man or Jinn before them has touched"), lotus-pool illustration | ❌ (wrong surah, but consistent with an "extra" frame) |

**Interpretation.** The numbered set is a **mixed Quranic folio series** — consistent with the gallery's documented **"70 Surah Rehman folios"** archive (plus 1 extra detail frame = 71, exactly matching the deck's own line "71 frames total — 70 folios + additional details" and the website's 01–70 folio archive). These are **not** the Surah Yaseen folios the deck sells.

**Gaps**

- `4.png`, `46.png` missing → the 71-frame set is incomplete (recover the photos or document the gaps).
- **No per-frame metadata exists** (surah, verse, title, dimensions, edition, availability) — yet the gallery's own plans require a record for every work, and any collector inquiry would be unanswerable from this repo alone.

---

## 4. Component B — The 28-Slide Yaseen Deck

**Build & metadata**

- Generated by **python-pptx** (`docProps` literally states "generated using python-pptx"; `dc:creator` is empty; leftover template metadata from the python-pptx default template — "lastModifiedBy: Steve Canny", 2013 timestamps). The "FIXED" in the filename indicates a prior defective version; the metadata was never properly set.
- True slide size is **16:9** (12191969×6858000 EMU) although `app.xml` claims 4:3 — a harmless generator artifact.
- Contains a `printerSettings1.bin` (a PowerPoint save artifact).

**Structure** (all text extracted and verified)

| Slides | Section |
|--------|---------|
| 1 | Title — "A Handmade Third Art Masterpiece", 70 Physical Folios, Biya Jee / Biya Gallery, Lahore |
| 2–4 | Introduction: the chapter (83 verses, Makki, "Heart of the Quran") · the artist (practice since 1985, "First Lady of Third Art") · project vision (Preserve / Legacy / Bridge) |
| 5–9 | Design & Craftsmanship: 70-folio treatment · materials (24K gold leaf, evergreen base, archival paper) · content architecture (Arabic / Urdu / English, "71 frames total") · typography (Garamond/Caslon, gold ink, ivory) · QA |
| 10–15 | Content Showcase: Folio 01 (uses `1.png`) · Folio 35 (uses `35.png`) · Folio 70 (uses `70.png`) · gold-leaf calligraphy close-ups (2 images **not present in the repo**) · translation layout |
| 16–19 | Market Positioning: rarity ("No body can make and match" — grammar error) · investment value · comparison · target collectors |
| 20–23 | Acquisition: complete collection / individual folios / pricing tiers / preservation & care |
| 24–26 | Touring exhibition: concept · logistics & security · sponsorship |
| 27–28 | Contact & close ("A masterpiece for the ages") |

**Issues**

1. 🔴 **Misattributed imagery** (see §3) — the deck's three "evidence" folios are from another surah series. This conflicts with the gallery's own non-negotiable publishing rules found in the zip ("never publish… repeated placeholder or sample imagery as real artwork"; "do not describe a placeholder 70-folio grid as a real archive").
2. 🟡 **Unexplained 70-vs-83 gap:** Surah Yaseen has **83 verses** but the collection is **70 folios**; the deck never states how the mapping works (multi-verse folios? abridgement?). Museums and serious collectors will ask.
3. 🟡 **Copy errors:** "No body can make and match" (slide 16); eyebrow labels on slides 16–18 use the slide number ("| 16", "| 17", "| 18") instead of the 01/02 sub-numbering used everywhere else.
4. 🟡 **Two calligraphy-detail images (slides 13–14) exist only inside the PPTX** — if they're real gold-leaf close-ups they should be in the asset library; if they're stand-ins, same misrepresentation risk.
5. 🟡 Metadata (title/author/company) unset — unprofessional for a B2B acquisition document.

---

## 5. Component C — `biyas-art-gallery.zip` (Website Project)

A **self-contained, earlier/larger project**: a static marketing site for the gallery with heavy AI-assisted planning documentation.

**Site (15 pages, no framework, no build step)**

- Brand: "Biya Gallery Art & Craft | Art, Poetry & Thread Art from Lahore"; luxury system (deep evergreen, espresso, rich gold, champagne paper); scroll-reveal/parallax motion in `app.js`; reduced-motion support.
- Pages: home, founder, services, collections (filterable), artwork detail quick-view, portfolio, gallery, third-art (70-tile interactive folio archive), visit/private-viewing, faq, events, journal, poetry, product, b2b, custom-studio.
- SEO: titles, meta, Open Graph, ProfessionalService schema on Services.
- **Forms are front-end only** — no backend/email/CRM/WhatsApp wiring (documented as pending).
- The 70-tile "Third Art" archive **uses placeholder visuals** (per their own TODO and the non-negotiable rule "do not describe a placeholder 70-folio grid as a real archive").

**Planning documentation (~23 MD files)** — unusually rigorous for an art project:

- `PROJECT_START.md` — Stage 1 authorization: **planning only, no production edits**; lists 6 owner inputs still required (official founder spelling, **real 70-folio images and metadata**, book-library data, Punjabi Verha archive, approved records, business contacts).
- `PROJECT_COMPLETION_MASTER.md` — 3-stage delivery (Brand/Content/Archive → Frontend/WordPress → QA/SEO/Launch) and the non-negotiable publishing rules cited above.
- `PROJECT_TODO.md` (last updated 23 Aug 2026) — status: design, core pages and services experience **complete**; content, commerce and production **pending**; long "Needed from Biya Gallery" list (contact info, address, approved CV/portrait/quote, 12–20 launch artworks, 70 folio images/details, pricing & shipping policy, payment path decision).
- `WEBSITE_AUDIT.md` — a completed UI/UX audit pass with 4 content follow-ups.
- `agents/01–03` — role prompts for a 3-agent pipeline (Brand/Content/Archive, Frontend/WordPress, QA/SEO/Launch).
- `SURAH_REHMAN_ARCHIVE_PLAN.md` — interaction spec for the **70-folio Surah Rehman archive** (viewer + rail, prev/next, full-screen, keyboard support, inquiry hand-off prefilling "Surah Rehman — Folio XX").
- `templates/stage2-template-package.json` — WordPress Stage 2 plan, `stage: "planning_only"`, with a query contract requiring `verification_status: "Verified"` before any folio may appear in the archive.
- `GALLERY_CONTENT_AGENT_SYSTEM_PROMPT.txt` — a chat-agent spec for collectors/B2B (tone: "Not decoration. A presence."; hard rules against inventing availability/provenance/prices).

**Status (per its own docs):** Stage 1 complete; the site is a **designed but content-unfinished prototype**; WordPress migration is planned but not started; nothing is launch-ready.

---

## 6. Cross-Cutting Issues

1. **Two folio series are tangled.** The repo named *surahyaseen* sells a Yaseen collection (deck) but stores a **mixed/Rehman-series** image set (frames). The real Yaseen folios are absent. Either the Yaseen series isn't finished/photographed, or the wrong series was used as proof imagery.
2. **Brand-name instability:** "Biya Gallery Art & Craft" (site) vs "Biya's Art Gallery" (docs/zip name) vs "BIYA GALLERY | ART & CRAFT | LAHORE" (deck) — the zip's own TODO flags this as an unresolved owner decision. Artist spelling is likewise unresolved: **Naghmana Khursheed vs Khurshid** (explicitly "Pending Verification").
3. **Ownership of assets:** the website zip is committed as a zip blob — it cannot be diffed, linked, or evolved in-place.
4. **No metadata layer** for 69 unique artworks that are the core value of the repo.

## 7. Risk Assessment

| Risk | Severity | Notes |
|------|----------|-------|
| Misrepresentation of the Yaseen collection to museums/collectors (wrong surah imagery) | **High** | Directly conflicts with the gallery's own verified-records-only policy; could damage credibility with institutional buyers |
| Incomplete frame inventory (4, 46 missing) | Medium | Undermines "one-of-a-kind complete set" claims |
| Unversioned 249 MB binaries in git history, no LFS/ignore | Low–Medium | Bloated clones; history cannot be slimmed once committed |
| No per-frame records (title/verse/status) | Medium | Blocks verified publication, catalogue export, and collector inquiries |
| Deck copy/metadata quality (python-pptx defaults, grammar, numbering) | Low | Fixable in minutes |
| Unresolved brand/artist spelling | Medium | Affects every public artifact |
| Security | **None found** | No code, no secrets, no network surface |

## 8. Recommendations (prioritized)

1. **Resolve the folio attribution before any distribution** — photograph the actual Yaseen folios for slides 10–12, or re-label them "examples of the artist's Quranic folio work." Get the owner's explicit sign-off, per their own publishing rules. *(Owner decision required.)*
2. **Recover `4.png` and `46.png`** (or document their absence in an inventory file).
3. **Restructure the repo** for provenance and future work:
   ```
   assets/folios/       (frames, ideally renamed e.g. folio-001-ar-rahman-55-1-2.png)
   assets/details/      (gold-leaf close-ups currently only inside the PPTX)
   deck/                (PPTX)
   website/             (unzipped biyas-art-gallery, promoted to a subfolder or its own repo)
   ```
4. **Add a frame metadata file** (`assets/folios/metadata.csv` or JSON): frame #, surah, verse(s), title, dimensions, medium, series, verification status, availability — exactly the fields their Stage-2 WordPress query already expects.
5. **Add `.gitignore`**; consider **Git LFS** (or object storage) for future large binaries; generate web-sized derivatives if the site will serve these frames.
6. **Expand README.md** into a real project README: what the repo is, the three components, inventory status, open owner decisions, and a link to the website TODO list (the de-facto work queue).
7. **Deck polish:** set proper core properties (title/author/company), fix "No body can make and match", fix eyebrow numbering on slides 16–18, and add a short "verse mapping" note explaining 70 folios vs 83 verses.
8. **Unify naming** (owner decision): pick one public brand spelling and one artist-name spelling, then sweep deck + site + docs.
9. **Decide the website's fate:** keep it as a sibling repo/`website/` subdirectory with its own README, since it has its own living TODO and 3-stage plan; it is the right place to host the Yaseen folio archive once real imagery and metadata exist.

---

## Appendix — Verification Log

- PPTX: unpacked as OPC zip; 28 `slideN.xml` parsed; all `<a:t>` text extracted; `docProps` read; slide sizes read from `presentation.xml`; image→slide mapping from `slides/_rels`; media files md5-compared against repo PNGs (exact matches: `image3.png`=`1.png`, `image4.png`=`35.png`, `image5.png`=`70.png`; `image6/7.png` unique to deck).
- PNG set: count, missing-number scan, PNG header width/height for all 69 files (uniform 1613×1314), sizes; visual inspection of frames 1, 35, 70, 71.
- ZIP: full inventory (82 files); read `PROJECT_START`, `PROJECT_TODO`, `PROJECT_COMPLETION_MASTER`, `WEBSITE_AUDIT`, `SURAH_REHMAN_ARCHIVE_PLAN`, agent prompts, template JSON, system-prompt file, page titles/meta.
- Git: `git log`, `git ls-files` (72 files), remote/branch/commit metadata.
