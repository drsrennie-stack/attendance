# Attendance Engine

A single-file, data-driven interactive roll sheet that any professor can reuse every term. It generalizes the BIO 004 roll tool: instead of a roster baked into the page, students are stored as data, the rows render live, and a setup wizard builds each course.

## What it does

- **Multi-course.** Set up any number of classes. Switch between them from the **Course** menu. Each course remembers its own roster, schedule, teams, and attendance.
- **Course setup wizard.** Enter identity (title, institution, course and section, term, CRN, instructor), pick the meeting schedule, choose team-based or not, and import a roster. **Course setup** edits the current course; **+ New course** starts a fresh one.
- **Schedule generator.** Set a first class date, number of weeks, and which weekdays the class meets. The day columns generate automatically (Mon = M, Tue = T, Wed = W, Thu = R, Fri = F).
- **Roster import.** Upload a CSV or paste names.
  - CSV headers are auto-detected: it looks for `Name` (or `Last Name` plus `First Name`), and optional `Add Code`, `Position`, and `Confidential` columns.
  - No headers? One name per line as `Last, First` for the class list, or `Last, First, CODE` for wait-list rows (the add code as a third comma field).
  - Add `[C]` after any name to flag FERPA confidential / directory hold.
- **Three tabs.** Enrolled, Wait List, and Dropped / No-show, each with live counts.
- **Attendance.** Click a day cell to cycle blank to present to absent. The toolbar tally updates live for the active tab.
- **Drop and No-show.** Every enrolled and wait-list row has both a **Drop** (withdrew) and a **No-show** (never attended) button. Either one records the date and the reason and moves the student to the Dropped / No-show tab. **Restore** puts them back where they were.
- **Wait List to Enrolled.** The arrow Enroll button promotes a wait-list student to Enrolled.
- **Add a student.** Files a typed `Last, First` name into the active sheet in alphabetical order.
- **Teams (TBL).** A Team-based toggle shows or hides all team features. When on: rename the six teams, pick a team per student to color the name, and Auto-assign to split Enrolled into balanced teams. Colors are fixed and contrast-checked.
- **Export CSV.** Downloads one file with status, position, name, confidential flag, team, add code, every class day marked Present or Absent, and the dropped reason and date.
- **Print.** A landscape print layout hides controls and prints the active sheet.

## How state is stored

Everything saves in the browser only, using `localStorage`. No server, no accounts, no student data leaves the machine.

- `attn_engine_index_v1` lists the courses (id and label).
- `attn_engine_current_v1` is the id of the active course.
- `attn_engine_course_<id>` holds one course (meta, schedule, generated days, teams, and the full student array with attendance).

Because storage is per-browser, a course set up on one computer does not appear on another. Use Export CSV to move records out for your own files. Clearing browser data for this site erases the courses, so export anything you want to keep.

## First run

On first open with no saved courses, the engine seeds your existing **BIO 004, CRN 60099** course (23 enrolled, 20 wait-list with add codes, Mon to Thu across Weeks 1 and 2, teams on, team names Femur, Scapula, Cranium, Patella, Sternum, Mandible) so nothing from the original tool is lost and you have a live example to copy.

## Reuse and accessibility

- The file is self-contained. For reuse, this one HTML file is all you need.
- It bakes the iframe height-sender (postMessage with id, ResizeObserver, load and resize listeners) for Kajabi and GitHub Pages embeds.
- WCAG 2.2 AA is the floor, AAA where achievable. See `compliance-notes.md` for the audit. A live screen-reader pass still needs a human.

## Files in this folder

- `Attendance_Engine.html` is the app.
- `README.md` is this file.
- `compliance-notes.md` is the accessibility audit.

Dr. Sharilyn Rennie
