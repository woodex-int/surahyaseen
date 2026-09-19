# Surah Yaseen — Biya Gallery / The Third Art

Lahore gallery project: Quran folio art (Thread Art) and its presentation decks.

## Current deliverables

| File | What it is |
|---|---|
| **`Surah Yaseen - Master Pitch Deck (71 Folios) - v1.pptx`** | **THE SALE DECK (current)** — 93-slide, 16:9, fully editable. 4-part pitch (Vision · The Work · The Seventy-One Folios · Acquisition). Exactly **71 folio slides, one per image, every folio with its polished + compressed frame attached**. Each carries the transcribed panel caption, Uthmani Arabic, and Pickthall English. Refrain folios (31) are marked "the recurring question"; 18 refrain verse-numbers are flagged for verification. No Urdu. Pricing is placeholder ranges, to be confirmed before release |
| **`Surah Yaseen - The Sacred Letters Edition (83 Verses) - v1.pptx`** | The Yaseen edition — 103-slide editable master deck: chapter analysis, commission plan, all **83 verses one slide each** (reserved plates), timeline, acquisition, exhibition |
| **`YASEEN_INVENTORY.csv`** | 83-row release checklist — every verse verified against the Uthmani codex (alquran.cloud, 19 Sep 2026) with Pickthall renderings |
| **`YASEEN_EDITION_PLAN.md`** | The edition's master plan: architecture, ten movements, design system, pipeline, 2026 timeline |
| `Surah Yaseen - The Heart of the Quran (28 Slides) - FIXED.pptx` | Original 28-slide deck (source of the design system; media re-extracted per turn) |
| `1.png` … `71.png` | The 69 folio frame images from the original deck (missing 4, 46) — all are Surah Ar-Rahman (55), verified frame-by-frame |
| `biyas-art-gallery.zip` | Gallery website project (design-system source) |
| `PROJECT_ANALYSIS_REPORT.md` | Initial project analysis (per-frame surah IDs in it were later corrected: all 71 frames = Ar-Rahman) |

## Working notes

- The workspace was reset to the original repo state on 19 Sep 2026; earlier-session
  artifacts (the 106-slide Rahman master deck, its print zip and inventory CSV) are no
  longer on disk. The Yaseen edition above was rebuilt from verified source data and is
  the current, self-contained deliverable.
- The Yaseen deck is fully editable: each of the 83 verse slides carries its own
  reserved plate — finished artwork drops straight into the frame on its slide.
- The master pitch deck's 71 folio labels were transcribed from the physical panel
  captions and matched to the Uthmani codex (alquran.cloud) — this corrected four
  wrong `reference` values in `FOLIO_METADATA.csv` (F33=55:37, F37=55:41, F40=55:43,
  F41=55:44). F70 and F71 are verified codex repeats (55:66, 55:74). F04 and F46
  remain reserved frames (photography pending). Frames are polished (contrast/color/
  sharpen) and compressed to 1250 px / JPEG q75 for the deck.
- Fonts: install **Playfair Display** + **Jost** (Google Fonts) for an exact match;
  the deck falls back to Georgia/Arial gracefully. Uthmani script uses the
  **Simplified Arabic** typeface (ships with Microsoft Office).
