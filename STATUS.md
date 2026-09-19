# CA PE Civil Surveying CBT — Project Status

Last updated: September 18, 2026 (PassPE-2026-1 transcription session, complete)

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
5. **Stay scoped to what the owner asked for.** If a pre-existing backlog
   item (e.g. a bug noted in an earlier session) is discovered while doing
   unrelated work, log it in this file rather than pivoting to fix it
   mid-session unless the owner explicitly asks. Silently chasing side
   issues instead of delivering the requested work is a process failure,
   not initiative — see the "KaTeX renderer gap" item below, which was
   flagged but deliberately NOT touched this session for exactly this
   reason.

---

## Current state (as of last push)

**`unified_simulator.html`** — 835 questions total (FS-AM 85, FS-PM 85,
CPESR-Exam1 55, CPESR-Exam2 55, CPESR-Exam3 55, CPESR-Exam4 55,
CPESR-Exam5 55, CPESR-Exam6 55, CPESR-Exam7 55, CPESR-Exam8 55,
CPESR-Exam9 55, Chelapati-17 55, CPESR-Timed1 55, PassPE-2026-1 60). Zero
duplicate ids confirmed across the full set; max id 40060. **CPESR
Exams 1–9, Chelapati-17, and CPESR-Timed1 remain complete; a new source
track (PassPE-2026-1) was added this session — see below. CPESR-Untimed1
is still the next planned workstream (unaffected by this session — see
"Not yet started" and the kickoff prompt at the end of this file).**

