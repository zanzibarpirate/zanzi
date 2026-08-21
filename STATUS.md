# CA PE Civil Surveying CBT — Project Status

Last updated: August 20, 2026 (Chelapati-17 transcription session, complete)

Read this first, before touching anything. It exists so a new chat session
doesn't have to reconstruct project history from scratch or accidentally
duplicate/undo work another session already did.

---

## Process rules (read before doing anything else)

1. **Only one active working session on this repo at a time.** Multiple
   parallel Claude chats editing and pushing independently is the single
   cause of every major bug this project has hit so far (mis-tagged
   questions, a vanished CSS fix, a duplicate Exam4 build). If you're
   starting a new session, treat any other open chat on this project as
   dead — don't return to it later and push from it.
2. **Pull before you start.** First action in any session: pull
   `zanzibarpirate/zanzi` from GitHub. Never assume an attached or
   remembered copy of `unified_simulator.html` is current — it's a large
   file and easy to accidentally work from a stale copy.
3. **Push before you stop**, even if the work feels incomplete. A session's
   changes sitting unpushed on someone's machine is exactly how the
   divergence problems happened before.
4. **Update this file before you stop**, if anything below changed. Keep it
   short — a few lines is enough for the next session to orient.

---

## Current state (as of last push)

**`unified_simulator.html`** — 720 questions total (FS-AM 85, FS-PM 85,
CPESR-Exam1 55, CPESR-Exam2 55, CPESR-Exam3 55, CPESR-Exam4 55,
CPESR-Exam5 55, CPESR-Exam6 55, CPESR-Exam7 55, CPESR-Exam8 55,
CPESR-Exam9 55, Chelapati-17 55). Zero duplicate ids confirmed across the
full set; max id 20055. **CPESR Exams 1–9 remain complete; a new,
separate source track (Chelapati-17) was added this session — see below.**

