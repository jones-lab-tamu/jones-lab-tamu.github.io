# Visit the Jones Lab website at: [jones-lab.org](https://jones-lab.org)!

---

# Maintaining the site

Everything below is plain text files. You never need to touch HTML.

After any change: `git add .`, `git commit -m "..."`, `git push origin main`. The site
rebuilds itself and is live in a minute or two.

## How everything is wired together

The whole site is cross-linked with three short ID lists. Nothing else connects a person,
a paper, a project, or an approach — so these are the only values that work.

**Every one of them fails silently on a typo.** `lab: [Vanesa]` or `tags: circuitstate`
produces no error, no warning, nothing in the build log. The paper simply doesn't appear
where you expected. If something is missing after a deploy, check the spelling here first.

| Field | Goes in | Valid values are the |
|---|---|---|
| `lab:` | a paper or project | **member handles** below |
| `tags:` | a paper | **project tags** below |
| `techs:` | a paper | **approach keys** below |

### Member handles — for `lab:`

Set by the `handle:` line in each file in `team/_posts/`.

| Handle | Person | | Handle | Person |
|---|---|---|---|---|
| `Jeff` | Jeff Jones | | `Logan` | Logan Perry *(alum)* |
| `Jordan` | Jordan Cook | | `Blanca` | Blanca Perez *(alum)* |
| `Nicole` | Nicole Keene | | `Ashley` | Ashley Starnes *(alum)* |
| `Vanessa` | Vanessa Muhl | | `Emma` | Emma Ellisor *(alum)* |
| `Farina` | Farina Pourmir | | `Jason` | Jason Armitage *(alum)* |
| `Sam` | Sam Sweck | | `Arthur` | Arthur Mayo III *(alum)* |
| `Danny` | Daniela López Lorenzo | | | |

Alumni handles stay valid — keep them in the `lab:` list of papers they authored.

Because links use the handle and not the person's name, **renaming someone breaks
nothing**. Change the `title:` in their team file and everything keeps working.

### Project tags — for a paper's `tags:`

Set by the `tag:` line in each file in `projects/_posts/`.

| Tag | Project |
|---|---|
| `pacemaker-dynamics` | Pacemaker dynamics |
| `output-pathways` | Output pathways |
| `circuit-state` | Circuit state |
| `behavioral-organization` | Behavioral organization |

A paper can belong to more than one. Use a YAML list: `tags: [circuit-state, pacemaker-dynamics]`.

### Approach keys — for a paper's `techs:`

Set by the `key:` lines in `_data/approaches.yml`.

| Key | Approach |
|---|---|
| `behavior` | Circadian behavioral analysis |
| `opto` | Neuromodulation |
| `photometry` | In vivo imaging |
| `liveslice` | In vitro imaging |
| `crispr` | Neurogenetics |
| `tracing` | Neuroanatomy |
| `hormones` | Manipulation and measurement of hormones |
| `machinelearning` | Complex behavioral analysis |
| `3dprint` | Open-source tool development |

A paper can list several, separated by spaces: `techs: opto tracing behavior`.

### If these tables go stale

The files are always the truth. To regenerate the lists:

```
grep -h '^handle:' team/_posts/*.md          # member handles
grep -h '^tag:'    projects/_posts/*.md      # project tags
grep '^- key:'     _data/approaches.yml      # approach keys
```

---

## Adding a paper

**1. Save the graphical abstract** in `images/papers/`, e.g. `2026_iscience.jpg`.
JPG, PNG, or GIF.

**2. Create** `papers/_posts/YYYY-MM-DD-shortname.md`

- The date is the publication date. It sets the ordering — newest first.
- The shortname becomes the URL: `2026-08-21-iscience.md` becomes
  `jones-lab.org/papers/paper/iscience/`. Lowercase, no spaces.
