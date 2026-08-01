# YiminGao0113.github.io

Personal academic website for Yimin Gao, published at <https://YiminGao0113.github.io>.

Built with [Jekyll](https://jekyllrb.com/) using the
[Academic Pages](https://github.com/academicpages/academicpages.github.io) template
and hosted on GitHub Pages.

## Editing content

| What | Where |
| --- | --- |
| Homepage / bio | `_pages/about.md` |
| Publications | one Markdown file per paper in `_publications/` |
| Teaching | `_pages/teaching.html` |
| CV page | `_pages/cv.md` (PDF lives at `files/cv.pdf`) |
| Site title, sidebar links, social profiles | `_config.yml` |
| Header menu | `_data/navigation.yml` |
| Profile photo | `images/profile.jpg` |

Publications are grouped by the `category` field in each file's front matter.
Valid values are defined under `publication_category` in `_config.yml`:
`manuscripts` (journal articles), `conferences`, `patents`, and `books`.
Entries are sorted by their `date` field, newest first.

## Local preview

Requires Ruby 3.x:

```bash
bundle install
bundle exec jekyll serve -l -H localhost
```

Then open <http://localhost:4000>.

Pushing to `master` triggers the GitHub Pages build; the `Jekyll build` workflow
in `.github/workflows/` runs the same build as a check.
