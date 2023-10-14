---
title: ArxivHero - A hyper-specialized daily arxiv paper digest creation.
date: 2023-10-14
math: true
diagram: true
highlight: true
image:
  placement: 3
  caption: ''
---


{{< toc >}} 

# Specialized LLM summarizer

With the flood of great papers and ideas coming up every day it is particularly difficult to stay up to date with current research.

In particular for the ones that are not full time researchers, but would like to stay up to speed with research, it is valuable to get a specialized digest of papers on topics they are interested.

The different ML digest newsletters that one can subscribe to are expected to be slightly "biased" to what the editors find interesting. Also, simply searching 
and filtering the latest papers is time-consuming, and perhaps slightly tedious because one needs to read through a lot of papers one finds out of their core interests, to finally reach the core of the good ones. Moreover, abstracts are sometimes slightly "pompous", trying hard to market for the paper, and it makes it hard to read through the to the contributions of each paper and see if the developed methodologies are in any way worth devoting some time to understand. 

With that in mind, I set out to create a summarizer for my daily personalized "ML News". I wanted the system, given a query and a summarization prompt, to 
1. Topic ranking:
   * Perform topic modeling for abstracts of the latest papers in arxiv. 
   * Find the topics that are interesting to me (e.g., LLMs, GNNs, Neural Network Efficiency, Knowledge graphs)
   * Keep the top-K (~20-30 papers) that are somehow connected to these topics
2. Query similarity re-ranking 
   * Compute the similarity with these papers and the provided query (the query can also only have topics) and return only the top-10 most similar papers.
3. Summarization:
   * Use an LLM to summarize the abstracts **with a particular focus**.
   * Use an LLM to create a digest for all the summarized abstracts.
4. Auto-deploy:
   * Publish an HTML webpage daily containing the digest and the abstract summaries.

Although PaaS LLMs like ChatGPT can be used in every step of this process, I decided to use some classical techniques for extracting topics and the first ranking of the papers. 
Also, the embeddings (used for the prompt relevance re-ranking) are computed locally to save some more costs.

# Code
See more in the corresponding [github repo](https://github.com/mylonasc/arxiv_llm_assistant)

