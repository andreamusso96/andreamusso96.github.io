---
layout: distill
title: Phone traffic and french elections
description: Some correlation plots between mobile phone traffic in the major french cities and french election results
giscus_comments: true
date: 2023-06-01
img: /assets/election_project/french_election.jpeg

authors:
  - name: Andrea Musso
    affiliations:
      name: ETH Zurich
  - name: Gianluca Risi
    affiliations:
      name: Politecnico di Milano
  - name: Theodore Taillent
    affiliations:
      name: Sciences Po Paris

bibliography: 2018-12-22-distill.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Definitions
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Plots
  - name: Literature

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

## Definitions

Let $p$ be the probability distribution of votes in an election in a given location.
That is, $$p_i$$ is the probability that a randomly chosen voter in the location votes for party $$i$$.
The entropy ofthe distribution $p$ is defined as

$$
H(p) = - \sum_{i=1}^n p_i \log p_i
$$

where $$n$$ is the number of parties in the election. It is a measure of how diverse the votes in the location are.
The more diverse the votes, the higher the entropy. See [this](https://en.wikipedia.org/wiki/Entropy_(information_theory)) for more details.

***

# Plots

## Entropy of election results vs entropy of mobile phone traffic consumption

For the city of Paris, we plot the entropy of election results in the 2019 european election and the entropy of mobile traffic consumption for every iris (smallest unit at which the French government published local information).

Here is an interactive map of the **entropy of election results**:

<div class="l-page">
  <iframe src="{{ '/assets/election_project/vote_entropy_map.html' | relative_url }}" frameborder='0' scrolling='yes' height="700px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

What do we observe? It looks like central regions of Paris have a lower entropy of election results than the periphery. 
That is, people in central regions vote more similarly than people in the periphery. What about mobile traffic consumption?

Here is an interactive map of the **entropy of mobile traffic consumption**:

<div class="l-page">
  <iframe src="{{ '/assets/election_project/consumption_entropy_map.html' | relative_url }}" frameborder='0' scrolling='yes' height="700px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

It looks like central regions of Paris have a lower entropy of mobile traffic consumption than the periphery.
That is, people in central regions consume mobile traffic more similarly than people in the periphery.
However, there is much less variation in the entropy of mobile traffic consumption than in the entropy of election results.

We can plot the two quantities against each other in a **correlation plot**:

<div class="l-page">
  <iframe src="{{ '/assets/election_project/entropy_service_vs_entropy_election.html' | relative_url }}" frameborder='0' scrolling='yes' height="700px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

***
