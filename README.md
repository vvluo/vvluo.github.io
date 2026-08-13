# vvluo.github.io

Personal site. Plain HTML/CSS, no build step — GitHub Pages serves it as-is.

- `index.html` — home
- `gallery.html` — photos
- `styles.css` — shared styles for both pages
- `gallery/` — web-ready photos (metadata stripped)
- `resume.pdf`

## Adding a photo

Camera originals carry GPS coordinates, timestamps, and device info, and anything
committed here becomes public and stays in git history. Never commit a file straight
from the camera — `.gitignore` blocks `IMG_*` for that reason.

Run it through this first:

```bash
magick INPUT.jpg -auto-orient -resize 2000x2000\> -colorspace sRGB -strip -quality 82 gallery/NAME.jpg
```

- `-auto-orient` bakes rotation into the pixels — required, because `-strip` removes the
  EXIF orientation tag that would otherwise keep the photo upright.
- `-strip` removes EXIF/GPS/IPTC/XMP/ICC.
- `-colorspace sRGB` converts before the profile is dropped, so colors don't shift.

Verify nothing survived:

```bash
magick identify -verbose gallery/NAME.jpg | grep -iE "exif|gps|icc|iptc|xmp"
```

Then add a `<figure>` to `gallery.html`. Keep captions region-level (a park or campus,
not an address).
