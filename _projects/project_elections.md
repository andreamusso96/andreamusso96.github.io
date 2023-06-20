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
  - name: Plots
  - name: Literature

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fixed-prop-container {
    position: relative;
    padding-bottom: 56.25%; /* for 16:9 ratio, adjust as needed */
    height: 0;
    overflow: hidden;
    }
    .fixed-prop-container iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

---

***
# Data Analysis

## Correlation Between Election Results' Diversity and Mobile Traffic Consumption's Diversity

We explore a captivating question - does a correlation exist between the diversity in election outcomes and the variance in mobile phone data usage?

Focusing on Paris, we delve into the variability of voting preferences during the 2019 European election. This diversity is quantified using the concept of entropy, an effective measure of the divergence in the public's voting decisions (For further information on entropy, see [here](https://en.wikipedia.org/wiki/Entropy_(information_theory))). A higher entropy indicates a more heterogeneous range of voting choices. The interactive map below presents the **entropy of election results** in Paris:

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/vote_entropy_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Upon observation, it appears that Paris' central regions exhibit lower entropy in election results compared to their peripheral counterparts, suggesting a more homogeneous voting pattern in the city center. What about mobile data consumption? Similar to our analysis of election results, we can apply the concept of entropy to mobile traffic consumption, highlighting differences in data usage across the population. The map of Paris below illustrates this:

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/consumption_entropy_map.html' | relative_url }}" frameborder='0' scrolling='yes' height="700px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

Similarly, Paris' central regions display a lower entropy in mobile traffic consumption than the periphery, pointing towards more uniform data usage patterns in these areas. However, the fluctuation in mobile traffic entropy seems less pronounced than that of the election results.

To better understand the relationship between these two parameters, a **correlation plot** is provided:

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/entropy_service_vs_entropy_election.html' | relative_url }}" frameborder='0' scrolling='yes' height="700px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

The correlation seems ambiguous at this point, warranting further examination.


## Facebook Usage and Electoral Polarization

The correlation between social media consumption, specifically Facebook, and political polarization is a well-documented phenomenon. However, to the best of my knowledge, no studies have delved into this association on a granular spatial scale using actual election results.

In the map below, we depict the **electoral polarization** during the 2019 European election in Paris. This polarization is measured as the standard deviation of votes along the political spectrum (right-left axis). The broader the spread of votes along this axis, the higher the polarization.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/polarization_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Interestingly, peripheral regions of Paris seem to exhibit greater polarization than the city center. Essentially, voting patterns in these outlying areas tend to span a wider range along the right-left axis. 

Facebook usage data mirrors this trend. In the following map, we display the proportion of time spent on Facebook relative to total online time. Peripheral regions, as observed, spend a greater fraction of their online time on Facebook compared to central areas.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/fb_share_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Our visual intuition from the maps is backed up by a correlation plot,

 showing a significant association between Facebook usage and electoral polarization. This correlation remains robust even after adjusting for a variety of potential confounding factors, including age, income, education, region's centrality, immigrant population, and unemployment rates. The variables we controlled for include DEC_MED19 (median income), DEC_GI19 (Gini index), P19_POP1529 (population share aged 15-19), P19_ACT_DIPLMIN (share of population without a Bac), P19_ACT_SUP2 (share of population with Bac +2), P19_CHOM1524 (unemployment rate among 15 to 24-year-olds), and P19_POP_ETR (share of population that is non-French). The correlation plot is presented below:

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/fb_share_vs_polarization.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

A striking finding from our analysis is that a 1% increase in the proportion of time spent on Facebook corresponds to an approximately 2% surge in electoral polarization, even when controlling for an array of variables.
***
