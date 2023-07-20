# NCSA Visual Analytics, Thihan

## Intro

<strong>What is this?</strong></br>
This page contains the contents of the progresses in GWAS & EWAS researches in collaboration with the NCSA [Healthcare Innovation Program Office](https://ncsamainsite.web.illinois.edu/research/health-sciences/healthcare-innovation-program-office/) and the [STRONG KIDS 2](https://www.familyresiliency.illinois.edu/strong-kids-2-cells-society-approach-nutrition) study (specifically the parts that I am involved in). I will be using this website to track my progresses. That being said, the files shared within UIUC and NCSA will be shared internally only and will only be shared publicly when all affiliated members agree to make it public.

### What is project about?

Primarily, the direction that I went into this project is about improving data visualization in GWAS and EWAS study, especially in how to make the manhattan plot to be more interactive and easy for the research scientist to use. The aim of the project is to use the state-of-the-art packages available in open-source community and adding features in the source code. A traditional researcher in biology focus on the research and analysis and need to train themselves in coding to use state-of-the-art tools or get help from more knowledgeable research engineers. For this project, we aim to develop data visualizations based in google colab for dashboards.

#### Why Google Colab?

The packages we used are python based and we wanted a tool that we can share the researchers easy to use everywhere without the need to computational resources, while being very easy for minimal for the researchers to use. Because google colab offer free compute for everyone (at least at the time of writing), we decided to develop our dashboard to optimize with google colab.

## Useful links

-  A guide to performing Polygenic Risk Score analyses ([link](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7612115/))
- GWAS lectures from github ([link](https://github.com/timeu/gwas-lecture)) 
-  Plotly Manhattan Plot ([link](https://plotly.com/python/manhattan-plot/))
    - Their [repo](https://github.com/plotly/dash-bio/blob/master/dash_bio/component_factory/_manhattan.py) (the documentation is not that useful as this point so you may have to go here for more info)

## Tasks

-  [ ] (optional) make the run gwas function parallelizable
-  [X] Prototype the graph Charles talked about
-  [X] Implement Plotly to old graphs (Manhattan Plot)
-  [X] Review Dash Poltly ([link](https://www.youtube.com/watch?v=hSPmj7mK6ng&t=93s))
-  [ ] ~~Reproduce Charles' code in my way~~ 

## Progress notes

### April 11th, 2024

#### Update: Demo Manhattan Plot

As part of the NCSA Student Research Conference, we made a prototype with a easy interface in google colab for researcher to test and evaluate.

#### Changes Made

1. Under supervision of Charles Blatti, the "IN_PATHWAY" parameter is changed to kegg annotation information, where the data is taken form the "kegg_annotation.txt" in the data cleaning function and merging with the processed dataframe. 
2. There is a bug in the annotations of the `NCSA_ManhattanPlot` function and fixed it (took a while but FINALLYYYYY)
3. Added radio buttons for the user to use either used the `Benjamini_Hochberg_val` function or to use the slider for the red line in the vizualization.
4. Added a dropdown menu where user can select the gene pathway they want to display. The user can select multiple.
5. For now, as a demonstration purpose, I changed the code so that the datafiles do not need authentication when runned on colab.

#### Next Steps

I will be preparing for the NCSA conference. After the conference, I will add more features such as ability to insert user's own gwas data. With Fatma's feedback (researcher for the GWAS study for the Strong Kids 2 study), I will make the visualization display orange dots even above the threshold line (the red line in the plot) if it is in the gene pathway.

### April 3th, 2023

#### Update: Manhattan Plot with Gene Pathway Highlighting

#### Description

We have made progress in adding a new feature to the existing Manhattan Plot implementation using the `dash_bio` package. The new feature allows the visualization of a specific gene pathway by highlighting the corresponding data points with a distinct color (green).

#### Changes Made

1. Modified the `NCSA_ManhattanPlot` function and the `_ManhattanPlot` class to accept an optional "IN_PATHWAY" parameter, which is a boolean column indicating whether a data point is part of the gene pathway of interest.  `NCSA_ManhattanPlot` is the modified version of the `ManhattanPlot` source code from dash_bio python library. 

2. Updated the figure generation code to adjust the color of the data points based on the "IN_PATHWAY" column values.

3. Provided a method to process the existing "UCSC_REFGENE_GROUP" column in the input pandas dataframe, creating a new "IN_PATHWAY" column that can be used with the modified `NCSA_ManhattanPlot` function.

#### Usage

To use the updated Manhattan Plot with gene pathway highlighting:

1. Process the input dataframe to create a new "IN_PATHWAY" boolean column based on the "UCSC_REFGENE_GROUP" column and the pathway keyword of interest (e.g., "Body").

```python
pathway_keyword = "Body"
df["IN_PATHWAY"] = df["UCSC_REFGENE_GROUP"].apply(lambda x: pathway_keyword in str(x))
```

2. Pass the modified dataframe with the "IN_PATHWAY" column to the `NCSA_ManhattanPlot` function.

```python
fig = NCSA_ManhattanPlot(df, in_pathway="IN_PATHWAY")
```

This will generate a Manhattan Plot with data points in the specified gene pathway highlighted in green.

#### Next Steps

The team can now use the updated Manhattan Plot implementation to visualize specific gene pathways in their data. If needed, further customization or additional features can be added to the existing code.

### March 7th, 2023

- I implemented a Manhattan plot in the Google Colab version using JupyterDash and Dash Bio.

- The first thing I did was to implement the notebook in the NCSA server with a JupyterLab Docker container. I extracted the necessary data and reduced the data to the bare minimum requirements to plot it using the dash_bio package.
  - Side note: I also made a pull request to improve the documentation (it was very incomplete at the time of writing this).

- After making things reliable, I ported the notebook to work in Google Colab. Our notebook is meant for researchers with some Python experience to use state-of-the-art tools in GWAS studies, making it reliable in Google Colab. Currently, these are the main things I have implemented so far for the Manhattan plot:
  - [Bonferroni Correction](https://en.wikipedia.org/wiki/Bonferroni_correction): a method of adjusting the p-value threshold for statistical significance when conducting multiple hypothesis tests
  - [Benjamini-Hochberg Procedure](https://www.statology.org/benjamini-hochberg-procedure/): a multiple testing correction method used to control the False Discovery Rate (FDR) in statistical hypothesis testing.

- After porting, I did a lot of testing to predict how long the graphing function is going to take. Here are some steps I've taken:
  - Gathered data on the runtime of the Manhattan plot to display (I put it in a dictionary).

  - I graphed the runtime relative to the number of rows in the data. I found out that the graph function runs in linear time.

  - I performed linear regressions to predict how long it takes to make the plot in 25 seconds.

## Some notes

### Match 8th, 2023

- why raw p-value and not FDR corrected p-value?
  - wait, it is the same as Benjamin Hochberg or no?
  - It is a good idea to remove the teeny tiny genes in the analysis
  - Biomarkers?
  - The meeting said about focusing on particular sites. 
  - Maybe we get the extra chromosome function into the thingy

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