- **The shortname must be unique across every file in `papers/_posts/`.** Two files
  sharing a shortname silently collapse into one page — the second overwrites the first
  and a paper disappears from the site with no error anywhere. Journal names collide
  easily, so for a second paper in the same venue, add the first author:
  `2026-05-22-biorxiv-keene.md` and `2026-05-04-biorxiv-purvines.md`.

**3. Paste this in and fill it out:**

```yaml
---
layout: paper
category: paper
title: "Circadian pacemaker dynamics differ between diurnal and nocturnal mammals"
year: "2026"
shortref: "Muhl <i>et al.</i>, iScience (2026)"
journal: "iScience"
authors: "Muhl V, Lopez-Lorenzo D, Pourmir F, Sweck SO, Ono D, Jones JR"
lab: [Vanessa, Danny, Farina, Sam, Jeff]
image: /images/papers/2026_iscience.jpg
fulltext: https://www.sciencedirect.com/science/article/pii/S2589004226023837
pdflink: 
github: 
pmid: 
doi: "10.1016/j.isci.2026.117005"
dryad_doi: 
tags: 
---
```

| Field | Notes |
|---|---|
| `lab` | **The one that matters.** Handles of lab members on the paper. Order doesn't matter. |
| `category` | Always `paper`. No template reads it, but it shapes the URL (`/papers/paper/...`). Leave it out and this paper's link won't match every other one. |
| `authors` | The citation string shown on the paper page, verbatim. Cosmetic only — it does not affect linking. Non-lab coauthors go here and nowhere else. |
| `year` | Keep the quotes. After 2021 lands in the main grid; 2021 and earlier go under "Previous papers". |
| `shortref` | The small line under the thumbnail. `<i>et al.</i>` gives the italics. |
| `image` | Path from the site root, with the leading slash. |
| `fulltext`, `pdflink`, `pmid`, `doi`, `dryad_doi` | All optional. Leave blank rather than deleting — blank ones are skipped automatically. |
| `tags` | Optional. **Project tags** (see the table above) to also show this paper under those projects. One value, or a YAML list for several: `tags: [circuit-state, pacemaker-dynamics]`. |
| `techs` | Optional. Space-separated **approach keys** (see the table above), e.g. `opto tracing behavior`. Works both ways — the paper appears under those approaches on the Approaches page, and those approaches are listed on the paper's own page. |

Occasionally useful: `preprint: true` adds a "PREPRINT (not yet peer-reviewed)" banner,
`supplement: /pdfs/...` adds a supplement link, `skip: true` hides it from the papers index.

---

## Adding a lab member

**1. Save their photo** in `images/team/`, e.g. `images/team/Jane.jpg`.

**2. Create** `team/_posts/YYYY-MM-DD-First-Last.md` — the date is roughly when they joined.

```yaml
---
layout: member
title: Jane Doe
position: PhD Student
nickname: Jane
handle: Jane
email: jane.doe@tamu.edu
github: 
scholar: 
image: /images/team/Jane.jpg
cv: 
alumni: false
---

A paragraph about Jane. Shows on her page.
```

- **`handle`** must be unique. First name is the convention. If you ever have two Janes,
  make the second one something like `Jane D.` — it's matched exactly, so the two never
  collide. Quote it if it contains a comma.
- **`alumni: false`** puts them under Current members. This is the field that controls it —
  there is no `alum:` field, so don't use that spelling.
- Add `undergrad: true` for undergraduates. They appear under their own heading, which
  stays hidden when there are no current undergrads.
- `email`, `github`, `scholar`, `cv`, `twitter`, `website`, `calendar` are all optional and
  are skipped when blank.

**3. Add their handle** to the `lab:` field of any paper or project they're on.

## When someone leaves

Change `alumni: false` to `alumni: true` in their team file. They move to Past members.

**Leave their handle in any paper's `lab:` list** — they keep credit on papers they
authored, which is what you want.

Taking them off a *project* is a separate, manual step: delete their handle from that
project's `lab:` field. Marking someone alumni does not remove them from project pages
on its own.

---

## Adding a project

**1. Save an image** in `images/misc/`.

