Introduction


Berlin and Hamburg are two of Germany's largest cities and each year many people move from one city to the other.

In this analysis I will explore how similar or dissimilar their neighbourhoods are based on Foursquare location data.

My target audience are people moving from one city to another and wanting to know where they should rent their new apartment.

Specifically, if you move from Hamburg to Berlin which neighbourhood should you move to based on your previous neighbourhood? What characteristics do these neighbourhoods have?

The analysis will show that for several neighbourhoods we will not find a similar counterpart in the other city. Two clusters, however, have a distinct venue mix and are represented in both cities.

Data




For this analysis I will be using foursquare data to analyze different neighbourhoods in two major German cities: Hamburg and Berlin.

One concern is that data for Germany may not be as extensive as it would be for the U.S. and the analysis may therefore not be as comprehensive.

I will be looking mainly at venue data which will enable me to identify neighbourhoods that share certain traits such as having many cafés or restaurants.

Because the official neighbourhoods in Hamburg are sized very differently (e.g. there are seven boroughs that range from 50 km^2 to 155 km^2 which are in turn split into localities of different sizes) I decided to use a regularly spaced grid of locations, centred around each city center, to define the neighbourhoods. But I will also look at the boroughs to confirm my assumption that they are not suitable for clustering.

The following data sources will be needed to extract/generate the required information:

Geopy Nominatim will be used to obtain the city centres, using the Außenalster for Hamburg and the Brandenburg Gate for Berlin.

The neighbourhoods will be generated algorithmically with a fixed radius. Approximate addresses of the centres of those areas will be obtained using geopy Nominatim reverse geocoding.

The number of venues and their category in every neighbourhood will be obtained using the Foursquare API.

Methodology



Generate neighbourhood dataset
To generate the dataset of the neighbourhood locations, the city centers of Hamburg and Berlin were used as starting points. For Hamburg the Außenalster and for Berlin the Brandenburg Gate was used as the center address. From these addresses the geocoordinates were derived using the geocode function from Nominatum.

These latitude and longitude coordinates needed to be transformed into UTM coordinates to enable defining a radius around the city center and a smaller radius for each neighbourhood. For the cities this was set to 5 km and for the neighbourhoods to 1.5 km. Looping over this radius in a hexagonal grid generated UTM coordinates for each neighbourhood. These were transformed back into geocoordinates resulting in a list of 39 neighbourhoods for each city.

To check whether the neighbourhoods were generated correctly, folium was used to map their locations.

The Foursquare Places API uses addresses as search entries. Therefore, the reverse function from Nominatim was used to generate neighbourhood addresses from the latitude and longitute values. In addition, from the resulting addresses the borough names could be extracted. For Berlin this resulted in 14 boroughs vs. 13 boroughs in Hamburg.

Cleaned up, the dataset includes the neighbourhood address, latitude, longitude, borough and city.

Get venue data from Foursquare
The Foursquare Places API provides venue recommendations using the "explore" functionality. It was used to request the 100 most popular venues within 1.5 km of each neighbourhood center. Along with the venue name, Foursquare provides many additional details on the venue such as the category (e.g. bakery or theater).

Those neighbourhoods for which less than 100 venues were found were exluded from the dataset.

For each remaining neighbourhood and borough the top 10 venue categories were identified. This was done using one hot encoding and calculation of the mean per category.

For the following analysis the resulting tables were simplified and geo-coordinates generated for each borough.

Cluster neighbourhoods and boroughs
The neighbourhoods and boroughs were clustered using the Kmeans algorithm from sklearn. Kmeans groups each observation (in this case each neighbourhood or borough) into clusters minimizing the variance within each cluster. Important to note is that it converges to a local optimum, so each computation may lead to different results.

A high number of clusters were specified (15 for the neighbourhoods and 5 for the boroughs) with the aim of getting very specific clusters with an average of 4 neighbourhoods or boroughs.

The results for the neighbourhood clustering will be dicussed in more detail in the next section. The clustering of the boroughs, however, led to inconclusive results because they appear to be too large to be distinct from one another or base a recommendation on.
