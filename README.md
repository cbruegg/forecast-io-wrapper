Forecast.io Java Wrapper [![Build Status](https://travis-ci.org/MartinSeeler/forecast-io-wrapper.png?branch=master)](https://travis-ci.org/MartinSeeler/forecast-io-wrapper)
===================

> A Java wrapper library for the v2 Forecast API provided by The Dark Sky Company, LLC.

##About

The Forecast API lets you query for most locations on the globe, and returns:

- Current conditions
- Minute-by-minute forecasts out to 1 hour (where available)
- Hour-by-hour forecasts out to 48 hours
- Day-by-day forecasts out to 7 days

##Samples

A simple request for the current temperature:
```java
// specify your API key
final String apiKey = "replace-with-your-key";
final ForecastIO forecastIO = new ForecastIO(apiKey);

// coordinates for Dresden, Germany
final double latitude = 51.0504d;
final double longitude = 13.7373d;

// retrieve the current forecast
final Forecast forecast = forecastIO.getForecast(latitude, longitude);

System.out.println("Current temperature is " + forecast.getCurrently().getTemperature());
System.out.println("Apparent temperature is " + forecast.getCurrently().getApparentTemperature());
```

Get sunrise and sunset time for the specified timezone:
```java
// specify your API key
final String apiKey = "replace-with-your-key";
final ForecastIO forecastIO = new ForecastIO(apiKey);

// coordinates for New York, New York, United States
final double latitude = 40.7142d;
final double longitude = -74.0064d;

// retrieve the current forecast
final Forecast forecast = forecastIO.getForecast(latitude, longitude);

// get current day block
final DailyDataPoint today = forecast.getDaily().getDataPoints()[0];

// java is expecting milliseconds, so we have to multiply the timestamp with 1.000
final Date sunriseDate = new Date(today.getSunriseTime() * 1000L);
final Date sunsetDate = new Date(today.getSunsetTime() * 1000L);

// prepare time format
final SimpleDateFormat isoFormat = new SimpleDateFormat("HH:mm:ss");
isoFormat.setTimeZone(TimeZone.getTimeZone(forecast.getTimezone()));

System.out.println("Sunrise today was at " + isoFormat.format(sunriseDate));
System.out.println("Sunset today will be at " + isoFormat.format(sunsetDate));
```

## Scala

If you`d like to use Scala instead, have a look at [forecast-io-scala](https://github.com/knutwalker/forecast-io-scala), which runs on top of [Akka](http://akka.io).