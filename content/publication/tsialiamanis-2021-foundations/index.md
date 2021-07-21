---
title: "Foundations of population-based SHM, Part IV: The geometry of spaces of structures and their feature spaces" 

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- George Tsialiamanis
- admin
- Eleni Chatzi
- Nicolaos Dervilis
- David Wagg
- Keith Worden

# Author notes (optional)
author_notes:
 - "GT Implemeted the idea, wrote the first draft, made connections to topology of feature spaces corresponding to structures"
 - "We came up together with GT with the attributed graph idea, proposed some fixes for the dataset construction and algorithm implementation."

date: "2021-01-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2019-01-28T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
#publication: GNNs for defining a space of structures
#publication_short: GNNs for structures

abstract: One of the requirements of the population-based approach to Structural Health Monitoring (SHM) proposed in the earlier papers in this sequence, is that structures be represented by points in an abstract space. Furthermore, these spaces should be metric spaces in a loose sense; i.e. there should be some measure of distance applicable to pairs of points; similar structures should then be ‘close’ in the metric. However, this geometrical construction is not enough for the framing of problems in data-based SHM, as it leaves undefined the notion of feature spaces. Interpreting the feature values on a structure-by-structure basis as a type of field over the space of structures, it seems sensible to borrow an idea from modern theoretical physics, and define feature assignments as sections in a vector bundle over the structure space. With this idea in place, one can interpret the effect of environmental and operational variations as gauge degrees of freedom, as in modern gauge field theories. One can then regard data normalisation procedures like cointegration as gauge-fixing operations. This paper will discuss the various geometrical structures required for an abstract theory of feature spaces in SHM, and will draw analogies with how these structures have shown their power in modern physics. Having motivated a number of problems in Population-Based SHM (PBSHM) in geometrical terms, it remains to show how these problems might be solved. In the second part of the paper, the problem of determining the normal condition cross section of a feature bundle is addressed. The solution is provided by the application of Graph Neural Networks (GNN), a versatile non-Euclidean machine learning algorithm which is not restricted to inputs and outputs from vector spaces. In particular, the algorithm is well suited to operating directly on the sort of graph structures which are an important part of the proposed framework for PBSHM. The solution of the normal section problem is demonstrated for a heterogeneous population of truss structures for which the feature of interest is the first natural frequency. The GNN approach is shown to not only solve the normal section problem, but also to accommodate varying temperatures across the population; it thus provides a means of data normalisation.

# Summary. An optional shortened abstract.
summary: GNNs for automated embedding of structural systems to a feature space.
tags: ["GNNs", "Machine learning" ,"Structural"]

# Display this page in the Featured widget?
featured: false 

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://www.sciencedirect.com/science/article/abs/pii/S088832702100087X'
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
