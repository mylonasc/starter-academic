---
title: "Structural identification with physics-informed neural ordinary differential equations"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- Zhilu Lai
- admin
- Satish Nagarajaia
- Eleni Chatzi

# Author notes (optional)
 author_notes:
 - "Implementation"
 - "Contributed the initial idea, and review"

date: "2021-01-01T00:00:00Z"
doi: "https://doi.org/10.1016/j.jsv.2021.116196"

# Schedule page publish date (NOT publication's date).
publishDate: "2019-01-28T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: NeuralODEs for system ID
publication_short: NeuralODEs application

abstract: This paper exploits a new direction of structural identification by means of Neural Ordinary Differential Equations (Neural ODEs), particularly constrained by domain knowledge, such as structural dynamics, thus forming Physics-informed Neural ODEs, aiming at governing equations discovery/approximation. Structural identification problems often entail complex setups featuring high-dimensionality, or stiff ODEs, which pose difficulties in the training and learning of conventional data-driven algorithms who seek to unveil the governing dynamics of a system of interest. In this work, Neural ODEs are re-casted as a two-level representation involving a physics-informed term, that stems from possible prior knowledge of a dynamical system, and a discrepancy term, captured by means of a feed-forward neural network. The re-casted format is highly adaptive and flexible to structural monitoring problems, such as linear/nonlinear structural identification, model updating, structural damage detection, driving force identification, etc. As an added step, for inferring an explainable model, we propose the adoption of sparse identification of nonlinear dynamical systems as an additional tool to distill closed-form expressions for the trained nets, that embed a more straightforward engineering interpretation. We demonstrate the framework on a series of numerical and experimental examples, with the latter pertaining to a structural system featuring highly nonlinear behavior, which is successfully learned by the proposed framework. The proposed structural identification with Physics-informed Neural ODEs comes with the benefits of direct approximation of the governing dynamics, and a versatile and flexible framework for discrepancy modeling in structural identification problems.


# Summary. An optional shortened abstract.
summary: Using NeuralODEs to deal with non-linear discrepancies in system identification.
tags: ["Deep Learning", "NeuralODEs","System Identification"]

# Display this page in the Featured widget?
featured: false 

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://www.research-collection.ethz.ch/handle/20.500.11850/488395'
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
  caption: ''
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
