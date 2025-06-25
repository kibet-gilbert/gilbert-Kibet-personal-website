# Gilbert Kibet – Personal Genomics & Bioinformatics Website

This document is a complete **step‑by‑step workflow** plus ready‑to‑use **code & content** for building and publishing your academic portfolio website on **GitHub Pages** with **Jekyll** (using the AcademicPages or Al‑Folio template).

---

## 0  Prerequisites

1. **GitHub account** (you already have one).
2. **Git** installed locally (or use GitHub’s web editor).
3. **Ruby ≥ 3 + Bundler** for local preview *(optional)*:

   ```bash
   # macOS (Homebrew example)
   brew install ruby
   gem install bundler
   # ubuntu (example)
   apt install ruby bundler
   ```

   Or use **Docker**:

   ```bash
   docker run --rm -it -p 4000:4000 \
     -v "$PWD":/srv/jekyll jekyll/jekyll:4 jekyll serve --watch --drafts
   ```
4. Decide **URL**:

   * **User‑site** (recommended): `kibet-gilbert.github.io`
     → create / rename repo **exactly** `kibet-gilbert.github.io`.
   * **Project‑site** (current): `kibet-gilbert.github.io/Gilbert-Kibet/`.

---

## 1  Fork & Bootstrap the Template

Pick **one** of these widely‑used academic Jekyll templates:

