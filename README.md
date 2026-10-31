# YiminGao0113.github.io

Personal academic website for Yimin Gao, published at <https://YiminGao0113.github.io>.

Built with [Jekyll](https://jekyllrb.com/) on a vendored copy of the
[Minimal Light](https://github.com/yaoyao-liu/minimal-light) theme (CC0), and
hosted on GitHub Pages. The previous Academic Pages version is kept on the
`backup-academicpages` branch.

## Editing content

| What | Where |
| --- | --- |
| Name, sidebar details and links | `_config.yml` |
| Homepage (bio, interests, service, teaching) | `_pages/about.md` |
| Publications | one Markdown file per paper in `_publications/` |
| Talks | `_data/talks.yml` |
| Research projects (homepage list + subpages) | one Markdown file per project in `_projects/` |
| Beyond research | `_pages/personal.md` |
| CV | `files/Yimin_Gao_CV.pdf` |
| Profile photo | `images/profile.jpg` |
| Layout / styles | `_layouts/default.html`, `_sass/_site.scss` (theme: `_sass/minimal-light*.scss`) |

Publications are grouped by the `category` field in each file's front matter.
Valid values are defined under `publication_category` in `_config.yml`:
`conferences`, `manuscripts` (journal articles), and `patents`.
Entries are sorted by their `date` field, newest first.

## Local preview

Requires Ruby 3.1 (the `github-pages` gem does not run on 3.2+):

```bash
bundle install
bundle exec jekyll serve -l -H localhost
```

Then open <http://localhost:4000>.

Pushing to `master` triggers the GitHub Pages build; the `Jekyll build` workflow
in `.github/workflows/` runs the same build as a check.
