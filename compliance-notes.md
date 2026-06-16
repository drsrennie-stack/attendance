# Accessibility Compliance Notes

**Project:** Attendance Engine
**Files covered:** Attendance_Engine.html
**Date:** June 15, 2026
**WCAG version and target:** WCAG 2.2, Level AA floor, AAA targeted where achievable

## 1. Summary

The Attendance Engine is a single-file interactive roll sheet. All text pairs meet AA, and most meet AAA. Structure, keyboard operation, and ARIA were verified programmatically. One non-text contrast item (the focus ring on a white background) is just below the 3:1 target and is listed under known limitations with a remediation option. A live screen-reader pass by a human is still required before final sign-off.

## 2. Color contrast audit

Ratios computed with the WCAG relative-luminance formula. Normal text passes at 4.5:1 (AA) or 7:1 (AAA). Large or bold text passes at 3:1 (AA) or 4.5:1 (AAA).

| Foreground | Background | Ratio | Result |
|---|---|---|---|
| Navy #1E3D4C text | White #FFFFFF card | 11.49:1 | AAA |
| Navy #1E3D4C text | Off-white #FAFAF9 page | 11.01:1 | AAA |
| Navy #1E3D4C text | Navy-tint #EDF1F3 present cell | 10.11:1 | AAA |
| Terra-dark #A0522D eyebrow and h2 | White #FFFFFF | 5.62:1 | AA (AAA for large) |
| Terra-dark #A0522D | Off-white #FAFAF9 | 5.38:1 | AA |
| Gray #6b6b6b helper text | White #FFFFFF | 5.33:1 | AA |
| Gray #6b6b6b helper text | Off-white #FAFAF9 | 5.10:1 | AA |
| White #FFFFFF | Navy #1E3D4C header, selected tab | 11.49:1 | AAA |
| White #FFFFFF | Team 2 gold #8A6A2F | 5.02:1 | AA |
| White #FFFFFF | Team 3 terra #A0522D | 5.62:1 | AA |
| White #FFFFFF | Team 4 teal #2C6E6A | 5.92:1 | AA |
| White #FFFFFF | Team 5 plum #6E3A52 | 8.79:1 | AAA |
| White #FFFFFF | Team 6 blue #3E6B8C | 5.70:1 | AA |
| Terra-dark #A0522D absent mark | Absent cell #f6e9e2 | 4.73:1 | AA |

All foreground text and the six team-chip pairs pass AA. Team colors are fixed in the code so a professor cannot accidentally choose a low-contrast pairing.

## 3. Keyboard navigation

Verified the full operating path is reachable and operable by keyboard:

- Skip link to the roll sheet is the first focusable element.
- Tabs use the ARIA tabs pattern: arrow keys move between Enrolled, Wait List, and Dropped, Home and End jump to first and last, and the selected tab is the only one in the tab order (roving tabindex).
- Course menu, setup, new course, export, and delete buttons are standard focusable controls.
- Each attendance cell is a real button, reachable by Tab and activated by Enter or Space, cycling blank to present to absent.
- Team dropdowns, team-name inputs, the TBL toggle, and all row action buttons are native form controls.
- The setup wizard is a dialog: it traps nothing destructively, Escape closes it, clicking the backdrop closes it, and focus moves to the first field on open and returns to the trigger on close.
- Visible focus indicators use a 3px gold outline with offset on every interactive element.

## 4. Screen reader testing

Programmatically verified semantics and ARIA:

- Semantic landmarks: `header`, `main`, and section tabpanels.
- Heading hierarchy: one h1 for the course title, h2 for the dialog.
- Tabs and tabpanels wired with `role`, `aria-selected`, `aria-controls`, and `aria-labelledby`.
- The dialog uses `role="dialog"` and `aria-modal="true"` with `aria-labelledby`.
- Every attendance button has an `aria-label` naming the student, the date, and the current state (present, absent, unmarked), and the label updates on each click.
- Team dropdowns and team-name inputs have accessible names.
- The tally region is `aria-live="polite"` so present, absent, and unmarked counts are announced.
- The icon-only roster logo has `role="img"` and an accessible label.

**Not yet done:** a human pass with VoiceOver and NVDA to confirm announced order and wording in practice. This is required before final sign-off.

## 5. Known limitations and remediation plan

1. **Focus ring on white is 2.90:1**, just below the 3:1 WCAG 2.2 non-text minimum (1.4.11). The same gold ring is high-contrast against navy buttons. Remediation if needed: darken the focus outline color, or add a second contrasting outline so it meets 3:1 on both light and dark backgrounds. Low risk, since the ring is thick (3px) with an offset and is paired with a state change.
2. **Live screen-reader verification pending** (see section 4).
3. **Schedule changes after attendance is recorded** keep marks by column position, not by date, so editing the meeting days later can shift which date a mark belongs to. The setup screen warns about this. No accessibility impact; noted for data accuracy.
4. **Browser-only storage** means records live in one browser. Not an accessibility issue, but export regularly so nothing is lost.

## 6. Reviewer

Dr. Sharilyn Rennie