| Template      | Repo                                                                                                                 | Notes                                                                 |
| ------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| AcademicPages | [https://github.com/academicpages/academicpages.github.io](https://github.com/academicpages/academicpages.github.io) | Research‑oriented, sidebar nav, collections for publications & talks. |
| Al‑Folio      | [https://github.com/alshedivat/al-folio](https://github.com/alshedivat/al-folio)                                     | Minimal, dark‑mode, CV auto‑builder, gallery.                         |

### 1.1  Clone

```bash
# OPTION A: AcademicPages
git clone https://github.com/academicpages/academicpages.github.io.git kibet-gilbert.github.io
# OPTION B: Al‑Folio
# git clone https://github.com/alshedivat/al-folio.git kibet-gilbert.github.io
cd kibet-gilbert.github.io
```

Commit history starts fresh; your future pushes go to your GitHub remote.

---

## 2  Site‑wide Configuration

Edit **\_config.yml** (root).  Here is a ready starter:

```yaml
# _config.yml
# ————————————————————————————
title: "Gilbert Kibet"
description: "Genomics & Bioinformatics Data Scientist"
url: "https://kibet-gilbert.github.io"      # production URL
repository: "kibet-gilbert/kibet-gilbert.github.io"
baseurl: ""                                # leave empty for user‑site

# Author meta
owner:
  name: "Gilbert Kibet"
  email: "gkibet@example.com"   # replace
  avatar: "/assets/img/avatar.jpg"
  bio: "Data‑driven scientist working at ILRI‑Nairobi on pathogen genomics, HPC pipelines & data stewardship."

# Social links (show icons automatically in many themes)
social:
  github: kibet-gilbert
  linkedin: gilbert‑kibet
  orcid: 0000‑0002‑1234‑5678

markdown: kramdown
highlighter: rouge
permalink: /:categories/:title/

# Gems used by AcademicPages / Al‑Folio
plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-sitemap
  - jekyll-scholar        # for publications bib parsing (AcademicPages)
  - jekyll-include-cache

# Build settings
future: true
strict_front_matter: false
```

Add/adjust any template‑specific options (navigation, theme\_color, google\_analytics etc.).

---

## 3  Add Your Content

Below are minimal, copy‑paste‑ready files.  Place them in the indicated folders (create if absent).

### 3.1  About Page → **about.md**

```markdown
---
layout: page
title: About
permalink: /about/
---

# About Me
I am a genomics & bioinformatics data scientist at the **International Livestock Research Institute (ILRI), Nairobi**.  
My work spans pathogen genomics, population genetics and **high‑throughput computational pipelines** on HPC clusters.  I enjoy turning raw sequencing data into actionable biological insight and building reproducible workflows that scale.

## Current Focus
* Wastewater‑based surveillance of antimicrobial resistance.
* HIV‑1 integrase variant discovery using long‑read sequencing.
* Development of open‑source Nextflow pipelines for phylogenomics.

## Skills Snapshot
| Category | Tools |
| --- | --- |
| Languages | Python, R, Bash, Nextflow, Snakemake |
| Genomics | BWA‑MEM, GATK, Nanopore guppy/barcoding, IQ‑TREE |
| Databases | PostgreSQL, MongoDB, FAIR data principles |
| Data Viz | R/ggplot2, Python/Altair, Plotly/Dash |

Outside of research I mentor early‑career scientists in computational reproducibility.
```

### 3.2  Publications → **\_publications/2025-kibet-sarscov2-kenya.md**

```markdown
---
layout: publication
title: "Genomic Epidemiology of SARS‑CoV‑2 Lineages in Kenya, 2020‑2022"
authors: "Kibet G*, Onyango C, et al."
journal: Journal of Virology
year: 2025
url: "https://doi.org/10.1101/2025.01.15.123456"
---
We sequenced 1,200 SARS‑CoV‑2 genomes and reconstructed importation pathways across East Africa…
```

*(Add one Markdown file per paper; templates auto‑list them.)*

### 3.3  Projects → **\_projects/hpc-pipeline.md**

```markdown
---
layout: project
title: "Scalable Metagenomic Pipeline on ILRI HPC"
summary: "A Nextflow + Singularity pipeline processing 500 wastewater samples/day on a 64‑node Slurm cluster."
links:
  github: https://github.com/kibet-gilbert/wastewater-pipeline
  pdf: /assets/pdf/pipeline_poster.pdf
---

![workflow diagram](/assets/img/pipeline_workflow.png)

Key features:
* Modular processes (Prefetch → QC → Assembly → Taxonomy → AMR calling).
* Containerized (BioContainers) for full reproducibility.
* Automatic MultiQC & Slack notifications.
```

### 3.4  Homepage → **index.md**

```markdown
---
layout: home
selected: true
---

> *Transforming sequencing data into insight.*

Welcome! I’m **Gilbert Kibet**, a data‑driven genomics scientist at ILRI‑Nairobi.  Explore my [research](/research/), [publications](/publications/), and [projects](/projects/) or [get in touch](/contact/).
```

### 3.5  Navigation (AcademicPages)

Update **\_data/navigation.yml** (create if absent):

```yaml
- title: Home
  url: /
- title: About
  url: /about/
- title: Research
  url: /research/
- title: Publications
  url: /publications/
- title: Projects
  url: /projects/
- title: CV
  url: /assets/pdf/GKibet_CV.pdf
- title: Contact
  url: /contact/
```

### 3.6  Contact Page → **contact.md**

```markdown
---
layout: page
title: Contact
permalink: /contact/
---

Email: <gkibet@example.com>  
GitHub: <https://github.com/kibet-gilbert>  
LinkedIn: <https://www.linkedin.com/in/gilbert-kibet/>
```

### 3.7  CV PDF

Place your compiled **CV** at `/assets/pdf/GKibet_CV.pdf`.  Link via nav and optionally embed:

```markdown
[Download my full CV](/assets/pdf/GKibet_CV.pdf)
```

---

## 4  Install & Preview Locally (Optional)

```bash
bundle install          # installs gems from Gemfile
bundle exec jekyll serve --livereload
# Preview at http://localhost:4000
```

---

## 5  Commit & Push

```bash
git add .
git commit -m "Initial personal site with bio, pubs, projects"
git remote add origin git@github.com:kibet-gilbert/kibet-gilbert.github.io.git
git push -u origin main
```

---

## 6  Enable GitHub Pages

1. In **Repo → Settings → Pages**:

   * **Source**: branch `main`, folder `/` (or `/docs`).
2. Click **Save** → GitHub builds the site via Actions.
3. Visit `https://kibet-gilbert.github.io` (may take 1‑2 min).

---

## 7  Dark Mode & Styling Tips

* **Al‑Folio** auto‑detects `prefers-color-scheme`; AcademicPages can be tweaked with custom CSS:
  `assets/css/custom.scss` →

  ```scss
  body { --accent: #006d77; }
  ```
* Keep color palette minimal (gray/white + one accent, e.g. ILRI green `#6aa84f`).
* Use SVG icons (DNA helix, database) sparingly.

---

## 8  Publishing Figures & Interactive Content

* Embed static plots (PNG/SVG) in project pages.
* Link out to Jupyter Notebook rendered on nbviewer or jovian.
* For interactive D3/Plotly, place HTML in `/_includes/plot‑xyz.html` and embed with `{% include plot‑xyz.html %}`.

---

## 9  Maintenance Workflow

| Task          | Command                            | Frequency        |
| ------------- | ---------------------------------- | ---------------- |
| Add new paper | `cp _publications/2025-example.md` | When published   |
| Update CV     | Replace PDF                        | Quarterly        |
| Gem updates   | Dependabot PRs                     | Auto             |
| Site preview  | `bundle exec jekyll serve`         | Before each push |

Happy publishing!  Your site will now serve as a central, professional hub for your genomics & data‑science work.

