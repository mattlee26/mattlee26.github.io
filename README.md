# mmlee.me

Personal academic website of Matthew M. Lee, PhD, built with [al-folio](https://github.com/alshedivat/al-folio) (v1.x) and hosted on GitHub Pages at <https://mmlee.me>.

## Where things live

| To change…                            | Edit                                                                                |
| ------------------------------------- | ----------------------------------------------------------------------------------- |
| Bio, photo caption, homepage sections | `_pages/about.md` (photo: `assets/img/prof_pic.jpg`)                                |
| News items on the homepage            | `_news/*.md` (one file per item)                                                    |
| Publications                          | `_bibliography/papers.bib` (`selected = {true}` puts a paper on the homepage)      |
| Research and teaching pages           | `_pages/research.md`, `_pages/teaching.md`                                          |
| CV page and CV PDF                    | `_data/cv.yml` (RenderCV format); the PDF is rebuilt automatically on push         |
| Social links (email, Scholar, ORCID…) | `_data/socials.yml`                                                                 |
| Site title, URL, feature flags        | `_config.yml`                                                                       |

### Adding a publication

Add a BibTeX entry to `_bibliography/papers.bib`. Useful extra fields: `abbr` (badge text, e.g. `{AJPH}`), `abstract`, `doi`, `selected = {true}`, `altmetric = {true}`, `dimensions = {true}`, `pdf` (a file in `assets/pdf/` or a URL), `code`, `slides`. Mark co-first authors by appending `†` to the last name (e.g. `Lee†, Matthew M.`) and add `annotation = {† Co-first authors}`. Then add the entry to the `Publications` list in `_data/cv.yml` so it appears on the CV too.

### CV PDF

`.github/workflows/render-cv.yml` runs [RenderCV](https://rendercv.com) whenever `_data/cv.yml` changes, commits `assets/rendercv/rendercv_output/Matthew_Lee_CV.pdf`, and triggers a redeploy. To use a PDF you design yourself instead, put it in `assets/pdf/`, point `cv_pdf` in `_pages/cv.md` and `_data/socials.yml` at it, and delete the render-cv workflow.

## Previewing locally

Requires Ruby 3.2+ (e.g. `brew install ruby`) and a UTF-8 locale.

```bash
bundle install
LANG=en_US.UTF-8 bundle exec jekyll serve
```

Then open <http://localhost:4000>. Responsive images need ImageMagick (`brew install imagemagick`); without it, set `imagemagick: enabled: false` in a local override config.

## Deploying to GitHub Pages with the mmlee.me domain

1. **Create the repository.** On GitHub, create an empty public repository named `leem26.github.io` (no README, license, or .gitignore).
2. **Push this folder** (it is already a git repository on branch `main`).

   ```bash
   git add .
   git commit -m "Initial al-folio site"
   git remote add origin https://github.com/leem26/leem26.github.io.git
   git push -u origin main
   ```

3. **Allow the workflow to publish.** Repository **Settings → Actions → General → Workflow permissions → Read and write permissions → Save**. If the first "Deploy site" run failed before this was set, re-run it from the **Actions** tab.
4. **Turn on Pages.** Once "Deploy site" succeeds (it creates a `gh-pages` branch), go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, branch **`gh-pages`**, folder **`/ (root)`**.
5. **Set the custom domain.** In **Settings → Pages → Custom domain**, enter `mmlee.me` and save. The `CNAME` file in this repo keeps it set on every deploy.
6. **Point DNS at GitHub.** `mmlee.me` currently uses Netlify DNS (nameservers `dns1–4.p02.nsone.net`) and points at the old Netlify site. In Netlify:
   - Remove `mmlee.me` (and `www.mmlee.me`) from the old site's **Domain management** so Netlify releases the records.
   - In **Domains → mmlee.me → DNS records**, delete any remaining apex/`www` records, then add:

     | Type  | Name  | Value                 |
     | ----- | ----- | --------------------- |
     | A     | @     | `185.199.108.153`     |
     | A     | @     | `185.199.109.153`     |
     | A     | @     | `185.199.110.153`     |
     | A     | @     | `185.199.111.153`     |
     | AAAA  | @     | `2606:50c0:8000::153` |
     | AAAA  | @     | `2606:50c0:8001::153` |
     | AAAA  | @     | `2606:50c0:8002::153` |
     | AAAA  | @     | `2606:50c0:8003::153` |
     | CNAME | www   | `leem26.github.io`    |

   (Alternatively, switch the domain's nameservers back to your registrar and add the same records there.)

7. **Enable HTTPS.** After GitHub's DNS check passes (minutes to a few hours), tick **Enforce HTTPS** in **Settings → Pages**.
8. **Recommended:** verify the domain under your GitHub account's **Settings → Pages → Add a domain** (adds a TXT record) to protect it from takeover.

Every push to `main` rebuilds and redeploys the site in a few minutes.
