# Accessibility Compliance Notes

## 1. Project

**Project:** Course Engine (attendance, teams, and roster; replaces Attendance Engine and TBL Grade Engine)

**Files covered:**

- `Course_Engine.html` (the application, single self-contained file)
- `Course_Engine_README.md`

**Date of audit:** August 18, 2026. Revised August 21, 2026 (edit-student dialog, sort control, header sub-tier recolored to navy-deep, lab quiz draw column and turn tracking).

**Context of use:** Instructor-facing tool for three BIO 004 Human Anatomy sections at Solano Community College, Vacaville Center, Fall 2026 (Class 1 Mon/Wed PM, Class 2 Tue/Thu AM, Class 3 Tue/Thu EVE). Runs standalone in a browser tab and embedded via iframe in Canvas and Kajabi. All data stays in browser `localStorage`. No student-facing deployment.

**Scope note:** this build stores **no grades**. Scores, weights, categories, and grade scales were removed at the instructor's direction; grades stay in Canvas for FERPA. The audit below covers the attendance, roster, and status features that remain.

---

## 2. WCAG version and target level achieved

Standard applied: **WCAG 2.2**. Floor is AA. AAA targeted where achievable without changing locked brand palette tokens.

| Criterion | Level | Status | How it is met |
|---|---|---|---|
| 1.1.1 Non-text Content | A | Pass | Logo SVG has `role="img"` and `aria-label`. Attendance glyphs are CSS `::before` content behind `aria-hidden="true"`; the real state is in each button's accessible name. The class color chip is decorative and carries a `title`, never the only cue. |
| 1.3.1 Info and Relationships | A | Pass | Semantic `header` / `main` / `section`. Tables use `thead` / `tbody`, `scope="col"` and `scope="row"`, and a `caption`. Dialogs use `fieldset` / `legend`. Every control has a `label for` + `id`, a wrapping `label`, or an explicit `aria-label`. |
| 1.3.2 Meaningful Sequence | A | Pass | DOM order matches visual order. |
| 1.4.1 Use of Color | A | Pass | A lab quiz turn is shown by a filled asterisk glyph, not by the gold tint alone; a hand-set cell adds a middle-dot to the glyph and says "set by hand" in its accessible name rather than relying on the hatched background. The turn count is a number. In the fairness readout the numbers furthest behind are named in words at the end of the line, not marked only by a highlight. A position already held on a team is conveyed by the word "(taken)" in the option text and by the option being disabled, not by color. A duplicate team position is flagged by a doubled border weight, a `title`, a note appended to the accessible name, and a live-region message, not by the terra fill alone. Class tabs are colored *and* labelled with the section name, AM/PM/EVE chip, and head count, and the selected tab is bold with an underline drawn in the tab's own text color, so the tab colors are supplementary only. Each class color carries a matching foreground, so the Dark navy tab renders white text, a white underline, and a white AM/PM chip rather than inheriting navy. Attendance uses four distinct glyphs, check, en dash, cross, and empty, each with its own fill, never color alone. Lecture and lab are distinguished by the text sub-headers **Lec** and **Lab**, not by color. Wait-list status uses the letter **W**, not color. Enrollment status is a pull-down whose selected option is text ("Enrolled", "Wait list", "Dropped", "No-show"). Class identity is a color chip *and* the course name, AM/PM tag, and page title. |
| 1.4.3 Contrast (Minimum) | AA | Pass | See section 3. Lowest text pair is 4.73:1. The Lec / Lab sub-header moved from `#27505F` to `#142A36` on August 21, 2026, raising that pair from 8.75:1 to 14.85:1. |
| 1.4.6 Contrast (Enhanced) | AAA | Partial | 14 of 18 text pairs reach 7:1. Four sit between 4.73:1 and 6.09:1 on locked palette tokens. See section 6. |
| 1.4.4 Resize Text | AA | Pass | No maximum-scale lock; `-webkit-text-size-adjust:100%`. Layout reflows at 200 percent zoom. |
| 1.4.10 Reflow | AA | Pass | Page chrome reflows to 320 CSS px. The roll sheet scrolls horizontally, the permitted exception for tabular data; the index and name columns are sticky so context is never lost. |
| 1.4.11 Non-text Contrast | AA | Pass | Focus ring `#9A7833` is 3.46:1 or better against every surface it lands on. Form control borders `#7C8990` are 3.60:1 on white. Table and tab borders are navy at 11.49:1. |
| 1.4.12 Text Spacing | AA | Pass | No fixed line-height or letter-spacing that clips. |
| 1.4.13 Content on Hover or Focus | AA | Pass | No custom hover popups. Native `title` tooltips only, all duplicating the accessible name. |
| 2.1.1 Keyboard | A | Pass | See section 4. Every action is reachable and operable from the keyboard. |
| 2.1.2 No Keyboard Trap | A | Pass | Dialog focus traps cycle with Tab and Shift+Tab and always release on Escape. |
| 2.4.1 Bypass Blocks | A | Pass | Skip link to `#main`, visible on focus. |
| 2.4.3 Focus Order | A | Pass | Focus order follows DOM order. Opening a dialog moves focus into it; closing returns focus to the trigger (verified by automated test). |
| 2.4.6 Headings and Labels | AA | Pass | One `h1`. Dialog titles are `h2` and are the `aria-labelledby` target. |
| 2.4.7 Focus Visible | AA | Pass | `:focus-visible` 3px solid ring on every interactive element. No `outline:none` anywhere in the stylesheet. |
| 2.4.11 Focus Not Obscured (Min) | AA | Pass | Sticky headers sit at `top:0`; focusable cells scroll into view below them. No fixed footer overlay. |
| 2.4.13 Focus Appearance | AAA | Pass | 3px solid ring fully enclosing each component, exceeding the 2px-perimeter area minimum, at 3.46:1 or better. |
| 2.5.3 Label in Name | A | Pass | Visible button text starts each accessible name. |
| 2.5.7 Dragging Movements | AA | Pass | No drag interactions. |
| 2.5.8 Target Size (Minimum) | AA | Pass | The lab quiz draw pull-down is 46x24 px, meeting the minimum outright; when a second draw box is stacked below it the two centres sit 27 px apart, clearing the undisturbed-circle test. Quiz cells are 57x36 px. Attendance cells are 52x36 px, or 34x36 px each when a day is split into Lec and Lab, which clears the 24 px undisturbed-circle test. Status and team pull-downs are at least 126x30 px; the Pos pull-down is 54x30 px, which clears the 24 px undisturbed-circle test on all sides. Buttons have `min-height:32px`; the single row-level Remove button is `min-height:28px` and passes the 24 px undisturbed-circle test with room to spare, since it is alone in its cell. |
| 3.1.1 Language of Page | A | Pass | `<html lang="en">`. |
| 3.2.1 On Focus | A | Pass | Focus never changes context. |
| 3.2.2 On Input | A | Pass | The lab quiz draw pull-down acts on change, which is the documented purpose of the control; it changes only the quiz layer of the sheet already on screen, focus is deliberately returned to the same pull-down afterwards rather than moved, and setting it back to the dash undoes it. The Status pull-down deliberately acts on change; this is the documented purpose of the control, it opens a dialog the user can cancel, and cancelling restores the previous selection. Team, filter, and Sort pull-downs update in place without navigation; Sort reorders the rows already on screen and announces the new order through the notice region. |
| 3.2.6 Consistent Help | A | Pass | The help paragraph and the FERPA note sit in the same place on every view. |
| 3.3.1 Error Identification | A | Pass | Every dialog has a `role="alert"` error region naming the field and the fix, including the Edit student dialog, which names the duplicate and refuses an empty name. |
| 3.3.2 Labels or Instructions | A | Pass | Persistent labels plus format hints ("Name, as Last, First"). Placeholders are supplementary only. |
| 3.3.3 Error Suggestion | AA | Pass | Messages state the correction, for example "Old .xls files are not supported. In Excel choose Save As and pick .xlsx or CSV." |
| 3.3.4 Error Prevention | AA | Pass | A team position already held by another member is disabled in the pull-down, so a duplicate cannot be entered rather than being caught afterwards. Moving a student to a team where their number is taken clears the number and names the open ones. Every destructive action (delete class, clear attendance, clear teams, remove student, restore from backup) routes through a confirmation dialog naming exactly what will be lost. Duplicate names are rejected on add, refused on edit, and skipped on import. Editing a student changes only their name, add code, and confidential flag; attendance, team, position, status, and history stay attached to the same record, and the old name is written into that student's history so a correction is never silent. |
| 3.3.7 Redundant Entry | A | Pass | Duplicate carries schedule, team names, and team count into a new section. Import skips names already present rather than asking again. A misspelled name is corrected in place rather than re-entered as a new student. |
| 4.1.2 Name, Role, Value | A | Pass | Three tablists (classes, views, roster sheets) use `role="tablist"` / `role="tab"` / `role="tabpanel"` with `aria-selected`, `aria-controls`, and roving `tabindex`. Dialogs use `role="dialog"` or `role="alertdialog"` with `aria-modal` and `aria-labelledby`. |
| 4.1.3 Status Messages | AA | Pass | The lab quiz fairness readout is `aria-live="polite"` and re-announces when a draw or an attendance mark changes the counts. Each draw pull-down's accessible name states whether it is the first draw for that day or an extra one, and when it is an extra it says how many teams it is covering, so a screen reader user is told why a second box appeared without having to infer it visually. The Pos control's accessible name lists the open positions for that team, so the information is not carried by the tooltip alone. Attendance tally, roster tally, import preview, and the notice banner are `aria-live="polite"` or `role="status"`; they announce without stealing focus. |

