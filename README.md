![image](https://github.com/dmamontova/andan-project/assets/121117316/8052d70c-b2cf-43fb-bf55-9c0a444957f8)
## Привет, мой единственный читатель! 
### Над этим проектом кровью и потом трудились:
- Старощук Богдан
- Фоменко Андрей
- Мамонтова Дарья

Проект посвящен анализу влияния различных видов насилия против гражданского населения и политических конфликтов на экономику страны, для этого мы будем использовать крупные датасеты с классфикацией и краткой характеристикой событий отсюда: https://acleddata.com/about-acled/. 
Эти данные мы дополнили индексом человеческого развития (HDI) и классификацией страны (country classifications by income level).

Основная цель работы - проверка гипотезы о том, что ненасильственные политические столкновения сведетельствуют о высоком развитии страны, а также применение методов машинного обучения для предсказания класса страны, а также уровня HDI

Для более удобного восприятия, мы разделили работу над проектом на несколько осмысленных частей.

# 1. Парсинг

Для получения данных об индексе человческого развития и экономической классификации стран за интересующий период мы запарсили следующие сайты с необходимой информацией: 
https://countryeconomy.com/hdi?year=1997 - HDI, 
https://datatopics.worldbank.org/world-development-indicators/the-world-by-income-and-region.html - классификация

На выходе мы получили [таблицу](https://drive.google.com/file/d/1O3jwPG2JOHn5F90vUD4X7JsYtyZNSIrM/view?usp=share_link), с которой будем работать на дальнейших этапах. 
> Она достаточная большая, поэтому по ссылке залита на диск

Часть с парсингом залита в этой [папке](https://github.com/dmamontova/andan-project/tree/87a7f0d3a5f77ad247e396c24bead5b56523d917/parsing)

# 2. EDA

На этом этапе мы разделили всю работу на несколько частей.

Теперь подробнее:

[EDA I](https://github.com/dmamontova/andan-project/blob/main/EDA/EDA%20I.ipynb). В этом файле была проведена первичная предобработка данных: описание переменных, анализ таблицы на пропуски и их заполнение.

[EDA II.1](https://github.com/dmamontova/andan-project/blob/main/EDA/EDA%20II.1.ipynb) Здесь мы рассмотрели определённые категориальные переменные в отдельности, построили визуализации для них.

[EDA II.2](https://github.com/dmamontova/andan-project/blob/main/EDA/EDA%20II.2.ipynb) В этой части были рассмотрены внутренние связи между категориальными переменными

[EDA III](https://github.com/dmamontova/andan-project/blob/main/EDA/EDA%20III.ipynb) Завершающий этап, с рассмотрением числовых переменых и визуализацией

# 3. Гипотезы и машинное обучение

Попытаемся проверить следующую гипотизу:

$H_0: \mu_1 > \mu_2$

$H_1: \mu_1 = \mu_2$

Где $\mu_1$  - математическое ожидание индекса для стран, где доминируют ненасильственные конфликты, a $\mu_2$ наоборот. Тогда $H_0$ - страны с ненасильственными конфликтами в среднем богаче, а $H_1$ - отсутствие устойчивой разницы 

При помощи моделей градиентого бустинга попытаемся решить задачу классификации стран на группы, а так же задачу регрессии для предсказания индекса HDI





