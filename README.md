# DATA 607 - Final Project

Final project repo for Data 607.

Authors: Naomi Buell, Kaylie Evans, Nick Kunze

## Introduction

The code in this repo builds on what we've learned in class to analyze our research question: **how** **do film reviews differ between professional critics and the general audience?** This project utilizes the Article Search API from the New York Times to retrieve movie review data in JSON format. The retrieved data is then transformed into an R data frame and merged with movie data from Letterboxd.

## Data Sources

To analyze two types of film reviews, we examine New York Times (NYT) critics’ reviews (as text) and film ratings posted by [Letterboxd](https://letterboxd.com/) users (numeric rating from 1 to 5). We pull data using [NYT’s API](https://developer.nytimes.com/docs/movie-reviews-api/1/overview) and sourced a [CSV containing Letterboxd movie ratings data from Kaggle](https://www.kaggle.com/datasets/gsimonx37/letterboxd?select=movies.csv).

## Methods

### Required Packages

This project utilizes several R packages, including:

-   tidyverse

-   janitor

-   jsonlite

-   qdapDictionaries

-   tidytext

-   rvest

-   vader

Ensure that these packages are installed and loaded before running the code.

### Connect to NYT API, Load JSON data into R

To access the New York Times API, you need to sign up for an API key. The API key is kept private using the **`rstudioapi::askForPassword()`** function. The base HTTP request URL is defined to retrieve article search results. A function called **`get_movies()`** is created to pull data from the NYT API based on filter and page number parameters. This function retrieves movie review data from the API and paginates through the results. The retrieved NYT data is cleaned by subsetting to variables of interest and performing data transformation operations. This includes extracting movie names from keywords, cleaning movie names, and converting publication dates to datetime format.

### Load Letterboxd data

Letterboxd movie data is loaded and cleaned by transforming movie names to lowercase and dropping movies released before the earliest review in the NYT data.

### Merge NYT and Letterboxd data

We merge both sets of movie review data, matching as many movies as possible. The cleaned NYT and Letterboxd data are merged based on movie names. The merge process selects the best matches based on the closest dates between review publication and movie release.

Descriptive statistics are generated to validate the merged data set. This includes checking the distribution of dates, movie durations, and user ratings. Data quality assessment is performed to identify duplicates and ensure the accuracy of the merged data.

Then we perform a sentiment analysis on the NYT film reviews in order to compare the favorability of the movie from the perspective of both sources.

### Data Dictionary

All cleaning and tidying was completed in R. Below describes steps taken to prepare the following variables for analysis.

-   `name`: the name of the film (string). Source: NYT and Letterboxd.

    -   Retrieved from NYT by un-nesting value from nested `keywords` column.

    -   Cleaning performed: changed case to lowercase, removed tailing “, the” and leading “the” (e.g., “The Notebook” and “Notebook, the” are both changed to "Notebook"), and removed parentheticals.

-   `abstract`: abstract of the review (string). Source: NYT.

-   `lead_paragraph`: lead paragraph of the review article (string). Source: NYT.

-   `pub_date`: review publication date (string). Source: NYT.

-   `headline_main`: main headline of the review (string). Source: NYT.

-   `headline_kicker`: headline kicker of the review, appearing above the headline (string). Source: NYT.

-   `headline_print_headline`: print headline of the review (string). Source: NYT.

-   `date`: year of release of the film (datetime). Source: Letterboxd.

-   `tagline`: the slogan of the film (string). Source: Letterboxd.

-   `description`: description of the film (string). Source: Letterboxd.

-   `minute`: movie duration (in minutes). Source: Letterboxd.

-   `rating`: average rating of the film (numeric rating from 1 to 5). Source: Letterboxd.

## Analysis

[Insert analysis text here]

## Conclusion

This README provides an overview of the code and data analysis conducted for our Final Project. Further details and insights can be found within the code and associated analysis outputs.

[Insert conclusion text here]
