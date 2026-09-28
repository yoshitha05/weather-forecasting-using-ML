# Weather Forecasting Using Machine Learning

A Django web app that shows live weather for any city and predicts the next 5 hours of temperature and humidity, plus whether it will rain tomorrow, using Random Forest models trained on historical weather data.

**Live demo:** https://weather-forecasting-using-ml.onrender.com

> Hosted on Render's free plan. If the site has been idle, the first load can take 30–60 seconds while the server wakes up.

## Features

- **Current weather** for any city: temperature, feels-like, min/max, humidity, cloud cover, wind, pressure and visibility (via the OpenWeatherMap API)
- **Rain prediction:** a Random Forest classifier predicts whether it will rain tomorrow
- **5-hour forecast:** Random Forest regressors predict hourly temperature and humidity
- **Interactive chart** of the forecast (Chart.js)
- **Dynamic backgrounds** that match the current conditions (clear, cloudy, rain, fog, snow, thunder and more)

## How it works

1. The user enters a city, and the app fetches its current conditions from OpenWeatherMap.
2. Historical data from `weather.csv` (366 daily records) is cleaned: missing values and duplicates are dropped, and categorical columns are label-encoded.
3. **Rain model:** `RandomForestClassifier` trained on `MinTemp`, `MaxTemp`, `WindGustDir`, `WindGustSpeed`, `Humidity`, `Pressure` and `Temp` to predict `RainTomorrow`.
4. **Temperature and humidity models:** `RandomForestRegressor` models learn how each value changes from one step to the next, then predict 5 steps ahead from the current reading.
5. Wind direction in degrees is converted to a 16-point compass direction so it matches the training data.
6. The results are shown on the page with a forecast chart.


## Project structure

```
weatherProject/
├── forecast/              # Django app
│   ├── static/            # CSS, JS (chart setup), background images
│   ├── templates/
│   │   └── weather.html   # Main page
│   ├── views.py           # API calls, ML models, predictions
│   └── urls.py
├── weatherProject/        # Project settings
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── weather.csv            # Historical weather dataset
├── manage.py
└── requirements.txt
```

## Run locally

**1. Clone the repo**
```bash
git clone https://github.com/yoshitha05/weather-forecasting-using-ML.git
cd weather-forecasting-using-ML
```

**2. Create a virtual environment and install dependencies**
```bash
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

**3. Run the server**
```bash
python manage.py migrate
python manage.py runserver
```

Open http://127.0.0.1:8000 and search for a city.

## Author

**Yoshitha**
