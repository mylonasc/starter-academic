---
title: "Bayesian graph networks for strain-based crack localization"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- admin
- George Tsialiamanis
- Keith Worden
- Eleni Chatzi

# Author notes (optional)
# author_notes:
# - "Equal contribution"
# - "Equal contribution"

date: "2020-12-08T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2019-01-28T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: IMAC 2021
publication_short:

abstract: A common shortcoming of vibration-based damage localization techniques is that localized damages, i.e. small cracks, have a limited influence on the spectral characteristics of a structure. In contrast, even the smallest of defects, under particular loading conditions, cause localized strain concentrations with predictable spatial configuration. However, the effect of a small defect on strain decays quickly with distance from the defect, making strain-based localization rather challenging. In this work, an attempt is made to approximate, in a fully data-driven manner, the posterior distribution of a crack location, given arbitrary dynamic strain measurements at arbitrary discrete locations on a structure. The proposed technique leverages Graph Neural Networks (GNNs) and recent developments in scalable learning for Bayesian neural networks. The technique is demonstrated on the problem of inferring the position of an unknown crack via patterns of dynamic strain field measurements at discrete locations. The dataset consists of simulations of a hollow tube under random time-dependent excitations with randomly sampled crack geometry and orientation.

# Summary. An optional shortened abstract.
summary: Implemented Graph Networks with weight uncertainty for crack localization while using arbitrarily positioned strain sensors with good results.

tags: ["deep learning", "weight uncertainty", "GNN"]

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://arxiv.org/abs/2021.06791'
url_code: ''
url_slides: 'https://docs.google.com/presentation/d/1XP6iinfQwWuLhSZpDPLclxkbAdx0S2RhunNINhXvHKg/edit?usp=sharing'
url_source: ''
url_video: 'https://www.youtube.com/watch?v=_2UqsidmosY'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: ''
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: example
---

