# Images

Drop image files straight into this folder. Nothing else is needed — they're
served from `/images/<filename>`.

## What's here

All of these came across from the old site and are already wired into the
pages. Originals were 11 MB in total; they've been resized and re-compressed
to 1.5 MB with no visible quality loss.

| File | Used on |
| --- | --- |
| `rev-it-up-cover.jpg` | Home, Rev-It-Up |
| `letters-to-our-daughters-cover.jpg` | Home, Letters to Our Daughters |
| `tales-from-the-trail-cover.jpg` | Home, Tales from the Trail |
| `call-to-witness-cover.jpg` | Home, Call to Witness |
| `author-photo.jpg` | About |
| `field-notes-1.jpg` … `field-notes-6.jpg` | Field Notes gallery |

`call-to-witness-cover.jpg` is only 336×500 — that's the largest version the
old site had. It's fine at its current display size but would pixelate if
shown any larger. A higher-resolution original from the publisher would be
worth getting.

The Field Notes photos have empty `alt=""`, because the old carousel had no
captions. Worth writing; Sherry can add them in qikEdit's gallery editor.

## Images added through qikEdit

qikEdit's media picker doesn't use this folder. Images uploaded there go to
`/media/` on qikSites and are referenced as `/media/<filename>`, so a page can
end up with a mix of `images/` and `/media/` paths. Both work on qikSites.

Uploads are capped at 2560px on the longest edge, turned the right way up and
stripped of camera and GPS metadata. The size advice below still applies: a
2560px photo can be several megabytes.

## Deliberately not migrated

The five photographs on the Delaware Water Gap blog post are credited on the
old site to @SitesofConscience, not to Sherry, so they weren't downloaded.
Retailer and press logos (Amazon, Barnes & Noble, Books-A-Million) weren't
brought over either — the buy buttons are styled text, which avoids using
other companies' trademarks.

## Practical notes

- **Book covers** look best at roughly 800px wide, portrait, 2:3 ratio.
- **Gallery photos** at roughly 1200px wide.
- **Keep files under ~400KB each.** Large photos straight off a phone or
  camera are often 5MB+ and will make the site slow to load. Resize before
  adding.
- **JPG** for photographs, **PNG** only if something needs a transparent
  background.
- Use lowercase filenames with dashes instead of spaces — `author-photo.jpg`,
  not `Author Photo.jpg`.

## Permissions

Only add images there's the right to publish: Sherry's own photographs,
publisher-supplied cover art, or press photos cleared for use. This repo is
public, so anything added here is world-readable.
