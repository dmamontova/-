![image](https://github.com/dmamontova/andan-project/assets/121117316/8052d70c-b2cf-43fb-bf55-9c0a444957f8)
## Привет, мой единственный читатель! 
### Над этим проектом кровью и потом трудились:
- Старощук Богдан
- Фоменко Андрей
- Мамонтова Дарья

Проект посвящен анализу влияния различных видов насилия против гражданского населения и политических конфликтов на экономику страны, для этого мы будем использовать крупные датасеты с классификацией и краткой характеристикой событий отсюда: https://acleddata.com/about-acled/. 
Эти данные мы дополнили индексом человеческого развития (HDI) и классификацией страны (country classifications by income level).

Основная цель работы - проверка предположения о том, что ненасильственные политические столкновения свидетельствуют о высоком развитии страны, а также применение методов машинного обучения для предсказания класса страны и уровня HDI.

Для более удобного восприятия, мы разделили работу над проектом на несколько осмысленных частей.


# 1. [Парсинг](https://github.com/dmamontova/andan-project/tree/all-work_main/parsing)

С помощью парсинга мы получили информацию о следующих признаках:
- HDI или индекс человеческого развития. Подробная информация о том, как происходил парсинг этого индекса, содержится в [тетрадке](https://github.com/dmamontova/andan-project/blob/project_main/parsing/index_parse.ipynb). Стоит отметить, что данные были получены со следующего [сайта](https://countryeconomy.com/hdi?year=1997). На выходе мы получили таблицу с HDI по странам.
- Индекс экономической классификации. Опять же вся техническая часть залита в [ноутбук](https://github.com/dmamontova/andan-project/blob/project_main/parsing/parsing_income.ipynb). Также на этом этапе мы объединили полученные данные с тем, что получили касаемо HDI, в общую таблицу.

И, наконец, последний этап парсинга.

[Предобработка данных](https://github.com/dmamontova/andan-project/blob/project_main/parsing/final_predobr.ipynb). Немного поработали с тем, чтобы привести все полученные данные в аккуратный вид. На выходе мы получили [таблицу](https://drive.google.com/file/d/1O3jwPG2JOHn5F90vUD4X7JsYtyZNSIrM/view?usp=share_link), с которой будем работать на дальнейших этапах. 
> Она достаточная большая, поэтому по ссылке залита на диск

И теперь,сперва, неплохо было бы покапаться в наших данных и понять, что они из себя представляют.


# 2. [EDA](https://github.com/dmamontova/andan-project/tree/all-work_main/EDA)


На этом этапе мы разделили всю работу на несколько частей.

Теперь подробнее:

[EDA I](https://github.com/dmamontova/andan-project/blob/all-work_main/EDA/EDA%20I.ipynb). Для начала, мы провели первичную предобработку данных: описание переменных, анализ таблицы на пропуски и их заполнение, определение типов переменных, содержащихся в данных. 

После того как данные были подготовлены к дальнейшему анализу, мы решили рассмотреть категориальные и числовые переменные в отдельности, поискать взаимосвязи и построить понятные визуализации, поэтому:

[EDA II.1](https://github.com/dmamontova/andan-project/blob/all-work_main/EDA/EDA%20II.1.ipynb) Здесь мы рассмотрели определённые категориальные переменные в отдельности, а именно: Disorder_type, Event_type, Sub_event_type. Были выбраны именно они, так как, на наш взгляд, именно эти признаки обладают важной информацией, и понимание того, что они из себя представляют, поможет нам на этапе машинного обучения. Для лучшей интерпертируемости результатов, были построены гистограммы и диаграммы.

Очевидно, что рассмотрение категориальных признаков в отдельности недостаточно, хотелось бы посмотреть на них в комбинации с другими переменными, что мы и делали далее:

[EDA II.2](https://github.com/dmamontova/andan-project/blob/all-work_main/EDA/EDA%20II.2.ipynb) В этой части были рассмотрены внутренние связи между категориальными переменными. Кроме того, так как планируемой на этапе машинного обучения является задача классификации стран/регионов по экономическому индексу, мы рассмотрели целевую переменную в разрезе признаков, выделенных на предыдущем этапе. Так как мы использовали именно внутренние связи, самым удобным способом визуализации стали круговые диаграммы.

Ещё на первом этапе ED'ы мы обнаружили, что числовых признаков в наших данных не так уж и много, тем не менее, их без внимания мы тоже не оставили:

[EDA III](https://github.com/dmamontova/andan-project/blob/all-work_main/EDA/EDA%20III.ipynb) Завершающий этап с рассмотрением числовых переменых. В ходе работы мы выяснили, на какие года пришлось наибольшее количество конфликтов и, как следствие, выявили скорее возрастающий тренд в их количестве. Кроме того, используя в качестве визуализации интерактивную карту мира и данные из таблицы о координатах места события, выяснили, какие регионы наиболее сильно подвержены столкновениям. А также, конечно же, ввиду того, что ещё одной из целевых переменных является HDI, посмотрели на корреляцию числовых признаков с ней.

Теперь, когда мы потрогали данные, можно выдвинуть определённые гипотезы, проверка которых пригодится на следующих этапах.

# 4. [Проверка гипотез](https://github.com/dmamontova/andan-project/blob/all-work_main/Hypotheses.ipynb)


В первую очередь нас интересовали гипотезы, которые как-либо связанными с целевыми переменным: Index и Classification. Мы рассмотрели 5 основных гипотез, на основании которых сделали определённые выводы, и в зависимости от отвержения/ не отвержения $H_0$ сделали выводы о влиянии независимых признаков на целевые, а также о внутренних взаимосвязях.

После чего, мы приступили к самому сладкому этапу - создание новых признаков и машинное обучение.

# 5. [Создание признаков и машинное обучение](https://github.com/dmamontova/andan-project/tree/project_main/ML)

Для того чтобы обучаемые нами модели обладали хорошей предсказательной силой, мы создали новые важные и информативные признаки. В частности, например, была предложена собственная формула для расчёта степени тяжести конфликта на основе уже имеющихся переменных. Также, для дальнейшего обучения моделей, мы взяли отдельную подвыборку, проверив её репрезентативность с помощью теста Колмогорова-Смирнова. Более подробно можно ознакомиться в [этой тетрадке](https://github.com/dmamontova/andan-project/blob/project_main/ML/%D0%9D%D0%BE%D0%B2%D1%8B%D0%B5_%D0%BF%D1%80%D0%B8%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8ML.ipynb). 

После того как все подготовительные этапы сделаны, можно приступать к обучению моделей.

Ввиду того, что целевых переменных у нас две - Index и Classification, и они являются числовой и категориальной соответственно, были использованы модели из разных категорий. Теперь немного подробнее:

[Предсказание переменной Index](https://github.com/dmamontova/andan-project/blob/project_main/ML/%D0%A0%D0%B5%D0%B3%D1%80%D0%B5%D1%81%D1%81%D0%B8%D0%B8.ipynb). Так как целевая переменная Index является числовой, мы использовали вполне классические модели:линейную регрессию с регуляризацией и без, а также случайный лес(regressor). В итоге получили, что наиболее подходящей для нашей задачи оказалась модель случайного леса - именно она показала лучшее значение метрик MSE и MAE.

Более интересная картина получилась при построении прогнозов для переменной Classification.

[Предсказание переменной Classification](https://github.com/dmamontova/andan-project/blob/project_main/ML/%D0%9A%D0%BB%D0%B0%D1%81%D1%81%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8.ipynb). Так как эта переменная принимает только 4 значения, мы решали задачу многоклассовой классификации. Изначально, были рассмотрены типичные для этого модели: kNN, логистическая регрессия и случайный лес. Однако нельзя сказать, что какая-то из моделей справилась сильно лучше. Значения метрик качества были примерно равны. 

Тем не менее, нам захотелось всё же добиться улучшения основных метрик, поэтому было решено пустить в ход тяжелую артиллерию.

[Предсказание переменных Classification и Index](https://github.com/dmamontova/andan-project/blob/project_main/ML/%D0%A2%D0%B5%D0%BA%D1%81%D1%82_%D0%B8_%D0%B1%D1%83%D1%81%D1%82%D0%B8%D0%BD%D0%B3.ipynb). Удрученные неудачным опытом, мы решили слегка изменить подход к классификации. Во-первых, в дело пошёл раннее неиспользованный признак 'Notes', содержащий краткие сводки новостей о событиях. Текстовые данные были векторизированы, благодаря чему получилось так, что мы добавили еще больше признаков для обучения. Во-вторых, основной моделью стал CatBoost, который показал лучшие результаты и для задачи регрессии, и для задачи классификации.

Таким образом, мы проделали большую работу от сбора данных до обучения моделей.

Спасибо за внимание!
