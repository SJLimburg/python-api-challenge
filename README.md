# Python –  API - Challenge


This particular challenge is divided into two sections; weatherPy and vacationPy. The problem solving goal of this exercise Is to find at least 500 random places around the world in order to find a vacation spot with the best weather.
Programmatically, the goal of this exercise is to understand how to use API calls to gather information and to use the Google Maps API to create and display maps in The jupyter Notebook using python code. 

## WeatherPy
The first section, weatherPy, generates a random sample of latitude and longitude into a list. the latitude and longitude list is used to find at least 500 unique city names for the next step of the program.
After the list of city names is compiled an API call is made to openweathermap to obtain desired weather data in imperial units. 
The API call uses cities list to loop through and return the following data points into their respective lists:

- Latitude
- Longitude
- Maximum temperature
- Humidity
- Cloudiness
- Wind speed
- Country name
- City name
- City number
- Date

**Warning:** This API call originally ran too quickly to limit the quantity of calls to 60 requests per minute, which is the maximum under the free account license. To remedy this issue the time.sleep(1) function was used to add 1 second between each successive API call.

The results were then added to a Pandas DataFrame for subsequent manipulation and Output to a CSV file for the second half of the project. 

The pandas dataframe was used to populate the weather characteristics vs. latitude and longitude in a series of Scatter Plots.

#### The first plot compared Temperature vs Latitude

Figure 1 - Maximum Temperature vs Latitude 19_Oct_2020

![MaxTempvsLat](https://github.com/SJLimburg/python-api-challenge/blob/main/WeatherPy/Maximum%20Temperature%20vs%20Latitude%2019_Oct_2020.png)

The splatter chart illustrated the relationship between Maximum temperature and latitude as expected:

> Maximum daily temperature in October is higher near the equator, as one would suspect!
> The northern hemisphere has many more cities than the southern hemisphere, which is shown by the asymmetry of the data points
> Also there are more far northern cities than far southern cities which is illustrated by the lack of datapoints south of -60 degree latitude

#### The second plot compared Humidity vs Latitude
Figure 2 - Humidity (%) vs Latitude 19_Oct_2020

![HumidityvsLat](https://github.com/SJLimburg/python-api-challenge/blob/main/WeatherPy/Humidity%20(%25)%20vs%20Latitude%2019_Oct_2020.png)

> Humidty has no discernable relationship to latitude

#### The third plot compared Cloudiness (%) vs. Latitude
Figure 3 - Cloudiness (%) vs Latitude 19_Oct_2020

![cloudsvsLat](https://github.com/SJLimburg/python-api-challenge/blob/main/WeatherPy/Cloudiness%20(%25)%20vs%20Latitude%2019_Oct_2020.png)

> Cloudiness shows no visible relationship to latitude - wind patterns and water features are more likely to affect cloud formation

#### The fourth/final plot compared Wind Speed (mph) vs. Latitude
Figure 4 - Wind Speed (mph) vs Latitude 19_Oct_2020

![WindvsLat](https://github.com/SJLimburg/python-api-challenge/blob/main/WeatherPy/Wind%20Speed%20(mph)%20vs%20Latitude%2019_Oct_2020.png)

> Wind speed is relatively mild across all data points at this date in October 


## VacationPy

Now that the data for the cities from weatherPy has all the data for the next step; Finding the dream vacation spot based on weather. This requires converting the personal preferences into methods of selecting the desired data.

Use Pandas to read the cities from the previopus step into a DataFrame then proceed.

## Use Gmaps to map our dataset - follows the next steps to produce the desired map

- Configure gmaps
- Use the Lat and Lng as locations and Humidity as the weight
- Add Heatmap layer to map

#### GMAPS Humidity Heatmap
Figure 2.1 - Humidity heat map

![heatmap](https://github.com/SJLimburg/python-api-challenge/blob/main/output_data/Humidity%20Heat%20map.PNG)

#### Create new DataFrame fitting weather criteria as defined by my preferences - also drop null values

> Since I am a redhead I need some clouds but not so much that it signals rain
> I also do not like too much heat so 65-75 is my range 
> I need a little breeze too

##### My Pandas code looked like this as a result of my weather preferences - others may prefer more stillness or higher temperatires

>>  dream_df = my_city_df.loc[my_city_df['Max Temp'] < 75, :]
>>  dream_df = dream_df.loc[dream_df['Max Temp'] > 65, :]
>>  dream_df = dream_df.loc[dream_df['Wind Speed'] < 15, :]
>>  dream_df = dream_df.loc[dream_df['Wind Speed'] > 2, :]
>>  dream_df = dream_df.loc[dream_df['Cloudiness'] < 30, :]
>>  dream_df = dream_df.loc[dream_df['Cloudiness'] > 10, :]
>>  dream_df.dropna()

#### Weather is important and so is a place to stay. The next step looked for hotels using google nearby API.

The first step used numpy to populate Nan values into a new "Hotel" field in the Pandas DataFrame
Next parameters were set  to search for hotels within 5000 meters of our lat/Lng values.
Using Google Places API for each city's coordinates, the first Hotel result was stored into the DataFrame.
Finally using HTML code we set up an info_box_template to record data into markers on top of the heatmap and generate the markers

#### Using the template add the hotel marks to the heatmap

> info_box_template = """
> <dl>
> <dt>Name</dt><dd>{Hotel}</dd>
> <dt>City</dt><dd>{City}</dd>
> <dt>Country</dt><dd>{Country}</dd>
> </dl>
> """

> hotel_info = [info_box_template.format(**row) for index, row in hotel_df.iterrows()]
> locations = hotel_df[["Lat", "Lng"]]

- Add marker layer ontop of heat map
- Assign the marker layer to a variable
- Add the layer to the map

>>  markers = gmaps.marker_layer(locations,info_box_content = hotel_info)
>>  heat_map.add_layer(markers)
>>  heat_map

#### Display figure 2.2 - Off to Madagascar!

![Vacation](https://github.com/SJLimburg/python-api-challenge/blob/main/output_data/vacation%20map2.PNG)
