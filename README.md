import sqlite3
import requests
import time
from datetime import datetime
import tkinter as tk
from tkinter import messagebox

# Створення БД
conn = sqlite3.connect("exchange_rates.db")
cursor = conn.cursor()
cursor.execute("""
CREATE TABLE IF NOT EXISTS exchange_rate (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp TEXT,
    usd_rate REAL
)
""")
conn.commit()

# Функція для отримання курсу долара (замініть URL на актуальний сайт НБУ)
def get_usd_rate():
    response = requests.get("https://bank.gov.ua/NBUStatService/v1/statdirectory/exchange?valcode=USD&json")
    if response.status_code == 200:
        try:
            data = response.json()
            return float(data[0]["rate"])
        except (ValueError, KeyError, IndexError):
            return None
    return None

# Функція для додавання запису в БД
def insert_exchange_rate():
    usd_rate = get_usd_rate()
    if usd_rate is not None:
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        cursor.execute("INSERT INTO exchange_rate (timestamp, usd_rate) VALUES (?, ?)", (timestamp, usd_rate))
        conn.commit()
        print(f"[{timestamp}] Додано курс USD: {usd_rate} грн")
    else:
        print("Не вдалося отримати курс валют.")

# Функція для конвертації
class CurrencyConverter:
    def __init__(self, rate):
        self.rate = rate
    
    def convert_to_usd(self, amount):
        return round(amount / self.rate, 2)

# Графічний інтерфейс
def convert_currency():
    try:
        amount = float(entry.get())
        rate = get_usd_rate()
        if rate:
            converter = CurrencyConverter(rate)
            result = converter.convert_to_usd(amount)
            messagebox.showinfo("Результат", f"{amount} грн = {result} USD")
        else:
            messagebox.showerror("Помилка", "Не вдалося отримати курс валют")
    except ValueError:
        messagebox.showerror("Помилка", "Введіть коректне число")

# GUI налаштування
root = tk.Tk()
root.title("Конвертер Валюти")

tk.Label(root, text="Введіть суму в грн:").pack()
entry = tk.Entry(root)
entry.pack()
tk.Button(root, text="Конвертувати", command=convert_currency).pack()

root.mainloop()

# Запуск циклічного оновлення
try:
    while True:
        insert_exchange_rate()
        time.sleep(1800)  # Оновлення раз на 30 хвилин
except KeyboardInterrupt:
    print("Зупинено користувачем.")
    conn.close()
