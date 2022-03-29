# hw-09 Analyzing Text Data

# Required Packages
```
library(tidyverse)
library(knitr)
library(rvest)
library(tidytext)
library(readr)
library(devtools)
library(here)
install_github("fernandabruno/musixmatchR")
library(musixmatchR)
library(base)
library(evaluate)
library(tm)
library(ggwordcloud)

```

# Instruction
More detailed homework instruction can be found at [here](https://cfss.uchicago.edu/homework/text-analysis/). 
</br> Analyze the text for sentiment OR topic. Or build a statistical learning model using text features to predict some outcome of interest. You don’t have to do all these things, just pick one. The lecture notes and Tidy Text Mining with R are good starting points for templates to perform this type of analysis, but feel free to expand beyond these examples.

# Text Analysis of Lyrics of Most Popular Songs

In this analysis, I used two different ways to extract lyrics from [Musixmatch](https://developer.musixmatch.com/) to do text analysis. 
</br>I used the first method only to extract data for the top ten most popular songs and the second to extract data for as much as 100 top popular songs.
The analysis I did include: 
</br>**1. Finding the most Frequent words appeared in lyrics** 
</br>**2. Worldcloud**
</br>**3. Sentiment analysis of lyrics**

# Reproducibility
I adopted [R wrapper](https://github.com/fernandabruno/musixmatchR) developed by fernandabruno to extract data from musixmatch.
</br>First things first: To use the package without difficulty, it is important that you create an application to provide you with an API Key from MusixMatch. An easy way to do so is accessing MusixMatch Developers Page . After you create an application, a Key will be provided to you. This key is very important for you to be able to access all features on the package.
</br>To get musixmatchR running, you have to use devtools since it is not available on CRAN yet.
To make the package simpler to use, it is important that you create an object called apikey to store your API Key and to use it as a parameter as you call the functions.

```
library(devtools)
install_github("fernandabruno/musixmatchR")
library(musixmatchR)
```

# Reflections 
This week's assignment is really interesting!
I did frequency, sentiment and worldcloud analysis to analyze lyrics of the top 10 most popular songs and top 100 most popular songs on Spotify (yes I did them two times using different methods to extract the data).
There are also many challenges that I came across,
</br> 1. It really took me a long time to write the function to extract lyrics based on an R wrapper developed by fernandabruno. I find it hard to sort out the logical order of the code when you have a bunch of things to be compressed into one function. I also stumbled for a moment when I tried to iterate 2 inputs at the same time.
</br> 2. I kept forgetting to omit the stopwords when tried to do text analysis.

</br> Overall speaking, I really enjoyed analyzing text, especially the process of creating a wordcloud *(it's really beautiful!!)*.
