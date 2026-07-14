# AI Reading Group Website — Complete Guide

This document explains everything about how this website works, written for
someone who has never touched it before. If you're taking over this site from
someone who graduated or left, start here — you don't need to know how to code
to maintain this.

---

## Fill this in first

Whoever sets this up should fill in the three blanks below, right at the top,
so the next person doesn't have to go hunting:

- **The Google Sheet (the data):** `[paste the Google Sheet link here]`
- **The live website address:** `[paste the website URL here]`
- **Where the website file is hosted** (GitHub Pages / department server /
  other): `[describe here]`

---

## The short version

If you just want to add a session or a person and don't want to read the whole
guide:

1. Open the Google Sheet linked above.
2. Click the `Sessions` tab (for a talk) or `Members` tab (for a person).
3. Add a new row with the details, following the existing rows as examples.
4. That's it — the website reads the sheet automatically. Refresh the page
   after a minute or two and your change will be there.

Nobody needs to touch the website file itself for routine updates. The rest of
this guide covers that in more detail, plus what to do if something looks
wrong, and how to hand this off to someone else.

---

## 1. How this whole thing works

There are two pieces:

1. **The Google Sheet** — this is where all the actual information lives:
   every session, every member, the homepage text. Think of it as a filing
   cabinet.
2. **The website file (`index.html`)** — this is just a window that displays
   whatever is in the filing cabinet. It doesn't store anything itself; every
   time someone visits the site, it asks the Google Sheet "what's the current
   schedule?" and shows the answer.

Because of this split, **you almost never need to edit the website file**.
Adding, changing, or removing content is just editing spreadsheet rows, the
same way you'd edit any Google Sheet.

The website file only needs to be touched again if:
- You're setting the site up for the very first time (see [Section 9](#9-first-time-setup-only-do-this-once)), or
- You want to change the site's design (colors, fonts, layout).

---

## 2. Adding a new session

1. Open the Google Sheet and click the **`Sessions`** tab at the bottom.
2. Click into the first empty row and fill in each column. Here's what each
   one means:

