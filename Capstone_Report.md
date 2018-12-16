
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
To run neighborhoods analysis, I need the description of  NYC neighborhoods geographic boundaries. I downloaded JSON file with names and coordinates of neighborhoods in all five boroughs from https://geo.nyu.edu/download/file/nyu-2451-34572-geojson.json. After loading JSON data from that file, the list of neighborhoods with latitude and longitude coordinates can be extracted from "features" key. We load all the neighborhoods for each borough with latitude and longitude coordinates of the neighborhood's center point into Pandas dataframe. Here I used the code from course's labs, with slight modification. After looking at the neighborhoods closely, it appears that there are several instances of neighborhoods overstepping borough's boundaries, so there are entries with the same neighborhood name in different boroughs. So I added borough's name to the name of the neighborhood, to make it unique.

After that we can render all the neighborhoods on the map of New York using folium mapping library, to check that the data looks right so far:
![NYC Map](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/NYC_Neighborhoods.jpg)

Now we need the data about restaurants in every neighborhood. I used Foursquare API for that purpose. Foursquare API has search method that allows you to find venues in particular category (in our case, restaurants) around particular location. Unfortunately, when I tried to search for restaurants in every neighborhood by sending requests one by one for all of them, API stopped responding before I reached the end of the list. So I had to split my requests to send them in series for one borough at a time. So eventually, I have the list of restaurants in all neighborhoods in all five boroughs. 

Another limitation in the free version of Foursquare API is that it seems to return no more that 50 venues for each search. That might adversely affect the results of the analysis, so it would be interesting to try it with full version and see what difference it would make.

Looking at the venue categories counts for Brooklyn, for example, it is easy to see that a lot of categories are rather generic (like _coffee shop_, _doughnut shop_, just _food_, or _restaurant_). Such categories would probably not be terribly useful in our analysis, so I filtered them out, and only left the entries for categories that might point at particular ethnic background. Categories used in the subsequent analysis are:
- Italian Restaurant
- Mexican Restaurant
- Chinese Restaurant
- French Restaurant
- Ramen Restaurant
- Thai Restaurant
- Mediterranean Restaurant
- Japanese Restaurant
- Indian Restaurant
- Spanish Restaurant
- Sushi Restaurant
- Latin American Restaurant
- Asian Restaurant
- Greek Restaurant
- Taco Place
- Noodle House
- Korean Restaurant
- Caribbean Restaurant
- Vietnamese Restaurant
- Tapas Restaurant
- Dim Sum Restaurant
- Cuban Restaurant
- Dumpling Restaurant
- Udon Restaurant
- Falafel Restaurant
- Lebanese Restaurant
- Burrito Place
- Southern / Soul Food Restaurant
- German Restaurant
- Beer Garden
- Filipino Restaurant
- Australian Restaurant
- Swiss Restaurant
- Moroccan Restaurant
- Peruvian Restaurant
- Sake Bar
- Ethiopian Restaurant
- Middle Eastern Restaurant
- Poke Place
- Taiwanese Restaurant
- Malay Restaurant
- Szechuan Restaurant
- Hawaiian Restaurant
- Soba Restaurant
- Turkish Restaurant
- Kosher Restaurant
- Israeli Restaurant
- Jewish Restaurant
- Cantonese Restaurant
- South Indian Restaurant
- Creperie
- Shanghai Restaurant
- Arepa Restaurant
- African Restaurant
- Tex-Mex Restaurant
- Irish Pub
- Halal Restaurant
- English Restaurant
- Paella Restaurant
- Japanese Curry Restaurant
- Kebab Restaurant
- Argentinian Restaurant
- Ukrainian Restaurant


After filtering the datasets, I concatenated all the rows from these five datasets into single dataset.

After applying one hot encoding to the venue categories in that dataset and calculating frequency of occurrence for each category in every neighborhood, we get the dataset that we are going to use for clustering.

I used _k-means_ algorithm implementation from **sklearn** package to do the clustering. Same package has been used to calculate _silhouette score_ for different numbers of clusters, to find an optimal number of clusters.

<a name="results"/>

## Results



<a name="discussion"/>

## Discussion



<a name="conclusion"/>

## Conclusion





