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

Figure 1 - Maximum Temperature vs Latitude 19_Oct_2020

![MaxTempvsLat](http://localhost:8888/files/WeatherPy/Maximum%20Temperature%20vs%20Latitude%2019_Oct_2020.png)

- Maximum daily temperature in October is higher near the equator, as one would suspect!
- The northern hemisphere has many more cities than the southern hemisphere, which is shown by the asymmetry of the data points
- Also there are more far northern cities than far southern cities which is illustrated by the lack of datapoints south of -60 degree latitude




