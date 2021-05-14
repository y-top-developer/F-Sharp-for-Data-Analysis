---
marp: true

---

# F#4DS

## Загрузка и визуализация

[@anton_shumakov](https://t.me/anton_shumakov)

---

<!-- paginate: true -->

# F# или Python? [@fsharp_chat](https://t.me/fsharp_chat)

![image-20210514182448713](images\image-20210514182448713.png)

---

# Особенности F#

1. Поставщики типов
2. Функциональность
3. .NET

---

# Настройка удаленного окружения

[Binder](https://mybinder.org/v2/gh/dotnet/interactive/main?urlpath=lab)

![image-20210514055153166](images\image-20210514055153166.png)

![image-20210514055251714](images\image-20210514055251714.png)

---

# Настройка локального окружения c  [.NET Interactive](https://github.com/dotnet/interactive/)

```powershell
> python -m pip install jupyterlab
> dotnet tool install -g dotnet-try
> dotnet try jupyter install
> jupyter lab
```

![image-20210514053148947](images\image-20210514053148947.png)

[.NET Core with Jupyter Notebooks | devblogs.microsoft](https://devblogs.microsoft.com/dotnet/net-core-with-juypter-notebooks-is-here-preview-1/)

---

# Введение в Type Providers

```F#
type Person = 
  { Name:string; Age:int; Countries:string list; }
```

Стало:

![image-20210514064128489](images\image-20210514064128489.png)

---

# Type Providers для CSV

![image-20210514072154404](images\image-20210514072154404.png)

![image-20210514072608718](images\image-20210514072608718.png)

---

# Работа Type Providers с сетью

![image-20210514064417938](images\image-20210514064417938.png)

![image-20210514064927402](images\image-20210514064927402.png)

---

# Исследование API

https://freegeoip.app/json/

1. Какие есть поля в ответе?

2. В какой вы стране?

3. Как обработается ответ от https://xkcd.com/info.0.json ?

---

# Решение 

1. 

```F#
type GeoIp = JsonProvider<"https://freegeoip.app/json/">
let geoIp = GeoIp.GetSample()
geoIp.CountryName
```

2. 

![image-20210514132855321](images\image-20210514132855321.png)

3. 

![image-20210514134204360](images\image-20210514134204360.png)

---

# Применение Type Providers для смены формата

data.csv:

```csv
Title,Author,Average Rating                                                                              
Readme,Octocat,10
Robots.txt,Admin,3
Name,Author Name,3
Name2,Name2 Author,7
Some,Another,1
Another,Name,1
Titorial,Kio,10
```

---

# Применение Type Providers для смены формата

```F#
type Data = CsvProvider<"data.csv">
type BookTypes = JsonProvider<"sample.json">

Data.GetSample().Rows
|> Seq.sortByDescending (fun book -> ???)
|> Seq.take 5
|> Seq.map (fun book -> BookTypes.Root(???, ???))
BookTypes.GetSample()
```

1. Дополнить код так, чтобы он выделял 5 лучших по рейтингу книг и их авторов
2. Создать `sample.json` для поставщика JSON

---

# Применение Type Providers для смены формата

![image-20210514152840329](images\image-20210514152840329.png)

![image-20210514152859093](images\image-20210514152859093.png)

---

# Визуализация с [XPlot.Plotly](https://fslab.org/XPlot//chart/plotly-bar-charts.html)

![image-20210514081011416](images\image-20210514081011416.png)

---

# Виды графиков в XPlot.Plotly

|                                                         |                                                         |
| ------------------------------------------------------- | ------------------------------------------------------- |
| ![image-20210514081658968](images\image-20210514081658968.png) | ![image-20210514084037214](images\image-20210514084037214.png) |
| ![image-20210514082302804](images\image-20210514082302804.png) | ![image-20210514082549141](images\image-20210514082549141.png) |
| ![image-20210514082801286](images\image-20210514082801286.png) | ![image-20210514083233278](images\image-20210514083233278.png) |

---

# Анализ данных

![image-20210514161215289](images\image-20210514161215289.png)

---

# Анализ данных 

![image-20210514165021916](images\image-20210514165021916.png)

---

# Дополнительно

- https://www.oreilly.com/library/view/analyzing-and-visualizing/9781492048350 <- короткая книга
- https://www.youtube.com/watch?v=rmSgNJLLfSM <- F# for DATA ANALYSIS, 2017 год
- https://jvaneyck.wordpress.com/2017/06/19/exploring-data-and-apis-with-f-type-providers/ <- про поставщики типов