- ✅ **Chelapati-17: new source track, transcribed from scratch and
  merged** (55/55 questions, new ids 20001–20055). This is the project's
  first non-CPESR source: Chelapati, *P.E. (Civil) License Review Manual,
  Volume IX*, Section 15/Chapter 17, "Practice Examination for Engineering
  Surveying" (Professional Engineering Development Publications, 2001),
  supplied by the owner as a 17-page PDF scan. Chosen `source` tag:
  `Chelapati-17` (book+chapter, not `CPESR-ExamN`, to keep it visually and
  structurally distinct); id range 20001–20055, deliberately a separate
  block from the CPESR range (1–9055) so a future Chelapati chapter could
  get its own 21001+, 22001+, etc. without colliding.
  Notable characteristics of this source, different from every CPESR exam
  so far:
  - **The source contains zero worked solutions and zero marked answers**
    — only stems and four/five-way multiple choice. Every one of the 55
    solutions was independently derived using standard formulas and
    verified to land exactly on one of the source's own answer choices,
    each carrying a `Flagged item:` disclosure (same treatment as the
    Exam4 Q11/Q23 precedent, just applied to the entire exam rather than
    two questions).
  - **5 of 55 questions (28, 30, 44, 49, 50) had a completely blank
    "Paste-up Figure" placeholder in the source** — a pre-press production
    gap in the original 2001 printing (confirmed by direct inspection of
    the page rasters: genuinely blank, not a scan/crop artifact). Per
    owner's instruction this session, each of the 5 got an **illustrative
    reconstructed diagram** (stadia rod, transit vernier, contour hill,
    slope stake, contour-spacing comparison) built with assumed data
    chosen so the derivation lands on one of the given choices. Each is
    watermarked "RECONSTRUCTED — illustrative only, not the original
    figure" directly on the image and flagged in a separate `.recon-note`
    CSS block (new class, distinct from `.user-note`) explaining the gap
    and the assumption. These are placeholders standing in for lost
    source content, not real book figures — revisit if the owner ever
    locates a copy of the book with the figures intact.
  - 11 diagrams total embedded (6 cropped from the real source scans —
    Q1, Q9, Q15, Q16, Q18, Q20, Q21, Q38 — note that's 8 real ones, plus
    the 5 reconstructed ones above = 13 `<img class="diagram">` tags
    across the exam; optimized to 1-bit B&W PNGs for the real scans,
    small adaptive-palette PNGs for the color-coded reconstructions).
  - 2 real HTML `<table>` transcriptions for source data tables (Q2 DMD
    traverse latitude/departure table, Q41 field-notes D/R circle-reading
    table) plus a third shared table (Q51–54's BM/leveling notes,
    duplicated into each of the four questions so they're self-contained
    for standalone display, per the simulator's one-question-at-a-time
    rendering — the source itself presents it once as shared data ahead
    of all four).
  - One low-confidence item flagged distinctly from the rest: Q39 (rough
    grade stake cut/fill threshold) is a field-practice convention with
    no way to verify by calculation; answered with the most commonly
    cited value (5 ft) but explicitly marked lower-confidence in its note.
  - **23 cross-source fingerprint matches found (refined numeric filter,
    3+ digit / decimal numbers only — the naive 2+-digit filter produced
    217 near-total false positives from generic bearing/station notation
    like "00"/"20"/"12" and was discarded), none excluded**, consistent
    with established policy (only same-exam duplicates get tagged). The
    strongest and most interesting: Chelapati Q51–54 (the BM1=102.23
    leveling dataset) numerically matches **CPESR-Exam9 id 9023** and
    **CPESR-Exam2 id 2054** almost exactly (BS 2.12, FS 5.60/8.20/11.32/
    2.10/4.20, grades 88.00/91.15) — this is a known classic leveling
    problem already flagged once before as an Exam2↔Exam9 cross-match;
    it now appears in a third, entirely different source, which is a
    useful cross-check (Chelapati Q54's independently-derived "cut ≈ 2.7"
    matches CPESR 9023's marked answer of 2.75 almost exactly). Other
    matches are generic round-number coincidences (e.g. many traverse/
    curve problems sharing values like 400, 600, 100) and were not
    investigated further.
  - Standard validation suite all passed clean: 55 questions/55 answers,
    div-balance (both per-batch and after full merge), 112 KaTeX
    expressions in the standalone review file / 1949 across the full
    merged simulator, zero render failures, zero `\'` apostrophe-trap
    hits, zero `\"` arcsecond-accent-trap hits (a new instance of the
    same family of bug — backslash-escaped seconds marks in Q21 and Q41
    needed to be plain `"` characters, caught by extending the existing
    `\'`-trap scan to also check for `\"`), zero `\dfrac` blind-spot
    hits, zero duplicate ids post-merge (720 total, max id 20055).
  - Updated the one hardcoded string that needed it: landing subtitle
    (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6, 7, 8 & 9 (495) +
    Chelapati Ch.17 (55) — 720 questions combined"). The "not loaded"
    placeholder chip (`'PPI Sample'`) was left untouched — it refers to a
    different, still-not-loaded planned source unrelated to Chelapati.
- ✅ Exam9: **transcribed from scratch and merged** (55/55 questions, new
  ids 9001–9055). Source was an owner-provided PDF (`Exam_9_Solutions.pdf`,
  55 pages, one page per question) capturing the live
  CivilPESurveyingReview.com review site — stem, choices, marked
  correct/incorrect answer highlighting, diagram, and full worked solution
  all on one page per question. The repo's `Exam9_CBT_Simulator.html` was
  confirmed usable too (same embedded question/solution-image JSON pattern
  as Exam4's original source) and was used as a secondary/cross-check
  source, mainly for higher-resolution diagram crops.
  Notable findings from this session:
  - **No missing question this round** — sequential Question 1 through 55
    confirmed via OCR spot-check with zero gaps, unlike Exam7 (missing
    Q43) and Exam8 (missing Q23). No substitute question was needed.
  - **One stem/solution numeric discrepancy found in the source**, on Q2
    (id 9002): the stem states ∠B = 31°11'53", but the source's own Law
    of Sines substitution and marked correct answer are only consistent
    with ∠B = 31°11'55" (a 2" discrepancy). Transcribed the stem verbatim
    as given; the solution steps use 55" to match the source's own worked
    math and marked answer, flagged with a `Flagged item:` user-note —
    same treatment as the Exam7 Q23 diagram/text discrepancy precedent.
  - 30 diagrams cropped (38 embedded images total, some questions had
    both a question-stem diagram and a distinct solution diagram) from
    the 250-DPI PDF page rasters — each crop individually viewed and
    verified before embedding, per §6 of the formatting standard.
  - 5 real HTML `<table>` transcriptions for field-note/coordinate/data
    table source material (Q17 roadway grade BS/HI/FS, Q19 Roundhill Road
    profile leveling — question and filled solution versions, Q23
    BM1/grade cut-fill notes, Q27 cut/fill end-area data, Q38 NAD27/83
    northing/easting coordinate table) — real `<table>` markup, not
    cropped images, per §6.
  - 1 `.qa-thread` transcribed verbatim (Q33, a 2-comment student/
    instructor exchange about the sea-level-factor formula being removed
    from the course, including original timestamps).
  - **20 cross-exam fingerprint matches found, none excluded** — per
    established policy, cross-exam question reuse is expected and normal
    for this course, so no `duplicate_of` tags were added:
    - Q1 → id 3025 (Exam3): compound curve length
    - Q15 → id 4025 (Exam4): vertical angle to hilltop elevation
    - Q16 → ids 1038 (Exam1), 5048 (Exam5): rectangular lot area error
    - Q17 → ids 1045 (Exam1), 8045 (Exam8): roadway repaving cut/fill
    - Q18 → id 2037 (Exam2): bearing of CD from given points
    - Q21 → ids 4027 (Exam4), 7018 (Exam7): highway catchpoint station
    - Q23 → id 2054 (Exam2): BM1/grade cut-fill at station
    - Q24 → id 5042 (Exam5): vertical curve G2 from sign elevation
    - Q28 → ids 3035 (Exam3), 6029 (Exam6), 7025 (Exam7), 8013 (Exam8):
      antenna tower height (five-way match, earliest is Exam3)
    - Q3 → ids 4042 (Exam4), 6055 (Exam6): dirt road paving elevation
    - Q43 → id 3018 (Exam3): map scale cabinet-to-building distance
    - Q47 → ids 2016 (Exam2), 8034 (Exam8): sewer MH1/MH2 lowered-invert
      slope
  - Standard validation suite all passed clean: 55 questions/55 answers,
    div-balance (both per-file and after merge), 228 KaTeX expressions in
    the standalone review file / same count extracted post-merge from the
    parsed JSON, zero render failures, zero `\'` apostrophe-trap hits,
    zero `\dfrac` blind-spot hits (after fixing several unit-label wraps —
    `miles`/`mile`, `elevation`, `Rise`/`Run`, `acre` — to use `\text{}`),
    zero duplicate ids post-merge (665 total, max id 9055).
  - Updated the two hardcoded strings that don't auto-update: landing
    subtitle (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6, 7, 8 & 9 (495)
    — 665 questions combined") and the "not loaded" placeholder chip list
    (now just `['PPI Sample']` — `'CPESR 9'` removed since it's now
    loaded; no CPESR exams remain in the not-loaded placeholder).
- ✅ Exam8: **transcribed from scratch and merged** (55/55 questions, new
  ids 8001–8055). Source was an owner-provided PDF (`Exam_8_Solutions.pdf`,
  54 pages) capturing the live CivilPESurveyingReview.com review site
  (question stem, choices, marked answer, worked solution, per page).
  Notable findings from this session:
  - **Question 23 had no source page at all** — the PDF's page sequence
    jumps directly from Q22 to Q24, confirmed by both Claude and the owner
    independently before any transcription began. Per owner's instruction,
    substituted in a self-contained, no-diagram question from the existing
    bank (FS-AM id 33, dual-frequency GPS receivers, transcribed verbatim)
    rather than leaving a gap or fabricating content. Flagged clearly with
    a `Flagged item:` note disclosing the substitution — this item is not
    native Exam8 content and should be revisited if the owner ever locates
    the real Q23.
  - 33 diagrams cropped from the source PDF's page rasters (200 DPI) and
    embedded as base64 PNGs — each crop individually viewed and verified
    before embedding, per §6 of the formatting standard. Several questions
    had two diagrams (one accompanying the question stem, a different one
    in the solution) — both were kept distinct rather than reusing one.
  - 4 real HTML `<table>` transcriptions for field-note/data-table source
    material (Q28 traverse coordinates, Q37 field notes, Q45 level notes,
    Q46 borrow areas) — not rendered as cropped images, per §6's rule that
    genuine tables in the source should become real `<table>` markup.
  - 1 `.qa-thread` transcribed verbatim (Q55, a 3-comment student/
    instructor discussion, including original timestamps).
  - **7 cross-exam fingerprint matches found, none excluded** — per this
    session's explicit instruction, cross-exam question reuse is expected
    and normal for this course, so no `duplicate_of` tags were added; only
    genuine same-exam duplicates would be tagged, and none were found:
    - Q1 → ids 2023 (Exam2), 7047 (Exam7): plan/profile vertical scale
    - Q4 → id 7054 (Exam7): map planimeter area
    - Q12 → id 3024 (Exam3): sewer lateral/mainline manhole elevation
    - Q13 → ids 3035 (Exam3), 6029 (Exam6), 7025 (Exam7): antenna tower
    - Q26 → ids 5025 (Exam5), 6037 (Exam6): ditch construction staking
    - Q34 → id 2016 (Exam2): sewer MH1/MH2 lowered-invert slope
    - Q52 → ids 1014 (Exam1), 5017 (Exam5), 6022 (Exam6): highway slope
    (One additional fingerprint hit on Q39 against ids 4/49 (FS-AM) was
    checked and dismissed as a false positive — Q39's stem contains only
    a single trivial 2-digit number, its real data lives in the diagram.)
  - Standard validation suite all passed clean: 55 questions/55 answers,
    div-balance (both per-file and after merge), 259 KaTeX expressions in
    the standalone review file / 1609 across the full merged simulator,
    zero render failures, zero `\dfrac` blind-spot hits (after fixing
    several unit-label wraps — `Photo Scale`, `Rise`/`Run`, `compacted
    volume`, etc. — to use `\text{}`), zero duplicate ids post-merge.
  - Updated the two hardcoded strings that don't auto-update: landing
    subtitle (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6, 7 & 8 (440) —
    610 questions combined") and the "not loaded" placeholder chip (now
    `'CPESR 9'`, was `'CPESR 8-9'`).
- ✅ Exam7: **transcribed from scratch and merged** (55/55 questions, new
  ids 7001–7055). Source was a 92-screenshot owner-provided capture of the
  live CivilPESurveyingReview.com review site (questions + solutions,
  chronological order, confirmed via OCR spot-check before transcribing).
  Notable findings from this session:
  - **Question 43 had no source screenshot at all** — genuinely absent
    from the capture (confirmed by both Claude and the owner
    independently). Per owner's instruction, substituted in a
    self-contained, no-diagram question from Exam1 (original id 1001,
    LiDAR topic, transcribed verbatim) rather than leaving a gap or
    fabricating content. Flagged clearly with a `Flagged item:` note
    disclosing the substitution — this item is not native Exam7 content
    and should be revisited if the owner ever locates the real Q43.
  - Caught and fixed a **source typo** in Q22's area-under-curve formula
    (owner explicitly approved the fix): the trapezoidal-rule formula's
    final term was written as `h₀/2` (duplicating the first term) instead
    of `h₅/2`. Numeric substitution was already correct in the source;
    only the symbolic label needed correcting.
  - Q23 had a **minor diagram/text mismatch** in the source itself: the
    solution diagram's angle label at point E reads `266°37'57"` but the
    typed-out computation two lines below (and the marked correct answer)
    uses `266°37'55"`. Owner confirmed the computed value is correct.
    Used `266°37'55"` throughout the worked steps and added a `user-note`
    flagging the 2-second diagram/text discrepancy rather than silently
    reconciling it.
  - **4 cross-exam duplicates found and tagged** (`duplicate_of`), via the
    numeric-fingerprint scan against the other 500 questions already in
    the simulator:
    - 7018 → 4027 (Exam4): highway catchpoint-station cut-slope problem
    - 7025 → 3035 (Exam3), also matches 6029 (Exam6) — three-way
      duplicate, tagged against the earliest (Exam3)
    - 7030 → 1009 (Exam1): highway centerline grade calculation
    - 7041 → 5015 (Exam5): Johnson Street storm-drain elevation problem
  - Standard validation suite all passed clean: 55 questions/55 answers,
    div-balance (both per-file and per-entry after merge), 203 KaTeX
    expressions in the standalone review file / 1350 across the full
    merged simulator, zero render failures, zero `\dfrac` blind-spot
    hits, zero duplicate ids post-merge.
  - Updated the two hardcoded strings that don't auto-update: landing
    subtitle (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6 & 7 (385) — 555
    questions combined") and the "not loaded" placeholder chip (now
    `'CPESR 8-9'`, was `'CPESR 7-9'`).
- ✅ Exam4 Q11 and Q23: the two previously-flagged independently-derived
  solutions (see `CBT_Formatting_Standard.md` §7.6) have been **replaced
  with the owner's supplied source solutions** and un-flagged, this
  session, prior to starting Exam7. Q11's source method (approximate by
  breaking the cross-section into triangles/rectangles) was genuinely
  different from what had been derived; Q23's source method matched the
  prior derivation almost exactly and was just reformatted to the
  source's exact line breaks/notation. Mirrored into
  `unified_simulator.html` (ids 4011, 4023) and re-validated.
- ✅ Exam1–6: formatting standard applied, topic-tag audits complete,
  fully merged. No new issues found or touched this session — see prior
  session history in git log / earlier versions of this file for details
  on those audits if needed.
- ✅ Data-integrity: 555-question baseline (pre-Exam8) previously verified
  duplicate-free and gap-free; Exam8's merge preserved that (610 total,
  zero duplicate ids, all div-balanced, all KaTeX clean).

**Not yet started:**
- **No further CPESR source material is known to exist.** Exam9 completed
  the 1–9 numbering scheme. If the owner provides additional exams, treat
  it as a new track and confirm scope/numbering with them before starting
  — don't assume it continues at Exam10 without asking.
- **Chelapati Volume IX likely has other chapter-based practice exams**
  beyond Chapter 17 — if the owner supplies another chapter, treat it as
  its own new source (e.g. `Chelapati-<N>`) with its own id block
  (21001+, 22001+, ...), don't assume it continues Chelapati-17's range.
- Chelapati-17 Q28/30/44/49/50 reconstructed diagrams are placeholders
  standing in for a source that was genuinely blank in the original 2001
  printing — if the owner ever obtains a different printing/edition of
  the book with the figures intact, replace these five with the real
  content and drop the `.recon-note` flags.
- Systematic per-exam audit (line structure, comment format, broader
  topic-tag check beyond `vc`) — same treatment Exam1–3 already got —
  is still outstanding for **Exam4 through Exam9**. This is now the main
  remaining quality-assurance backlog for the project.
- **Watch for the `\'` KaTeX trap**: always use a plain apostrophe `'` for
  minute-marks in formulas, never `\'` (a LaTeX accent command that mostly
  "succeeds" with wrong visual output rather than throwing an error).
- **Cross-exam duplicate policy** (confirmed across multiple sessions,
  supersedes any earlier "tag all fingerprint matches" language elsewhere
  in project history): cross-exam question reuse is normal and expected
  in this course's mock-exam bank. Only genuine *same-exam* duplicates
  should ever get a `duplicate_of` tag; cross-exam fingerprint matches are
  logged for awareness only and left untagged/included.
- Open owner-facing items, not yet resolved:
  1. No real source for Exam7 Q43 or Exam8 Q23 was ever located — the
     substitutes (Exam1 id 1001 for Q43; FS-AM id 33 for Q23) are
     placeholders, not fixes. Revisit if the owner finds the missing
     source material for either.
  2. Exam9 Q2's ∠B stem/solution discrepancy (53" vs 55") was resolved
     per the established precedent (use the source's own worked value,
     flag the stem discrepancy) rather than asked about directly this
     session — worth a quick owner confirmation that this was the right
     call, same as it would be worth revisiting Exam7 Q23's precedent if
     the owner ever disagrees with it.
  3. `CBT_Formatting_Standard.md` §10's file list and status notes are
     stale (references Exam1–4 only) — worth a cleanup pass.
  4. Chelapati-17 Q28/30/44/49/50: the owner explicitly asked this session
     to reconstruct illustrative diagrams and derive answers rather than
     leave placeholders, given the source pages were genuinely blank —
     worth a quick owner confirmation that the reconstructed figures and
     assumed data are an acceptable stand-in, same spirit as the Exam7
     Q43/Exam8 Q23 substitute-question precedent but a new variant of it
     (reconstructed figure instead of a substituted whole question).
  5. Chelapati-17 Q39 (rough grade stake threshold) and Q13 (offset stake
     spacing) are field-practice-convention questions with no way to
     verify by calculation — answered with the most commonly cited
     convention but flagged as lower-confidence; worth owner review if
     they have access to the actual source's answer key.

---

## Files in this repo relevant to the simulator

- `unified_simulator.html` — the live combined simulator (large; mostly
  base64 image data, don't put this in Project Knowledge — attach directly
  to a chat or have Claude pull it from GitHub instead)
- `Exam1_Compiled_Review.html` through `Exam9_Compiled_Review.html` —
  standalone formatted review docs per exam, source of truth for their
  respective exam's content in the simulator
- `Chelapati17_Compiled_Review.html` — standalone formatted review doc for
  the new Chelapati-17 source (55/55 questions), same role as the ExamN
  review docs above but for this non-CPESR track
- All raw CPESR source material (Exams 1–9) has now been consumed; no
  outstanding unprocessed `ExamN_CBT_Simulator.html` raw-source files
  remain in the repo as of this update.

## Where the formatting rules live

See the separate formatting-standard doc (in Project Knowledge) for the
detailed rules: line-by-line solution structure, KaTeX/`\dfrac`
conventions, CSS sizing values, comment format (`.user-note` vs
`.qa-thread`), diagram-handling rules, and the checklist for adding new
questions. This file is status/history; that one is the rulebook.
