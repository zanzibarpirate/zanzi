# CA PE Civil Surveying CBT — Project Status

Last updated: August 18, 2026 (Exam6 transcription session, in progress)

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

**`unified_simulator.html`** — 445 questions total (FS-AM 85, FS-PM 85,
CPESR-Exam1 55, CPESR-Exam2 55, CPESR-Exam3 55, CPESR-Exam4 55,
CPESR-Exam5 55).

- ✅ Exam5: **transcribed from scratch and merged** (55/55 questions) —
  first exam done as greenfield transcription rather than an audit-and-fix
  pass on existing content. Source images extracted from
  `Exam5_CBT_Simulator.html`'s embedded `EXAM_DATA`, same technique as
  Exam4. Notable findings from this session:
  - **This source file had a much higher rate of missing/incomplete
    solutions than Exam4 or earlier exams** — roughly 20-25% of questions
    had some form of gap (missing solution entirely, cut-off scan,
    incomplete comment thread), vs. a handful in Exam4. Every gap was
    flagged transparently rather than silently filled in.
  - Several questions initially had no visible worked solution and were
    independently derived, then verified against the marked answer. The
    owner subsequently supplied clean source images for most of these
    (Q1, Q3, Q6, Q9, Q23, Q36, Q39, Q43, Q7, Q54), which either confirmed
    the independent derivation or — in Q1 and Q23's case — **revealed the
    actual source used a different method than what was independently
    derived**:
    - Q1 (circular curve shaded area): source method uses a constructed
      point D that turns out to be the circle's center, making the
      answer a simple "sector minus triangle" calculation. The
      independently-derived triangle+segment approach had landed close
      (1,911,070 vs marked 1,911,082.45) but wasn't exact; replaced with
      the verified-exact source method.
    - Q23 (slope-stake grade problem): source method computes an
      intermediate `Elevation at D_CL` using the RPSS box's cut/fill
      sub-values, which had been avoided in the independent derivation
      because they couldn't be verified without a worked example. With
      the source image, the correct value (1.30% exactly) is now used;
      this was cross-confirmed by finding a duplicate of this exact
      question in Exam1 (id 1049) with the same correct answer.
  - Caught a **KaTeX blind-spot bug**: 27 instances of minute-marks
    written as `\'` (LaTeX accent command syntax) instead of a plain
    apostrophe. Only 4 threw hard render errors; the other 23 would have
    silently rendered an accent mark over the wrong character instead of
    a prime symbol. Fixed with a global find-replace, re-validated clean.
    Also found and cleaned up a harmless-but-untidy double-brace
    escaping artifact (`{{1}}` instead of `{1}`) left over from an
    f-string mistake, confined to 3 questions.
  - **3 new cross-exam duplicates found and tagged** (`duplicate_of`),
    on top of the 1 pre-existing tagged pair:
    - 5017 → 1014 (Exam1), 5023 → 1049 (Exam1): caught by the numeric
      fingerprint scan.
    - 5027 → 4046 (Exam4): **missed by the numeric fingerprint scan**
      because this question's numeric data lives entirely in an embedded
      diagram (an RPSS slope-stake box), not in the text stem — the
      fingerprint method only scans stem text. Found by recognizing the
      identical diagram data during transcription. Worth remembering:
      the numeric-fingerprint dedup method has this specific blind spot
      for diagram-heavy questions with generic-sounding stems.
  - Simulator merge used the same wholesale-parse-and-append approach
    proven on Exam4 (new ids 5001–5055, appended rather than
    field-patched since Exam5 had no prior simulator presence).
