# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Нагнибеда Алиса Александровна
- РИ-210941
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 80 |
| Задание 2 | * | 20 |

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
Ознакомиться с интеграцией экономической системы в проект Unity и обучением ML-Agent.

## Задание 1
### Изучить работу данного преподавателем проекта для обучения программы простым, направленным на улучшение экономической системы действиям. Изменить параметры файла yaml-агента и определить какие параметры и как влияют на обучение модели.

**Ход раобты:**

1. Для начала работы над заданием я скачала и подробнее рассмотрела работу представленного преподавателем проекта:

![Скриншот 01-12-2022 110420](https://user-images.githubusercontent.com/113305087/205043858-387b0b68-f8dd-4edc-9767-f9f3b5512427.jpg)

Основные действия в этом проекте ложатся на шар - он пермещается между шахтой, в которой собирает золото, и городом, в котором он это золото продаёт по расчитываемой им цене. Код, который отвечает за эти действия:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class Move : Agent
{
    [SerializeField] private GameObject goldMine;
    [SerializeField] private GameObject village;
    private float speedMove;
    private float timeMining;
    private float month;
    private bool checkMiningStart = false;
    private bool checkMiningFinish = false;
    private bool checkStartMonth = false;
    private bool setSensor = true;
    private float amountGold;
    private float pickaxeСost;
    private float profitPercentage;
    private float[] pricesMonth = new float[2];
    private float priceMonth;
    private float tempInf;

    // Start is called before the first frame update
    public override void OnEpisodeBegin()
    {
        // If the Agent fell, zero its momentum
        if (this.transform.localPosition != village.transform.localPosition)
        {
            this.transform.localPosition = village.transform.localPosition;
        }
        checkMiningStart = false;
        checkMiningFinish = false;
        checkStartMonth = false;
        setSensor = true;
        priceMonth = 0.0f;
        pricesMonth[0] = 0.0f;
        pricesMonth[1] = 0.0f;
        tempInf = 0.0f;
        month = 1;
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(speedMove);
        sensor.AddObservation(timeMining);
        sensor.AddObservation(amountGold);
        sensor.AddObservation(pickaxeСost);
        sensor.AddObservation(profitPercentage);
    }

    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        if (month < 3 || setSensor == true)
        {
            speedMove = Mathf.Clamp(actionBuffers.ContinuousActions[0], 1f, 10f);
            Debug.Log("SpeedMove: " + speedMove);
            timeMining = Mathf.Clamp(actionBuffers.ContinuousActions[1], 1f, 10f);
            Debug.Log("timeMining: " + timeMining);
            setSensor = false;
            if (checkStartMonth == false)
            {
                Debug.Log("Start Coroutine StartMonth");
                StartCoroutine(StartMonth());
            }

            if (transform.position != goldMine.transform.position & checkMiningFinish == false)
            {
                transform.position = Vector3.MoveTowards(transform.position, goldMine.transform.position, Time.deltaTime * speedMove);
            }

            if (transform.position == goldMine.transform.position & checkMiningStart == false)
            {
                Debug.Log("Start Coroutine StartGoldMine");
                StartCoroutine(StartGoldMine());
            }

            if (transform.position != village.transform.position & checkMiningFinish == true)
            {
                transform.position = Vector3.MoveTowards(transform.position, village.transform.position, Time.deltaTime * speedMove);
            }

            if (transform.position == village.transform.position & checkMiningStart == true)
            {
                checkMiningFinish = false;
                checkMiningStart = false;
                setSensor = true;
                amountGold = Mathf.Clamp(actionBuffers.ContinuousActions[2], 1f, 10f);
                Debug.Log("amountGold: " + amountGold);
                pickaxeСost = Mathf.Clamp(actionBuffers.ContinuousActions[3], 100f, 1000f);
                Debug.Log("pickaxeСost: " + pickaxeСost);
                profitPercentage = Mathf.Clamp(actionBuffers.ContinuousActions[4], 0.1f, 0.5f);
                Debug.Log("profitPercentage: " + profitPercentage);

                if (month != 2)
                {
                    priceMonth = pricesMonth[0] + ((pickaxeСost + pickaxeСost * profitPercentage) / amountGold);
                    pricesMonth[0] = priceMonth;
                    Debug.Log("priceMonth: " + priceMonth);
                }
                if (month == 2)
                {
                    priceMonth = pricesMonth[1] + ((pickaxeСost + pickaxeСost * profitPercentage) / amountGold);
                    pricesMonth[1] = priceMonth;
                    Debug.Log("priceMonth: " + priceMonth);
                }

            }
        }
        else
        {
            tempInf = ((pricesMonth[1] - pricesMonth[0]) / pricesMonth[0]) * 100;
            if (tempInf <= 6f)
            {
                SetReward(1.0f);
                Debug.Log("True");
                Debug.Log("tempInf: " + tempInf);
                EndEpisode();
            }
            else
            {
                SetReward(-1.0f);
                Debug.Log("False");
                Debug.Log("tempInf: " + tempInf);
                EndEpisode();
            }
        }
    }

    IEnumerator StartGoldMine()
    {
        checkMiningStart = true;
        yield return new WaitForSeconds(timeMining);
        Debug.Log("Mining Finish");
        checkMiningFinish = true;
    }

    IEnumerator StartMonth()
    {
        checkStartMonth = true;
        yield return new WaitForSeconds(60);
        checkStartMonth = false;
        month++;

    }
}
```

Главная идея заключается в том, чтобы цена обязательно была выгодной. В это и заключается цель обучения - заставить систему расчитывать наиболее удачную цену. Обучение происходит при помощи Economic.yaml файла:

```
behaviors:
  Economic:
    trainer_type: ppo
    hyperparameters:
      batch_size: 1024
      buffer_size: 10240
      learning_rate: 3.0e-4
      learning_rate_schedule: linear
      beta: 1.0e-2
      epsilon: 0.2
      lambd: 0.95
      num_epoch: 3      
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    checkpoint_interval: 500000
    max_steps: 750000
    time_horizon: 64
    summary_freq: 5000
    self_play:
      save_steps: 20000
      team_change: 100000
      swap_steps: 10000
      play_against_latest_model_ratio: 0.5
      window: 10
