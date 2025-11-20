# mini-weather-app
import requests
from config import API_KEY, BASE_URL

def get_weather(city):
    if not API_KEY:
        return "⚠️ API key missing! Add it to .env file."

    params = {"q": city, "appid": API_KEY, "units": "metric"}
    res = requests.get(BASE_URL, params=params)

    if res.status_code != 200:
        return "❌ City not found. Try again."

    data = res.json()
    name = data["name"]
    temp = data["main"]["temp"]
    humidity = data["main"]["humidity"]
    desc = data["weather"][0]["description"].title()

    return f"""
    🌤️ Weather Report for **{name}**
    --------------------------------
    🌡️ Temperature : {temp}°C
    💧 Humidity    : {humidity}%
    🌥️ Condition   : {desc}
    """

if __name__ == "__main__":
    city = input("Enter a city name: ")
    print(get_weather(city))
