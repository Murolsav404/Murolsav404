import sqlite3
import requests
import time
from datetime import datetime

# Створення БД
conn = sqlite3.connect("weather.db")
cursor = conn.cursor()
cursor.execute("""
CREATE TABLE IF NOT EXISTS weather (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp TEXT,
    temperature REAL
)
""")
conn.commit()

# Функція для отримання температури (замініть URL на актуальний сайт погоди)
def get_temperature():
    response = requests.get("https://wttr.in/?format=%t")
    if response.status_code == 200:
        try:
            return float(response.text.strip().replace("°C", ""))
        except ValueError:
            return None
    return None

# Функція для додавання запису в БД
def insert_weather_data():
    temperature = get_temperature()
    if temperature is not None:
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        cursor.execute("INSERT INTO weather (timestamp, temperature) VALUES (?, ?)", (timestamp, temperature))
        conn.commit()
        print(f"[{timestamp}] Додано температуру: {temperature}°C")
    else:
        print("Не вдалося отримати температуру.")

# Запуск циклічного оновлення
try:
    while True:
        insert_weather_data()
        time.sleep(1800)  # Оновлення раз на 30 хвилин
except KeyboardInterrupt:
    print("Зупинено користувачем.")
    conn.close()
