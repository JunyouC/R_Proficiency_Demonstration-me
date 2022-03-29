# hw-08 Collecting and analyzing data from the web
### Required Packages
```
library(countrycode)
library(geonames)
library(gapminder)
library(tidyverse)
library(knitr)
library(broom)
library(devtools)
library(usethis)
library(rvest)
library(readr)
library(httr)
library(jsonlite)
library(base)

```
### Instruction
More detailed homework instruction can be found at [here](https://cfss.uchicago.edu/homework/webdata/).

### Introduction
This homework is consisted of 3 parts.
<br/>**- Part 1. Density**
<br/>Here's what I did:
<br/>1. Get the country information using `geonames` 
<br/>2. Merge `gapminder` and the country information from `geonames`
<br/>3. Calculate the population density for each observation
<br/>4. Produce an updated graph using population density
<br/>5. Use pearson's R to see if the correlation is statistically significant
<br/>6. Compare the relationship across continents
<br/>**- Part 2. Web scrape Practice**
<br/>Here's what I did:
<br/>1. Scrape latest 200 most popular movies' information from the Internet.
<br/>2. Clean the data and form a dataframe. 
<br/>3. Make movie analysis you can find it [here](https://github.com/JunyouC/hw08/blob/main/Part2_Webscrape_Practice_MovieAnalysis.md).
<br/>**- Part 3. API practice**
<br/>*I only did this part to practice how to use API to download information from Web. Therefore, I didn't make any further analysis. *
<br/>Here's what I did:
<br/>1. I get data for Asteroids near earth from [Jet Propulsion Laboratory](https://www.jpl.nasa.gov/) by practicing API and unnested the data using `unnest_longer()` and `unnest()`.
[Here](https://ssd-api.jpl.nasa.gov/doc/cad.html) is where I get the API.
<br/>2. Exhibit the table I formed after unnesting deeply nested data. 
