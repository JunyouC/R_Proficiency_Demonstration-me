Part2_Asteroids_Movie
================
Junyou Chen
3/9/2022

-   [Required Packages](#required-packages)
-   [Asteroids Near Earth](#asteroids-near-earth)

## Required Packages

``` r
knitr::opts_chunk$set(echo = TRUE, warning = FALSE, message = FALSE)

library(tidyverse)
library(knitr)
library(httr)
library(jsonlite)
library(base)
```

## Asteroids Near Earth

In this part, I tried to practice API query to request information from
the website. I get data for Asteroids near earth from [Jet Propulsion
Laboratory](https://www.jpl.nasa.gov/) by practicing API and unnested
the data using `unnest_longer()` and `unnest()`.
[Here](https://ssd-api.jpl.nasa.gov/doc/cad.html) is where I get the
API. The table below only showed the first 6 rows of data.

``` r
## retrieve the data

asteroid_api <- function(start, end) {
  # send GET request
  link <- sprintf("https://ssd-api.jpl.nasa.gov/cad.api?date-min=%s&date-max=%s", start, end)
  response <- GET(
    url = link
  )
  # parse response to JSON
  response_df <- content(response)

  return(response_df)
}
## to extract asteroid near earth data from 2020-01-01 to 2021-01-01.
data <- asteroid_api("2020-01-01", "2021-01-01")
## to first store data$data in a dataframe 
data_df <- tibble(data$data)
## to add a new column with repeated values from `fields`
x<-rep(c("des","orbit_id","jd","cd","dist","dist_min","dist_max","v_rel","v_inf","t_sigma_f","h"),times = 1444)

asteroid_df<- data_df %>%
unnest_longer(col=1) %>%
  add_column(x, .before = 1) %>%
  rename(value = `data$data`) %>%
  pivot_wider(names_from = x, values_from = value,values_fn = list) %>%
  unnest(cols = c(des, orbit_id, jd, cd, dist, dist_min, dist_max, v_rel, v_inf, 
    t_sigma_f, h))

kable(head(asteroid_df))
```

| des      | orbit_id | jd                | cd                | dist                | dist_min            | dist_max            | v_rel            | v_inf            | t_sigma_f | h    |
|:---------|:---------|:------------------|:------------------|:--------------------|:--------------------|:--------------------|:-----------------|:-----------------|:----------|:-----|
| 2020 AY1 | 19       | 2458849.537524375 | 2020-Jan-01 00:54 | 0.0211660462302475  | 0.0211628282597546  | 0.021169264192927   | 5.62203034144512 | 5.59959426682482 | \< 00:01  | 25.2 |
| 2019 YK  | 11       | 2458849.587204797 | 2020-Jan-01 02:06 | 0.0361009647238789  | 0.0360768259080859  | 0.0361251034508466  | 7.35926278450408 | 7.34922690439657 | \< 00:01  | 24.0 |
| 2020 AP3 | 4        | 2458849.967322953 | 2020-Jan-01 11:13 | 0.0167404854088158  | 0.0165847722715622  | 0.0168961658040387  | 5.19125028298636 | 5.16049919025748 | 00:05     | 26.6 |
| 2020 AN2 | 2        | 2458850.387698712 | 2020-Jan-01 21:18 | 0.0202143163095242  | 0.0196465482155464  | 0.0207820804994879  | 15.3528157321644 | 15.3442278367922 | 00:33     | 26.5 |
| 2020 AX  | 6        | 2458850.450408059 | 2020-Jan-01 22:49 | 0.0496561823173887  | 0.0491870437725472  | 0.0501253029712591  | 7.31673540674871 | 7.30939805239444 | 00:04     | 26.3 |
| 2020 AC  | 7        | 2458850.788622537 | 2020-Jan-02 06:56 | 0.00865672387978391 | 0.00864974336834992 | 0.00866370421544426 | 5.79319898159094 | 5.73982302560126 | \< 00:01  | 26.7 |

Here are further explanations for variables. <br/>**des** - primary
designation of the asteroid or comet (e.g., 443, 2000 SG344)
<br/>**orbit_id** - orbit ID <br/>**jd** - time of close-approach (JD
Ephemeris Time, TDB) <br/>**cd** - time of close-approach (formatted
calendar date/time, TDB) <br/>**dist** - nominal approach distance (au)
<br/>**dist_min** - minimum (3-sigma) approach distance (au)
<br/>**dist_max** - maximum (3-sigma) approach distance (au)
<br/>**v_rel** - velocity relative to the approach body at close
approach (km/s) <br/>**v_inf** - velocity relative to a massless body
(km/s) <br/>**t_sigma_f** - 3-sigma uncertainty in the time of
close-approach (formatted in days, hours, and minutes; days are not
included if zero; example “13:02” is 13 hours 2 minutes; example
“2_09:08” is 2 days 9 hours 8 minutes) <br/>**h** - absolute magnitude H
(mag)