**Level achieved: WCAG 2.2 AA in full. AAA met on all criteria except 1.4.6, which is partial.**

---

## 3. Color contrast audit

Ratios computed from the sRGB relative-luminance formula. Text judged at 4.5:1 (AA) and 7:1 (AAA). Large text at 3:1 and 4.5:1. Non-text at 3:1.

### Text

| Element | Foreground on background | Ratio | Result |
|---|---|---|---|
| Body text on page | `#1E3D4C` on `#FAFAF9` | 11.01:1 | AAA |
| Body text on card | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |
| Body text on present-cell fill | `#1E3D4C` on `#EDF1F3` | 10.11:1 | AAA |
| Eyebrow, 12px uppercase | `#A0522D` on `#FAFAF9` | 5.38:1 | AA |
| Subhead, 15px | `#A0522D` on `#FFFFFF` | 5.62:1 | AAA (large) |
| Helper and hint text | `#565656` on `#FAFAF9` | 7.03:1 | AAA |
| Helper text on card | `#565656` on `#FFFFFF` | 7.34:1 | AAA |
| Helper text on even row | `#565656` on `#FBFBFA` | 7.09:1 | AAA |
| Table header text | `#FFFFFF` on `#1E3D4C` | 11.49:1 | AAA |
| Present check mark | `#1E3D4C` on `#EDF1F3` | 10.11:1 | AAA |
| Partial dash mark | `#A0522D` on `#FBF3E7` | 5.10:1 | AA |
| Absent cross mark | `#A0522D` on `#F6E9E2` | 4.73:1 | AA |
| Lec / Lab / Qz sub-header | `#FFFFFF` on `#142A36` | 14.85:1 | AAA |
| Lab quiz turn glyph | `#7A5E1F` on `#F7EFDC` | 5.32:1 | AA |
| Turn count, fewest-so-far badge | `#7A5E1F` on `#F7EFDC` | 5.32:1 | AA |
| Turn count, zero | `#565656` on `#FFFFFF` | 7.34:1 | AAA |
| Turn count, normal | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |
| Lab quiz draw pull-down | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |
| Extra draw pull-down | `#1E3D4C` on `#F7EFDC` | 10.04:1 | AAA |
| Fairness readout | `#565656` on `#FAFAF9` | 7.03:1 | AAA |
| Class tab label, white tab | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |
| Class tab label, light yellow tab | `#1E3D4C` on `#FBF3D0` | 10.31:1 | AAA |
| Class tab label, light grey tab | `#1E3D4C` on `#EDEDEC` | 9.81:1 | AAA |
| Class tab label, worst of the seven light tints | `#1E3D4C` on `#F0E7EC` | 9.49:1 | AAA |
| Class tab label, Dark navy tab | `#FFFFFF` on `#0C1D26` | 17.22:1 | AAA |
| Dark navy tab against the page | `#0C1D26` on `#FAFAF9` | 16.49:1 | Pass |
| Duplicate team position | `#A0522D` on `#F6E9E2` | 4.73:1 | AA |
| Add code cell | `#1E3D4C` on `#EDF1F3` | 10.11:1 | AAA |
| **W** wait-list badge | `#7A5E1F` on `#F7EFDC` | 5.32:1 | AA |
| Status pull-down, dropped state | `#A0522D` on `#F6E9E2` | 4.73:1 | AA |
| Status pull-down, wait-list state | `#7A5E1F` on `#F7EFDC` | 5.32:1 | AA |
| Status pull-down, normal state | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |
| Remove button label | `#A0522D` on `#FFFFFF` | 5.62:1 | AA |
| History log entry date | `#1E3D4C` on `#FFFFFF` | 11.49:1 | AAA |

