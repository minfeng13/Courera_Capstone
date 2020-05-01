# Coursera_Capstone
<h1>Comparing boroughs of London using K-means clustering</h1>
<p><h5><b>Introduction:</b> I did my undergraduate degree in London and it was one of the best times of my life. I spent most of my time living at the same post code (in Bloomsbury), but am considering moving to another borough. In this project, I will be using Foursquare API to compare different boroughs and determine how similar or dissimilar they are to Bloomsbury.</h5></p>

<h3>Obtaining the postcodes of the different boroughs of London</h3>
<p><h4><b>The Data:</b> Post codes of the different boroughs were scraped from wikipedia with the help of BeautifulSoup.</h4></p>

![pic1](https://user-images.githubusercontent.com/60607999/80818863-7e026500-8c06-11ea-8e5c-f18441a92a54.PNG)

![image](https://user-images.githubusercontent.com/60607999/80814638-d33a7880-8bfe-11ea-8bde-375822deebe3.png)

<h3>Getting Latitude and Longitudes of postcodes</h3>
<p><h4>Longitude, Latitude and Average Income was obtained from a csv file available on Office for National Statistics (ONS). As I was only interested in the boroughs and not specific locations within the boroughs, the dataframes were merged by their "OS grid ref" and duplicates dropped to get an approximation of the boroughs latitude and longitude.</h4></p>

![pic2](https://user-images.githubusercontent.com/60607999/80812686-02e78180-8bfb-11ea-8e7f-feaa0b7139f8.PNG)

<h4>As there were boroughs with missing information, they were dropped from the data. This resulted in 57 boroughs.</h4>

<h3>Exploratory Data Analysis</h3>
To ensure the data is accurate, I plotted the boroughs of London using the Folium library. The map is as below:

![image](https://user-images.githubusercontent.com/60607999/80815345-0f220d80-8c00-11ea-9ab3-c4d0a1c23787.png)

<h4>All looks good. Majority of the boroughs are represented, except for a few missing boroughs such as Greenwich, Fitzrovia, etc, which may be attributed to the inconsistencies of the data obtained from wikipedia and ONS.</h4>
<h3>Exploring popular venues of Bloomsbury within a 500 m radius</h3>
<h4>I first wanted to explore what venues are in Bloomsbury, and queried Foursquare API for the relevant information. The json file extracted from Foursquare contained a lot of information, and so a function was created to select the necessary information. 30 unique venues were extracted, limit due to free developer account with Foursquare. The 30 venues within 500m of Bloomsbury are as in the image below:</h4>

![image](https://user-images.githubusercontent.com/60607999/80818920-9a060680-8c06-11ea-80ba-ccbc0a5cb741.png)

![image](https://user-images.githubusercontent.com/60607999/80814197-03354c00-8bfe-11ea-8225-e68257dba603.png)

<h3>Now to collect the venues of the different boroughs for clustering later</h3>
<h4>The getNearbyVenues function was written to loop through the various boroughs and collect it as one dataframe.</4>
![image](https://user-images.githubusercontent.com/60607999/80817097-5a89eb00-8c03-11ea-8e72-636fc1e26f54.png)
<h4>To determine the popularity of the various venues, the venues were one hot encoded and the mean of frequency of occurrence of each venue was calculated. Once that was done, the data was collated into a dataframe and sorted. To make things easier, only the top 5 venues were selected.</h4>

![image](https://user-images.githubusercontent.com/60607999/80817514-28c55400-8c04-11ea-9a4a-cb8113805e67.png)

![image](https://user-images.githubusercontent.com/60607999/80817532-32e75280-8c04-11ea-993b-e245e586255d.png)

<h3>K-Clustering</h3>
<p><h4>With all the cleaning and sorting done, the next step was to determine the best number of clusters.</h4></p>
![image](https://user-images.githubusercontent.com/60607999/80817734-93768f80-8c04-11ea-993d-1cf4bb155438.png)
<h4>Not the best elbow curve expected.. London is after all a metropolitan and many other factors not included in this project could influence the results. As there are 57 boroughs, and based on the elbow plot, k=5 is probably a good number of clusters to have.</h4>
<p><h4>With the number of clusters decided, the K-means clustering could be done and the result is as below:</p></h4>

![image](https://user-images.githubusercontent.com/60607999/80818127-3e874900-8c05-11ea-9a55-e15c249893b4.png)


<h3>Conclusion:</h3>
<p><h4>London is divided into several zones (Zone 1, Zone 2, etc), beginning at its heart and spreading out like a non-concentric circle. It is to be expected that boroughs within the same zones would be clustered together. Bloomsbury, for example, located within Zone 1 and its neighbouring boroughs have been clustered together. However, it is surprising to see boroughs further from the central clustered with it, suggesting some similarities in venues or demographics to Bloomsbury. These boroughs may serve as options to move to.</h4></p>

<h3>Further research</h3>
<h4>There are many other factors that would influence borough clustering that were not included in this project. Factors such as rental rates, crime rate, median age, proximity to a park or tube station, etc, that may be explored. </h4>

<h4><p>Thanks for reading!</p></h4>
