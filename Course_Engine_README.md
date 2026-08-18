# Course Engine

An attendance sheet. One file, every section.

**This is not a gradebook.** No scores, points, percentages, or letter grades are stored anywhere in this file. Grades stay in Canvas. What lives here is a roster, attendance marks, team assignments, and a dated record of who joined, who was waitlisted, and who left.

It replaces `Attendance_Engine.html` and `Grade_Engine.html`. Both are now legacy.

## What changed

| Then | Now |
|---|---|
| Two files, two browser stores, two rosters to keep in sync | One file, one store, one roster per class |
| A separate gradebook holding scores and weights | Removed. Grades stay in Canvas, per FERPA |
| A separate Wait List tab | Waitlisted students sit on the class list marked **W** |
| Drop and No-show buttons in two places | One Status pull-down per student, in one place |
| **Restore** erased the drop date and reason | Restore keeps the original drop and adds a dated reinstatement |
| Drop date was always today | Every change takes an effective date you can back-date |
| Drops and no-shows mixed together | One exit sheet, filterable to drops only or no-shows only |
| Roster only importable when creating a class | **Import roster** on both toolbars, any time |
| CSV only | Excel `.xlsx` and CSV, plus paste |
| Auto-assign teams | Removed. Teams are assigned by hand from each student's pull-down |
| Present or absent only | Four states: present, **partial**, absent, blank |
| One mark per class day | Optional separate **Lec** and **Lab** marks per day |
| Holidays generated attendance columns | **No-class dates** are skipped, so closures never get a column |
| Six teams, same everywhere | 2 to 8 teams, set per class, named per class |
| Team only | Team **plus a position within the team**, 1 to N, with duplicate detection |
| No way to tell two sections apart at a glance | Each class is a **colored tab** across the top with its own **AM / PM / EVE** chip |
| Classes chosen from a drop-down | Class tabs, one click to switch, each showing a live head count |
| Wait list always on the roll sheet | **Show wait list** toggle, so you can hide it once the class is full |
| `alert` / `confirm` / `prompt` | In-page dialogs, because sandboxed Canvas iframes swallow the native ones |
| Silent failure if browser storage was blocked | Storage is probed on load and a warning names the fix |
| No way to move classes off one machine | **Backup all** and **Restore** as one JSON file |

Your existing data is not lost. On first load the page imports every Attendance Engine class (roster, teams, attendance, drops) and every Grade Engine class. From the Grade Engine it takes **the roster only**: names, teams, and drop records. No scores are imported. The old storage keys are left untouched, so the old pages still open if you need them.

## Switching classes

Your sections are **tabs across the top**, in your colors: Class 1 white, Class 2 light yellow, Class 3 light grey. Each tab shows the section name, its AM / PM / EVE chip, and a live head count. One click switches everything under it, the roll sheet, the teams, the roster. The selected tab is bold with a navy underline, so the current section is never in doubt.

Each tab is a complete roll sheet in its own right. Set up teams per class and assign students to them independently; nothing is shared between sections except the file they live in.

Colors are chosen per class in Class setup, from eight light tints. They are a supplementary cue only: every tab is also labelled, so the sheet works fine in greyscale or for a colorblind reader.

## The two views

### Attendance

The roll sheet: everyone currently in the section, enrolled and waitlisted together, with a column per class meeting.

Click a cell to cycle through four states:

| Mark | Means |
|---|---|
| **✓** | Present |
| **–** | Partial. There for some of the session |
| **✕** | Absent |
| blank | Not yet marked |

The tally above the sheet counts Present, Partial, Absent, and Unmarked live.

**Separate lecture and lab.** When a class meets for both in one day and students can attend one without the other, turn on **Separate lecture and lab attendance** in Class setup. Each class day then splits into two marks, **Lec** and **Lab**, under a shared date header, so you can record that someone came to lecture and skipped lab. Use the dash instead when you just want "partial" without saying which part.

Waitlisted students are marked **W** so you can see who is provisional while still taking their attendance. Dropped and no-show students are not on this sheet.

**Hiding the wait list.** Once the semester has started and the class is filled, untick **Show wait list** in the toolbar. Waitlisted students drop off the roll sheet and the caption tells you how many are hidden. They stay on **Roster & Status**, so nothing is lost and you can still enroll or drop them. The setting is per class.

The team bar sits above the sheet: rename this class's teams, and see a live count per team.