**2. Create** `projects/_posts/YYYY-MM-DD-shortname.md`

```yaml
---
layout: research
title: "Output pathways"
question: "How does an SCN output pathway shape behavioral timing?"
lab: [Nicole, Farina, Danny, Jeff]
image: /images/misc/output_pathways.png
tag: output-pathways
---

A paragraph or three describing the project. Shows on the project page and on the
projects index.
```

- **`title`** — the short theme name. This is also what appears on member pages, and on
  the projects page it is the link through to this project (underlined to show that).
- **`question`** — the smaller question shown under the title. Optional.
- **`image`** — shown beside the text. Any aspect ratio works; the figure is sized as a
  percentage of the row, so wide images are fine. To resize every project figure, change
  the one `.project-figure` rule in `scss/custom.scss` (currently 30%). Crop white
  margins out of the file first — blank space inside the image makes the artwork look
  smaller than the space it occupies, and no CSS setting can compensate for that.
- **`lab`** — members are listed on the project page in exactly this order.
- **`tag`** — a short unique keyword, **no spaces** (use hyphens). Any paper with a
  matching value in its `tags:` shows up under Publications on this project's page.
  If no paper matches, that section reads "Coming soon!".
- **The date in the filename sets the order on the projects page** — newest first. To
  reorder the themes, change the dates.

Adding a project here adds a row to the **project tags** table near the top of this file —
worth updating so the reference stays accurate.

The no-spaces rule matters: Jekyll treats a paper's `tags:` as a list and splits a bare
string on whitespace, so a tag like `circuit state` would be read as two separate tags,
`circuit` and `state`, and would never match anything.

The intro paragraph and the "Where this is going" section at the bottom of the projects
page are page-level prose, not projects. They live in `projects/index.html` between the
clearly marked `INTRO PROSE` and `CLOSING PROSE` comments.

---

## Adding or renaming an approach

The Approaches page is generated entirely from `_data/approaches.yml`. Don't edit
`approaches/index.html` — add an entry to the data file and drop the image in
`images/misc/`:

```yaml
- key: ephys
  name: Electrophysiology
  detail: patch clamp, multielectrode array
  image: /images/misc/ephys.png
  alt: Electrophysiology
  width: 230
  height: 230
```

- **`key`** is what papers put in their `techs:` field. Short, lowercase, no spaces.
  Changing a key later means updating every paper that uses it.
- **`name`** is the heading, and is also what shows on each paper's page.
- The order of entries here is the order of sections on the page, and the order the
  approaches are listed on a paper.
- **`width`/`height`** are the image's real pixel size (right-click the file >
  Properties). They don't set the display size — CSS does — they just let the browser
  reserve space before the image loads, so that links to `/approaches/#key` land on the
  right section instead of drifting as images arrive. Safe to omit, but include them.

Because the page and the paper listings read the same file, they can't drift apart.
A `techs:` value with no matching `key` simply shows nothing — no error — so check
your spelling against the data file.

## Running the site locally (optional)

Only needed if you want to preview before pushing.

```
bundle exec jekyll serve
```

Then open http://localhost:4000. Ctrl-C to stop.

For a build byte-identical to what actually deploys, add `--safe`:

```
bundle exec jekyll build --safe
```

### If gems are missing

This project installs its gems into the project folder rather than into Ruby's system
directory, which avoids needing administrator rights. On a fresh clone, run these once:

```
bundle config set --local path vendor/bundle
bundle install
```

`vendor/` and `.bundle/` are gitignored and are excluded from the built site.

### A note on the Jekyll version

GitHub Pages builds this site with its own pinned gem set, currently Jekyll 3.x, and the
`Gemfile` deliberately matches it. That means what you build locally is what deploys.

Do **not** bump the Gemfile to Jekyll 4 — GitHub Pages would ignore it and build with 3.x
anyway, and the two versions differ enough that templates can work locally and fail on
deploy. (Jekyll 3's `where_exp` accepts only a single condition, no `and`, which is exactly
that trap.)