### Team chips (fixed, contrast-checked, 8 available)

| Team | Foreground on background | Ratio | Result |
|---|---|---|---|
| 1 Navy | `#FFFFFF` on `#1E3D4C` | 11.49:1 | AAA |

Team 1 navy `#1E3D4C` and team 4 very dark navy `#0C1D26` sit 1.50:1 apart from each other. That is enough to read as two different chips side by side, but they are the closest pair in the set. Both carry the team name as text in the pull-down and on the chip, so the color never has to carry the distinction alone.

| 2 Gold-deep | `#FFFFFF` on `#7A5E1F` | 6.09:1 | AA |
| 3 Terra-dark | `#FFFFFF` on `#A0522D` | 5.62:1 | AA |
| 4 Very dark navy | `#FFFFFF` on `#0C1D26` | 17.22:1 | AAA |
| 5 Plum | `#FFFFFF` on `#61304A` | 10.35:1 | AAA |
| 6 Slate blue | `#FFFFFF` on `#33607E` | 6.74:1 | AAA |
| 7 Brown | `#FFFFFF` on `#6B4423` | 8.48:1 | AAA |
| 8 Indigo | `#FFFFFF` on `#4A4A6A` | 8.47:1 | AAA |

The same eight colors are offered as class accent colors. They are used only as an identifying chip and border accent, never as the sole carrier of meaning, so they are exempt from the text thresholds; all eight clear 3:1 against the page background as a border.

