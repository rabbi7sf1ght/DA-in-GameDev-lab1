# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Нагнибеда Алиса Александровна
- РИ-210941
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
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения.
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello World на Python и Unity

1. Скриншот программы, написанной на Python в PyCharm:

![Скриншот 26-09-2022 013157](https://user-images.githubusercontent.com/113305087/192334358-0e4483c9-0784-41bd-a535-7bb0ade39b7e.jpg)

2. Скриншот программы, написанной на Unity:

![image](https://user-images.githubusercontent.com/113305087/192335708-f5f3ff88-3f4a-4c96-8221-150dbd58a6b5.png)

## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач.

Ход работы:
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

![image](https://user-images.githubusercontent.com/113305087/192359777-fed21ba0-1e14-4dbc-8cc8-8afa55d91118.png)

- Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

![image](https://user-images.githubusercontent.com/113305087/192363322-6bb02598-c2a3-4fc2-a40d-28df85944c84.png)

- Начать итерацию

1. Инициализация и модель итеративной оптимизации:

![image](https://user-images.githubusercontent.com/113305087/192367077-f166bd86-1d86-401d-a2f1-c4828172558b.png)
![image](https://user-images.githubusercontent.com/113305087/192458592-1490a9ee-1c3f-4cc7-a841-955ff282e057.png)

2. На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации:

![image](https://user-images.githubusercontent.com/113305087/192458806-a67719d6-e499-4827-9c2b-c55437b8c2b3.png)

3. Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации:

![image](https://user-images.githubusercontent.com/113305087/192459149-ea1ff3b8-de81-4eab-94ee-9e40afd0587d.png)

4. На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации:

![image](https://user-images.githubusercontent.com/113305087/192459375-87852522-9a80-4293-9422-373716b6bc63.png)

5. Пятая итерация показывает значения параметра, значения потерь и эффект визуализации после итерации:

![image](https://user-images.githubusercontent.com/113305087/192459515-2a35af57-f3fe-42c2-96e4-dbc18b0d2f04.png)

6. 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации:

![image](https://user-images.githubusercontent.com/113305087/192459650-00270eed-64ff-43be-8ba0-1c8e59e5d6c8.png)


## Задание 3
### Изучить код задач и ответить на вопросы:
1. Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Величина loss отображает то, какие потери были получены при вычислении линейной регрессии. Она должна стремиться к нулю при изменении количества итераций в большую сторону. Это можно подтвердить результатами итераций, представленными во втором задании (2-6 пункты). Чем больше итераций совершенно, тем точнее результат и тем меньше потери.
Привожу новые примеры того, как на loss влияет количество итераций (7, 100 и 4444 итераций):
![image](https://user-images.githubusercontent.com/113305087/192465992-fb97c351-b75b-4f68-aa4d-2fe0a26ae5cc.png)

Можно также предположить, что стремление loss к нулю зависит и от того факта, насколько явна зависимость между x и y. При изменении исходных данных на явную зависимость, я увидела то, что стремление loss к нулю становится более явным:

![image](https://user-images.githubusercontent.com/113305087/192468422-b4ed26ab-ae91-4619-a1ca-d91388b28825.png)

![image](https://user-images.githubusercontent.com/113305087/192468522-3541458e-21a1-4311-92bb-1a0579b8d1f6.png)

2. Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Lr - это параметр, отвечающий за изменения значений a и b, совершающиеся, каждый вызов функции optimize, а соответственно именно от него зависит изменение погрешности результатов: чем меньше значение параметра Lr, тем больше итераций понадобится для получения результата с наименьшей погрешностью. Для доказательства привожу скриншоты итераций с различным значением параметра Lr

Lr = 0.00003:

![image](https://user-images.githubusercontent.com/113305087/192464365-8782075a-3af8-4bfe-a7f7-6934e779fa9e.png)

Lr = 0.00001:

![image](https://user-images.githubusercontent.com/113305087/192464480-4624e2d4-11a1-4ff8-b1dc-1c82f4f9da66.png)

Lr = 0.0000001:

![image](https://user-images.githubusercontent.com/113305087/192464611-05b605d4-f1a2-4e3c-b170-ec947f26af2d.png)

Lr = 0.000000001:

![image](https://user-images.githubusercontent.com/113305087/192464726-20750a9a-f3a6-4af6-a37d-770784340b83.png)

На приведённых примерах выполнения кода заметна описанная выше зависимость. Однако важно отметить, что если значение Lr, отвечающее за изменения a и b в каждую итерацию, будет слишком большим, то это приведёт к возникновению ещё больших неточностей, чем слишком маленькое значение этого параметра. Привожу пример выполнения кода, за итерации которого a и b меняются так быстро, что это приводит к большим потерям и ошибкам:

![image](https://user-images.githubusercontent.com/113305087/192465590-dc7a0a9b-1d43-4039-9a5d-8d1e19ee7706.png)


## Выводы

Во время выполнения лабораторной работы, я смогла поработать с основными операторами языка Python, рассмотрев и проанализировав написанный на нём алгоритм линейной регрессии и изучив его возможности. Помимо этого, я смогла получше узнать возможности Google Colab и понять, насколько полезен он может быть для работы с алгоритмами языка Python. 


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
