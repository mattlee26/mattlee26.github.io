# Agent Guidelines for mmlee.me

This is Matthew M. Lee's personal site, created from the [al-folio](https://github.com/alshedivat/al-folio) v1.x starter. Layouts, includes, Sass, and feature code live in the pinned `al-*` gems (see `Gemfile`); edit content and config here, and read `README.md` for where each kind of content lives.

- `baseurl` is empty and `url` is `https://mmlee.me` (custom domain via `CNAME`). Do not set a baseurl.
- `Gemfile` and the `plugins:` list in `_config.yml` must agree; a plugin in only one of them is silently inert.
- `_data/cv.yml` must stay valid [RenderCV](https://docs.rendercv.com) input: extra keys are allowed inside entries, but not at the top level of `cv:`. Validate with `rendercv render _data/cv.yml --settings assets/rendercv/settings.yaml`.
- MathJax is off (`enable_math: false`) because abstracts contain dollar amounts.
- Build with `LANG=en_US.UTF-8 bundle exec jekyll build`; without a UTF-8 locale the theme's file scan fails on non-ASCII characters.
- Local overrides of gem-owned layouts/includes are allowed for this site, but keep them minimal and run `bundle exec al-folio upgrade overrides audit` after adding one.
- Upstream reference docs are in `docs/` (from the al-folio template).
