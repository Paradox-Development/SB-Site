# Sherry Blackman — sherryblackman.com

Author site for Sherry Blackman. Static HTML/CSS, no build step, deployed via
GitHub Pages. Generated from
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

1. **Contact form.** `contact-sherry-blackman/index.html` posts to a Formspree
   placeholder (`REPLACE_WITH_FORM_ID`). Until a real endpoint is wired up and
   tested, submissions go nowhere.
2. **Press & Media** needs real content — it has none on either site.
3. **Field Notes captions and alt text.** The six photos came over with no
   captions (the old carousel had none) and empty `alt=""`.
4. **The three third-party items above** need a decision each.
5. **Legal pages.** Privacy policy and terms are skeletons. The privacy policy
   in particular needs to describe the contact form once it's connected.
6. **`CNAME` + DNS.** Not added yet, and deliberately so: `sherryblackman.com`
   currently serves the live WordPress site. Adding `CNAME` and cutting DNS
   over is the last step, once the content above is actually ready.

Eight `.editor-note` boxes remain, one per outstanding item. They're visible on
the page by design. Find them with
`grep -rl editor-note --include=*.html .`

## Note on paths

Every internal link and asset is **depth-relative** (`styles.css` at the root,
`../styles.css` one level down, `../../styles.css` two). This is deliberate:
root-relative paths (`/styles.css`) only resolve when the site is served from a
domain root, so they render the site completely unstyled on the GitHub Pages
project URL and when a page is opened straight off disk. Relative paths work in
all three places, which means the site can be reviewed anywhere before the
domain is switched over:

- `paradox-development.github.io/SB-Site/` ✓
- the local preview server ✓
- double-clicking `index.html` ✓
- `sherryblackman.com` after cutover ✓

`<link rel="canonical">` and `og:url` stay absolute and point at
`sherryblackman.com` — that's correct, and tells search engines where the real
site lives regardless of where a copy is being previewed.

**If you add a page, keep paths relative to that page's depth.** A `/`-prefixed
link will look fine on the live domain and silently break everywhere else.

## Previewing

From the repo root:

```
npx --yes serve . --listen 8765
```

or `python -m http.server 8765`, then open <http://localhost:8765>.

## Publishing

Automated — see [claude.md](claude.md). Changes on a `session/*` branch open a
PR; `.github/workflows/auto-publish.yml` validates and squash-merges it, and
Pages rebuilds. `CNAME` and `.github/workflows/**` are excluded from
auto-publish and go through the site admin.
