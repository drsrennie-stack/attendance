# TBL Grade Engine

A single-file, data-driven weighted gradebook that any professor can reuse every term. It is the sibling of the Attendance Engine and uses the same method: students are stored as data, the rows render live, a setup wizard builds each course, and everything saves in the browser only.

## What it does

- **Multi-course.** Set up any number of classes. Switch between them from the **Course** menu. Each course keeps its own roster, categories, columns, weights, grade scale, and scores.
- **Course setup wizard.** Enter identity (title, institution, course and section, term, CRN, instructor), choose team-based or not, choose whether to show a weighted final grade, edit categories and weights, set the grade scale, and import a roster. **Course setup** edits the current course; **+ New course** starts a fresh one.
- **Flexible categories and columns.** Start from TBL defaults (RAT, Lab Quizzes, Lab Practicals, Lecture Exams, Cumulative Final) and change anything. Add as many assessment columns as you need inside each category, so the number of labs, lecture exams, quizzes, and RAT sessions is entirely up to you. Each column has its own max points and an optional date.
- **TBL totals for Canvas.** A category can be set to type **TBL (iRAT + tRAT)**. Each column in it is one RAT session that holds a separate iRAT score, a tRAT score, an optional bonus point column, and an automatic **Total** column (iRAT + tRAT + bonus). The Total is the single number you record in Canvas, and it is labeled accordingly in the export. iRAT is individual; tRAT and bonus are team-scored. Bonus is included in the Total but treated as extra credit in the weighted percent (it is not added to the denominator).
- **Weighting engine, toggleable.** Turn **Compute weighted grade** on or off any time. Off, you get a clean raw-score gradebook with per-column class averages. On, each category contributes its weight to a running weighted percent and a letter grade. Weights do not have to total 100; the running grade is computed only across categories that already have at least one scored column, so a mid-term grade stays fair.
- **Editable grade scale.** Default A 90, B 80, C 70, D 60, F 0. Change the lower bound of any letter to match your syllabus.
- **Team-scored categories (TBL).** Mark a category as team-scored (tRAT is by default). Entering a score for one student fills every member of that student's team for that column.
- **Roster import, three ways.**
  - **Upload your Attendance Engine HTML page.** Open the class you record attendance on, in your browser choose File then Save Page As and pick "Webpage, HTML Only", then upload that file in the wizard. The roster is read straight from it: names and confidential flags import exactly, and team assignments import when your browser saves the selected team. Dropped and no-show students are left out.
  - **Link from the Attendance Engine (same site).** If both tools are served from the same web address, pick the class in the wizard to pull the enrolled roster (names, team names, confidential flags) with no file at all. (This works only same-origin, because each tool's data lives in that site's browser storage.)
  - **CSV or paste.** Upload a CSV (auto-detects `Name`, or `Last Name` plus `First Name`, and optional `Team` and `Confidential`) or paste one name per line as `Last, First`. Add `[C]` after any name to flag FERPA confidential / directory hold.
- **Two tabs.** Active and Dropped / Withdrawn, each with a live count. A **Drop** button records a reason and date and moves the student; **Restore** puts them back.
- **Add a student.** Files a typed `Last, First` name into the active sheet in alphabetical order.
- **Export CSV.** One file with status, name, confidential flag, team, every column score (including each RAT session's iRAT, tRAT, bonus, and its Canvas Total), each category percent, the weighted final and letter (when weighting is on), and drop reason and date.
- **Print.** A landscape print layout hides controls and prints the active sheet.

## How state is stored

Everything saves in the browser only, using `localStorage`. No server, no accounts, no student data leaves the machine.

- `grade_engine_index_v1` lists the courses (id and label).
- `grade_engine_current_v1` is the id of the active course.
- `grade_engine_course_<id>` holds one course (meta, options, categories, weights, grade scale, the assessment columns, and the full student array with scores).

The roster-link feature reads the Attendance Engine's own keys (`attn_engine_index_v1`, `attn_engine_course_<id>`) but never writes to them.

Because storage is per-browser, a course set up on one computer does not appear on another. Use Export CSV to move records out. Clearing browser data for this site erases the courses, so export anything you want to keep.

## First run

The engine starts blank and opens the setup wizard. Enter the course identity, pick options, adjust categories and weights, set the grade scale, and import or link a roster. Clicking **Save course** creates and stores it. From then on the engine opens to the last course used.

## Reuse and accessibility

- The file is self-contained. For reuse, this one HTML file is all you need.
- It bakes the iframe height-sender (postMessage with id, ResizeObserver, load and resize listeners) for Kajabi and GitHub Pages embeds.
- WCAG 2.2 AA is the floor, AAA where achievable. See `Grade_Engine_compliance-notes.md` for the audit. A live screen-reader pass still needs a human.

## Files

- `Grade_Engine.html` is the app.
- `Grade_Engine_README.md` is this file.
- `Grade_Engine_compliance-notes.md` is the accessibility audit.

Dr. Sharilyn Rennie
