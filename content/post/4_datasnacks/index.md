---
authors:
- admin
categories: []
date: "2021-06-18"
draft: false
featured: false
image:
  caption: "Image credit: pixabay"
  focal_point: ""
lastMod: "2021-06-18"
projects: []
subtitle: 
summary: 
math: true
tags: 
- RETINA
title: 'Mini-workshops on open source software tools for data science'
---

[Let’s Enjoy Cricket with R!](/workshops/Introduction-to-TIdy-Tools.html)

In this [blogpost](/workshops/Introduction-to-TIdy-Tools.html) we will use `cricketdata` R package by Rob Hyndman and his team, to get a better understanding of the concepts of exploration, visualization, and potential analyses.

This post was inspire by Rob Hyndman’s recent post on [The cricketdata package](https://robjhyndman.com/hyndsight/cricketdata/).

## Introduction to Tidy Tools in R

##  Load R packages

```{r}
library(cricketdata)
library(tidyverse)
```

## Data

In this workshop we will use `cricketdata` R package by [Rob Hyndman](https://robjhyndman.com/hyndsight/cricketdata/) and his team,  to get a better understanding of the concepts of exploration, visualization, and potential analyses. 

This post was inspire by Rob Hyndman's recent post on ["The cricketdata package"](https://robjhyndman.com/hyndsight/cricketdata/).

There are four key functions in the `cricketdata` package:

  - `fetch_cricinfo()`: Fetch team data on international cricket matches provided by ESPNCricinfo.
  - `fetch_player_data()`: Fetch individual player data on international cricket matches provided by ESPNCricinfo.
  - `find_player_id()`: Search for the player ID on ESPNCricinfo.
  - `fetch_cricsheet()`: Fetch ball-by-ball, match and player data from Cricsheet.
  
### Sri Lanka men’s ODI data by innings

This example shows Sri Lankan men’s ODI batting results by innings.

```{r}
menODI <- fetch_cricinfo("ODI", "Men", "Batting", type = "innings", country = "Sri Lanka")

colnames(menODI)
```

## Data Import and Export

```{r}
# Export Data
write_csv(menODI, "SLmenODI.csv")
```


```{r}
# Import Data
data <- read_csv("SLmenODI.csv")
head(data)
```

## Data wrangling

Data wrangling is the process of cleaning and unifying messy and complex data sets for easy access and analysis.

There are five dplyr functions that you will use to do the vast majority of data manipulations:

 - `filter()`: pick observations by their values
 - `select()`: pick variables by their names
 - `mutate()`: create new variables with functions of existing variables
 - `summarise()`: collapse many values down to a single summary
 - `arrange()`: reorder the rows


### Pipe (%>%) Operator

 - The principal function provided by the `magrittr` package is `%>%`, or what’s called the “pipe” operator. 
 - This operator will forward a value, or the result of an expression, into the next function call/expression. 

```{r}

menODI %>%
  filter(Date == "2022-06-19")
```

```{r}
menODI %>%
  select(Date, Player, Runs, StrikeRate, NotOut)
```


```{r}
menODI %>%
  group_by(Player) %>%
  summarise(Runs = mean(Runs), matches = n()) %>%
  arrange(desc(Runs))
```

```{r}
menODI %>% 
  filter(Player == "BKG Mendis") %>% 
  arrange(desc(Date))
```

## Data Visualization

```{r}
p <- menODI %>%
  filter(Opposition %in% c("Australia", "Bangladesh", "Pakistan") )%>%
  ggplot(aes(y = Runs, x = Date, col = Opposition)) +
  geom_point(alpha = 0.7) +
  geom_smooth()+
  ggtitle("Sri Lanka Men ODI: Runs per Innings")
  
print(p) 
```


The average number of runs per innings for Bangladesh is higher than that for Australia and Pakistan, even though the performance has gradually declined over time.

### Sri Lanka test fielding data

Next, we demonstrate some of the fielding data available, using Test match fielding from Sri Lankan men’s players.

```{r}
SLfielding <- fetch_cricinfo("Test", "Men", "Fielding", 
                              country = "Sri Lanka")
head(SLfielding)

colnames(SLfielding)
```

We can plot the number of dismissals by number of matches for all male test players. 

```{r}
p1 <- SLfielding %>%
  ggplot(aes(x = Matches, y = Dismissals)) +
  geom_point() +
  ggtitle("Sri Lanka Men Test Fielding")

print(p1)
```


Because wicket keepers typically have a lot more dismissals than other players, let's show them in a different colour.


```{r}
p2 <- SLfielding %>%
  mutate(wktkeeper = (CaughtBehind > 0) | (Stumped > 0)) %>%
  ggplot(aes(x = Matches, y = Dismissals, col = wktkeeper)) +
  geom_point() +
  ggtitle("Sri Lanka Men Test Fielding")

print(p2)
```

We can see two outlying points. I would like to do further investigation into them.

### Interactive data visualization

Interactive data visualization is the use of tools and processes to create a visual representation of data that can be explored and analyzed directly within the visualization itself. This interaction can help to uncover insights that lead to better, data-driven decisions.

`plotly` R package allows us to create interactive and publication-quality charts/graphs in R. 

```{r}
p3 <- SLfielding %>%
  mutate(wktkeeper = (CaughtBehind > 0) | (Stumped > 0)) %>%
  ggplot(aes(x = Matches, y = Dismissals, col = wktkeeper,
             text=Player)) +
  geom_point() +
  ggtitle("Sri Lanka Men Test Fielding")

library(plotly)
ggplotly(p3)


```

The high number of dismissals, just above 200, is due to Kumar Sangakkara. Another interesting statistic is the non-wicketkeeper with over 200 dismissals.This is Mahela Jayawardene who took 205 catches during his career.

### Kusal Mendis’s ODI batting

Finally, consider the data for individual players. The Cricinfo player ID is required for the `fetch_player_data()` function, which you can find on their website or by using the `find_player_id()` function. We'll look at Kusal Medis's ODI results.

```{r}
KMendis_id <- find_player_id("BKG Mendis")$ID
KMendis <- fetch_player_data(KMendis_id, "ODI") %>%
  mutate(NotOut = (Dismissal == "not out"))

head(KMendis)
```

Let's can plot his runs per innings on the vertical axis over time on the horizontal axis.

```{r}
# Compute batting average
KMave <- KMendis %>%
  filter(!is.na(Runs)) %>%
  summarise(Average = sum(Runs) / (n() - sum(NotOut))) %>%
  pull(Average)
names(KMave) <- paste("Average =", round(KMave, 2))
KMave


# Plot ODI scores
ggplot(KMendis) +
  geom_hline(aes(yintercept = KMave), col="gray") +
  geom_point(aes(x = Start_Date, y = Runs, col = NotOut)) +
  ggtitle("Kusal Mendis ODI Scores") 
```

Around 2021, a significant blank space is visible. In July 2021, Mendis was suspended from playing in international cricket for one year. Sri Lanka Cricket agreed to lift the ban early, removing the punishment in January 2022. Now Kusal Mendis is back in the squad.


**Keep Exploring! Happy Learning with R!!**

### Additional Resources {-}

[R for Data Science by by Hadley Wickham and Garrett Grolemund](https://r4ds.had.co.nz/)

This is a great data science book for beginners interested in learning data science with R.

### References {-}

Rob Hyndman, Timothy Hyndman, Charles Gray, Sayani Gupta and Jacquie Tran (2022). cricketdata: International Cricket Data. R package version 0.1.1. https://CRAN.R-project.org/package=cricketdata
