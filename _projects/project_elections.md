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
  - name: Theodore Tallent
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
    padding-bottom: 70%; /* for 16:9 ratio, adjust as needed */
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

## Social Media Usage and Electoral Polarization

### Data Aggregation and Preparation

Our data sets include mobile traffic data provided at the tile level (100x100 meter tiles) and electoral data available at the polling station level. Considering the prevalence of polling stations, most locations have a station within 300 meters. To facilitate a harmonized analysis, we aggregated both data sets at the iris level.

Mobile traffic data was attributed to the iris intersecting the most with each 100x100 meter tile. For electoral data, we took the centroid of each iris and performed a recursive search. We initially focused on all polling stations within a 300-meter radius of the centroid, averaging their results and attribiting them to the iris. If an iris did not have polling stations within this initial radius, the radius was increased to 600 meters and the process repeated.

Here is a map, at the iris level, of the diversity of voting preferences for the european election (measured by entropy). 

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/entropy_elections_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Upon observation, it appears that Paris' central regions exhibit less diverssity in voting preferences compared to their peripheral counterparts, suggesting a more homogeneous voting pattern in the city center.

### Polarization of Electoral Results

The first step in our analysis was to calculate the polarization of the electoral results for each iris. Each party was assigned a number between -1 and 1, representing its position on the left-right axis. Then, we computed the average position in an iris: this is the weighted average of party positions, with the weighting based on the number of votes each party received. Finally, polarization is defined as the average distance of a vote from the average position of the iris. The larger this average distance, the more the iris is polarized because people vote farther away from the average (and so more extreme).

### Mobile Traffic Data and Polarization
In the next phase of our research, we turned our attention towards mobile traffic data. Our focus was on analyzing the traffic between 7pm and midnight on weekdays, deliberately excluding holidays and anomaly days. This selective approach was taken to minimize the impact of confounding factors on our data.

Our primary metric for assessing the "consumption" of a specific mobile service was its share of the total traffic within an iris. The rationale behind this choice lies in the differing market penetration rates of telecom operators like Orange across various irises.

Absolute usage data can potentially skew results due to variations in the operator's market presence across different irises. In contrast, comparing the proportional share of a given service in total traffic neutralizes this potential source of bias, making this a more robust measure for our analysis.

### Results

First we plot the correlation of turnout, vote diversity (measured be entropy), polarization and party affiliation with shares of mobile service usage for some of the main mobile services:
<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/entropy_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/turnout_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/polarization_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/renaissance_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/la_france_insoumise_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/prenez_le_pouvoir_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/europe_ecologie_correlation.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

What do we find?

### More Details on Facebook Usage and Electoral Polarization

We explore in greater detail the relationship between Facebook usage and electoral polarization in Paris.

In the map below, we depict the **electoral polarization** during the 2019 European election in Paris.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/polarization_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Interestingly, peripheral regions of Paris seem to exhibit greater polarization than the city center. Essentially, voting patterns in these outlying areas tend to span a wider range along the right-left axis. 

Facebook's usage data mirrors this trend. In the following map, we display the proportion of time spent on Facebook relative to total online time. Peripheral regions spend a greater fraction of their online time on Facebook compared to central areas.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/fb_share_map.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Our visual intuition from the maps is backed up by a correlation plot, showing a significant association between Facebook usage and electoral polarization. This correlation remains robust even after adjusting for a variety of potential confounding factors, including age, income, education, region's centrality, immigrant population, and unemployment rates. The variables we controlled for include DEC_MED19 (median income), DEC_GI19 (Gini index), P19_POP1529 (population share aged 15-19), P19_ACT_DIPLMIN (share of population without a Bac), P19_ACT_SUP2 (share of population with Bac +2), P19_CHOM1524 (unemployment rate among 15 to 24-year-olds), and P19_POP_ETR (share of population that is non-French). The correlation plot is presented below:

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/election_project/fb_share_vs_polarization.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

***
