# Виртуальное окружение

## Задача 1

```python
import requests
response = requests.get('https://docs.python.org/')
print(response.status_code)
```

## Задача 2

```python
import pyscreenshot
import time
import os

os.chdir("C:\scr")
for i in range(5):
    time.sleep(5)
    image = pyscreenshot.grab()
    image.save("scr" + str(i) + ".png", sep='')
```

## Задача 3

```python
import psutil
import pyttsx3

battery = psutil.sensors_battery()
percent = str(battery.percent)
print('Состояние батареи: осталось' + percent + '% заряда')
if battery.percent < 100:
    engine = pyttsx3.init()
    voices = engine.getProperty('voices')
    engine.setProperty('voice', voices[0].id)
    engine.say('Низкий заряд батареи')
    engine.runAndWait()
 ```

## Задача 4

```python
from win11toast import toast
from datetime import datetime

def validate_time(alarm_time):
    if len(alarm_time) != 5:
        return 'Неверный формат'
    else:
        if int(alarm_time[0:2]) > 23:
            return 'Неверный формат часов'
        elif int(alarm_time[3:5]) > 59:
            return 'Неверный формат минут'
        else:
            return True

while True:
    alarm_time = input("Укажите время будильника в формате 'HH:MM' \nВремя будильника: ")
    validate = validate_time(alarm_time)
    if validate:
        name = input('Введите название: ')
        print(f'Будильник установлен на время {alarm_time}')
        break
    else:
        print(validate)

alarm_HH = int(alarm_time[0:2])
alarm_MM = int(alarm_time[3:5])

while True:
    now = datetime.now()
    current_hour = now.hour
    current_min = now.minute
    if alarm_HH == current_hour:
        if alarm_MM == current_min:
            toast('Будильник', name, button='Выключить', audio='C:\Windows\Media\Alarm01.wav')
            break
```

## Задача 5

```python
import os
from dotenv import load_dotenv

load_dotenv()
USERNAME = os.getenv("USERNAME")
PASSWORD = os.getenv("PASSWORD")
API_KEY = os.getenv("API_KEY")

print(USERNAME, PASSWORD, API_KEY)
```
