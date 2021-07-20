---
title: "Deep unsupervised learning for condition monitoring and prediction of high dimensional data with application on windfarm SCADA data"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- admin
- Imad Abdallah
- Eleni Chatzi

# Author notes (optional)
# author_notes:
# - "Equal contribution"
# - "Equal contribution"

date: "2019-02-01T00:00:00Z"
doi: "https://doi.org/10.3929/ethz-b-000315814"

# Schedule page publish date (NOT publication's date).
publishDate: "2019-01-28T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *Proceedings of the 37th IMAC, A Conference and Exposition on Structural Dynamics 2019*
publication_short: In *IMAC*

abstract: In this work we are addressing the problem of statistical modeling of the joint distribution of data collected from wind turbines interacting due to collective effect of their placement in a wind-farm, the wind characteristics (speed/orientation) and the turbine control. Operating wind turbines extract energy from the wind and at the same time produce wakes on the down-wind turbines in a park, causing reduced power production and increased vibrations, potentially contributing in a detrimental manner to fatigue life. This work presents a Variational Auto-Encoder (VAE) Neural Network architecture capable of mapping the high dimensional correlated stochastic variables over the wind-farm, such as power production and wind speed, to a parametric probability distribution of much lower dimensionality. We demonstrate how a trained VAE can be used in order to quantify levels of statistical deviation on condition monitoring data. Moreover, we demonstrate how the VAE can be used for pretraining an inference model, capable of predicting the power production of the farm together with bounds on the uncertainty of the predictions. Examples employing simulated wind-farm Supervisory Control And Data Acquisition (SCADA) data are presented. The simulated farm data are acquired from a Dynamic Wake Meandering (DWM) simulation of a small wind farm comprised of nine 5MW turbines in close spacing using OpenFAST

# Summary. An optional shortened abstract.
summary: Using conditional latent variable models for wind farm monitoring data.
tags: ["Deep Learning", "VAE","GNN", "Variational Bayes"]

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://www.research-collection.ethz.ch/bitstream/handle/20.500.11850/315814/4586_myl.pdf?sequence=1&isAllowed=y'
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- WINDMIL 

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: example
---