| Column | What to put | Example |
|---|---|---|
| `title` | The talk's title | `Diffusion Models Beyond Images` |
| `presenter` | The presenter's full name | `Ananya Rao` |
| `photo` | Optional — a link to their photo, see [Section 6](#6-adding-profile-photos) | *(leave blank, or a link)* |
| `program` | `PhD` or `MTech` | `PhD` |
| `batch` | Their batch/cohort year | `2024` |
| `date` | The session date — **see the warning below** | `2026-08-03` |
| `slides` | Optional — a link to the slides | `https://drive.google.com/...` |
| `about` | Optional — a sentence or two describing the talk | `A look at...` |
| `references` | Optional — reading list for the talk, see [Section 4](#4-adding-clickable-links) | `Vaswani et al. (2017)` |
| `profile` | Optional — only needed for guest presenters not in the `Members` tab, see [Section 5](#5-linking-names-to-profile-pages) | *(usually leave blank)* |

**⚠️ Important — the date column:** it must be typed as `YYYY-MM-DD`
(e.g. `2026-08-03` for August 3rd, 2026) and the column must be formatted as
**plain text**, not as a date. If it's not already set that way:

1. Click the column letter at the top to select the whole `date` column.
2. Go to **Format → Number → Plain text**.
3. Type dates as `YYYY-MM-DD` from then on.

(This matters because Google Sheets likes to "help" by reformatting dates,
which can silently break how the website sorts sessions into upcoming vs.
past.)

That's the whole process — no need to decide whether it's "upcoming" or
"past." The website checks today's date automatically and puts it in the
right place. See [Section 3](#3-how-upcoming-vs-past-is-decided) for how that
works.

---

## 3. How "upcoming" vs. "past" is decided

You never choose this yourself. Every time the website loads, it:

1. Looks at today's actual date.
2. Compares it to the `date` you typed for each session.
3. Anything today or later → shown under **Upcoming Sessions**.
4. Anything before today → shown under **Past Sessions**, most recent first.

So a session you add today for next month will automatically "move itself"
into Past Sessions the day after it happens — you don't need to go back and
change anything.

---

## 4. Adding clickable links

Both the `slides` and `references` columns can contain clickable links. There
are two ways to write them:

**A bare link** — just paste the URL by itself:
```
https://drive.google.com/file/d/abc123/view
```
This shows up as a link, using a default label ("Slides" for the slides
column).

**A named link** — write it as `Label => URL` to control what text shows
instead of a raw link:
```
Lecture slides (PDF) => https://drive.google.com/file/d/abc123/view
```
This shows up as clickable text reading "Lecture slides (PDF)" instead of the
full link.

**Multiple links in the `references` column:** separate several entries with
a `|` (the character above the Enter key, usually `Shift + \`), like this:
```
Original paper => https://arxiv.org/abs/1706.03762|Code repo => https://github.com/example/repo|A related survey, no link yet
```
This produces three separate bullet points — two clickable with custom names,
one plain text.

**A note on files (PDFs, datasets, etc.):** this website can't store files
itself — it's just a webpage, not a file server. Upload the actual file to
Google Drive (or Dropbox, or a department server) first, get a shareable
link from there, and use that link the way described above.

**Why not just use Google Sheets' own "Insert link" (Ctrl+K)?** It's a
reasonable instinct, but it doesn't work here — Ctrl+K stores the link in a
way this website's simple data feed can't read; it would just show the name
with no link. Typing it as `Label => URL` like above is the reliable way.

---

## 5. Linking names to profile pages

Presenter and member names can link out to that person's own page (a
personal website, department profile, LinkedIn, etc.) instead of being
plain text.

**For members:** add a `profile` column to the `Members` tab (if it's not
already there) and put their profile link in it. That's it — their name
becomes clickable everywhere it appears, including as a presenter in the
Sessions tables.

| Column | Example |
|---|---|
| `profile` | `https://yourdept.edu/people/ananya-rao` |

**How this connects to Sessions:** you don't need to enter a profile link
twice. When someone presents a session, the website automatically looks up
their name in the `Members` tab and reuses the profile link from there — as
long as the `presenter` name in `Sessions` is spelled exactly the same as
their `name` in `Members` (capitalization doesn't matter, but the words
need to match).

**For guest speakers who aren't in the Members tab:** add a `profile`
column to the `Sessions` tab too, and fill it in just for their row. A
profile link entered directly on a session always takes priority over the
automatic lookup.

Leave the `profile` cell blank for anyone who doesn't have one — their name
just stays as plain, non-clickable text.

---

## 6. Adding profile photos

Yes — both `Sessions` (for the presenter) and `Members` have a `photo`
column. Fill it in with a link to an image and it replaces the colored
initials circle with the actual photo (cropped to a circle automatically).

**The tricky part:** the link has to point directly at the image file, not
at a webpage that happens to show the image. A regular Google Drive "share"
link doesn't work here — it opens a preview page, not the raw picture.

The easiest reliable option:

1. Go to [imgur.com](https://imgur.com) (no account needed).
2. Upload the photo.
3. Right-click the uploaded image → **"Copy image address"**.
4. Paste that link into the `photo` column.

That link will end in something like `.jpg` or `.png` — that's how you know
it's a direct image link and will actually work.

**If you'd rather use Google Drive:** upload the photo, share it as
"Anyone with the link — Viewer", then copy the file ID out of the share
link (the long string between `/d/` and `/view`) and build a direct link in
this format:
```
https://drive.google.com/uc?export=view&id=PASTE_FILE_ID_HERE
```
This works, but Google occasionally rate-limits or blocks these links for
sites that get a lot of traffic, so Imgur tends to be more reliable for a
public website.

**Photo tips:** roughly square photos look best, since they're cropped into
a circle. Leave the `photo` cell blank for anyone without one — they'll just
show initials instead, which is a perfectly normal look for this site.

---

## 7. Adding, updating, or graduating a member

| Column | What to put |
|---|---|
| `name` | Full name |
| `photo` | Optional — a link to their photo, see [Section 6](#6-adding-profile-photos) |
| `batch` | Batch/cohort year |
| `program` | e.g. `PhD`, `MTech (2-Year)` |
| `status` | Exactly `current` or `alumni` (lowercase) |
| `profile` | Optional — a link to their profile page, see [Section 5](#5-linking-names-to-profile-pages) |

**When someone graduates or leaves:** you don't need to delete their row or
move it anywhere. Just change their `status` cell from `current` to `alumni`,
and the website automatically moves them from the "Current Members" table to
the "Alumni" table.

---

## 8. Editing the homepage text

There's a third tab called **`Site`** with just two cells:

- `description` — the short intro line shown at the top of the homepage
- `about` — the longer paragraph shown in the About section

Edit either cell directly; there's nothing else to it.

---

## 9. First-time setup (only do this once)

Skip this section if the site is already up and running — it's only needed
if you're setting this up from scratch, or rebuilding it after something
went badly wrong.

1. Create a new Google Sheet.
2. Rename the first tab to exactly `Sessions`. Add two more tabs named
   exactly `Members` and `Site` (tab names are case-sensitive).
3. In each tab: **File → Import → Upload**, choose the matching CSV file
   from this package (`Sessions.csv`, `Members.csv`, `Site.csv`), and select
   **"Replace current sheet"**. This gives you the correct column headers
   plus a few example rows — edit or delete those examples.
4. Set the `date` column in `Sessions` to Plain Text format (see the warning
   in Section 2).
5. Click **Share** (top right) → **General access** → change to **"Anyone
   with the link"** → make sure the role is set to **Viewer**. The website
   only ever reads this sheet, so Viewer access is enough; nobody can edit
   your data through the website itself.
6. Copy the Sheet ID from the URL. It's the long string of letters and
   numbers between `/d/` and `/edit`:
   ```
   https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/edit
                                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^  <- this part
   ```
7. Open `index.html` in any plain text editor (Notepad, TextEdit, VS Code —
   right-click the file → "Open with" → choose a text editor, **not** a web
   browser). Near the top, inside the `<script>` section, find:
   ```
   var SHEET_ID = "PASTE_YOUR_SHEET_ID_HERE";
   ```
   Replace the placeholder text between the quotes with the ID you copied,
   then save the file.
8. Upload `index.html` to wherever the site is hosted (GitHub Pages, a
   department web server, etc.). If you don't already have hosting set up,
   GitHub Pages is free — search "GitHub Pages" for their setup guide, or
   ask your department's IT support.
9. Fill in the three blanks at the top of this document with the Sheet link,
   the live site URL, and where it's hosted, so the next person has them.

---

## 10. Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| The website shows a message saying it isn't connected to a Google Sheet | The `SHEET_ID` in `index.html` is still the placeholder text | Follow the matching step in Section 9 |
| The website shows an error about not being able to load data | The sheet isn't shared publicly, the Sheet ID is wrong, or a tab is misnamed | Check sharing is "Anyone with the link — Viewer"; check tab names are exactly `Sessions`, `Members`, `Site` |
| A session shows up in the wrong section (upcoming/past) | The date wasn't typed as `YYYY-MM-DD`, or the column isn't set to Plain Text | Reformat the column as Plain Text (Section 2) and retype the date |
| A link isn't clickable | Typo in the `Label => URL` syntax, or the URL doesn't start with `http://` or `https://` | Check spacing around `=>` and that the link is complete |
| I edited the sheet but the website still looks the same | Browser cache, or the page hasn't been reloaded | Reload the page (Ctrl+R or Cmd+R); try a hard refresh (Ctrl+Shift+R or Cmd+Shift+R) if that doesn't help |
| Multiple references in one cell aren't separating properly | Missing or wrong `\|` character between entries | Make sure it's a straight pipe character `\|`, not a comma or semicolon |

---

## 11. A few terms explained

- **Sheet ID** — the long code in a Google Sheet's URL that uniquely
  identifies it, needed once to connect the website to the sheet.
- **Tab** — one of the pages inside a single Google Sheet, shown along the
  bottom (this project uses three: `Sessions`, `Members`, `Site`).
- **Hosting** — the place where the actual `index.html` file lives so that
  visiting a web address shows the page. Examples: GitHub Pages, a
  university web server.
- **Plain text formatting** — a Google Sheets setting for a column that
  stops it from auto-converting what you type (like dates) into its own
  format.
- **Hard refresh** — reloading a webpage while ignoring anything the browser
  has saved from a previous visit, useful when a page seems "stuck" on old
  content.

---

## 12. Handing this off to someone new

When the person currently responsible for this site is about to leave
(graduating, changing groups, etc.), here's the checklist to actually
transfer responsibility, not just the information:

- [ ] Share the Google Sheet with the new maintainer's email as an **Editor**
      (Share button → add their email → set role to Editor).
- [ ] Give them access to wherever the site is hosted (e.g. add them as a
      collaborator on the GitHub repository, or share department server
      credentials through your institution's normal process).
- [ ] Send them the link to this document, or make sure it's easy to find —
      e.g. pin it as a comment on the Google Sheet, or keep a copy alongside
      `index.html` wherever it's hosted.
- [ ] Update the three blanks at the very top of this document if anything
      has changed (new Sheet, new hosting location, etc.).
- [ ] Do a quick test together: have the new maintainer add a test session,
      confirm it shows up on the live site, then delete the test row.

That last step matters more than it sounds like — confirming end-to-end that
the new person can actually make a change and see it work, rather than just
handing over access and hoping for the best.

---

## 13. Getting further help

For anything not covered here — wanting a different design, adding new
fields, moving to a system with login-protected editing, or anything else —
this whole site was built with an AI assistant (Claude, from Anthropic).
Whoever maintains this can go back to a Claude conversation, describe what
they need, and reference this guide and the existing `index.html` file for
context.