**Team and position.** Each student row has two pull-downs side by side. **Team** picks the team; **Pos** picks that student's position within it, 1 to however many positions you set for the class. So if the team is Oak with six members, you choose Oak, then 1 through 6 in the next column.

Pos stays greyed out until a team is chosen, since a position without a team means nothing. If two students on the same team end up on the same position, both cells turn terra with a heavier border and a tooltip naming the clash, and a notice tells you which team and which number. The same position on a *different* team is fine and is not flagged. Clearing a student's team clears their position.

Both columns hide together when **Team-based (TBL)** is off.

### Roster & Status

Two sheets, and the only place enrollment status changes.

**Class list** holds everyone currently in the section. **Dropped / No-show** holds everyone who left, with a filter for drops only or no-shows only.

Each row has a **Status** pull-down with four choices: Enrolled, Wait list, Dropped, No-show.

- Wait list to Enrolled happens immediately. The W disappears and the promotion is dated in that student's history.
- Dropped and No-show open a short dialog: pick a reason, set the effective date, and it is recorded.
- Bringing someone back from the exit sheet opens the same dialog. The original drop stays in the history; the reinstatement is added on top with its own date and reason.

Every row carries a **History** disclosure listing every status change ever recorded for that student, oldest change kept forever.

**Remove** is different from Drop. Drop keeps a record. Remove erases the student and everything attached to them, for someone added by mistake. It asks first and says exactly what will be lost.

## Setting up your sections

1. Open the page. On first run the setup wizard opens by itself.
2. Fill in the class identity. **Course and section** is what shows in the Class menu.
3. Pick a **Class color**. Each section gets its own, shown as a chip beside the class name and as the accent on the sheet borders.
4. Set the first class date, number of weeks, and meeting days.
5. List **No-class dates**: holidays, campus closures, professional development days, separated by commas. No attendance column is generated for them, so your roll sheet has exactly the sessions you actually meet. The day preview tells you how many were skipped.
6. Set **AM**, **PM**, or **EVE**. Do this whenever you teach two sections on the same weekdays. It appears on every day column, in the Class menu, in the header, in the page title, and in your export filenames, so the two roll sheets cannot be confused. There is also an optional exact-time field.
7. Turn **Team-based (TBL)** on if the section uses teams, then set **how many teams** (2 to 8) and **positions per team** (2 to 12, usually the number of members). The two pull-downs on each student's row list only those.
8. Import a roster now, or skip it and import later.

For your second and third sections use **Duplicate** rather than + New class. It copies the schedule, team names, and team count, advances to the next class color, and flips AM to PM. The roster starts empty on purpose.

## Getting the roster in

**Import roster** is on both toolbars and works on a class that already exists, so your normal order works: import the wait list first, then import the enrolled list, then assign teams.

The dialog asks which list to add to (Wait list or Enrolled), then takes an upload or a paste. Before you commit it tells you how many names it read and how many are already on the roster and will be skipped. Re-importing an updated list is safe and never creates duplicates.

Accepted files:

- **Excel `.xlsx`.** The first worksheet is read. No add-ins, no conversion, no internet.
- **CSV.**
- **A saved attendance page** (File then Save Page As, "Webpage, HTML Only").

Headers are auto-detected: `Name`, or `Last Name` plus `First Name`, and optionally `Add Code`, `Position`, `Team`, `Confidential`, and `Status` or `Registration Status`.

**College exports work as-is.** A Banner **Summary Class List** puts a block of course information, CRN, term, and enrollment counts above the roster. The importer scans down for the real header row rather than assuming the first row, so you can upload the workbook straight from the portal with no cleanup. Student IDs, credit hours, registration status, level, and the grade columns are all ignored; only the name is taken. A name ending in `[CONFIDENTIAL]` is converted to the `[C]` directory-hold flag. Rows whose status reads dropped, withdrawn, deleted, cancelled, or no-show are skipped, and stray label rows like "Enrollment Counts" are never mistaken for students.

No headers? One name per line:

```
Addison, Tobias
Anderson, Sidney [C]
```

For wait-list rows put the add code as a third comma field:

```
Marin, Alexandra, 4MFFEV
Patindol, Bianca, 4TJRF6
```

`[C]` after a name flags FERPA confidential / directory hold and renders as a `[C]` superscript throughout.

Old `.xls` files are not supported; save as `.xlsx` or CSV first.

## Exports

