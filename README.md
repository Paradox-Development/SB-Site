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

## Before this can go live

1. **Real content.** Every page ships with placeholder copy in yellow
   `.editor-note` boxes saying what belongs there. They're visible on the page
   by design — they should all be gone before launch. Find them with:
   `grep -rl editor-note --include=*.html .`
2. **Images.** Book covers and gallery photos are dashed grey boxes until
   files land in `images/` — see [images/README.md](images/README.md).
3. **Contact form.** `contact-sherry-blackman/index.html` posts to a Formspree
   placeholder (`REPLACE_WITH_FORM_ID`). Until a real endpoint is wired up and
   tested, submissions go nowhere.
4. **Legal pages.** Privacy policy and terms are skeletons. The privacy policy
   in particular needs to describe the contact form once it's connected.
5. **Endorsements.** The home page has four empty quote cards. Nothing was
   invented — real endorsements need pasting in, or the section deleting.
6. **`CNAME` + DNS.** Not added yet, and deliberately so: `sherryblackman.com`
   currently serves the live WordPress site. Adding `CNAME` and cutting DNS
   over is the last step, once the content above is actually ready.

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
