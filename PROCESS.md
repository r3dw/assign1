# Building the CLC Home Page Gallery: Process and Token Usage

A record of how the 25-page gallery of Chicago Language Center home page concepts was built, and what each step cost in tokens.

## How to read the token numbers

- **What is counted:** the figures are the `subagent_tokens` totals reported when each background agent or workflow finished. That covers the work the agents did to write, check and edit the pages.
- **What is not counted:** my own (main conversation) token usage is not exposed to me, so it is **not included anywhere in this document**. That covers reading the screenshots, planning, writing prompts, running checks and talking with you. It is real usage, and it is not zero. For the full session total, check Claude Code's `/cost` or `/context` command.
- **Percentages** are each step's share of the **subagent total of 1,346,499 tokens**. They are *not* a share of total session usage.
- **Per-page numbers:** Round 2 and the image-swap step ran as single workflows, so only the total for the whole step is known. Per-page figures for those two steps don't exist. Rounds 1 and 3 have per-page figures.

## Summary

| # | Step | Subagent tokens | % of subagent total |
|---|------|----------------:|--------------------:|
| 1 | Status line setup (two agent runs) | 22,313 | 1.66% |
| 2 | Round 1: 10 concept pages (01–10) | 291,587 | 21.66% |
| 3 | Analysis of the peer-university screenshots | 113,525 | 8.43% |
| 4 | Round 2: 10 concept pages (11–20) | 385,571 | 28.64% |
| 5 | Round 3: 5 audience and intent pages (21–25) | 158,219 | 11.75% |
| 6 | Image swap on pages 01–20 | 375,284 | 27.87% |
| | **Total (subagents only)** | **1,346,499** | **100.00%** |

Steps with no subagent cost (gallery index, image cropping, backups, verification) are described below. Their cost sits in my uncounted main-session usage.


| Steps | % of Usage |
|------|---------:|
| 1-2 | approx 5% |
| 3-4 | approx 8% |
| 5-6 | approx 6% |
|TOTAL| approx 19%|

## Step by step

### 1. Status line setup (22,313 tokens, 1.66%)
You asked for the status line to be configured from your shell PS1. The `statusline-setup` agent found no PS1 (only conda init and a PATH export) and changed nothing. You then picked what to show: directory and git branch, model name, context % used, and rate limits. The agent wrote the status line to `~/.claude/settings.json`. It has not been run or tested, and it needs `jq` installed.

### 2. Round 1: 10 concept pages, 01–10 (291,587 tokens, 21.66%) [Approx 5% of Usage]
- I read your two UChicago screenshots (`inputs/primary/`) and four of the inspiration screenshots (Harvard, Oxford, Stanford, Yale) to understand the current page.
- I wrote a shared content file with the real text: mission, OLA and ELI, stories teaser, visit info, three blog posts and footer.
- I picked ten concepts meant to differ in structure, information architecture and interaction, not just styling, and launched ten agents in parallel, one per page.
- Each page is plain HTML and CSS in one file, with minimal JavaScript and no external resources.

| Page | Concept | Tokens | % of subagent total |
|---|---|---:|---:|
| 01 | Broadsheet | 29,412 | 2.18% |
| 02 | Terminal | 29,936 | 2.22% |
| 03 | Bento Dashboard | 30,041 | 2.23% |
| 04 | Long Hallway (horizontal scroll) | 27,327 | 2.03% |
| 05 | Hello in 50 Languages | 31,825 | 2.36% |
| 06 | Swiss Grid | 27,819 | 2.07% |
| 07 | Passport and Boarding Pass | 31,967 | 2.37% |
| 08 | Split-screen Handbook | 28,259 | 2.10% |
| 09 | The Conversation | 27,675 | 2.06% |
| 10 | Card Catalog | 27,326 | 2.03% |

I then wrote the gallery `index.html` with a live thumbnail of each page. I checked that every page's JavaScript parses and that no page loads external resources.

**Fix, after your first review:** the gallery thumbnails were blank and clicking a card opened a Finder window. Cards linked to folders (`01-broadsheet/`), which doesn't work when opened from disk. I changed every card link and thumbnail to point at `…/index.html`.

### 3. Peer-university screenshot analysis (113,525 tokens, 8.43%) 
For Round 2 you asked me to draw on the screenshots in `inputs/inspiration/`. One agent read all 19 screenshots (Brown, Cambridge, Columbia, Harvard, Oxford, Princeton, Stanford, UNC, Yale). It wrote a per-school analysis, a list of content and UI patterns the UChicago page lacks, and 12 ideas worth borrowing. Examples were events feeds, a language directory, "I am a…" audience paths, placement-test calls to action, testimonials and room booking.

