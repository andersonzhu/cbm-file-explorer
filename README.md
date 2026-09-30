# CBM File Explorer

Open a THECB CBM fixed-width report file in your browser and read it as named, filterable columns instead of a wall of characters. You can also correct individual records and save the file back out.

**Use it now: <https://andersonzhu.github.io/cbm-file-explorer/>**

Everything runs in your browser tab. Files are read locally and never uploaded, so it is safe to use with student-level data.

## What it does

- **Finds the right layout for you.** CBM submission files start with an `HY2K` header record that names the report. The explorer reads it and picks the matching record layout. If there is no header, it tries the file name, then the record code and line length.
- **Splits every record into named columns**, each labeled with its manual item number and character positions (for example `#12 Major (CIP) · 53–60`).
- **Filters and sorts.** Type in the box under any column, or use the column's value list with counts. Search the whole raw record from the box at the top.

  | Type | Meaning |
  |---|---|
  | `5138` | contains 5138 (codes also match their labels, so `nonres` finds tuition status 3) |
  | `=3` / `=1,2` | exactly 3 / exactly 1 or 2 |
  | `!=2` | anything except 2 |
  | `>6`, `<=12`, `1300..1399` | numeric comparisons and ranges |
  | `=` | blank |
- **Shows what codes mean.** Semester `1` shows as Fall, Tuition Status `3` as Nonresident, Grade `7` as Withdrawn. Credit-hour fields stored as `0300` display as `3.00`.
- **Checks the file.** It compares the trailer's record count with the file, and flags records with the wrong length or record code.
- **Inspects one record.** Select a row to see the raw line under a character ruler, with every field shaded and matched to its column.
- **Profiles fields.** The Fields view shows how often each field is filled, how many distinct values it has, and the most common values. It flags "unused" positions that contain data.
- **Exports.** Copy the table for Excel (leading zeros kept), or save it as CSV.

## Editing records

1. Select a row, then choose **Edit record** (or double-click the row).
2. Change values. Each one is checked against the layout as you type: field length, numeric and date formats, and codes not listed in the manual. The raw record updates live.
3. Press **Enter** to apply, or **Esc** to cancel. Edited records and cells are marked in blue, and hovering an edited cell shows the old value.
4. Choose **Save as text file**. The saved file is identical to the original except the characters you changed: same header and trailer, record order, line endings and encoding.

In Chrome and Edge, saving opens a Save As dialog and later saves write to the same file. Other browsers download the file.

Edits live only in the open tab until you save. Closing a file (the × on its tab) with unsaved edits asks whether to save first. Closing the whole browser tab shows only the browser's own generic "Leave site?" warning, because browsers do not allow pages to customize it.

## Built-in layouts

All 14 fixed-width reports in the *Reporting and Procedures Manual for Texas Community, Technical, and State Colleges* (Fall 2025):

| Report | Name |
|---|---|
| CBM0C1 | Student Census Report |
| CBM0E1 | Student End of Semester Report |
| CBM0CS | Census Student Schedule Report |
| CBM00S | Student Schedule Report |
| CBM002 | Texas Success Initiative Report |
| CBM009 | Graduation Report |
| CBM008 | Faculty Report |
| CBM00A | Students in Continuing Education Courses Report |
| CBM00C | Continuing Education Class Report |
| CBM00M | Occupational Skills Achievement Report |
| CBM00N | Student Number Change Report |
| CBM005 | Building and Room Use Report |
| CBM011 | Facilities Room Inventory Report |
| CBM014 | Facilities Building Inventory Report |

Files from before Fall 2025 open too. CBM00S and CBM0CS records were 128 characters and CBM00A records were 152; the fields added in Fall 2025 are simply blank.

Manual: <https://reportcenter.highered.texas.gov/reporting-manual-ctc-fall-2025>

## Adding your own layouts

Open **Layouts → New layout** and paste the rows of a record layout, one field per line: a name, then its start position and length (or start–end). Rows copied from Excel work. Optional tags at the end of a line: `[unused]`, `[dec=2]`, `[date]`, `[codes=SEM]`.

Layouts you make are saved in your browser only. To share them:

- **With a colleague:** Layouts → Share → Copy export, then they paste it and choose Import.
- **With everyone who uses your copy:** paste the export between the `office-layouts` script tags near the top of `index.html`.

## Limitations

- **Older CTC reports** (CBM001, CBM004 and other pre-Summer 2022 formats) are not built in. Add them under Layouts.
- **Universities, health-related institutions and career schools** use different manuals. Their layouts are not built in.
- **Code meanings** were transcribed by hand from the manual's item instructions. The record layouts (positions and lengths) were checked to chain with no gaps or overlaps, but spot-check any code label you rely on.
- Web fonts load from Google Fonts; offline, the page falls back to system fonts.

## Running it locally

There is nothing to build or install. It is a single self-contained HTML file: download `index.html` and double-click it.

## Data and privacy

No server, no analytics, no uploads. The page reads files with the browser's file APIs, and layouts you create are stored in the browser's local storage on your computer.
