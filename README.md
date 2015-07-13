# Analyzing tagged data
**Author**: Srikanth K S (aka talegari)  
**Repository**: https://github.com/talegari/analyzing-tagged-data

----

## Objective

We intend to explore the data with tags.

Here is an example of tagged data.



| MS Word | Libreoffice Writer | abiword | notepad++ |
|:---------:|:--------------------:|:---------:|:-----------:|
|         | free               | free    | free      |
| docx    | odt                | abw     | txt       |
| all     | all                |         | limited   | |




* There are four objects: **MS Word**, **Libreoffice Writer**, **abiword**, **notepad++**

* Each object have their respective tags. For example: The object **abiword** as tags 'free' and 'abw'. The order of tags does not matter.

We provide,

* A *tiny* recommender system to suggest objects or tags based on set of *visited* objects or tags. (*tiny* in sense, we do not do anything fancy)

* A report of different visualizations of the tagged data. See *output.html* or *output.pdf* in the repository for a trial data.

----

## Usage

Please place the repository(named `vis_tag_data`) in the R's working directory or set the working directory with `setwd()` appropriately.

----

## Requirements

The code is written in **R**, statistical programming language (R version 3.2.0). Apart from *base* R, we make use of the following packages:

*dplyr*,*reshape2*, *ggplot2*, *knitr*

If you need to check or install any of the packages, you are suggested to run the following.


`source("~/vis_tag_data/vistagdata.R")`

`lapply(c("dplyr","reshape2","ggplot2","knitr"),pkgTest)`

If run for the first time, the previous command might take some minutes. Please be patient.

For pdf generation on linux based systems, you might require *pandoc*.

----

## Format of input data

Data input format: **csv**

* The first line is considered as the set of objects
* The corresponding columns are considered as their tags.
* All the data is considered as *text*. That is, we do not recognize any data type as say *date*, *number* etc.

For example, see 'taggeddataset.csv' in the repository. We create a R object of the input dataset as follows:

<code>inputdata <- read.csv("~/vis_tag_data/taggeddataset.csv",fill=T,colClasses="character")</code>

----

## Files in the repository

* **vistagdata.R** -- the code used for recommender system and visualization. You will have to source it to run the recommender system functions.

* **output.Rmd** -- code used to generate the html or pdf with the visualizations. This will be processed by *knitr*.

* **taggeddataset.csv** -- the example dataset. The *output.Rmd* uses this name all through. Hence it suggested to name your own dataset as *taggeddataset.csv*.

Repository contains *output.pdf*, *output.html* which are outputs of the *output.Rmd* on the trial dataset.

----

### Recommender system

* Source the **vistagdata.R** using the source() command. For example:

`source('~/vis_tag_data/vistagdata.R')`

* There are four functions.



|   Function  |                     task                     |
|:-----------:|:--------------------------------------------:|
| oorecommend | ... recommends  objects based on visited objects |
| ttrecommend | ... recommends tags based on visited tags |
| otrecommend | ... recommends tags based on visited objects |
| torecommend | ... recommends objects based on visited tags |


* The syntax of the functions are similar. They take the inputdata as the first argument and visited character vector as the second argument. They return a dataframe. For example:

`inputdata <- read.csv("~/vis_tag_data/taggeddataset.csv",fill=T,colClasses="character")`

`source('~/vis_tag_data/vistagdata.R')`

`View(oorecommend(inputdata,visited=c("bear","monkey")))`


gives the following output

|   |  object  | percentageMatch |
|---|:--------:|:---------------:|
| 1 | tiger    |               62 |
| 2 | elephant |               62 |
| 3 | dog      |               38 |
| 4 | fish     |               38 |
| 5 | cat      |               29 |

----

### Tagged data visualization

* On knitting **output.Rmd**, we can produce pdf or html or docx output. Its suggested to use Rstudio IDE for R for easy knitting. Else, try knit() function in R commandline.

* These visualizations are generated:

    1. Visualizing objects versus tags
    2. Visualizing tags versus objects
    3. Hierarchical object clustering (a dendogram)
    4. Hierarchical tag clustering (a dendogram)
    5. Heatmap of objectwise hierarchical clustering
    6. Heatmap of tagwise hierarchical clustering
    7. Clusters among objects (using kmeans)
    8. Clusters among tags (using kmeans)
    9. Number of tags shared by objects
    10. Number of objects shared by tags

* 7th and 8th visualizations above use kmeans algorithm that requires the input of number of clusters. We currently employ a crude estimate for this, please try different values and decide the best number.

* By default, the report displays the code too. You may want to put it off by setting 'echo=F' in the *global settings* at the beginning of the *output.Rmd*

----

## Technical details

Coming soon!

----