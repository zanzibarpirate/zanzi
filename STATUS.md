# CA PE Civil Surveying CBT — Project Status

Last updated: August 19, 2026 (Exam7 transcription session, complete)

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

**`unified_simulator.html`** — 555 questions total (FS-AM 85, FS-PM 85,
CPESR-Exam1 55, CPESR-Exam2 55, CPESR-Exam3 55, CPESR-Exam4 55,
CPESR-Exam5 55, CPESR-Exam6 55, CPESR-Exam7 55).

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
- ✅ Data-integrity: 500-question baseline (pre-Exam7) previously verified
  duplicate-free and gap-free; Exam7's merge preserved that (555 total,
  zero duplicate ids, all div-balanced, all KaTeX clean).

**Not yet started:**
- Exams 8–9: raw source files should exist in the repo following the same
  pattern as Exam5–7 (`ExamN_CBT_Simulator.html` with embedded
  `EXAM_DATA`, or owner-provided screenshots) — not yet confirmed present,
  check before starting. Follow the same process used for Exam5–7: OCR/
  spot-check chronological order if screenshots, transcribe verbatim with
  batch checkpointing, flag (don't silently fill) any missing/cut-off
  content, run the full validation suite (KaTeX incl. the `\'` apostrophe
  trap, div balance, duplicate-fingerprint scan against all 555 existing
  questions — including a manual check for diagram-only duplicates the
  fingerprint scan can't see), then merge as new ids (8001–8055 etc.).
  Treat each exam as its own session for context-window reasons.
- **Watch for the `\'` KaTeX trap**: always use a plain apostrophe `'` for
  minute-marks in formulas, never `\'` (a LaTeX accent command that mostly
  "succeeds" with wrong visual output rather than throwing an error).
- Two open owner-facing items from this session, not yet resolved:
  1. No real source for Exam7 Q43 was ever located — the Exam1 substitute
     is a placeholder, not a fix. Revisit if the owner finds the missing
     screenshot.
  2. `CBT_Formatting_Standard.md` §10's file list and status notes are
     stale (references Exam1–4 only, doesn't mention Exam5–7's completion
     or this session's Exam4 Q11/Q23 fix) — worth a cleanup pass.

---

## Files in this repo relevant to the simulator

- `unified_simulator.html` — the live combined simulator (large; mostly
  base64 image data, don't put this in Project Knowledge — attach directly
  to a chat or have Claude pull it from GitHub instead)
- `Exam1_Compiled_Review.html` through `Exam7_Compiled_Review.html` —
  standalone formatted review docs per exam, source of truth for their
  respective exam's content in the simulator
- `Exam5_CBT_Simulator.html` through `Exam9_CBT_Simulator.html` — raw,
  unformatted source material for exams not yet started (confirm which of
  8/9 actually exist in-repo before assuming)

## Where the formatting rules live

See the separate formatting-standard doc (in Project Knowledge) for the
detailed rules: line-by-line solution structure, KaTeX/`\dfrac`
conventions, CSS sizing values, comment format (`.user-note` vs
`.qa-thread`), diagram-handling rules, and the checklist for adding new
questions. This file is status/history; that one is the rulebook.