- ✅ **PassPE-2026-1: new source track, transcribed from scratch and
  merged** (60/60 questions, new ids 40001–40060). Source: two
  owner-provided PDFs from passpe.com (Dr. Shahin A. Mansour, PE),
  "Challenging Surveying Exam #1" (PassPE 2026 edition) — a clean
  problem-only PDF (machine text layer, used for verbatim stem/choice
  transcription and diagram cropping) and a handwritten worked-solutions
  PDF. This is the project's first source from passpe.com (distinct from
  both the CivilPESurveyingReview.com/CPESR track and the Chelapati book
  track). Chosen `source` tag: `PassPE-2026-1`; id range 40001–40060,
  deliberately a separate block from CPESR (1–30055) and Chelapati
  (20001–20055) so a future PassPE exam could get its own 41001+, etc.
  without colliding — also clear of the CPESR-Untimed1 block already
  reserved at 31001–31055.
  Notable characteristics of this session's work:
  - Stems and choices transcribed verbatim from the clean problem PDF's
    text layer (not OCR'd from images), giving high transcription
    confidence for that part.
  - 12 diagrams cropped from the clean problem PDF's page rasters (slope-
    stake notation tables ×2 variants shared across Q1–5/Q31–32 and
    Q49–50, a triangle-parcel figure, a sewer profile, two contour maps,
    a traverse diagram, a typical roadway section, a parcel diagram, and
    two solid-figure earthwork diagrams) — each viewed and verified before
    embedding per §6. One additional derivation-only sketch (the dimensioned
    cross-section used to work Q1–5/Q31–32) was cropped from the
    **handwritten solutions PDF** (not the clean problem PDF) since the
    source's own solution key relies on it and it isn't repeated on every
    question page — embedded as a solution-only diagram, not duplicated
    into the question diagram, per §6's "never duplicate a question's
    diagram into its solution" rule (this is the reverse case: a solution
    diagram not present on the question page).
  - Genuine data tables (traverse coordinates, stadia readings, level
    notes) transcribed as real `<table>` markup, not images, per §6.
  - Every answer independently verified by calculation before
    transcription. All 60 match the source's own marked/circled choice
    **except** where flagged below.
  - **4 questions had no worked solution in the source PDF — only a
    circled answer choice** (Q34 curve-arc-length, Q57 parcel-course
    length, Q59 solid-figure volume, and implicitly Q60 which *was*
    worked and was used to back-solve Q59). Treated per the established
    Exam4 Q11/Q23 and Chelapati precedent: independently derived,
    verified against the marked answer, and disclosed with a `Flagged
    item:` note in each. Q34's independent derivation (~214.5 ft) doesn't
    land exactly on the source's marked choice (C, 214.92 ft) — this
    discrepancy is disclosed explicitly rather than silently reconciled,
    same treatment as the Exam9 Q2 and Exam7 Q23 precedents.
  - **Q51** or (ditch offset/slope-stake question) is solved in the
    source by trial-and-error/back-substitution against the answer
    choices rather than a forward derivation — that method is reproduced
    faithfully rather than substituted with a cleaner derivation the
    source didn't use.
  - Standard validation suite all passed clean: 60 questions/60 answers,
    div-balance (per-question and after full merge), 105 KaTeX
    expressions, zero render failures (validated with the real `katex`
    npm package), zero `\'` apostrophe-trap hits, zero `\"` arcsecond-trap
    hits, zero `\dfrac` blind-spot hits (manual scan), zero stray Unicode
    whitespace, zero duplicate ids post-merge (835 total, max id 40060).
  - A **new failure mode was caught and fixed this session**: several
    plain-language conceptual answers (e.g. "infrared light has a longer
    wavelength than visible light") were initially wrapped in KaTeX math
    delimiters along with the real formulas, which both mis-renders prose
    as math and, in one case, caused a literal `%` character to be parsed
    as a LaTeX comment. Fixed by introducing a plain-text (non-KaTeX)
    variant of the solution-step span for non-formula conclusion lines —
    worth adding to the formatting standard as a new item to watch for
    (see suggested §3 addition below).
  - **Also caught and fixed**: the `qimg` vs `qhtml` JSON field
    distinction. `qimg` is expected to hold a bare base64 data-URI (the
    render code wraps its own `<img>` tag around it); a full `<img
    class="diagram" ...>` tag string belongs in `qhtml` instead. Several
    "given data" diagrams (the slope-stake tables, stadia/level/
    coordinate tables) were initially placed only inside the *solution*
    HTML, which would have hidden essential problem data from the person
    until after they answered — moved to `qhtml` so they display with the
    question itself, and removed the resulting duplication from the
    solution.
  - Numeric-fingerprint duplicate scan against the (then) 775-question
    baseline found only weak, generic round-number coincidences (100,
    200, 1000, 1910, etc. — the multiplying-constant/typical-station
    values common across many stadia and construction problems), none
    investigated further, consistent with established policy.
  - Built `PassPE2026-1_Compiled_Review.html`, the standalone review file
    for this source, using the same head/CSS structure as
    `Chelapati17_Compiled_Review.html`. Validated: 60/60 questions
    present, div-balanced.
  - Updated the one hardcoded string that needed it: landing subtitle
    (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6, 7, 8 & 9 (495) +
    Chelapati Ch.17 (55) + CPESR Timed 1 (55) + PassPE 2026 Challenging
    Exam 1 (60) — 835 questions combined"). The "not loaded" placeholder
    chip was not touched — unrelated to this source.
- ✅ Exam1–9, Chelapati-17, and CPESR-Timed1: complete, no changes this
  session — see prior versions of this file / git log for full detail.
- ✅ Data-integrity: 775-question baseline (pre-PassPE-2026-1) previously
  verified duplicate-free and gap-free; this session's merge preserved
  that (835 total, zero duplicate ids, all div-balanced, all KaTeX clean).

- ✅ **CPESR-Timed1: new source track, transcribed from scratch and
  merged** (55/55 questions, new ids 30001–30055). Source was an
  owner-provided PDF (`CPESR_TIMED_Test_1.pdf`, 84 pages) capturing the
  live CivilPESurveyingReview.com "Timed Test #1" — stem, choices, full
  worked "ANSWER EXPLANATION" solution, and (for most questions) a
  student/instructor Q&A comment thread, all in the same format as
  Exam1–9. Chosen `source` tag: `CPESR-Timed1`; id range 30001–30055,
  deliberately spaced apart from the CPESR-Exam1–9 range (1001–9055) and
  the Chelapati-17 range (20001–20055) so a same-format "Timed Test #2"
  or "Untimed Test 1/2" could get their own blocks (31001+, 32001+, ...)
  without colliding. **CPESR-Untimed1 is next — see "Not yet started"
  below and the ready-to-paste kickoff prompt at the end of this file.**
  Notable characteristics of this session's work:
  - Standard verbatim-transcription treatment throughout (not
    independently-derived like Chelapati-17) — every solution came
    straight from the source's own "ANSWER EXPLANATION" text.
  - 24 diagrams embedded (mix of question-stem and solution diagrams,
    cropped from the 200-DPI PDF page rasters, each individually viewed
    before embedding per §6 of the formatting standard); optimized to
    1-bit B&W PNGs for line art, small adaptive-palette PNGs kept in color
    for two diagrams where color was load-bearing (Q13's NGVD29→NAVD88
    datum-shift map, Q18's GIS raster/vector illustration).
  - 5 real HTML `<table>` transcriptions for source data tables (Q14
    road-centerline field notes with a stacked side-shot NOTES row, Q24
    Roundhill Road profile-leveling notes — **same dataset already in the
    bank at Exam3 id 3038/Exam5 id 5020**, Q31 OG/FG elevation table, Q37
    differential-leveling BS/FS notes, Q39's project-parameter table, Q40
    BS/FS points table, Q54 elevation/area contour table).
  - Roughly two dozen Q&A threads transcribed verbatim, ranging from
    single comments to a 6-sub-thread/14-comment discussion on Q15
    (roadway cross-slope ambiguity) — largest thread encountered in the
    project to date. Several threads had no visible author/timestamp
    metadata in the source; per the established Exam9 Q33 precedent, these
    got a blank `qa-author` for the student comment and generic
    `"Instructor"` for the reply rather than a fabricated name.
  - **20 cross-exam fingerprint matches found (tightened filter: ≥2
    numeric tokens in the stem AND ≥90% stem-word overlap, to cut down
    false positives from generic short stems), none excluded** — per
    established policy, cross-exam question reuse is expected and normal
    for this course. Two matches are worth flagging specifically:
    - Q14 and Q24 both reuse the "Roundhill Road" profile-leveling
      dataset already seen at Exam3 id 3038/Exam5 id 5020 — same table,
      different specific question asked each time (a recurring dataset
      across this course's question bank, now confirmed in a fourth
      place).
    - Q24 is a near-exact duplicate of Exam3 id 3038 (identical stem,
      identical table, choices reordered) — logged, not excluded,
      consistent with cross-exam policy.
    - Other matches (Q7↔8053, Q8↔3010, Q9↔3054, Q40↔3013, etc.) are
      exact-stem reuses with reordered choices, same treatment.
  - Standard validation suite all passed clean: 55 questions/55 answers,
    div-balance (per-batch and after full merge), 208 KaTeX expressions
    across the full standalone review file, zero render failures, zero
    `\'` apostrophe-trap hits, zero `\"` arcsecond-trap hits (checked
    carefully given heavy DMS/bearing notation in Q22/Q30/Q34/Q36/Q52),
    zero duplicate ids post-merge (775 total, max id 30055).
  - `\dfrac` blind-spot manual scan (per §3 of the formatting standard)
    caught **6 unit-label violations across the batch** that the
    automated KaTeX render check did not catch (bare `ft`/`cy`/`m³`/
    `hectare`/`Photo Scale` text inside `\dfrac{}` instead of wrapped in
    `\text{}`) — all fixed: Q4 (`1cy/27ft³`), Q6 (`30ft/1176ft`), Q13
    (`1ft/304mm`), Q25 (`ft²/acre`), Q31 (`ft/ft` ratio), Q39
    (`Photo Scale` label), Q47 (`1cy/27ft³`), Q54 (`m³`/`ft³`/`hectare`
    conversion factors). This confirms the blind-spot is a recurring
    pattern specifically around compound unit-conversion fractions and is
    worth extra attention in future batches, not a one-off.
  - Built `CPESR-Timed1_Compiled_Review.html`, the standalone review file
    for this source (same role as the `ExamN_Compiled_Review.html` files),
    using the exact head/CSS/KaTeX-script block copied from
    `Exam5_Compiled_Review.html` (a known-good file — confirmed to include
    both `katex.min.js` and the `auto-render` script, not just the CSS).
    Validated: 55/55 questions present, div-balanced, KaTeX renderer
    (CSS + JS + auto-render) all present.
  - Updated the one hardcoded string that needed it: landing subtitle
    (now "FS (170) + CPESR Exam 1, 2, 3, 4, 5, 6, 7, 8 & 9 (495) +
    Chelapati Ch.17 (55) + CPESR Timed 1 (55) — 775 questions combined").
    The "not loaded" placeholder chip was not touched this session — it
    still refers to a different, unrelated planned source.
- ✅ Exam9, Exam8, Exam7, Chelapati-17, and earlier exams: complete, no
  changes this session — see prior versions of this file / git log for
  full detail on those sessions if needed.
- ✅ Data-integrity: 720-question baseline (pre-Timed1) previously verified
  duplicate-free and gap-free; Timed1's merge preserved that (775 total,
  zero duplicate ids, all div-balanced, all KaTeX clean).

**Not yet started:**
- **CPESR-Untimed1 is still the next workstream** (unaffected by this
  session). Owner-provided source: `CPESR_UNTIMED_Test_1.pdf` (73 pages,
  same CivilPESurveyingReview.com format as Timed1 — full worked
  solutions + Q&A threads). Planned id block: 31001–31055 (leaving
  30001–30055 for Timed1 and 40001–40060 for PassPE-2026-1, both already
  taken — matching the spacing convention). A ready-to-paste kickoff
  prompt for this session is included at the end of this file (baseline
  numbers in it have been updated to reflect PassPE-2026-1's merge).
- **KaTeX JS-renderer gap — flagged, NOT fixed this session (see process
  rule 5 above).** While building the Timed1 standalone review file, it
  was noticed that `Exam6_Compiled_Review.html`, `Exam7_Compiled_Review.html`,
  and `Chelapati17_Compiled_Review.html` link `katex.min.css` but appear to
  be missing the `katex.min.js` and `auto-render.min.js` script tags —
  equations would display as raw LaTeX instead of rendering in those three
  standalone files. `Exam6_Compiled_Review.html` additionally appeared to
  be missing its `</head>`/`<body>` tags entirely, which is a bigger
  structural issue than the other two. **This was not touched or fixed —
  it needs its own dedicated session/task, explicitly scoped by the owner,
  rather than being folded into exam-transcription work.** Confirm still
  reproducible before fixing, since this note is based on a single grep
  pass, not a full audit.
- **No further CPESR-ExamN source material is known to exist** beyond
  Exam1–9. If the owner provides additional exams, treat it as a new
  track and confirm scope/numbering with them before starting.
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
  is still outstanding for **Exam4 through Exam9**. This is a long-running
  quality-assurance backlog item, not new this session.
- **Watch for the `\'` and `\"` KaTeX traps**: always use plain `'` and
  `"` characters for minute/second marks in formulas, never `\'`/`\"`
  (LaTeX accent commands that mostly "succeed" with wrong visual output
  rather than throwing an error).
- **Watch for the `\dfrac` unit-label blind spot**: bare unit/label text
  inside `\dfrac{}{}` (not wrapped in `\text{}`) passes automated KaTeX
  validation but renders wrong. This hit 6 times in the Timed1 batch alone
  (see above) — always do the manual eyeball scan per §3 of the
  formatting standard, don't rely on the automated render check alone.
- **Cross-exam duplicate policy** (confirmed across multiple sessions):
  cross-exam question reuse is normal and expected in this course's
  mock-exam bank. Only genuine *same-exam* duplicates should ever get a
  `duplicate_of` tag; cross-exam fingerprint matches are logged for
  awareness only and left untagged/included.
- Open owner-facing items, not yet resolved (carried forward from earlier
  sessions, unrelated to Timed1):
  1. No real source for Exam7 Q43 or Exam8 Q23 was ever located — the
     substitutes (Exam1 id 1001 for Q43; FS-AM id 33 for Q23) are
     placeholders, not fixes.
  2. Exam9 Q2's ∠B stem/solution discrepancy (53" vs 55") — worth a quick
     owner confirmation the established resolution was the right call.
  3. `CBT_Formatting_Standard.md` §10's file list and status notes are
     stale (references Exam1–4 only) — worth a cleanup pass.
  4. Chelapati-17 Q28/30/44/49/50 reconstructed diagrams — worth a quick
     owner confirmation the reconstructed figures/assumed data are an
     acceptable stand-in.
  5. Chelapati-17 Q39 and Q13 — field-practice-convention questions with
     no way to verify by calculation, flagged as lower-confidence.
  6. PassPE-2026-1 Q34 (curve arc length) — the source shows no worked
     steps, only a circled answer (C, 214.92 ft); an independent
     derivation lands closer to ~214.5 ft. The source's marked answer was
     used, with the discrepancy disclosed in the question's `Flagged
     item:` note — worth owner review if they have access to the
     official solution method.
  7. PassPE-2026-1 Q57 and Q59 — also had circled-only answers with no
     worked steps; independently derived and verified to land on the
     marked choice, flagged the same way as item 6.

---

## Files in this repo relevant to the simulator

- `unified_simulator.html` — the live combined simulator (large; mostly
  base64 image data, don't put this in Project Knowledge — attach directly
  to a chat or have Claude pull it from GitHub instead)
- `Exam1_Compiled_Review.html` through `Exam9_Compiled_Review.html` —
  standalone formatted review docs per exam, source of truth for their
  respective exam's content in the simulator
- `Chelapati17_Compiled_Review.html` — standalone formatted review doc for
  the Chelapati-17 source (55/55 questions)
- `CPESR-Timed1_Compiled_Review.html` — standalone formatted review doc
  for CPESR-Timed1 (55/55 questions), same role as the ExamN review docs
  above. Confirmed to include the full KaTeX renderer (CSS + JS +
  auto-render script).
- `PassPE2026-1_Compiled_Review.html` — **new this session** — standalone
  formatted review doc for PassPE-2026-1 (60/60 questions), same role as
  the other review docs. Built with the known-good KaTeX head (CSS + JS +
  auto-render script + init call, copied from `Exam5_Compiled_Review.html`
  after confirming `Chelapati17_Compiled_Review.html` — the file this
  file's CSS block was otherwise based on — is one of the files missing
  the JS renderer per the still-open "KaTeX JS-renderer gap" item below;
  that gap was NOT fixed in the older files this session, only avoided in
  the new one).
- All raw CPESR-ExamN source material (Exams 1–9) has been consumed.
  `CPESR_UNTIMED_Test_1.pdf` is the next unprocessed raw source, supplied
  by the owner outside the repo (see kickoff prompt below for path).

## Where the formatting rules live

See the separate formatting-standard doc (in Project Knowledge) for the
detailed rules: line-by-line solution structure, KaTeX/`\dfrac`
conventions, CSS sizing values, comment format (`.user-note` vs
`.qa-thread`), diagram-handling rules, and the checklist for adding new
questions. This file is status/history; that one is the rulebook.

---

## Ready-to-paste kickoff prompt for the next session (CPESR-Untimed1)

Copy everything below into a **fresh chat session** (not this one) along
with the project's Project Knowledge (this file + `CBT_Formatting_Standard.md`)
attached, plus the `CPESR_UNTIMED_Test_1.pdf` source file.

```
Continue the CA PE Civil Surveying CBT simulator project. Read
STATUS.md and CBT_Formatting_Standard.md first — STATUS.md is
authoritative over anything you remember from before.

This session's task: transcribe CPESR-Untimed1 from the attached
CPESR_UNTIMED_Test_1.pdf (73 pages) into the simulator, following the
exact same workflow used for CPESR-Timed1 (see STATUS.md's Timed1
section for the reference case, including the \dfrac unit-label
blind-spot pattern to watch for, and the PassPE-2026-1 section for two
more recently-caught gotchas: keep plain-language conceptual answers out
of \( \) KaTeX delimiters, and remember qimg wants a bare data-URI while
a full <img> tag belongs in qhtml).

Scope for this session:
1. Pull zanzibarpirate/zanzi fresh from GitHub first.
2. Confirm baseline: unified_simulator.html should have 835 questions,
   zero duplicate ids, max id 40060.
3. Transcribe all 55 questions from CPESR_UNTIMED_Test_1.pdf verbatim
   (stems, solutions, diagrams, and any Q&A threads), using id block
   31001–31055 and source tag "CPESR-Untimed1".
4. Work in batches of ~10 questions: transcribe, validate (KaTeX render
   check + manual \dfrac blind-spot eyeball scan + \\'/\\" trap scan +
   div-balance), checkpoint, then continue.
5. Run the numeric-fingerprint duplicate scan against the (by then)
   835-question baseline once all 55 are built; log cross-exam matches,
   don't exclude them, per established policy.
6. Merge into unified_simulator.html, update the landing-page subtitle
   (the only hardcoded string that needs it), and re-validate the merged
   file (890 questions expected, zero duplicate ids).
7. Build CPESR-Untimed1_Compiled_Review.html as a standalone review file,
   copying the head/CSS/KaTeX-script block from a known-good file (e.g.
   Exam5_Compiled_Review.html or the new CPESR-Timed1_Compiled_Review.html)
   — confirm it includes katex.min.js AND auto-render.min.js, not just
   the CSS.
8. Update STATUS.md with this session's results, following the same
   level of detail as the Timed1 entry.
9. Do NOT touch the KaTeX-renderer-gap issue noted in STATUS.md for
   Exam6/Exam7/Chelapati17 — that's an explicitly separate, not-yet
   scoped task. Stay focused on Untimed1 only unless I ask otherwise.
10. Push to GitHub before stopping (I'll provide a fresh token when
    you're ready to push), and confirm the push via a fresh clone.

Work through this systematically and check in with the compiled
CPESR-Untimed1_Compiled_Review.html and the updated unified_simulator.html
as the two deliverables at the end.
```
