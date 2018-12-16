
# Using Foursquare venues data to deduce predominant ethnic composition of New York City neighborhoods

## Table of Contents

<div class="alert alert-block alert-info" style="margin-top: 20px">

<font size = 3>

1. <a href="#introduction">Introduction</a>

2. <a href="#data">Data</a>

3. <a href="#methodology">Methodology</a>

4. <a href="#results">Results</a>

5. <a href="#discussion">Discussion</a>    

6. <a href="#conclusion">Conclusion</a>    
</font>
</div>

<a name="introduction"/>

## Introduction

In contemporary interconnected world, big cities population include people of diverse ethnic origins. They live together, work together, and intermingle on daily basis. However, quite often people of particular ethnic backgrounds tend to prefer particular neighborhoods. You can find Chinatown, Little Italy or something similar practically in any big city in America.

Knowing predominant ethnic composition of the neighborhood may help businesses and government agencies to allocate resources to better serve particular area of the city. For example, post office in predominantly Latino neighborhood may employ more Spanish speakers and stock more forms and materials in Spanish than in the neighborhood with mostly Asian population. Grocery chains may carry more tortillas in one area and more pasta sauce and olive oil in the other.

<a name="data"/>

## Data

I am going to use Foursquare venues location information to try to infer the predominant ethnic group in New York City neighborhoods and cluster neighborhoods accordingly.

In particular, I will be looking for Food category establishments. Food preferences tend to be a good indicator of ethnic background. Abundance of pizzerias and Italian restaurants may indicate that a significant percentage of the population is of Italian origin, as long as higher concentration of Chinese restaurants in the area may point at Chinese roots.

I am going to use NYC neighborhoods geographic boundaries data provided earlier in this course, also available at https://geo.nyu.edu/catalog/nyu_2451_34572. 

For restaurants data, I am going to use venues search available in Foursquare API. There may be a lot of generic entries, like coffee shop, cafe or burger joint. Data would have to be cleaned to remove these venues. I will then find frequencies for various food establishment categories in each neighborhood, take top ten for each one and try to find distinct clusters among NYC neighborhoods. Hopefully, some relevant information about ethnic composition may be deduced looking at those clusters.

<a name="methodology"/>

## Methodology
To run neighborhoods analysis, I need the description of  NYC neighborhoods geographic boundaries. I downloaded JSON file with names and coordinates of neighborhoods in all five boroughs from https://geo.nyu.edu/download/file/nyu-2451-34572-geojson.json. After loading JSON data from that file, the list of neighborhoods with latitude and longitude coordinates can be extracted from "features" key. We load all the neighborhoods for each borough with latitude and longitude coordinates of the neighborhood's center point into Pandas dataframe.
After that we can render all the neighborhoods on the map of New York using folium mapping library, to check that the data looks right so far:
![NYC Map](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/NYC_Neighborhoods.jpg)


<a name="results"/>

## Results


<a name="discussion"/>

## Discussion



<a name="conclusion"/>

## Conclusion





