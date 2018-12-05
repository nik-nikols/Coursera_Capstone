# Using Foursquare venues data to deduce predominant ethnic composition of New York City neighborhoods

## Data

I am going to use Foursquare venues location information to try to infer the predominant ethnic group in New York City neighborhoods and cluster neighborhoods accordingly.

In particular, I will be looking for Food category establishments. Food preferences tend to be a good indicator of ethnic background. Abundance of pizzerias and Italian restaurants may indicate that a significant percentage of the population is of Italian origin, as long as higher concentration of Chinese restaurants in the area may point at Chinese roots.

I am going to use NYC neighborhoods geographic boundaries data provided earlier in this course, also available at https://geo.nyu.edu/catalog/nyu_2451_34572. 

For restaurants data, I am going to use venues search available in Foursquare API. There may be a lot of generic entries, like coffee shop, cafe or burger joint. Data would have to be cleaned to remove these venues. I will then find frequencies for various food estblishment categories in each neighborhood, take top ten for each one and try to find distinct clusters among NYC neighborhoods. Hopefully, some relevant information about ethnic composition may be deduced looking at those clusters.
