---
layout: distill
title: Systems of Cities
description: 
giscus_comments: true
date: 2023-06-01
img: 

authors:

bibliography: zipf_project.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
  - name: Data
  - name: Methods

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fixed-prop-container {
    position: relative;
    padding-bottom: 60%; /* for 16:9 ratio, adjust as needed */
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
# Introduction

Zipf's and Gibrat's law are two of the most famous laws in urban economics.
There is, however, some debate about if and when they hold. 
One of the main issues in this debate, in my view, is the ill definition of the context in which these laws hold: the system of cities.
**What is a system of cities and how can we define it?**
To date, systems of cities have typically been associated to countries. However, the country is a political entity, not an economic one.
Therefore, it is not clear why the country should be the natural unit of analysis for systems of cities.
This project looks at the early days of the US and attempts to establish how many systems of cities were present in the 1800s and when they started forming a single system.
The idea is to use the US as a case study to understand how systems of cities form and how they evolve.

## Data

For the moment, I am using two sources of data. The first is a network database of transportation infrastructure in the US which comprises roads, railways and waterways from 1830 to 1920.
Donaldson and Hornbeck <d-cite key="donaldson2016railroads"></d-cite> provide this data to study the effect of the railways on the US economy. This data contains:
- A complete map of railways, waterways and wagon transport routes between counties.
- An estimate of the transport cost between counties between 1830 and 1920.


For the moment I only use the second part of the data, which is a matrix of transport costs between counties.
I do so out of simplicity rather than some theoretical reason.
The second data source is a [database reporting the population of US cities](https://github.com/cestastanford/historical-us-city-populations) from 1800 to today. 

## Methods

### Network of cities

As first step, I construct a city network, where cities represent nodes and edges are measured by a metric that approximates the "proximity" between two cities. 
The definition of this "proximity" is crucial and I consider three different definitions which capture different aspects of the problem:

 - **Inverse transport distance**: Calculated as $$1/c^T$$, where $$c^T$$ represents the transport cost between two cities. This definition, however, disregards city sizes and is purely geographic.
 - **Radiation proximity**: Based on the flows predicted by the radiation model  <d-cite key="simini2012universal"></d-cite>. **This approach tends to overestimate connections in sparse regions.** The issue is that if there are no cities between two very distant cities, the model with tend to have a high proximity between those two distant cities. In modern times, geography is quite dense so this almost never occurs. But in the 1830s its a problem.
 - **Gravity proximity**: Utilizes the flows predicted by the gravity model. However, **specifying the distance exponent remains an issue.**

### Clustering

After constructing the network of cities, my next step is to identify groups of cities within the network using community detection algorithms. I consider these groups to be "systems of cities". To do this, I've tested a few different algorithms, each one works in a unique way:

1. **Stochastic block model (SBM)**: This algorithm tries to find groups of cities that are likely to form communities based on the structure of the network. It does this by trying to maximize the fit of a stochastic block model to the network graph. What's interesting about this model is that it allows for different types of community structures, not just the typical type where each community is a closely knit group with few connections to the outside. It can also handle structures where there's a central core with peripheral nodes around it. I use the graph tool library to implement the SBM. This library also provides a way to force the model to only find assortative communities (those where nodes are more connected within the community than outside it) using the gt.PPBlockState function. However, this function can't handle weights.

2. **Nested stochastic block model**: This is like the regular SBM, but recursive. It works by first running the SBM on the network, then using the communities found to form a new graph where the nodes are the communities and the edges are weighted by the number of connections between the original communities. This process is then repeated. The graph tool library has an implementation for this as well, but it's not perfect. For example, I can't specify the mean of the distribution from which the edge weights are drawn (it bugs the code) and I can't force it to only detect assortative communities. However, I think it wouldn't be too difficult to create my own version of this algorithm that includes these features.

3. **Louvain**: This is a widely used algorithm for optimizing modularity, a measure of the strength of division of a network into communities. It uses a two-step process that's repeated until it reaches a local optimum for modularity. Initially, each city is its own community. Then, the algorithm repeatedly scans through all the cities to see if they can increase the overall modularity by joining a neighboring community. If so, the city joins the community that provides the biggest boost to modularity. If not, the city stays in its current community. After this, a new graph is created where the communities are the nodes and the edges are weighted by the number of connections between communities. This process then starts again with the new graph.

4. **Label propagation**: This one works by giving each city a unique label and then repeatedly updating the labels based on the most common label among each city's neighbors. Eventually, the labels stop changing and each community is made up of cities with the same label.

5. **Fluid**: This algorithm is similar to label propagation but has some differences. It requires specifying the number of labels in advance and each label has a total "density" of 1. This density is divided among the cities with that label. Larger communities will have lower densities for each city. The labels are then updated based on the label with the highest density among a city's neighbors.

6. **DBSCAN**: This algorithm uses two parameters, epsilon and min(p), to define what a "core point" is. A core point is a city that has at least min(p) cities within epsilon distance. A city is a "periphery point" if it's within epsilon distance of a core point, and an "outlier" if it's neither a core nor a periphery point. Communities are made up of the core and periphery points.

7. **HDBSCAN**: This is an upgraded version of DBSCAN that doesn't require specifying the epsilon parameter. Instead, it intelligently varies this parameter across different communities to detect groups with differing densities. For a more in-depth explanation, the sklearn library documentation is a good resource.

8. **Geographic**: Partition cities by latitude and longitude. For instance, cut the cities in two groups, each on one side of the Rocky Mountains.

**Question:** Which procedure seems most plausible to detect communities in cities?

In order to feed networks to most of these methods (except DBSCAN and HDBSCAN), I need to filter out edges. I have, for the moment, adopted two approaches:
- Maximum spanning tree: keep a maximum spanning tree as well as a percentage of the highest weighted edges.
- Nearest neighbor: keep the k nearest neighbors of each node.

# Results

## Evolution of the transport network

Here are plots of the transport network in different years using the maximum spanning tree method. The most notable feature is that most high weight edges are in the north west. 
The nodes are colored by the community they belong to as explained below. 


## Nested stochastic block model

Here are some results using the Nested stochastic block model algorithm for community detection on the 1890 cities network.
After running the algorithm, we observe the block matrices of communities. These matrices are symmetric and the entry $$i,j$$ represents the number of edges between communities $$i$$ and $$j$$.
<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/block_matrix_nested_sbm_spanning.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

Here we observe that at level 2 the algorithm detects 5 strongly assortative communities. 
On a map these communities can be observed below.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/1890_nested_sbm_map_spanning.pdf' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

On this map, the vertex halo color denotes the level 1 communities, the vertex color denotes the level 2 community and the shape the level three communities.

Here, I repeat the same exercise by using the nearest neighbor instead of the spanning tree method.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/block_matrix_nested_sbm_neighbor.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/1890_nested_sbm_map_neighbor.pdf' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

### Population statistics

Next, we can plot population statistics within these communities. Here are, a plot of Gibrat's and Zipf's law for the level 2 communities at the community level using the spanning tree method.  

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/zipf_1890_1890_nested_sbm.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/growth_rates_1830_1890_nested_sbm.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

## Geographic partition

I also tried to partition the cities in two groups, rockies and non-rockies.

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/geo_map.pdf' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

### Population statistics
<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/zipf_1890_1890_geo.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>

<div class="l-page fixed-prop-container">
  <iframe src="{{ '/assets/zipf_project/growth_rates_1830_1890_geo.html' | relative_url }}" style="border: 1px dashed grey;"></iframe>
</div>


***
