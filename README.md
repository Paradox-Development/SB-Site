# Sherry Blackman — sherryblackman.com

Author site for Sherry Blackman. Static HTML/CSS, no build step. Being
deployed on qikSites, where Sherry can edit it in the browser with qikEdit; the
original GitHub Pages deploy and Claude Code self-service flow are still in
the repo (see [Publishing](#publishing)). Generated from
[site-self-service-template](https://github.com/Paradox-Development/site-self-service-template).

**If you're Sherry, you want [WELCOME.md](WELCOME.md) instead** — this file is
for the site admin.

## Layout

```
index.html                              Home
author-sherry-blackman/                 About
rev-it-up/                              Book: Rev-It-Up
letters-to-our-daughters/               Book: Letters to Our Daughters
tales-from-the-trail-.../               Book: Tales from the Trail
call-to-witness-by-sherry-blackman/     Book: Call to Witness
field-notes/                            Photo gallery
author-press-and-media/                 Press & media
contact-sherry-blackman/                Contact form
blog/                                   Post index
404.html, privacy-policy.html, terms-and-conditions.html
styles.css                              All styling; design tokens in :root
images/                                 Image assets — see images/README.md
QIKEDIT_DESIGN_GUIDE.md                 qikEdit tag reference, from qikSites
claude.md                               Instructions for Sherry's Claude Code sessions
WELCOME.md                              Sherry's how-to
```

Page URLs deliberately match the existing WordPress site's paths so inbound
links and search rankings survive the move. Don't rename these folders without
setting up redirects — GitHub Pages has no redirect support, so a rename means
a dead link.

## Content migration status

Text copy has been migrated from the live WordPress site: the homepage bio and
hero, the full About biography, all four book descriptions with their real
subtitles and taglines, the four *Call to Witness* endorsements, reader reviews
on the *Call to Witness* and *Tales from the Trail* pages, and the contact
lede. Typography was normalised (curly quotes, em dashes) and a few obvious
typos in the source were corrected; wording is otherwise unchanged.

Two pages had nothing to migrate, because they're empty on the old site too:
**Press & Media** is a bare heading, and **Field Notes** is a photo carousel
with no text.

Images have been migrated too: four book covers, an author photo, and six
Field Notes photographs, all resized and re-compressed (11 MB of originals down
to 1.5 MB). Blog post pages exist at their original URLs.

## Third-party content deliberately left out

Three things on the old site aren't Sherry's to republish, and were **not**
copied across. Each has a note on the page explaining what's missing:

- **The Buechner post** (`/blog/books-are-to-read.../`) is, in substance, one
  long verbatim passage from Frederick Buechner's work. The page now carries a
  short description of the passage instead. Options: link out to it and add
  Sherry's own reflection, quote a couple of lines with attribution, or clear
  permission with the estate.
- **The outdoor-recreation post** reproduced a long passage from a news
  article, including direct quotes from an interviewee, with no citation. Only
  Sherry's own opening paragraph was carried over.
- **The Delaware Water Gap post's five photographs** are credited on the old
  site to @SitesofConscience. They were not downloaded.

Also worth a decision: the reader reviews on the *Tales from the Trail* and
*Call to Witness* pages read like Amazon customer reviews. They're already
published on Sherry's site, so carrying them is status quo rather than new
exposure — but reviewer-written text isn't automatically hers. The four named
*Call to Witness* endorsements are ordinary solicited blurbs and aren't a
concern.

## Before this can go live

1. **Contact form.** `contact-sherry-blackman/index.html` holds a qikForms
   placeholder (`<!-- qikform -->`). Build the form in the qikSites portal,
   assign it to the placeholder in qikEdit and send a test message. Until then
   no form renders on the page. Its styling is already in `styles.css`
   (`.qikforms-embed`).
2. **Press & Media** needs real content — it has none on either site.
3. **Field Notes photo descriptions.** The six photos came over with empty
   `alt=""` (the old carousel had none). They can be written in qikEdit's
   gallery editor.
4. **The three third-party items above** need a decision each.
5. **Legal pages.** Privacy policy and terms are skeletons. The privacy policy
   in particular needs to describe the contact form once it's connected.
6. **`.qikignore`.** qikSites serves everything in the synced path, so commit a
   `.qikignore` at the root for files the site shouldn't serve: `claude.md`,
   `WELCOME.md`, `.claude/`, `images/README.md`. (`README.md`, `.github/` and
   `QIKEDIT_DESIGN_GUIDE.md` are excluded by qikSites already.)
7. **How the two editing paths share the repo.** If qikSites syncs a branch of
   this repo, qikEdit commits straight to that branch, while the Claude Code
   flow merges `session/*` PRs into `main`. The same page edited from both
   sides raises a sync conflict in qikSites, and if the synced branch requires
   PRs, qikEdit can't publish at all. Decide which branch qikSites syncs before
   Sherry uses both.
8. **Domain cutover.** `sherryblackman.com` still serves the live WordPress
   site. Pointing it at the new host is the last step, once the content above
   is actually ready.

Eight `.editor-note` boxes remain, one per outstanding content item. They're
visible on the page by design, and each sits inside a qikEdit field so it can
be deleted from the editor. Find them with
`grep -rl editor-note --include=*.html .`

## Note on paths

Every internal link and asset is **depth-relative** (`styles.css` at the root,
`../styles.css` one level down, `../../styles.css` two). This is deliberate:
root-relative paths (`/styles.css`) only resolve when the site is served from a
domain root, so they render the site completely unstyled on the GitHub Pages
project URL and when a page is opened straight off disk. Relative paths work in
all three places, which means the site can be reviewed anywhere before the
domain is switched over:

- `paradox-development.github.io/SB-Site/` ✓ (except the menus, see below)
- the local preview server ✓
- double-clicking `index.html` ✓ (except the menus)
- qikSites, and `sherryblackman.com` after cutover ✓

`<link rel="canonical">` and `og:url` stay absolute and point at
`sherryblackman.com` — that's correct, and tells search engines where the real
site lives regardless of where a copy is being previewed.

**If you add a page, keep paths relative to that page's depth.** A `/`-prefixed
link will look fine on the live domain and silently break everywhere else.

**The exception is the header and footer menus**, which are `/`-prefixed on
purpose. They're `qik-nav` regions (`main-nav`, `footer-nav`), and qikEdit
writes one identical copy of each into every page, so their links can't vary by
depth. The menus therefore only resolve when the site is served from a domain
root (qikSites, `localhost`). The current-page highlight is set by the inline
script at the bottom of each page rather than a hardcoded `aria-current`.

Images uploaded through qikEdit's media picker are the same: they land in
`/media/` and are referenced with `/media/...` paths. The images already in
the repo stay in `images/` with relative paths.

## qikEdit tags

The site is tagged for qikEdit (full syntax in `QIKEDIT_DESIGN_GUIDE.md`) so
Sherry can click on a page in qikSites and edit it in the browser.

| What | Tag | Where |
| --- | --- | --- |
| Browser tab title | `qik-text page-title` | Every page |
| Header and footer menus | `qik-nav main-nav`, `qik-nav footer-nav` | Every page; qikEdit copies a menu edit to all pages |
| Headings, page text, book descriptions, bookseller buttons, each endorsement and review | `qik` | Per page |
| Book covers, author photo | `qik-img` | Home, book pages, About |
| Field Notes photos | `qik-gallery`, items are `<figure class="photo-item">` | Field Notes |
| Contact form | `<!-- qikform -->` placeholder | Contact |

Conventions:

- A single element is tagged *inside* the element
  (`<h1><!-- qik page-heading -->…<!-- qik-end --></h1>`), so qikEdit edits
  only its text and can't strip the element's class. Multi-paragraph regions
  are wrapped from outside.
- Field names are unique within a page. The same name on different pages
  (`page-heading`, `book-text`) is fine.
- Every yellow `.editor-note` sits inside a field, so it can be deleted from
  the editor once the real content is in.
- When adding content, tag it like the content around it. Start a new page
  from an existing page at the same depth so it gets `page-title` and both
  menus.

Not tagged, on purpose: the social links, the header *Buy on Amazon* button
and the colophon, which repeat on every page and have no cross-page sync in
qikEdit; and the meta description / Open Graph tags, which would need qik
comments inside attribute values (those would break outside qikSites).

**The blog doesn't use qikBlog.** qikBlog expects a root `blog.html` and flat
`blog/<post>.html` files, which would change the existing post URLs. The post
list on `blog/index.html` is an ordinary `qik` field, so a new post means
duplicating an existing post page and adding an entry to that list.

**Not yet exercised in a live qikEdit session.** The tags are validated
(balanced, unique names), but two fields are worth checking after the first
real edit: the bookseller buttons (classed `<a>` elements inside a WYSIWYG
field) and the blog post list (headings inside list items).

**Keep tooling off the HTML.** qikEdit writes back only the regions that
changed, so don't run Prettier or other formatters over the pages, and don't
store media in Git LFS. See the guide's *Setting the site up as a Git
repository* section.

## Previewing

From the repo root:

```
npx --yes serve . --listen 8765
```

or `python -m http.server 8765`, then open <http://localhost:8765>. Serve from
the repo root rather than opening files off disk, or the menus won't resolve.

## Publishing

There are two paths:

- **qikEdit.** Sherry edits in the browser on qikSites and publishes from the
  editor. If qikSites is synced to this repo, those edits come back as commits
  on the synced branch (see item 7 under *Before this can go live*).
- **Claude Code self-service**, automated — see [claude.md](claude.md).
  Changes on a `session/*` branch open a PR;
  `.github/workflows/auto-publish.yml` validates and squash-merges it, and
  Pages rebuilds. `CNAME` and `.github/workflows/**` are excluded from
  auto-publish and go through the site admin.
