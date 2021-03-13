# Coursera_Capstone
                                                          THE MOST LIVEABLE PLACE IN BERLIN FOR STUDENTS
Introduction and Business Problem:


Berlin is known with its high student and young professional population coming from all around the world. That creates the biggest problem of the berlin which is the problem of finding correct place to live.
There are already known important things when we consider young populations' needs which are not find in any corner of the Berlin. 
This project will answer the areas where a student can consider to live if they are looking for a nice experience in Berlin. 
Night life, various cafes, being close to schools and startup centres... etc. These will be the important aspects that the project will focus on the data.


Data:


Foursquare API:
This project would use Four-square API as its prime data gathering source as it has a database of millions of places, especially their places API which provides the ability to perform location search, location sharing and details about a business.

Work Flow:
Using credentials of Foursquare API features of near-by places of the neighborhoods would be mined. Due to http request limitations the number of places per neighborhood parameter would reasonably be set to 100 and the radius parameter would be set to 500.

Clustering Approach:
To compare the similarities of two cities, we decided to explore neighborhoods, segment them, and group them into clusters to find similar neighborhoods in a big city like New York and Toronto. To be able to do that, we need to cluster data which is a form of unsupervised machine learning: k-means clustering algorithm

Libraries Which are Used to Develope the Project:
Pandas: For creating and manipulating dataframes.

Folium: Python visualization library would be used to visualize the neighborhoods cluster distribution of using interactive leaflet map.

Scikit Learn: For importing k-means clustering.

JSON: Library to handle JSON files.

XML: To separate data from presentation and XML stores data in plain text format.

Geocoder: To retrieve Location Data.

Beautiful Soup and Requests: To scrap and library to handle http requests.

Matplotlib: Python Plotting Module.