### 4. Round 2: 10 concept pages, 11–20 (385,571 tokens, 28.64%)
- I wrote an extra file of **sample** content inspired by the peer sites (events, a language list, service tiles, audience pathways, a four-year pathway, FAQ). It was flagged as sample and limited to the real statistics, with no invented numbers or names.
- I ran a workflow of ten agents. The concepts: Switchboard (audience selector), Calendar First, Language Atlas, Four-Year Pathway, Placement Wizard, Story Wall, Campus Map, Plain Index, Launcher, and A Day at the CLS.
- Each agent was told not to resemble Round 1 and not to touch any other file.
- I added a "Round 2" section to the gallery index. The first 10 pages were untouched.
- Checks: JavaScript parses on every page, and no page loads external resources. Page 14 has no JavaScript by design.

### 5. Round 3: audience and search-intent pages, 21–25 (158,219 tokens, 11.75%)
You asked for five more pages that vary by audience (student, instructor, administrator…) and by what a visitor is searching for (classes, placement exam, certification…).

- **Image assets first (no subagent cost):** I cropped the logo, skyline strip, front-desk photo, student photo, statue photo, unit icons and footer wordmark from your two screenshots into `gallery/assets/`, and checked the crops by eye.
- Five agents ran in parallel:

| Page | Concept (audience and intent) | Tokens | % of subagent total |
|---|---|---:|---:|
| 21 | What Are You Looking For? (search-first, anyone) | 36,500 | 2.71% |
| 22 | Find a Class (students) | 29,782 | 2.21% |
| 23 | Instructor Hub (instructors, certification) | 30,858 | 2.29% |
| 24 | Testing and Certification (exams, flowchart) | 30,339 | 2.25% |
| 25 | Department Service Desk (administrators) | 30,740 | 2.28% |

- I added a "Round 3" section to the gallery index and checked JavaScript syntax, image paths and external references. Pages 01–20 were not modified.
- Exam types, certificates, class listings, workshops and policy documents are **sample content**, with no fees or dates. Each page notes this in its footer.

### 6. Real images in pages 01–20 (375,284 tokens, 27.87%)
You asked me to replace the placeholders on the first 20 pages with the real images and logos, changing nothing else.

- **Safety first (no subagent cost):** I copied the 20 original pages to `backup/first-20-before-images/` (outside `gallery/`, so it isn't deployed), and gave you restore commands.
- Ten agents, two pages each, swapped placeholders for the matching asset. Each image was styled to match its page (for example halftone on the broadsheet, a phosphor tint on the terminal, sepia on the card catalog) using CSS only.
- Where a page had no slot for an asset, that asset was skipped. Page 18 (Plain Index) was left unchanged because it is text-only by design.
- Checks: every image path resolves, JavaScript still parses, and each page differs from its backup by only 3 to 39 lines.

## Files and folders

| Path | Contents |
|---|---|
| `gallery/index.html` | Gallery index: 25 cards in three rounds, with live thumbnails |
| `gallery/01-…` to `gallery/25-…` | The 25 pages, one `index.html` each |
| `gallery/assets/` | Eight cropped images from the screenshots |
| `backup/first-20-before-images/` | Pristine copies of pages 01–20 from before the image swap |
| `PROCESS.md` | This document |

The working notes used to brief the agents (content, sample content, inspiration analysis) are in the session scratchpad, not in the project.

## Restoring the original 20 pages

From the project directory:

```
for d in backup/first-20-before-images/[0-9][0-9]-*; do rm -rf "gallery/$(basename $d)"; cp -R "$d" gallery/; done
```

Restore a single page (example: 03):

```
cp backup/first-20-before-images/03-bento/index.html gallery/03-bento/index.html
```

Don't use `git checkout` for this. Most of the gallery has never been committed, so it would not restore these pages.

## Known limitations

- **Testing:** none of the pages has been opened in a browser by me. Checks were scripted: JavaScript syntax, image paths and external references. Layout, responsiveness and interactions (carousels, tabs, filters, scroll effects) were reviewed only by you.
- **Page 08:** only the first story has real content; tabs 2–9 are placeholders, and its "Search" nav item does nothing.
- **Placeholders left in place:** a few carousels and postcard sets (pages 01, 07, 09) still use gradient placeholders for slides 2–9, since no matching images exist.
- **Page 25:** its agent said it skipped the inspiration notes, so it may borrow less from the peer sites.
- **Sample content:** Rounds 2 and 3 include sample content that doesn't exist on the real site. Replace or remove it before publishing.
- **Deployment:** deploy the whole `gallery` folder so `assets/` goes with the pages. It is plain static files, so no build step is needed.
