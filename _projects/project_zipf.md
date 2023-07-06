---
layout: distill
title: Systems of Cities
description: When and where does Zipf's law hold?
giscus_comments: true
date: 2023-06-01
img: /assets/election_project/french_election.jpeg

authors:

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
    <embed src="/assets/zipf_project/geo.pdf" type="application/pdf"/>
</div>

***
