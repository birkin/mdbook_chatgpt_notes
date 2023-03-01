# Code example - python weather-api

## Show an example of python code accessing a weather-api to get the forecast for a city.


Sure, here's an example Python code using the OpenWeatherMap API to get the current weather for a city:

(python)

```
import requests

# Enter your API key and the city you want to get the weather for
api_key = 'YOUR_API_KEY'
city = 'New York'

# Call the API and get the weather data
url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
response = requests.get(url)
data = response.json()

# Extract the relevant information from the JSON response
weather_description = data['weather'][0]['description']
temperature = data['main']['temp']
humidity = data['main']['humidity']

# Print the results
print(f'Current weather in {city}:')
print(f' - Description: {weather_description}')
print(f' - Temperature: {temperature}°C')
print(f' - Humidity: {humidity}%')
```

In this example, you need to replace YOUR_API_KEY with your actual OpenWeatherMap API key. You can sign up for a free API key on the OpenWeatherMap website.

The code sends a GET request to the OpenWeatherMap API endpoint with the city name and API key. It then extracts the relevant information from the JSON response and prints it out. This is just a basic example, but you can modify the API request to get more information or use a different weather API altogether.

## update that to show code to access the weather for two cities.

Sure, here's an example Python code that accesses the OpenWeatherMap API to get the current weather for two cities:

(python)

```
import requests

# Enter your API key and the cities you want to get the weather for
api_key = 'YOUR_API_KEY'
cities = ['New York', 'London']

# Loop through each city and call the API to get the weather data
for city in cities:
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    response = requests.get(url)
    data = response.json()

    # Extract the relevant information from the JSON response
    weather_description = data['weather'][0]['description']
    temperature = data['main']['temp']
    humidity = data['main']['humidity']

    # Print the results for each city
    print(f'Current weather in {city}:')
    print(f' - Description: {weather_description}')
    print(f' - Temperature: {temperature}°C')
    print(f' - Humidity: {humidity}%')
```

In this updated example, we create a list of two cities and loop through each city to call the OpenWeatherMap API and extract the relevant weather information. The rest of the code is very similar to the previous example.

You can modify the code to include more cities by adding them to the cities list. Just keep in mind that the more cities you include, the longer it will take to make all the API calls and get the weather data.

## update that to show code that would get the weather-api data for both cities simultaneously.

Sure! Here's an updated example that uses the concurrent.futures module to send requests to the OpenWeatherMap API for both cities simultaneously:

(python)

```
import requests
import concurrent.futures

# Enter your API key and the cities you want to get the weather for
api_key = 'YOUR_API_KEY'
cities = ['New York', 'London']

# Define a function to get the weather data for a single city
def get_weather(city):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    response = requests.get(url)
    data = response.json()

    # Extract the relevant information from the JSON response
    weather_description = data['weather'][0]['description']
    temperature = data['main']['temp']
    humidity = data['main']['humidity']

    # Return the results as a dictionary
    return {
        'city': city,
        'description': weather_description,
        'temperature': temperature,
        'humidity': humidity
    }

# Use a ThreadPoolExecutor to send requests for both cities simultaneously
with concurrent.futures.ThreadPoolExecutor() as executor:
    # Submit a task for each city and get the results
    results = executor.map(get_weather, cities)

# Print the results for each city
for result in results:
    print(f'Current weather in {result["city"]}:')
    print(f' - Description: {result["description"]}')
    print(f' - Temperature: {result["temperature"]}°C')
    print(f' - Humidity: {result["humidity"]}%')
```

In this example, we define a function called get_weather that takes a city name, sends a request to the OpenWeatherMap API, and returns the relevant weather information as a dictionary.

We then use a ThreadPoolExecutor to send requests for both cities simultaneously, by submitting a task for each city to the executor. The executor.map method returns an iterator that yields the results of each task as they complete.

Finally, we loop through the results and print the weather information for each city.

Using concurrent.futures allows us to send requests for both cities at the same time, which can significantly reduce the amount of time it takes to get the weather data for multiple cities.

## update that code to use python's asyncio package.

Sure! Here's an example that uses Python's asyncio package to asynchronously get the weather data for both cities:

(python)

```
import aiohttp
import asyncio

# Enter your API key and the cities you want to get the weather for
api_key = 'YOUR_API_KEY'
cities = ['New York', 'London']

# Define a coroutine to get the weather data for a single city
async def get_weather(session, city):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    async with session.get(url) as response:
        data = await response.json()

    # Extract the relevant information from the JSON response
    weather_description = data['weather'][0]['description']
    temperature = data['main']['temp']
    humidity = data['main']['humidity']

    # Return the results as a dictionary
    return {
        'city': city,
        'description': weather_description,
        'temperature': temperature,
        'humidity': humidity
    }

async def main():
    async with aiohttp.ClientSession() as session:
        # Create a list of coroutines to get the weather for each city
        coroutines = [get_weather(session, city) for city in cities]

        # Wait for all the coroutines to complete and get the results
        results = await asyncio.gather(*coroutines)

        # Print the results for each city
        for result in results:
            print(f'Current weather in {result["city"]}:')
            print(f' - Description: {result["description"]}')
            print(f' - Temperature: {result["temperature"]}°C')
            print(f' - Humidity: {result["humidity"]}%')

# Run the main coroutine to get the weather data for both cities
asyncio.run(main())
```

In this example, we define an async function called get_weather that takes a session and a city name, sends a request to the OpenWeatherMap API using the session, and returns the relevant weather information as a dictionary.

We then create a ClientSession using aiohttp, create a list of coroutines to get the weather for each city, and use asyncio.gather to wait for all the coroutines to complete and get the results.

Finally, we loop through the results and print the weather information for each city.

Using asyncio allows us to asynchronously send requests for both cities, which can significantly reduce the amount of time it takes to get the weather data for multiple cities.

## update that code to use the async "trio" python package.

Certainly! Here's an example that uses the trio package to asynchronously get the weather data for both cities:

(python)

```
import asks
import trio

# Enter your API key and the cities you want to get the weather for
api_key = 'YOUR_API_KEY'
cities = ['New York', 'London']

# Define an async function to get the weather data for a single city
async def get_weather(city):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric'
    response = await asks.get(url)
    data = response.json()

    # Extract the relevant information from the JSON response
    weather_description = data['weather'][0]['description']
    temperature = data['main']['temp']
    humidity = data['main']['humidity']

    # Return the results as a dictionary
    return {
        'city': city,
        'description': weather_description,
        'temperature': temperature,
        'humidity': humidity
    }

async def main():
    # Create a nursery for the trio
    async with trio.open_nursery() as nursery:
        # Create a list of tasks to get the weather for each city
        tasks = [nursery.start_soon(get_weather, city) for city in cities]

        # Wait for all the tasks to complete and get the results
        results = await trio.gather_all(*tasks)

        # Print the results for each city
        for result in results:
            print(f'Current weather in {result.result()["city"]}:')
            print(f' - Description: {result.result()["description"]}')
            print(f' - Temperature: {result.result()["temperature"]}°C')
            print(f' - Humidity: {result.result()["humidity"]}%')

# Run the main function using the trio.run method
trio.run(main)
```

In this example, we define an async function called get_weather that takes a city name, sends a request to the OpenWeatherMap API using the asks library, and returns the relevant weather information as a dictionary.

We then create a nursery using trio and create a list of tasks to get the weather for each city. We use trio.gather_all to wait for all the tasks to complete and get the results.

Finally, we loop through the results and print the weather information for each city.

Using trio allows us to asynchronously send requests for both cities, which can significantly reduce the amount of time it takes to get the weather data for multiple cities.

---