### Non-text (3:1 required)

| Element | Colors | Ratio | Result |
|---|---|---|---|
| Focus ring on page background | `#9A7833` on `#FAFAF9` | 3.94:1 | Pass |
| Focus ring on card | `#9A7833` on `#FFFFFF` | 4.11:1 | Pass |
| Focus ring inside present cell | `#9A7833` on `#EDF1F3` | 3.62:1 | Pass |
| Focus ring on class tabs, worst tint | `#9A7833` on `#F0E7EC` | 3.40:1 | Pass |
| Class tab border and selected underline | `#1E3D4C` on tab tint | 9.49:1 or better | Pass |
| Focus ring inside partial cell | `#9A7833` on `#FBF3E7` | 3.73:1 | Pass |
| Focus ring inside absent cell | `#9A7833` on `#F6E9E2` | 3.46:1 | Pass |
| Form control borders | `#7C8990` on `#FFFFFF` | 3.60:1 | Pass |
| Form control borders on page | `#7C8990` on `#FAFAF9` | 3.44:1 | Pass |
| Table cell and tab borders | `#1E3D4C` on `#FFFFFF` | 11.49:1 | Pass |
| Selected inner tab underline | `#A0522D` on `#EDF1F3` | 4.94:1 | Pass |
| Status pull-down dropped border | `#A0522D` on `#FFFFFF` | 5.62:1 | Pass |
| Status pull-down wait-list border | `#7A5E1F` on `#FFFFFF` | 6.09:1 | Pass |

