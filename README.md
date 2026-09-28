# mekty2012.github.io

Personal academic homepage, built with the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template and served at <https://mekty2012.github.io>.

## Where to edit

| What | File |
|---|---|
| Introduction (front page) | `_pages/about.md` |
| Name, sidebar bio, affiliation, links (email, Scholar, ORCID, ...) | `_config.yml` → `author:` |
| Talks | one Markdown file per talk in `_talks/` — copy `_talks/_TEMPLATE.md` |
| Publications | one Markdown file per paper in `_publications/` — copy `_publications/_TEMPLATE.md` |
| PDFs (papers, slides, CV) | `files/` → served at `/files/<name>` |
| Top menu | `_data/navigation.yml` |
| Education, teaching, service | `_pages/about.md` |

Push to `master` and GitHub Pages rebuilds the site in a minute or two.

## CV

The CV is written in LaTeX at `cv/cv.tex` (it is not generated from the site, so update both when
something changes). To rebuild and publish it:

```sh
cd cv
latexmk -pdf -outdir=build cv.tex
cp build/cv.pdf ../files/cv.pdf
```

The site's "CV" menu item links to `files/cv.pdf`.

## Local preview (optional)

Requires Ruby + Bundler:

```sh
bundle install
bundle exec jekyll serve -l -H localhost
```

Then open <http://localhost:4000>. See `AGENTS.md` and the upstream template's wiki for more.
