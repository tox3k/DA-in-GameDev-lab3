# DA-in-GameDev-lab3
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Колчин Андрей Алексеевич
- РИ-220950
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Разработать десять уровней игры Dragon Picker, распределив значения переменных так чтобы сложность возрастала от уровня к уровню

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 
Ход работы:
- Поизучав структуру проекта я заметил, что в скрипте EnemyDragon.cs есть переменные, отвечающие за частоту спавна яиц, скорость движения дракона, а также шанс изменить направление его движения:
![image](https://github.com/tox3k/DA-in-GameDev-lab3/assets/146218000/73e2a0af-cdab-45aa-98cc-a722b3555e21)
![image](https://github.com/tox3k/DA-in-GameDev-lab3/assets/146218000/5746baa0-a218-426c-8095-fb8d497df3d9)

Именно эти переменные я и выберу в качестве параметров, определяющих уровень сложности.
  Создам таблицу для распределения баланса уровней сложности.
  (за 1 уровень сложности я выбрал величины в 2 раза большие/меньшие(зависит от переменной), чем в изначальном проекте(стало в 2 раза легче))
  Методом ~~научного тыка~~ проб и ошибок было выявлено, что максимально играбельные значения (лично для меня) - это: 
  Скорость дракона: 20, 
  Время между спавном яиц: 0.3
  Шанс сменить направление: 10% (0.1)
![image](https://github.com/tox3k/DA-in-GameDev-lab3/assets/146218000/6982c619-d740-46d0-a5bf-f7fa2bf7d437)


а вот и сама табличка: https://docs.google.com/spreadsheets/d/1Qbvla0Osdm6UUfSFoRWp0lqy8FKmxTS0kaZJkE6lUck/edit?usp=sharing

## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

- Я создал 10 сцен, параллельно меняя уровни сложности, согласно приведенной выше таблице.
![image](https://github.com/tox3k/DA-in-GameDev-lab3/assets/146218000/b53792b9-2991-4665-8791-1e8cf51e07b8)



## Задание 3
### Решение в 80+ баллов должно заполнять google-таблицу данными из Python. В Python данные также должны быть визуализированы.

- Далее пишем скрипт (привет лаба номер 2), который заполнит нашу табличку GoogleDocs, а так же построит графики.

```py
import gspread
import numpy as np
import matplotlib.pyplot as plt
gc = gspread.service_account(filename='unitedatascience-c08f927977c4.json')
sh = gc.open("DragonDif")
spawn_rate = 2
speed = 2
change_direction = 0.01

spawn_rate_data = [2]
speed_data = [2]
change_direction_data = [0.01]

row = 2


def update_sheet():
    sh.sheet1.update(('B' + str(row)), str(round(spawn_rate, 2)).replace('.', ','))
    sh.sheet1.update(('C' + str(row)), str(speed))
    sh.sheet1.update(('D' + str(row)), str(round(change_direction, 2)).replace('.', ','))

update_sheet()
for i in range(0, 9):
    change_direction += 0.01
    change_direction_data.append(change_direction)
    speed += 2
    speed_data.append(speed)
    spawn_rate -= 0.2
    spawn_rate_data.append(spawn_rate)
    row += 1
    update_sheet()

plt.figure(figsize=(8, 8))
x = list(range(1, 11))

plt.plot(x, spawn_rate_data, label='Время между спавном яиц')
plt.plot(x, speed_data, label='Скорость дракона')
plt.plot(x, change_direction_data, label='Шанс изменения направления')

plt.legend()
plt.show()

```

Скрипт заполнил табличку и вывед на экран вот такой график:
![image](https://github.com/tox3k/DA-in-GameDev-lab3/assets/146218000/acb73cf1-f129-4152-a9b8-36171e4955a1)



## Выводы

В результате данной лабораторной работы я научился балансировать значения переменных для задания сложности уровня игры, а также вспомнил как заполнять гугл таблицы с помощью Python и Jupyter

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
