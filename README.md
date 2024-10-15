# UberRidesPeru
Uber trips dataset from Peru in 2010.
\\
This is a dataset uses a subset of samples from the Mobility Uber Perú dataset found at: https://www.kaggle.com/datasets/marcusrb/uber-peru-dataset
The original dataset is extended with additional features relating to the context of the date of the ride as well as the current weather at the location and time of each ride.
The weather information was extracted using the OpenWeatherMap API: https://openweathermap.org/
All additional contextual features and pre-processing are detailed below.

# Key Features
- **Trip ID (unique)**: the unique trip ID from the original.
- **Worker ID**: a simple integer ID for each of the 18 drivers.
- **driver_id**: the original driver ID in the Kaggle dataset.
- **start_type**: the type of the ride	(asap, reserved, or delayed). START_TYPE is an integer representation for this feature.
- **MONTH, DAY, YEAR, HOUR, MINUTE**: the date and time of the ride.
- **HOLIDAY**: 1 if the date was a public holiday in Peru. 0 otherwise.
- **DAYOFWEEKNUM**: integer representing the day of the week.
- **WEEKEND**: 1 if the date was a weekend. 0 otherwise.
- **start_X, start_Y, end_X, end_Y**: the coordinates of the start location and end location of each trip (in kilometers).
- **DRIVER_CANCELLED**:	1 if the driver cancelled the ride after accepting it. 0 if ride was completed.
- **DRIVER_REP**: rating of the driver at the time of the ride (float between 0-5).
- **REQUESTER_REP**: rating of the customer at the time of the ride (float between 0-5).
- **RAIN**: 1 if there was rain. 0 otherwise.
- **CLEARSKY**: 1 if there was a clear sky. 0 otherwise.
- **LIGHTCLOUDS**: 1 if there were light clouds. 0 otherwise.
- **HEAVYCLOUDS**: 1 if there were heavy clouds. 0 otherwise.
- **TEMPERATURE**: the average temperature of the day (in degrees K).
- **FEELSLIKE**: the 'feels like' temperature of the day (in degrees K).
- **PRESSURE**:	the atmospheric pressure of the day (in hPa).
- **HUMIDITY**:	the humidity level (percentage).
- **DEWPOINT**:	the dew-point temperature of the day (in degrees K).
- **WINDSPEED**: the wind speed of the day (in meters per second).
- **WINDDIR**: the wind direction of the day (in degrees, meteorological).
- **CLOUDPERC**: the percentage of clouds in the sky (percentage).
- **NUM_RIDES_COMPLETED_TODAY**: the number of rides that the driver has completed so far on this day.



# Pre-Processing 
1. From the Kaggle dataset, extracted rides with 'end_state'=='drop off' or 'end_state'=='driver cancel'.
2. Only consider drivers with 6 or more cancelled rides and more than 100 total rides. Resulting in 18 unique drivers.
3. Parse date and time. Append date context (example: weekends and holidays)
4. Convert latitude and longitude to x-y coordinates. Translate coordinates between 0 and 100 km.
5. Append weather data using OpenWeatherMap API.
6. Compute and append the driver and requester ratings at the time of the ride based on the average rating of preceding rides. If there is no history, assume the rating was 5.
7. For each ride, compute and append the number of rides completed by the driver that day prior to this ride.