- ✅ Exam1–3: formatting standard applied (line structure, KaTeX, CSS —
  from the original Exam1 fixing session), **and now the topic-tag audit
  is also complete** (this session). Two categories of tag bugs found and
  fixed, present in both the standalone review files and the simulator:
  - **Merged cat+topic bug**: Exam3 Q9–Q55 (47 questions) had `cat` and
    `topic` concatenated into a single string (e.g. `"Igis"` instead of
    `"I"` + `"gis"`), with `topic` empty — same pattern already found and
    fixed in Exam4. Exam1 and Exam2 did not have this bug.
  - **Semantically wrong topic values**: 11 questions across Exam1–3 had
    syntactically valid but incorrect topic tags, found by cross-checking
    topic against actual question content (same method used for Exam4's
    Q29/Q37/Q38/Q39/Q40). Fixed:
    - 1004 (`trav`→`hc`): finding a curve's central angle, not a traverse
    - 1008 (`trav`→`area`): question explicitly asks "what is the area?"
    - 1046 (`photo`→`area`): plot-scale-for-paper-size question, not
      aerial photography (matches the Exam4 Q30 pattern for this question
      type)
    - 1050 (`gis`→`trav`): horizontal control network accuracy — nothing
      GIS-related about it
    - 1055, 2009 (`stadia`→`level`): both are vertical-angle/zenith-angle
      trig-leveling problems with no stadia-interval reading involved;
      genuine stadia questions (1015, 2034) specifically use stadia
      intervals/K,C constants — that's the actual distinguishing feature
    - 2023, 3004 (`photo`→`constr`): plan-and-profile sheet scale
      conversions for pipeline construction drawings, not aerial photo
      scale (matches the Exam4 Q26 pattern for this question type)
    - 3009 (`gis`→`trav`): traverse position misclosure, not GIS
    - 3017 (`theory`→`ang`): azimuth/bearing calculation between lines
    - 3032 (`level`→`constr`): offset-stake construction layout question,
      near-identical wording to Exam4's Q46 which is correctly `constr`
  - **Note on topic vocabulary per exam**: each exam's own tag usage was
    checked before "fixing" anything — e.g. Exam3 legitimately uses `ang`
    for vertical-angle-based elevation problems (see Q3035), so a couple
    of initially-suspicious `ang`-tagged questions (3039, 3042) were left
    alone once compared against that exam's own established convention,
    rather than forced to match Exam4's tagging habits. Don't assume
    cross-exam consistency is required — check the specific exam's own
    pattern first.
  - Not touched, and not expected to need touching per this audit: stem
    fidelity, solution line structure, KaTeX, `.qa-thread`/`.user-note`
    formatting for Exam1–3 — these all went through dedicated fixing
    sessions previously and this pass found no evidence of similar
    problems recurring (the topic-tag issue was the one specific gap
    flagged as outstanding).
- ✅ Exam4: **fully audited and merged** (55/55 questions). Full manual
  verbatim pass done against the original source scans (extracted from
  `Exam4_CBT_Simulator.html`'s embedded `EXAM_DATA`). Key findings from
  that pass, in case similar bugs are suspected elsewhere:
  - Several `.user-note` entries had been paraphrased instead of
    transcribed verbatim (including silently "corrected" source typos
    like "vegatation", "January, 1 1982", "layed flat" — these were
    restored to match source exactly, informal wording and all).
  - Multiple `qa-thread` discussions had comments dropped entirely (up to
    3 participants missing from a single thread in one case) when they
    were originally transcribed — restored from source.
  - `qa-meta` timestamps were very consistently missing the time-of-day
    portion (only date) even though the source always has full
    timestamps — this pattern recurred across nearly every thread that
    needed touching.
  - Two questions (Q44, Q50) had solution content not actually visible in
    the source scan (image cut off before it could be transcribed); added
    `Flagged item:` notes disclosing this rather than presenting the
    content as verified-verbatim.
  - Tag formatting bug: 35 of 55 questions had malformed `cat`/`topic`
    tags in the standalone review file (merged into one string, missing
    category entirely, or one outright wrong value) — cross-checked
    against the simulator's already-correct tags and fixed.
  - **Simulator-side data-merge gap**: found 20 questions where the
    original Exam4→simulator merge had dropped the question/solution
    diagram(s) even though the standalone review file had them. Re-parsed
    all 55 questions from the corrected review file and did a full
    wholesale replacement of the simulator's Exam4 entries (ids
    4001–4055) rather than a field-by-field patch, which fixed this
    alongside all the verbatim-fidelity fixes.
- ✅ Data-integrity bugs fixed and verified zero remaining:
  - 25 empty question stems (all in Exam3)
  - 7 missing question tables (1 Exam1, 6 Exam4)
  - `vc` (Vertical Curve) topic tag audited across all 23 tagged questions;
    13 reassigned to their correct topic (`level`, `constr`, or `hc`), 10
    confirmed genuine and left as `vc`
- ✅ CBT choice-list layout fixed: single-column (was cramped 4-column
  grid), padding and line-height increased for readability
- ✅ Duplicate detection: 4 known duplicate pairs now tagged
  (`duplicate_of`) — 1 pre-existing (2039→1012) plus 3 found during the
  Exam5 session (see above) — excluded from sessions by default with an
  "include duplicates" toggle. The two previously-known
  correctly-unflagged near-matches (84/148, 127/1046 — shared data
  table, different question) remain correctly untagged.
