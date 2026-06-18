# Accessibility Compliance Notes — TBL Grade Engine

**Files covered:** `Grade_Engine.html`
**Date:** June 18, 2026
**Standard:** WCAG 2.2. Target level AA (floor), AAA where achievable.
**Reviewer:** Dr. Sharilyn Rennie

## 1. Summary

The TBL Grade Engine is a single-file, keyboard-operable gradebook. It uses the primary palette (navy, terra cotta, brushed gold on white and off-white). Sage and cream are not used. All interactive controls are native HTML form elements with accessible names, the gradebook is a real `<table>` with header associations, and dynamic regions announce changes. Automated color-contrast math and a scripted DOM pass (course creation, scoring, weighting, drop and restore, roster link, CSV export) were run; a live screen-reader pass by a human is still recommended before each term.

## 2. WCAG criteria addressed

| Criterion | Level | How it is met |
|-----------|-------|---------------|
| 1.1.1 Non-text content | A | Logo SVG has `role="img"` and an `aria-label`; it is `focusable="false"`. Icon meaning is never the only cue. |
| 1.3.1 Info and relationships | A | Semantic `header`, `main`, `table`/`thead`/`tbody`/`tfoot`. Category header cells use `scope="colgroup"`, column headers `scope="col"`, row labels are `<th>`. Form fields use `label`+`for`/`id`. |
| 1.3.2 Meaningful sequence | A | DOM order follows reading order; sticky columns are visual only. |
| 1.4.1 Use of color | A | Status is conveyed by text (Active/Dropped tabs, letter grade text, `[C]` flag), not color alone. |
| 1.4.3 Contrast (minimum) | AA | All text pairs meet or exceed 4.5:1. See section 3. |
| 1.4.6 Contrast (enhanced) | AAA | Primary text pairs (navy on white/off-white, white on navy) exceed 7:1. |
| 1.4.10 Reflow | AA | Layout is responsive; the wide table scrolls within a bordered region rather than forcing page-level horizontal scroll. |
| 1.4.11 Non-text contrast | AA | Control borders and the 3px gold focus ring meet 3:1 against adjacent colors. |
| 1.4.12 Text spacing | AA | No fixed line-height traps; content reflows with user text-spacing overrides. |
| 2.1.1 Keyboard | A | Every control (tabs, selects, score inputs, mini buttons, wizard fields, modals) is reachable and operable by keyboard. No custom widgets that trap focus. |
| 2.1.2 No keyboard trap | A | Modals close on Escape and on backdrop click; focus returns to the page. |
| 2.4.1 Bypass blocks | A | A visible-on-focus skip link jumps to the gradebook. |
| 2.4.3 Focus order | A | Focus order follows visual order through the toolbar, table, and dialogs. |
| 2.4.7 Focus visible | AA | All focusable elements show a 3px brushed-gold outline with offset. |
| 2.5.3 Label in name | A | Visible labels match accessible names on inputs and buttons. |
| 2.5.8 Target size (minimum) | AA | Score cells are 34px tall full-width; mini buttons and chips meet the 24px minimum with spacing. |
| 3.2.2 On input | A | Changing a select or score updates the sheet but never moves focus or navigates unexpectedly. |
| 3.3.1 Error identification | A | The wizard and add-column dialogs show inline `role="alert"` errors (missing title, bad max points). |
| 3.3.2 Labels or instructions | A | Every field has a label; hints explain CSV format, weighting, and roster linking. |
| 4.1.2 Name, role, value | A | Native controls expose role and value. Tabs use `role="tab"`/`aria-selected`; the panel uses `role="tabpanel"`. Dialogs use `role="dialog"`/`aria-modal`/`aria-labelledby`. |
| 4.1.3 Status messages | AA | The tally and parse-preview regions use `aria-live="polite"`; errors use `role="alert"`. |

## 3. Color contrast audit

Background tokens: White `#FFFFFF`, Off-white `#FAFAF9`, Navy `#1E3D4C`, Navy-deep `#142a36`, Navy-tint `#EDF1F3`.

| Foreground | Background | Ratio | Result |
|------------|-----------|-------|--------|
| Navy `#1E3D4C` text | White `#FFFFFF` | 11.5:1 | AAA |
| Navy `#1E3D4C` text | Off-white `#FAFAF9` | 11.2:1 | AAA |
| White `#FFFFFF` text | Navy `#1E3D4C` (headers, selected tab) | 11.5:1 | AAA |
| White `#FFFFFF` text | Navy-deep `#142a36` (category header row) | 13.6:1 | AAA |
| Navy `#1E3D4C` text | Navy-tint `#EDF1F3` (footer, team-scored cells) | 10.1:1 | AAA |
| Terra-dark `#A0522D` (eyebrow, labels, C/D letters) | Off-white `#FAFAF9` | 5.5:1 | AA |
| Gray `#6b6b6b` (hints) | Off-white `#FAFAF9` | 5.2:1 | AA |
| F-grade `#8a2b1a` | White `#FFFFFF` | 8.4:1 | AAA |
| Brushed gold `#B8924A` focus ring | White / Off-white (non-text) | 3:1+ | AA (non-text) |

No text pair falls below 4.5:1. Brushed gold is used only for focus rings and borders, never as text on a light background.

## 4. Keyboard navigation flow verified

Tab order: skip link, Course select, Course setup, + New course, Active tab, Dropped tab, Categories & weights, + Add column, + Add student, Compute weighted grade toggle, Export CSV, Print, then into the table (team selects, score inputs, Drop/Restore buttons in row order). Score inputs accept numeric entry and clamp to the column max. Enter submits dialogs; Escape closes any open dialog. No element is reachable by mouse only.

## 5. Screen reader testing

Scripted DOM verification passed for structure and announcements (table header associations, live regions, dialog roles). Pending: a manual pass with VoiceOver (macOS Safari) and NVDA (Windows Firefox) to confirm category-to-column grouping is announced as intended and that the weighted-grade toggle state is read clearly. Assign before first production use each term.

## 6. Known limitations and remediation plan

1. **Manual screen-reader pass outstanding.** Automated checks cover roles and names, not the lived reading experience. Remediation: schedule a VoiceOver and NVDA pass before term start.
2. **Wide table on small screens.** The gradebook scrolls horizontally inside its region on narrow viewports. This preserves header relationships and meets reflow, but a stacked card view could be added later for phone use.
3. **Roster linking depends on same-origin storage.** The Attendance Engine link only appears when both tools share the web address; this is a storage boundary, not an accessibility issue, and is explained in the wizard hint.

## 7. Reviewer

Dr. Sharilyn Rennie
