# Personal Site Redesign Design

## Goal

Reposition the site from an academic homepage to an industry-facing personal data profile. The site should still preserve research credibility, but the homepage should present Andrea as a data-oriented profile working with cities, networks, large-scale datasets, and economic complexity rather than as a current PhD student.

## Current Site Context

The repository is an al-folio Jekyll site. The main editable surfaces are:

- `_pages/about.md` for the homepage content and profile image.
- `_pages/publications.md` and `_bibliography/papers.bib` for research publications.
- `blog/index.html` for the current blog index.
- `_projects/*.md` for existing scrollytelling-style internal pieces.
- `_news/*.md` for homepage news.
- `_data/cv.yml` and `assets/pdf/CVAndreaMusso.pdf` for CV content.
- `_includes/scripts/mathjax.html` for the `polyfill.io` script that triggers a browser sign-in prompt.

## Information Architecture

The top navigation should read:

- `about`
- `research`
- `blog`
- `cv`

Research and blog content must stay separate:

- `research` is for peer-reviewed papers and research outputs.
- `blog` is a curated list of public-facing scrollytellies and articles, not a chronological Jekyll blog.

The visible research page should live at `/research/`. Existing links to `/publications/` should not break; keep a lightweight redirect or compatibility page if the current page is moved.

## Homepage

The homepage should:

- Use the uploaded LinkedIn-style profile photo.
- Replace the current academic bio with a slightly longer industry-facing bio.
- State that Andrea completed his PhD at ETH Zurich under Dirk Helbing.
- Mention the broad profile: large-scale data, cities, networks, economic complexity, and computational social science.
- Avoid a separate `research` heading on the about page.
- Keep news and selected publications as supporting credibility sections.

The tone should be direct, warm, and useful for an industry-facing data profile.

## News

Add or update news items for:

- Research stay at Harvard Growth Lab, January-March 2024.
- Research stay / junior fellowship at Complexity Science Hub Vienna, March-September 2024.
- PhD graduation at ETH Zurich on May 13, 2026, supervised by Dirk Helbing, with committee members Ulrik Brandes and Marta Gonzalez.
- Publication of the PNAS paper `Large cities lose their growth advantage as countries urbanize`, linked to `https://www.pnas.org/doi/10.1073/pnas.2529430123`.

Use concrete dates where available and month ranges otherwise.

## Research Page

The research page should:

- Be visible as `research` in the navigation.
- List Andrea's actual papers only, removing sample al-folio/Einstein bibliography entries.
- Include paper preview images where available.
- Include the new PNAS paper:
  - Title: `Large cities lose their growth advantage as countries urbanize`
  - Authors: Andrea Musso, Diego Rybski, Dirk Helbing, Frank Neffke
  - DOI/link: `10.1073/pnas.2529430123`
- Keep existing actual research entries:
  - `How networks shape diversity for better or worse`
  - `Equidistribution of rational subspaces and their shapes`
- Group papers by year if the current bibliography rendering supports it cleanly.

## Blog Page

The blog page should become a curated writing/scrollytelling list rather than a chronological post archive.

Initial entries:

- `megacities.ch`, described as the scrollytelling companion to the new PNAS paper.
- Existing internal scrollytelling/project pages that are public-facing can be listed as additional entries, while keeping research outputs on the research page.

The page should not surface al-folio example blog posts.

## CV

Update the structured CV data to reflect:

- PhD in Computational Social Science, ETH Zurich, completed in 2026.
- Dissertation supervision by Dirk Helbing.
- Committee members Ulrik Brandes and Marta Gonzalez.
- Harvard Growth Lab research stay, January-March 2024.
- Complexity Science Hub Vienna research stay / junior fellowship, March-September 2024.

If a newer PDF CV is not provided, keep the existing PDF asset but make the site-rendered CV accurate.

## Polyfill Fix

Remove the remote `https://polyfill.io/v3/polyfill.min.js?features=es6` script from MathJax loading. MathJax 3 should not require this polyfill for the site's target browsers, and removing it should stop the browser sign-in prompt.

## Verification

After implementation:

- Build the Jekyll site locally.
- Confirm the generated pages for `/`, `/research/`, `/publications/`, `/blog/`, and `/cv/` render without build errors.
- Search the built site for `polyfill.io` and confirm it is gone.
- Check the homepage and navigation in a browser-sized viewport if a local server is available.