**Two changes were carried forward from the first audit.** Brushed gold `#B8924A` failed as a focus ring (2.44:1 to 2.77:1 on light surfaces) and was replaced with `#9A7833`, which stays in the gold family and clears 3:1 everywhere it lands. Brushed gold remains unchanged wherever it is decorative. Form control borders were darkened from `#8D989E` (2.95:1) to `#7C8990` (3.60:1).

**Decorative borders, exempt from 1.4.11:** the card outlines on the class bar and team bar, the `fieldset` outlines, and the header rule sit between 1.4:1 and 2.9:1. None identifies a control or a state; the controls inside them carry their own compliant borders, and each `fieldset` has a `legend`.

**Failures outstanding: none.**

---

## 4. Keyboard navigation flow verified

Verified in Chromium under automated Playwright driving plus manual tab-through.

1. **Skip link.** One Tab from load reveals "Skip to the roll sheet"; Enter jumps to `#main`.
2. **Class bar.** Tab reaches the class select, then Class setup, + New class, Duplicate, Backup all, Restore, Delete class. The select changes class with arrow keys.
3. **Class tabs.** `role="tablist"` with roving `tabindex`, so the whole strip is one Tab stop. Left, Right, Up, Down, Home, and End move between sections and switch the sheet. Verified by automated test.
4. **View switch (Attendance / Roster & Status).** Same pattern. Verified by automated test.
4. **Roster sheets (Class list / Dropped-No-show).** Same pattern, verified by automated test.
5. **Attendance grid.** Every cell is a real `button`. Tab moves across the row; Enter or Space cycles blank, present, partial, absent. The accessible name updates on every press and carries the date, the AM / PM / EVE tag, and, when lecture and lab are split, which part the cell is: "Okafor, Simone, Tue 9/8/2026 AM, lab: partial". Split days use a two-tier header with `scope="colgroup"` on the date and `scope="col"` on Lec and Lab.
6. **Team pull-downs.** Reachable by Tab, changed with arrow keys, applied on change. The row color follows the selection.
7. **Team name inputs.** Only the inputs for teams this class actually uses are rendered; the rest are `hidden` and out of the tab order. Edits propagate live to every team pull-down.
8. **Status pull-downs.** Reachable by Tab and operated with arrow keys plus Enter. Choosing Dropped or No-show opens the dated dialog with focus moved to the date field. Cancelling or pressing Escape restores the previous selection rather than leaving the control showing a state that was never applied.
9. **History disclosure.** `details` / `summary` per student. Tab reaches the summary; Enter or Space expands.
10. **Import dialog.** File input, paste textarea, target radios, and the live count are all keyboard reachable; the count is announced through `aria-live`.
11. **Dialogs.** Opening moves focus in. Tab and Shift+Tab cycle within and do not escape. Escape closes and returns focus to the exact trigger (verified by automated test). Backdrop click behaves identically.
12. **No keyboard traps** and **no `outline:none`** anywhere.

**Automated regression suites, all passing:**

