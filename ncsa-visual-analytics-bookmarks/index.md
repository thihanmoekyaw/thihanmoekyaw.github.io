# NCSA Visual Analytics, Thihan's Bookmarks

## Intro

<strong>What is this?</strong></br>
This page contains the contents of the progresses in GWAS & EWAS researchs in collaboration with the NCSA [Healthcare Innovation Program Office](https://ncsamainsite.web.illinois.edu/research/health-sciences/healthcare-innovation-program-office/) and the [STRONG KIDS 2](https://www.familyresiliency.illinois.edu/strong-kids-2-cells-society-approach-nutrition) study (specifically the parts that I am involved in). I will be using this website to track my progresses. That being said, the files shared within UIUC and NCSA will be shared internally only and will only be shared publicly when all affiliated members agree to make it public.

## Useful links

-  A guide to performing Polygenic Risk Score analyses ([link](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7612115/))
- GWAS lectures from github ([link](https://github.com/timeu/gwas-lecture)) 
-  Plotly Manhattan Plot ([link](https://plotly.com/python/manhattan-plot/))
    - Their [repo](https://github.com/plotly/dash-bio/blob/master/dash_bio/component_factory/_manhattan.py) (the documentation is not that useful as this point so you may have to go here for more info)

## Tasks
-  [ ] Prototype the graph Charles taled about
-  [ ] (optional) make the run gwas function parallizable
-  [ ] Finish reviewing the [GWAS lectures](https://github.com/timeu/gwas-lecture) 
-  [X] Implement Plotly to old graphs (Mahantann Plot)
-  [X] Review Dash Poltly ([link](https://www.youtube.com/watch?v=hSPmj7mK6ng&t=93s))
-  [ ] ~~Reproduce Charles' code in my way~~ 

## Some notes

### March 7th, 2023

- I implemented a mahantann plot in the google colab version using JupyterDash and Dash Bio

- The first thing I did was to implement the notebook in the NCSA server with a JupyterLab docker container. I excrected the necessary data and reduce the data to the bare minimum requirement to plot it using dash_bio package.
  - Side note: I also did a pull request to improve the documentation (it was very incomplete at the time I am writing right now)

- After things became reliable, I port it make the notebook to work in Google Colab. Our notebook is meant for researchers with a few python experience to be able to use the state-of-the-art tools in GWAS studies (and thus, making it reliable in Google Colab). Currently, these are the main things I have implemented so far for the mahanttan plot:
  - [Bonferroni Correction](https://en.wikipedia.org/wiki/Bonferroni_correction): a method of adjusting the p-value threshold for statistical significance when conducting multiple hypothesis tests
  - [Benjamini-Hochberg Procedure](https://www.statology.org/benjamini-hochberg-procedure/): a multiple testing correction method used to control the False Discovery Rate (FDR) in statistical hypothesis testing.

- After porting, I did a lot of testing to predict how long the graphing function is going to take. Here are some steps I've taken:
  - Gathered data of the runtime of the mahantann plot to display (I put it in a dict)

  - I graph the runtime relative to the number of rows in the data. I found out that the graph function run in a linear time.

  - I performed linear regressions to predict how long it takes in order to be able to make the plot in 25 seconds

### March 1st, 2023

- It is more preferable to make jupyter notebook into a runnable dashboard. Chromosome is AI, start value is AJ (position on the chromosome), significant at the snip (colunmn I, this is -log_10 p vlaue)

- Our plan is to change things to plotly first, and then use jupyterDash to make it interactive if needed.

### Feb 28th, 2023

- Plotly released a version of dashboarding library in jupyter notebook called [JupyterDash](https://medium.com/plotly/introducing-jupyterdash-811f1f57c02e)

  - One thing about plotly dash is that it is also available for dashboarding on R and Julia (bioinformatics not available)

{{<typeit>}}
<strong>If you are not Thihan and looking at this page, you are probably one of my supervisors in NCSA!</strong> </br>
Hello Charles or Colleen, and thank you for checking my page! :heart: </br>
<p style="font-size: 8px">... or maybe I just bullied you into checking my website hehe :sweat_smile: </p>
{{</typeit>}}
