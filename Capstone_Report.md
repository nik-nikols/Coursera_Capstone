
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

After getting the data for New York neighborhoods and venues and preparing it as described above, and performing k-mean clustering, I found four distinct clusters of neighborhoods. To illustrate, here is a map of New York with resulting clusters of neighborhoods:

![NYC Map with Clusters](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/NYC_Neighborhoods_Clusters.jpg)

Colored markers correspond to four clusters:
- Red - Cluster 1
- Violet - Cluster 2
- Light Blue - Cluster 3
- Yellow-Green - Cluster 4

Now, let's look at each cluster's top ten categories:
### Cluster 1:
![Cluster 1](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/Cluster1.jpg)
This cluster is kind of a mix of various cuisines, probably showing neighborhoods with no particular ethnic trends.

### Cluster 2:
![Cluster 2](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/Cluster2.jpg)
This cluster indicates preeminence of Italian restaurants.

### Cluster 3:
![Cluster 3](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/Cluster3.jpg)
In this cluster, we can see a lot of Caribbean restaurants in top 10.

### Cluster 4:
![Cluster 4](https://github.com/nik-nikols/Coursera_Capstone/blob/master/images/Cluster4.jpg)
This cluster includes neighborhoods where Chinese food seems to be quite popular.




<a name="discussion"/>

## Discussion
We found that New York City neighborhoods fall into four distinct clusters based on the prevalence of particular types of food establishments. Let's see how we can interpret that result and check if our inferences are supported by known demographic data.

For the first cluster, there is no particular trend among top 10 restaurants, so we could presume that the ethnic composition of the neighborhoods included in that cluster is rather mixed. It is also the biggest cluster with 164 neighborhoods. 

Second cluster shows an abundance of Italian restaurants. We can presume that it might point to sizable Italian American population. 18 out of 28 neighborhoods in this cluster are on the Staten Island. According to Wikipedia, Italian Americans constitute about 36% of Staten Island's inhabitants[^1]. 

Third cluster has a lot of Caribbean restaurants in top 10. It would be reasonable to expect significant number of immigrants and their descendants who came from Caribbean islands in these communities. Indeed, let's look at some of the neighborhoods in this cluster and what Wikipedia tells about their demographics. For example, Cambria Heights in Queens "has a large middle class Caribbean and African American population"[^2]. Canarsie in Brooklyn has population which "is mostly black due to significant  West Indian immigration in the area"[^3].

Fourth cluster is dominated by Chinese and other Asian restaurants in top 10, so we can probably expect to find corresponding ethnic groups in these neighborhoods. And, in fact, Chinatown in Manhattan and Bensonhurst in Brooklyn fall into this cluster. However, there are also neighborhoods in this group with no big Asian groups, like Allerton in Bronx or Astoria Heights in Queens. That might point to the fact that Chinese restaurants may be popular among other groups, too.

<a name="conclusion"/>

## Conclusion
So what can we conclude from our exercise in clustering big city's neighborhoods by kinds of most popular restaurant categories in the area? Can we use it to infer ethnic composition of local population?

It looks like in some cases, it may be a viable approach, at least as a rough guess. Classification is not precise, of course. Some foods became widely popular among diverse groups, so it depends on how specific the categories we choose for analysis are. We saw that Chinese restaurants may be indicative of significant Asian portion in local demography if there are a lot of other Asian establishments, like noodle houses, sushi restaurants and dumpling restaurants in the area. In other cases, they may be just one part in a mixed food landscape of really diverse area, or their popularity may be explained by other factors, like low price and quick service, for example.

For Caribbean restaurants, on the other hand, their presence as most popular group in the neighborhood most often hints at significant numbers of inhabitants with Caribbean and West Indian roots.

There should also be a big enough number of restaurants in the area for this method to work, so the neighborhoods should be large and densely populated. It would not work for a small town, but produces some reasonable results for huge New York City with its millions of dwellers.

It would be interesting to see how the results would change if we use the complete data that might be available to paying Foursquare users, and not just 50 entries per neighborhood, as in free version.

The other possible improvement might be to try to group multiple entries into categories, like for example Asian for Vietnamese, Chinese, Malay, Japanese etc, European for Italian, French, German and other European restaurants, Middle Eastern for Falafel, Israeli, Jewish, Kosher, Halal, Lebanese and so on, and try clustering on those higher level categories.

But even with these limitations, neighborhoods clustering based on the publicly available data about restaurants can be used to discover ethnic enclaves in a big city. 

<hr/>

## Bibliography
[^1]: [Demographics of Staten Island](https://en.wikipedia.org/wiki/Demographics_of_Staten_Island) 
[^2]: [Cambria Heights, Queens](https://en.wikipedia.org/wiki/Cambria_Heights,_Queens#Demographics) 
[^3]: [Canarsie, Brooklyn](https://en.wikipedia.org/wiki/Canarsie,_Brooklyn#Demographics) 




