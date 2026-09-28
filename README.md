# mekty2012.github.io

Personal academic homepage, built with the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template and served at <https://mekty2012.github.io>.

## Where to edit

| What | File |
|---|---|
| Introduction (front page) | `_pages/about.md` |
| Name, sidebar bio, affiliation, links (email, Scholar, ORCID, ...) | `_config.yml` → `author:` |
| Profile photo | replace `images/profile.png` |
| Publications | one Markdown file per paper in `_publications/` — copy `_publications/_TEMPLATE.md` |
| PDFs (papers, slides, CV) | `files/` → served at `/files/<name>` |
| Top menu | `_data/navigation.yml` |
| Blog posts | `_posts/YYYY-MM-DD-title.md` |

Push to `master` and GitHub Pages rebuilds the site in a minute or two.

## Local preview (optional)

Requires Ruby + Bundler:

```sh
bundle install
bundle exec jekyll serve -l -H localhost
```

Then open <http://localhost:4000>. See `AGENTS.md` and the upstream template's wiki for more.