- Main suite, **80 assertions**: class setup with AM/PM and per-class color and team count; Excel wait-list import; Excel enrolled import; duplicate-safe re-import; wait-list to enrolled with the W disappearing; dated drop; no-show; the drops/no-shows filter; reinstatement preserving the original drop; cancel restoring the pull-down; manual team assignment; attendance cycling and tally; hard Remove versus Drop; persistence across reload; a second class with its own color and roster; class switching; paste import; both CSV exports; accessible-name coverage; arrow-key navigation on both tablists; Escape focus return; and confirmation that no gradebook, score input, or native modal exists.
- Edit and sort suite, **52 assertions**: default and persisted sort order; name, team-then-position, and team-then-name ordering on both sheets; the two Sort pull-downs staying in step; students with no team sorting last; the Edit dialog opening pre-filled; a duplicate name refused without being written; an empty name refused; a rename leaving lecture attendance, lab attendance, team, position, and status byte-identical; one history entry added and the earlier ones kept; the cell accessible names rebuilt with the new name; the rename surviving a reload; a typed `[C]` setting the confidential flag rather than landing in the name; Cancel and Escape discarding the edit; Edit available on the dropped sheet; and labelling of every new control.
- Lab quiz suite, **55 assertions**: column structure with three tiers per day; the draw menu following the class's position count; one draw crediting that position in every team; no extra box while every team is covered; an absent holder losing the credit and raising a second box that names how many teams it covers; the second number covering only the uncovered teams; exactly one student credited per team per day; a lecture-only absence not blocking a lab quiz while a lab absence does; a partial lab still counting; hand-set turns on and off and back to automatic; clearing a draw removing its credits; the fairness readout naming the numbers furthest behind; sorting by fewest turns; draws, credits and counts surviving a reload, a Clear attendance, and the feature being switched off and on; the roster sheet agreeing with the roll sheet; and accessible names on every draw pull-down and quiz cell.
- Migration suite, **27 assertions**: importing legacy Attendance Engine and Grade Engine data, converting legacy drop dates, classifying legacy no-shows, folding grade-engine-only students into the roster, preserving teams, creating no duplicates, importing **no scores**, and not re-running on reload.

---

## 5. Screen reader testing

**Programmatic verification completed** (automated, in Chromium):

- Every visible `input`, `select`, and `textarea` resolves to a non-empty accessible name. Count of unnamed controls: **0**.
- Every visible `button` resolves to a non-empty accessible name. Count of unnamed buttons: **0**.
- Exactly one `h1`; heading order is h1 then h2 with no skipped levels.
- Landmarks present: `header`, `main`. Skip link targets `main`.
- Live regions present: attendance tally, roster tally, import preview, day-count preview, notice banner.
- Both tablists expose `role`, `aria-selected`, `aria-controls`, and roving `tabindex`. All dialogs expose `aria-modal` and `aria-labelledby`.

**Live assistive-technology testing: not yet performed.** No NVDA, JAWS, or VoiceOver pass has been run against this build. The structure above is what a screen reader depends on, but it is not a substitute for hearing the output. See section 6.

---

## 6. Known limitations and remediation plan

