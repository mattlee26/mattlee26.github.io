# mattlee26.github.io

Personal academic website of Matthew M. Lee, PhD, built with [al-folio](https://github.com/alshedivat/al-folio) (v1.x) and hosted on GitHub Pages at <https://mattlee26.github.io>.

## Where things live

| To change…                            | Edit                                                                                |
| ------------------------------------- | ----------------------------------------------------------------------------------- |
| Bio and homepage sections             | `_pages/about.md` (photo: `assets/img/prof_pic.jpg`)                                |
| Bold name and page titles             | `assets/css/main.scss` (rules at the end; the rest is copied from the theme)       |
| Publications                          | `_bibliography/papers.bib` (`selected = {true}` puts a paper on the homepage)      |
| Research and teaching pages           | `_pages/research.md`, `_pages/teaching.md`                                          |
| CV page                               | `_data/cv.yml` (the on-page CV)                                                     |
| Downloadable CV PDF                   | replace `assets/pdf/Lee_Matthew_CV.pdf` (keep the file name)                        |
| Social links (email, Scholar, ORCID…) | `_data/socials.yml`                                                                 |
| Site title, URL, feature flags        | `_config.yml`                                                                       |

### Adding a publication

Add a BibTeX entry to `_bibliography/papers.bib`. Useful extra fields: `abbr` (badge text, e.g. `{AJPH}`), `abstract`, `doi`, `selected = {true}`, `altmetric = {true}`, `dimensions = {true}`, `pdf` (a file in `assets/pdf/` or a URL), `code`, `slides`. Mark co-first authors by appending `†` to the last name (e.g. `Lee†, Matthew M.`) and add `annotation = {† Co-first authors}`. Then add the entry to the `Publications` list in `_data/cv.yml` so it appears on the CV page too.

### CV PDF

The CV download button and the CV icon on the home page both link to `assets/pdf/Lee_Matthew_CV.pdf`. To update it, export your CV to PDF (without your home address or phone number) and overwrite that file. The CV page itself is built from `_data/cv.yml`, so update both when your CV changes.

## Previewing locally

Requires Ruby 3.2+ (e.g. `brew install ruby`) and a UTF-8 locale.

```bash
bundle install
LANG=en_US.UTF-8 bundle exec jekyll serve
```

Then open <http://localhost:4000>. Responsive images need ImageMagick (`brew install imagemagick`); without it, set `imagemagick: enabled: false` in a local override config.

## Publishing

The site is the GitHub repository `mattlee26/mattlee26.github.io`. Because the repository is named `<username>.github.io`, GitHub serves it at the root of <https://mattlee26.github.io>.

To publish a change, commit it and push to `main`:

```bash
git add -A
git commit -m "Describe the change"
git push
```

The **Deploy site** workflow builds the site and pushes the result to the `gh-pages` branch, and GitHub Pages serves it a minute or two later. Watch progress in the repository's **Actions** tab.

One-time settings this depends on (already done):

- **Settings → Actions → General → Workflow permissions:** Read and write permissions.
- **Settings → Pages → Build and deployment:** Deploy from a branch, branch `gh-pages`, folder `/ (root)`, no custom domain.
