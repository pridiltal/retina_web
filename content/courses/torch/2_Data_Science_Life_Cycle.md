---
date: "2021-03-30T00:00:00+01:00"
draft: false
linktitle: Data Science Life Cycle
menu:
  example:
    parent: TORCH 
    weight: 2
title: Data Science Life Cycle
toc: true
type: docs
weight: 2
---

### The OSEMN framework

![Data Science Process (a.k.a the O.S.E.M.N. framework)](/courses/torch/1_OSEMN.png)
Figure 1: Data Science Process (a.k.a the O.S.E.M.N. framework <br/>
Image source: https://towardsdatascience.com/5-steps-of-a-data-science-project-lifecycle-26c50372b492

-  The [OSEMN framework](https://towardsdatascience.com/5-steps-of-a-data-science-project-lifecycle-26c50372b492) is comprised of 5 major steps that help us to focus and prioritize the right data science tasks at different stages:   
  1. **O**btaining Data
  2. **S**crubbing Data
  3. **E**xploring Data
  4. **M**odelling Data 
  
  - Model parameter estimation
  - Hyper-parameter tuning
   
    - *Hyperparameters* are the parameters that define the model architecture.
    - Hyperparameters are external to the model and cannot be estimated from data.
    - *Hyperparameter optimization or tuning* is the process of searching for the ideal model architecture (a set of optimal hyperparameters).
    
![Model Data](/courses/torch/2_model_data.png  "Model Data")
Figure 2: Model Data  <br/>
Image source: https://towardsdatascience.com/5-steps-of-a-data-science-project-lifecycle-26c50372b492

  5. **I**nterpretation of Data.
  

# Tidy workflow in Data Science

- Tidy workflow in [R for Data Science (Wickham and Grolemund 2017)](https://r4ds.had.co.nz/introduction.html), describes the tools needed in a typical data science project. 

![Tidy Workflow in data science](/courses/torch/3_tidy_workflow.png)
Figure 3: Tidy Workflow in data science  <br/>
Image source: https://r4ds.had.co.nz/introduction.html

**R**

**Import** | **Tidy** | **Transform** | **Visualize** | **Model** | **Communicate**
-----------|----------|----------|-------------|----------|---------
readr  | tidyr | dplyr  | ggplot2 | broom | rmarkdown
heaven | tibble |lubridate | |tidymodels | bookdown
readxl  | | forcats | | modelr| knitr
htr    | | stringr | | | shiny
rvest | |  | | | 
xml2 | |  | | | 

**Python**

|**Import** | **Tidy** | **Transform** | **Visualize** | **Model** | **Communicate**|
|:--------:|:----------:|:----------:|:------------:|:----------:|:---------:|
|[pandas - tabular data](https://pandas.pydata.org/pandas-docs/stable/index.html) |pandas | pandas | [matplotlib](https://matplotlib.org/index.html) | [Scikit-Learn](https://scikit-learn.org/stable/index.html) |  Jupyter Notebook|
| |   | [numpy (numerical data)](https://numpy.org/)      |[seaborn](http://seaborn.pydata.org/) | [statsmodels](https://www.statsmodels.org/devel/) | [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/)|
| | | | [plotnine](https://plotnine.readthedocs.io/en/stable/) (GoG) |  [TensorFlow](https://www.tensorflow.org/) | [Dash](https://plotly.com/dash/)|
| | | |[plotly](https://plotly.com/python/) | [keras](https://keras.io/)| [streamlit](https://streamlit.io/)|
| | | || | [Flask](https://flask.palletsprojects.com/en/1.1.x/)|

### Jupyter Notebook vs JupyterLab

- Jupyter Notebook is a web-based interactive computational environment for creating Jupyter notebook documents. 

- JupyterLab is the next-generation user interface including notebooks. It has a modular structure, where we can open several notebooks or files (e.g. HTML, Text, Markdowns etc) as tabs in the same window. It offers more of an IDE-like experience.

[source](https://stackoverflow.com/questions/50982686/what-is-the-difference-between-jupyter-notebook-and-jupyterlab)


#### References

- [5 Steps of a Data Science Project Lifecycle](https://towardsdatascience.com/5-steps-of-a-data-science-project-lifecycle-26c50372b492)

- [R for Data Science](https://r4ds.had.co.nz/introduction.html)
