# Виртуальное окружение

## Задача 1

```python
pip show pip
pip --help
pip list
pip install numpy
pip show numpy
pip list
pip uninstall numpy
pip list
```

## Задача 2

```python
help('pyscreenshot')
from pyscreenshot import grab
dir(grab)
help(pyscreenshot.grab)
from pyscreenshot import save
dir(save)
help(pyscreenshot.save)

import pyscreenshot
import time
import os

os.chdir("C:\scr")
for i in range(5):
    time.sleep(5)
    image = pyscreenshot.grab()
    image.save("scr" + str(i) + ".png")
```

## Задача 3

```python
help('fuzzywuzzy')
from fuzzywuzzy import fuzz
dir(fuzz)
help(fuzz.ratio)

fuzz.ratio('Я разобрался с виртуальным окружением', 'Я разобрался с виртуальным окружением') 
fuzz.ratio('Я разобрался с виртуальным окружением!', 'Я разобрался с виртуальным окружением!')
fuzz.ratio('Я разобрался с виртуальным окружением?', 'Я разобрался с виртуальным окружением!')
 ```

## Задача 4

```python
help('psutil')
from psutil import sensors_battery
dir(sensors_battery)
help(psutil.sensors_battery)

help('pyttsx3')
from pyttsx3 import init
dir(init)
help(pyttsx3.init)
from pyttsx3 import say
dir(say)
help(pyttsx3.say)
from pyttsx3 import runAndWait
dir(runAndWait)
help(pyttsx3.runAndWait)

import psutil
import pyttsx3

battery = psutil.sensors_battery()
percent = str(battery.percent)
print('Состояние батареи: осталось' + percent + '% заряда')
if battery.percent <= 20:
    engine = pyttsx3.init()
    voices = engine.getProperty('voices')
    engine.setProperty('voice', voices[0].id)
    engine.say('Низкий заряд батареи')
    engine.runAndWait()
 ```

## Задача 5

```python
help('win11toast')
from win11toast import toast
dir(toast)
help(win11toast.toast)

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

## Задача 6

```python
import os
from dotenv import load_dotenv

load_dotenv()
USERNAME = os.getenv("USERNAME")
PASSWORD = os.getenv("PASSWORD")
API_KEY = os.getenv("API_KEY")

print(USERNAME, PASSWORD, API_KEY)
```