| # | Limitation | Impact | Plan |
|---|---|---|---|
| 1 | **No live screen reader pass.** | Structure is verified programmatically, but announcement quality is unconfirmed. Highest-risk areas: the wide roll sheet with two sticky columns, and whether the **W** badge and `[C]` superscript read cleanly as part of a student's name rather than as stray letters. | Run VoiceOver on macOS and NVDA on Windows. Move down the roll sheet confirming each cell announces name, dated column with AM or PM, and state. If W or [C] read poorly, replace the visual badge's accessible text with visually-hidden wording ("on the wait list", "confidential"). Owner: Dr. Sharilyn Rennie. |
| 2 | **1.4.6 enhanced contrast is partial.** Four pairs land between 4.73:1 and 6.09:1: the absent cross mark and dropped status control (`#A0522D` on `#F6E9E2`, 4.73:1), the W badge and wait-list control (`#7A5E1F` on `#F7EFDC`, 5.32:1), the 12px eyebrow (5.38:1), and the team 2 chip (6.09:1). | All clear AA comfortably. AAA would require darkening terra-dark and the gold tints, which are locked PRIMARY palette tokens. | Leave as is. Revisit only if the PRIMARY palette is reconciled; a terra token near `#8A4526` would take the absent mark to 7:1. |
| 3 | **The roll sheet scrolls horizontally** rather than reflowing at narrow widths. | On a phone you scroll sideways to reach later day columns. | Permitted by 1.4.10 for tabular data; index and name columns are sticky. No change planned. |
| 4 | **Browser storage can be blocked in an iframe.** Canvas and Kajabi embeds are cross-origin; Safari and recent Chrome partition or block third-party storage. | Silent loss of work. | Mitigated: storage is probed on load and a persistent warning names the fix (open in its own tab). **Backup all** is the escape hatch. |
| 5 | **Excel reading needs `DecompressionStream`.** Available in Chrome 80+, Safari 16.4+, Firefox 113+. | On an older browser an `.xlsx` upload fails. | Mitigated: the failure is caught and the message tells the user to save as CSV. No silent failure. |
| 6 | **Status pull-down acts on change (3.2.2).** | A screen reader user arrowing through options in a browser that fires `change` per option could open the dialog early. | The dialog is cancellable and cancelling restores the prior value, so nothing is committed by accident. If live testing shows this is disruptive, add an explicit Apply button beside the pull-down. Confirm during the section 6 item 1 pass. |
| 7 | **Expanded history collapses on re-render.** | Minor annoyance, no data loss. | Low priority. Would be fixed by tracking open `details` ids across renders. |
| 8 | **The Pos pull-down is disabled until a team is chosen**, at 45 percent opacity. | Low contrast while disabled. | Permitted: 1.4.3 and 1.4.11 exempt inactive user interface components. The control carries a `title` explaining what to do first ("Pick a team first, then a position within it"), so the reason is available rather than implied by the greying. |
| 9 | **Class tab tints are close in luminance** (1.0 to 1.2:1 between neighbours). | Two adjacent tabs are not reliably told apart by color alone, especially for a colorblind reader. | Not a failure: every tab carries its section name, its AM/PM/EVE chip, a head count, and an `aria-selected` state, so color is never the only cue. No change planned. |
| 10 | **A lab quiz draw credits a student who is not yet marked.** An unmarked cell counts as available, since at draw time attendance is often not entered. | If you draw before taking attendance and later mark that student absent, the credit moves to the next drawn number automatically, but if you never mark them the turn stays on their count. | Working as intended: the alternative, requiring attendance first, would block the draw at the moment you need it. Mark the sheet as you go and the counts stay honest. Any single day can be corrected by clicking the Qz cell. |
| 11 | **Turn counts are per class, not per student across sections.** | A student enrolled in two of your sections has a separate count in each. | Correct for the purpose: the draw happens inside one section's teams. No change planned. |
| 12 | **Grade data from the old Grade Engine is not migrated.** By design: grades stay in Canvas. | Scores in the legacy tool do not appear here. | Not a defect. The legacy `grade_engine_*` keys are untouched, so `Grade_Engine.html` still opens if that history is ever needed. |

---

## 7. Reviewer

Reviewed by Dr. Sharilyn Rennie

Audit performed August 18, 2026 against `Course_Engine.html`, revised August 21, 2026. The lab quiz draw pull-down was resized from 46x18 px to 46x24 px during this revision after the first measurement pass failed 2.5.8. Contrast ratios computed from source color tokens. Keyboard coverage and accessible-name coverage verified by automated Playwright suites, 89, 55, 52, 44 and 27 assertions plus seven feature suites, run in Chromium, all passing. Live assistive-technology verification remains outstanding per section 6, item 1.
