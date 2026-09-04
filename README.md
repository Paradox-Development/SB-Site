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

## Before this can go live

1. **Images.** Nothing has been migrated — book covers and gallery photos are
   dashed grey boxes until files land in `images/`. See
   [images/README.md](images/README.md).
2. **Blog post bodies.** The three post titles and opening lines are on
   `/blog/`, but the full post text wasn't brought across, so no title links
   anywhere yet. Each post needs its own folder.
3. **Contact form.** `contact-sherry-blackman/index.html` posts to a Formspree
   placeholder (`REPLACE_WITH_FORM_ID`). Until a real endpoint is wired up and
   tested, submissions go nowhere.
4. **Press & Media** needs real content — it has none on either site.
5. **Legal pages.** Privacy policy and terms are skeletons. The privacy policy
   in particular needs to describe the contact form once it's connected.
6. **Reader reviews — worth a permissions check.** The quotes on the *Tales
   from the Trail* and *Call to Witness* pages are reader reviews carried over
   from the old site; several read as Amazon customer reviews. They're already
   published on Sherry's site, so this is status quo rather than a new
   exposure, but reviewer-written text isn't automatically hers to republish.
   Worth confirming before launch. The four named *Call to Witness*
   endorsements are ordinary solicited blurbs and aren't a concern.
7. **`CNAME` + DNS.** Not added yet, and deliberately so: `sherryblackman.com`
   currently serves the live WordPress site. Adding `CNAME` and cutting DNS
   over is the last step, once the content above is actually ready.

Six `.editor-note` boxes remain, one per outstanding item above. They're
visible on the page by design. Find them with
`grep -rl editor-note --include=*.html .`

## Note on paths

Assets and links are root-relative (`/styles.css`, `/field-notes/`), which
assumes the site is served from a domain root. That's correct for
`sherryblackman.com`, and correct for the local preview server — but it means
the `paradox-development.github.io/SB-Site/` project URL will render unstyled.
Review locally, not there.

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
