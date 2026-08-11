# Visit the Jones Lab website at: [jones-lab.org](https://jones-lab.org)!

---

# Maintaining the site

Everything below is plain text files. You never need to touch HTML.

After any change: `git add .`, `git commit -m "..."`, `git push origin main`. The site
rebuilds itself and is live in a minute or two.

## How people get linked to papers and projects

Every lab member has a **handle** — a short unique nickname set by the `handle:` line in
their file in `team/_posts/`. Papers and projects list the handles of the lab members
involved in a `lab:` field. That is the only thing that connects a person to their work.

Current handles:

| Handle | Person | | Handle | Person |
|---|---|---|---|---|
| `Jeff` | Jeff Jones | | `Logan` | Logan Perry |
| `Jordan` | Jordan Cook | | `Blanca` | Blanca Perez |
| `Nicole` | Nicole Keene | | `Ashley` | Ashley Starnes |
| `Vanessa` | Vanessa Muhl | | `Emma` | Emma Ellisor |
| `Farina` | Farina Pourmir | | `Jason` | Jason Armitage |
| `Sam` | Sam Sweck | | `Arthur` | Arthur Mayo III |
| `Danny` | Daniela López Lorenzo | | | |

If that table goes stale, the real list is always the `handle:` lines in `team/_posts/`.

**A handle typo fails silently.** `lab: [Vanesa]` won't produce an error — the paper just
won't appear on her page. If someone is missing after a deploy, check the spelling first.

Because links use the handle and not the person's name, **renaming someone breaks
nothing**. Change the `title:` in their team file and everything keeps working.

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
| `tags` | Optional. One project tag to also show this paper on that project's page: `other`, `cholinergic`, `circadianda`, `cbas`, `scndmh`. |

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
title: "The project title" 
lab: [Nicole, Vanessa, Danny, Jeff]
image: /images/misc/scndmh.png
tag: scndmh
---

A paragraph describing the project. Shows on the project page and the projects index.
```

- **`lab`** — members are listed on the project page in exactly this order.
- **`tag`** — a short unique keyword. Any paper with a matching `tags:` value shows up
  under Publications on this project's page. If no paper matches, that section reads
  "Coming soon!".

---

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
