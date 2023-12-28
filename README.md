# Vue Weather Site

This is a simple weather application created using Vue.js. It allows users to check the current weather conditions for a specific location.

## Features

- **Current Weather:** Display the current weather conditions (temperature, humidity, wind speed, etc.) for a given location.
- **Search Functionality:** Users can search for weather by city name or ZIP code.
- **Responsive Design:** The app is designed to work seamlessly across various devices (desktop, tablet, mobile).

## Technologies Used

- **Vue.js:** Frontend JavaScript framework for building user interfaces.
- **OpenWeatherMap API:** Used to fetch weather data for locations.
- **Axios:** HTTP client for making API requests.
- **Bootstrap (optional):** Used for basic styling and layout.

## Getting Started

### Installation

1. Clone the repository: `git clone https://github.com/MellanieKP/WeatherSite`
2. `cd` into the project directory.
3. Install dependencies: `npm install`

### Configuration

1. Get an API key from [OpenWeatherMap](https://openweathermap.org/api) and replace `YOUR_API_KEY` in `src/utils/api.js` with your API key.
2. Install the vue framework [Quasar](https://quasar.dev/).

### Running the App

Run the app locally:

```
npm quasar dev
```

Open your browser and visit `http://localhost:8080` to see the app running.

## Usage

1. Enter a city name or ZIP code in the search bar.
2. Press Enter or click the search button to fetch the weather data.
3. View the current weather details for the entered location.

