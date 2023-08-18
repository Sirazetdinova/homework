# Сетевые запросы

Задачи:

1) NASA API
    
2) IP Geolocation API

3) API Calc

4) API Harry Potter

5) Translate API

6) ChatGPT API

## Задача 1

[NASA API]:#

[https://api.nasa.gov/]

```python
import requests
from nasapy import Nasa
from PIL import Image

api_key = 'EkfE8zX5HeEqn6v0nYFW5hYcFGdXQfp7bJsw8QM7'
nasa = Nasa(key=api_key)

today = '2022-08-17'
today_data = nasa.epic(date = today)
print(today_data)

today = today.replace('-','/')
index=0
for data in today_data:
    print(data['image'])
    response = requests.get(f'https://api.nasa.gov/EPIC/archive/natural/{today}/png/{data["image"]}.png?api_key={api_key}')
    file = open(f'image{str(index)}.png','wb')
    file.write(response.content)
    file.close()
    index+=1


photos = []
for num in range(11):
    photo = Image.open(f'image{num}.png')
    photos.append(photo)

photos[0].save(
    'earth.gif',
    save_all=True,
    append_images=photos[1:],
    optimize=True,
    duration=300,
    loop=0
)
```
# Задача 2

[IP Geolocation API on Map]: #

[https://www.geoapify.com/ip-geolocation-api]

```python
import requests
import folium

ip='104.21.84.214'
url ='http://ip-api.com/json/' + ip
response = requests.get(url).json()
a = response['lat']
b = response['lon']

point = folium.Map(location=[a, b], zoom_start=12)
folium.Marker(location=[a, b], popup = 'my_point').add_to(point)
point.save("point.html")
```

# Задача 3

[Translate API - NLP Cloud]: #

Аналог GPT: [https://nlpcloud.com/home/playground/]

```python
import nlpcloud

api_key = 'f10cf43ebc1c2d3ad3703c7c01903d91664e2b26'

client = nlpcloud.Client('stable-diffusion', api_key, True, 'en')
link = client.image_generation("""Lions roller skating in the square New York.""")
print(link)

prompts = ['proggrammer sitting in African savannah', 'an oil painting of a fox in the snow']
for prompt in prompts:
    l=client.image_generation(prompt)
    print(l)
```



