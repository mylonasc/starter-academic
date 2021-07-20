---
title: "Conditional variational autoencoders for probabilistic wind turbine blade fatigue estimation using Supervisory, Control, and Data Acquisition data"

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
doi: "https://doi.org/10.1002/we.2621"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-02-11T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: In *Wiley, Wind Energy*
publication_short: In *Wind Energy*

abstract: Wind turbine fatigue estimation is based on time-consuming Monte Carlo simulations for various wind conditions, followed by cycle-counting procedures and the application of engineering damage models. The outputs of the fatigue simulations are large in volume and of high dimensionality, as they typically consist of estimates on finite-element computational meshes. The strain and stress tensor time series, which are the primary quantities of interest when considering the problem of fatigue estimation, are dictated by complex vibration characteristics due to the coupled effect of aerodynamics, structural dynamics, geometrically non-linear mechanics, and control. A Variational Auto-Encoder (VAE) is trained in order to model the probability distribution of the accumulated fatigue on the root cross-section of a simulated wind turbine blade. The VAE is conditioned on historical data that correspond to coarse wind-field measurement statistics, such as mean hub-height wind speed, standard deviation of hub-height wind speed and shear exponent. In the absence of direct measurements of structural loads, the proposed technique finds applications in making long-term probabilistic deterioration predictions from historical Supervisory, Control, and Data Acquisition (SCADA) data, while capturing the inherent aleatoric uncertainty due to the incomplete information on strain time series of the wind turbine structure, when only SCADA data statistics are available.

# Summary. An optional shortened abstract.
summary: Using conditional latent variable models for wind farm monitoring data.
tags: ["deep learning", "VAE"]

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://onlinelibrary.wiley.com/doi/full/10.1002/we.2621'
url_code: 'https://github.com/mylonasc/fatigue_cvae'
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

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

#{{% callout note %}}
#Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference management software.
#{{% /callout %}}
#
#{{% callout note %}}
#Create your slides in Markdown - click the *Slides* button to check out the example.
#{{% /callout %}}
#
#Supplementary notes can be added here, including [code, math, and images](https://wowchemy.com/docs/writing-markdown-latex/).
