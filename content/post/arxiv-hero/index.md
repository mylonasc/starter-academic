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

With the flood of great papers and ideas appearing every day it is difficult to stay up-to-date with the latest research in ML.

In particular for the ones that are not full time researchers (like me), but would like to keep track of what is going on in the ML research world, it is valuable to get a specialized digest of papers on topics they are interested.

The different ML digest newsletters that one can subscribe to are obviously going to be slightly "biased" to what the editors find interesting. Also, simply searching 
and filtering the latest papers is time-consuming, and perhaps slightly tedious because one needs to read through a lot of papers before finding the ones that are interesting. To make things worse, abstracts are often slightly "pompous", trying hard to market for the paper, and it makes it hard to clearly extract the actual claimed contributions of a paper quickly and are worth a closer read. 

With that in mind, I set out to create a summarizer for my daily personalized "ML News". I wanted the system, given a query and a summarization prompt, to perform
1. Topic ranking:
   * Perform topic modeling for abstracts of the latest papers in arxiv. 
   * Find the topics that are interesting to me (e.g., LLMs, GNNs, Neural Network Efficiency, Knowledge graphs)
   * Keep the top-K (~20-30 papers) that are somehow connected to these topics
2. Query similarity re-ranking 
   * Compute the similarity with these papers and the provided query (the query can also only have topics) and return only the top-10 most similar papers.
3. Summarization:
   * Use an LLM to summarize the abstracts **while maintaining the prescribed topics focus**.
   * Use an LLM to create a digest for all the summarized abstracts.
4. Auto-deploy:
   * Publish an HTML webpage daily containing the digest and the abstract summaries.

Although PaaS LLMs like ChatGPT can be used in every step of this process, I decided to use some classical techniques for extracting topics and the first ranking of the papers. 
Also, the embeddings (used for the prompt relevance re-ranking) are computed locally to save some more costs.

# Code
See more in the corresponding [github repo](https://github.com/mylonasc/arxiv_llm_assistant)

You can find my minimalistic list of published digests [here](https://mylonasc.github.io/arxiv_llm_assistant/).