```

2. Проведу обучение модели, запустив созданную ранее виртуальную среду, на которую уже загружены все необходимые пакеты - mlagents 0.28.0 и torch 1.7.1. Обучение начинаю проводить на ранее созданных двенадцати префабах:

![Скриншот 01-12-2022 132252](https://user-images.githubusercontent.com/113305087/205044850-cac59341-9ff6-45cc-b739-a1f82607666b.jpg)

Однако результат обучения был настолько медленным, что я посчитала важным увеличить количество полей до тридцати шести: 

![Скриншот 01-12-2022 132855](https://user-images.githubusercontent.com/113305087/205044962-faac9275-aeed-4f63-98a2-5d7855d72769.jpg)

Результаты в консоли были следующие:

![Скриншот 01-12-2022 135151](https://user-images.githubusercontent.com/113305087/205045078-f954e35f-345f-4adb-bd07-730a6f8656be.jpg)

3. Для более явной оценки результатов в виртуальное окружение была установлена TensorBoard:

![image](https://user-images.githubusercontent.com/113305087/205045359-1727b554-2b1d-4dfb-9690-dab0ac62a1cf.png)

В неё при помощи команды

```
tensorboard --logdir=results
```
были представлены результаты прошедшего обучения экономической системы:

![Скриншот 01-12-2022 141832](https://user-images.githubusercontent.com/113305087/205045837-05a02dea-a58e-496f-baa5-6fd9ebf8ce24.jpg)

![Скриншот 01-12-2022 141841](https://user-images.githubusercontent.com/113305087/205045888-58b235f0-7064-46ec-9278-7e00155cc8b8.jpg)

![Скриншот 01-12-2022 141906](https://user-images.githubusercontent.com/113305087/205046541-4cc31f05-4935-469b-900f-4e54deb1471c.jpg)

![image](https://user-images.githubusercontent.com/113305087/205048234-19887dd2-b715-4c28-bc93-bcf2e517fa5c.png)

Заметно, например, что значение награды довольно сильно скачет.

Попробуем провести над файлом Economic.yaml некоторые изменения и повторить операции обучения нашей экономической систем. Также проанализируем их, сравнив друг с другом.


**1 изменение:**

Изменение касается данной строчки кода:

```
strength: 1.0
->
strength: 2.3
```

Сравнение результатов начальной итерации (голубой цвет) и той, что была совершена после изменений (красный цвет):

![image](https://user-images.githubusercontent.com/113305087/205050206-88d25521-882f-4d4d-a3bc-c50d3bf7075a.png)

Видно, что за счет отрицательного скачка в значении награды, график наград получается менее стабильным. Однако, уже в середине значение награды увеличивается, тренировка быстро становится успешнее той, что была проведена ранее.

![image](https://user-images.githubusercontent.com/113305087/205052017-3ea2ed17-9172-4fc6-95e4-2ef37060947e.png)

Потери держатся на примерно равном уровне.

![image](https://user-images.githubusercontent.com/113305087/205053247-93fde180-00a7-47b2-8061-56396c356744.png)

Рейтинг ELO ниже.

В результате, обучение можно назвать как успешным, так и не совсем, но значение strength точно влияет на некоторые позиции. Изменения первого пункта были сохранены на протяжении дальнейших итераций.

**2 изменение:** 

Изменение касается данных строчек кода:

```
batch_size: 1024
buffer_size: 10240
>>>
batch_size: 2024
buffer_size: 20240
```

Так как изменения, совершенные в первую измененную итерацию, были сохранены, проведём сравнение именно с ней (первая операция - красный цвет, вторая - голубой):

![image](https://user-images.githubusercontent.com/113305087/205054341-9a1cc435-de43-4b9a-aef4-10b3145c03cd.png)

Значения наград стали хуже, значение продолжительности эпизода осталось таким же.

![image](https://user-images.githubusercontent.com/113305087/205054573-6746966e-97df-4a02-96ae-bf1be66d76a2.png)

Значения потерь стали меньше - успех в случае policy loss, относительная неудача в случае value loss.

![image](https://user-images.githubusercontent.com/113305087/205054688-3e1d7faa-eea4-43b7-b357-8af695dc9e47.png)

Изменения ELO неоднозначные.

Можно сделать вывод, что изменения повлияли на обучения скорее положительно, чем отрицательно. Изменения этих параметров в большую сторону благоприятно влияют на значения потерь.


**3 изменение:**

Изменения прошлого пункта были сброшены, теперь значения таковы:

```
batch_size: 1024
buffer_size: 10240
>>>
batch_size: 500
buffer_size: 5240
```

Сравнение приведём с прошлой, второй, итерацией (она - голубого цвета, новая - розового):

![image](https://user-images.githubusercontent.com/113305087/205055917-fd64619e-44e6-49d8-a2e6-33c5cb362e32.png)

Значение наград растёт в положительную сторону!

![image](https://user-images.githubusercontent.com/113305087/205056622-2903a034-7582-4b34-947c-4b293e85d7dc.png)

Однако потери принятия решений велики, а потери значений стремятся вниз.

![image](https://user-images.githubusercontent.com/113305087/205056885-a1101224-1fc3-4697-8e6b-d91c289ebbea.png)

ELO все на том же уровне.

Обучение можно было бы назвать успешным, если бы не тенденции изменения значений потерь.

**4 изменение:**

Для этого этапа изменений вернёмся к состоянию файла на момент первого пункта изменений. Теперь они коснутся этой строчки:

```
learning_rate: 3.0e-4
>>>
learning_rate: 4.0e-4
```

Сравнение будем проводить с графиками первых изменений (они - красный цвет, 4 изменение - тёмно зелёный):

![image](https://user-images.githubusercontent.com/113305087/205057557-7e4375bd-586e-4f5b-b628-9fbb24510172.png)

Изменений почти нет.

![image](https://user-images.githubusercontent.com/113305087/205058063-3ec24e9b-14b7-42de-a7c7-e202caf93804.png)

Потери уменьшаются - изменения в лучшую сторону для policy loss, не в самую лучшую для value loss.

![image](https://user-images.githubusercontent.com/113305087/205058767-81f35e3a-c205-4164-a336-22a7dc224640.png)

Значения ELO уменьшаются, но всё равно могут считаться более успешными.

Как итог это изменение оказало положительный эффект на обучение системы.


**5 изменение:**

```
gamma: 0.99
strength: 2.3
>>>
gamma: 0.90
strength: 0.7
```

Помимо уменьшения значения gamma были решено уменьшить значение strength. Так как изменения ближе к нулевой, изначальной итерации, сравнение будет проводиться именно с ней (нулевая итерация - синий цвет, пятая - оранжевый):

![image](https://user-images.githubusercontent.com/113305087/205060135-7b0d3030-b9ba-4255-99c7-10a7ddba65de.png)

Значения наград стали гораздо стабильнее и лучше.

![image](https://user-images.githubusercontent.com/113305087/205060224-4a465ded-d37a-4c9e-a7cb-36d2163b5f9b.png)

Потери в обоих графиках уменьшаются.

![image](https://user-images.githubusercontent.com/113305087/205060352-8f9149dc-e8d5-4e57-8c1a-86cb027f579c.png)

ELO не меняется, но держится на хорошем уровне.

Пятая операция оказалась успешной

+ Графики всех итераций из категории Policy:

![image](https://user-images.githubusercontent.com/113305087/205138346-87a9007c-9e39-479a-b65e-f2598f2d87aa.png)

![image](https://user-images.githubusercontent.com/113305087/205138425-c39f648b-7e0b-45ce-a8b6-0bf28df66e47.png)
![image](https://user-images.githubusercontent.com/113305087/205138478-00000c00-6209-46fb-b29c-5da1506d3de5.png)

Большую часть времени все они придут примерно одинаково, а значения в некоторых были указаны в самом yaml файле, поэтому для анализа ранее приведены не были.

**Вывод.** Стоит отметить, что пятые изменения в файле yaml оказались самыми успешными, а значит, в какой-то степени значительнее всего повлияли на итоговые результаты именно значения полей strength и gamma. Помимо этого довольно успешно на работу системы появляли изменения learning rate в большую сторону. Остальные же параметры не оказали значимого влияния на рузльтаты.

## Задание 2
### Описать результаты, выведенные в TensorBoard.

- **Cumulative reward** - награда в совокупности - общее вознаграждение, максимизированное агентом. Оно может как увеличиваться, так и уменьшаться; в основном правильным и ожидаемым для успеха бывает именно увеличение значения этой награды и возрастание графика, но в некоторых случаях значение может и падать. Чаще всего вознаграждение максимизируется в интервале [-1, 1]. Оно не должно выходить за границы заданного интервала.
- **Episode length** - длительность эпизодов обучения. Чем меньше значение, тем лучше, ведь это означает что обучение занимает меньше времени и проходит более продуктивно. 

- **Policy loss** - величина изменения политики, элемента, определяющего действия, с проходом определенного количества временем. В основном график этого значения должен стремиться вниз, так как это показывает, что политика с каждым разом принимает решения все лучше и лучше.
- **Value loss** - средняя потеря функции значения. Этот график моделирует то, насколько хорошо агент прогнозирует значение своего следующего состояния. До стабилизации вознаграждения должна стремиться к нулю, уменьшаться, после же - расти. Несмотря на то, что во время всех проведённых тренировок это значение уменьшалось, я считаю такой результат довольно удачным для небольшого объема тренировочных данных

- **Beta** - сила регуляции энтропии, отвечающая за случайность принятия решений
- **Entropy** - энтропия, величина исследования агента. От этого значения ожидается уменьшение, так как оно должно показывать, что необходимые объемы изучения постепенно становятся меньше. У меня в основном возрастает.
- **Epsilon** - влияет на скорость изменения политики во время обучения. Чем меньше, тем стабильнее и медленнее обучение.
- **Extrinsic reward** -  среднее значения вознаграждения, полученного за эпизод обучения. Зависит от параметра strength.
- **Extrinsic value estimate** - оценка внешнего значения, среднее значение, посещенное агентом. Должно расти - это показывает получение агентом знаний. У меня в основном снижается.
- **Learning rate** - скорость обучения, параметр настройки в алгоритме оптимизации, который определяет размер шага на каждой итерации при движении к минимуму функции потерь. Значение должно постепенно линейно уменьшаться. Так этот параметр и действовал.

- **ELO** - рейтинг успешности решений агента.

## Выводы

Во время выполнения лабораторной работы, я смогла поближе познакомиться с работой обучения ML-Agent через работу с интегрированной в Unity экономической системы. Помимо этого, при помощи графиков я смогла более явно понять, от чего зависит успешность обучения и как именно оно происходит. Также я смогла закрепить полученные ранее знания о работе экономической системы и поиске баланса.




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