- **Export attendance CSV.** Status, wait-list flag, wait-list position, name, confidential flag, team, team position, add code, then every class day marked Present, Partial, or Absent. Column names carry the date and the AM / PM / EVE tag, and split into `... Lecture` and `... Lab` when that option is on. Ends with Present, Partial, and Absent totals plus status date and reason.
- **Export roster and history CSV.** One row per status change, so the whole join, promote, drop, and reinstate trail is auditable outside the browser.
- **Backup all.** Every class in one JSON file, including full history. The only way to move classes between browsers or machines.
- **Print.** Landscape on both views. Controls are hidden and history prints expanded.

## How state is stored

Everything saves in the browser only, using `localStorage`. No server, no accounts, nothing leaves the machine.

- `course_engine_index_v1` lists the classes.
- `course_engine_current_v1` is the id of the active class.
- `course_engine_course_<id>` holds one class: identity, schedule, generated days, team names and count, color, and the student array with attendance, status, and history.

**Storage is scoped to the exact web address the page loads from.** A copy on your Desktop, a copy on GitHub Pages, and a copy in Canvas each get their own separate box even though the file is identical. That is what caused the original several-stores problem. Pick one address, use only that one, and back up regularly.

**Embedded in Canvas or Kajabi, storage may be blocked entirely.** Those embeds are cross-origin, and Safari and recent Chrome partition or block third-party storage. The page probes storage on load and shows a warning if it cannot save. If you see it, open the page in its own browser tab and work there.

## Embedding

The iframe height-sender is baked in before the closing body tag: `postMessage` carrying `frameId`, `id`, `type`, and `height`, with `load` and `resize` listeners plus a `ResizeObserver`. There are no internal or same-domain links in the page, so no `target="_top"` is needed.

## Privacy

Attendance is an education record under FERPA even though no grades are here. The file keeps student names, attendance, team assignments, and enrollment status, all in your browser only. Treat exported CSV files as student records: college-managed storage, not personal cloud folders or email. Students marked `[C]` carry a directory hold and their names should not appear in anything shared beyond the roster.

## Your three Fall 2026 sections

`BIO004_Fall2026_three_sections.json` is a ready-made **Restore** file built from `schedule-fall2026.js` in the `new-build-bio4-solano` repo. Open Course Engine, click **Restore**, pick that file, confirm, and all three sections appear in the Class menu with empty rosters ready for import.

| Section | CRN | Days | Tag | Sessions | Color |
|---|---|---|---|---|---|
| BIO 004 Class 1 | 80650 | Mon / Wed | PM | 31 | Navy |
| BIO 004 Class 2 | 80654 | Tue / Thu | AM | 32 | Terra cotta |
| BIO 004 Class 3 | 80655 | Tue / Thu | EVE | 32 | Teal |

Term runs Mon Aug 17 to Fri Dec 11, 2026, 17 weeks. All three are set Team-based with 6 teams and separate lecture and lab attendance.

Closures are already excluded, so no attendance column exists for them: Labor Day Sep 7, Veterans Day Nov 11, and Travel Day Nov 25 for Class 1; Professional Development Oct 13 and Thanksgiving Nov 26 for Classes 2 and 3.

All five exam dates per section fall on generated class days, including the odd one: **Class 1 Exam 4 is Monday Nov 16**, not a Wednesday. That is intentional per the repo note and is preserved.

## Branding

The header carries your three-figure anatomy mark in navy, terra cotta, and brushed gold. Team names default to the anatomy set from your original roll sheet: Femur, Scapula, Cranium, Patella, Sternum, Mandible, plus Humerus and Clavicle if a class uses seven or eight teams. Rename any of them per class.

Everything uses the PRIMARY palette: navy `#1E3D4C`, brushed gold `#B8924A`, terra cotta `#C2734D` and terra-dark `#A0522D`, white cards on an off-white `#FAFAF9` page. No sage, no cream. Two derived tones exist for accessibility reasons and are documented in the compliance notes: a darker gold `#9A7833` for focus rings and a darker grey `#7C8990` for form borders, because the brand values fell below the WCAG contrast floor in those two roles.

## Files

- `Course_Engine.html` is the application.
- `BIO004_Fall2026_three_sections.json` is the Restore file for the three sections.
- `Course_Engine_README.md` is this file.
- `Course_Engine_compliance-notes.md` is the accessibility audit.

Dr. Sharilyn Rennie