- ✅ Nav grid: compact progress view for sessions over 100 questions;
  nudge modal when starting with zero filters selected
- ✅ Mandatory splash screen + Bismillah header graphic + credit line, per
  owner's request

- 🟡 Exam6: **transcription started** (6/55 questions done: Q1-Q6), not yet
  merged into the simulator. Source for this exam is a set of 100 owner-
  provided screenshots (`CSPER-_Exam6_Screenshots_2026-08-17_233146.zip`) of
  the live CivilPESurveyingReview.com review site, one (occasionally two,
  for longer solutions) screenshot per question, in strict chronological/
  question-number order — confirmed by OCR spot-check across the full set.
  This is a cleaner source than prior exams: stem, choices, correct-answer
  marking, and a typed answer explanation (with inline equations) are all
  directly legible, so less reconstruction-from-scan-images work is needed
  than Exam4/5. The underlying `Exam6_CBT_Simulator.html` also has the
  usual embedded `EXAM_DATA` (`<script id="exam-data">`) with 55 question/
  solution JPEGs, available as a fallback/cross-check source.
  - Diagrams embedded so far: Q1 (lot area sector diagram), Q4 (profile
    leveling field-note table, both blank-stem and answer-filled versions).
  - Topic tags applied are a first-pass best guess (`hc`, `gis`, `level`,
    `meas`, `theory`) — not yet cross-checked against the established
    taxonomy the way Exam1-4's tags were audited; treat as unverified until
    a dedicated tag-audit pass, same caveat as new exams historically.
  - Q7 (mass-diagram balance-point problem) has a long multi-step solution
    with two diagrams (profile + mass diagram) and was deferred rather than
    rushed — pick that up next.
  - KaTeX (17 expressions), div-balance, and dfrac-blind-spot checks all
    passed clean for the Q1-Q6 batch. Checkpointed to
    `Exam6_Compiled_Review.html` in outputs; **not yet in the repo** — needs
    the owner to pull this file down and place/merge it, or a future session
    with push access.

**Not yet started:**
- Exams 6–9: raw source files already exist in the repo
  (`Exam6_CBT_Simulator.html` through `Exam9_CBT_Simulator.html`),
  transcription/formatting/verification work has not begun. Follow the
  same process used for Exam5 this session: extract source images from
  `EXAM_DATA`, transcribe with composite-grid batches, flag (don't
  silently fill) any missing/cut-off solutions, ask the owner for source
  images to verify independently-derived answers where possible, run the
  full validation suite (KaTeX incl. the `\'` apostrophe trap below, div
  balance, duplicate scan — including a manual check for diagram-only
  duplicates the fingerprint scan can't see), then merge as new ids
  (6001–6055 etc.) via wholesale append. Treat each exam as its own
  session for context-window reasons.
- **Watch for the `\'` KaTeX trap** in future transcription: always use a
  plain apostrophe `'` for minute-marks in formulas, never `\'` — the
  latter is a LaTeX accent command that mostly renders "successfully"
  with the wrong visual output rather than throwing an error, so it
  won't get caught by a simple try/render validation pass alone. Also
  watch for accidental double-brace escaping (`{{x}}`) when writing
  KaTeX via Python string formatting — harmless to rendering but untidy.
- `Exam4_Compiled_Review.html`'s "not yet audited" note in the formatting
  doc (§10) is stale and should be updated to reflect the completed audit
  — same for any similar stale notes about Exam1–3's topic-tag status,
  and now Exam5's transcription-complete status.

---

## Files in this repo relevant to the simulator

- `unified_simulator.html` — the live combined simulator (large; mostly
  base64 image data, don't put this in Project Knowledge — attach directly
  to a chat or have Claude pull it from GitHub instead)
- `Exam1_Compiled_Review.html` through `Exam5_Compiled_Review.html` —
  standalone formatted review docs per exam, source of truth for their
  respective exam's content in the simulator
- `Exam6_CBT_Simulator.html` through `Exam9_CBT_Simulator.html` — raw,
  unformatted source material for the exams not yet started

## Where the formatting rules live

See the separate formatting-standard doc (in Project Knowledge) for the
detailed rules: line-by-line solution structure, KaTeX/`\dfrac`
conventions, CSS sizing values, comment format (`.user-note` vs
`.qa-thread`), diagram-handling rules, and the checklist for adding new
questions. This file is status/history; that one is the rulebook.

