# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity. При выполнении задания были использованы видео-материалы и исходные данные, предоставленные преподавателями курса.

1. Создайн новый пустой 3D проект на Unity:

![Скриншот 27-10-2022 155425](https://user-images.githubusercontent.com/113305087/200482474-76512c67-d36e-432e-8c2a-6e73ed0565e8.jpg)


2. В созданный проект добавлен ML Agent, предоставленный преподавателями. Добавлены следующие .json – файлы:
o ml-agents-release_19 / com,unity.ml-agents / package.json
o ml-agents-release_19 / com,unity.ml-agents.extensions / package.json

![Скриншот 27-10-2022 161931](https://user-images.githubusercontent.com/113305087/200483096-b83402ab-d901-4299-9043-afb9fe1537db.jpg)

Теперь во вкладке Components можно увидеть ML Agent:

![Скриншот 27-10-2022 162114](https://user-images.githubusercontent.com/113305087/200483164-db6d9627-49a1-4376-9772-09bfa392f30b.jpg)


3. Запускаем Anaconda Prompt, при помощи которого мы будем запускать команды. 
Подключаем библиотеку mlagents 0.28.0:

![Скриншот 27-10-2022 171728](https://user-images.githubusercontent.com/113305087/200483597-11f1bd0a-ac1f-4b0c-9929-07ab9dc2f4de.jpg)

![Скриншот 27-10-2022 171916](https://user-images.githubusercontent.com/113305087/200483643-c003d149-d295-416b-b2cb-aaf4ffde40d0.jpg)

![Скриншот 27-10-2022 172244](https://user-images.githubusercontent.com/113305087/200483662-ae8c4513-f5c4-463b-b784-e4f0460ca824.jpg)

Также подключаем библиотеку torch 1.7.1 (на скриншоте - результат подключения):

![Скриншот 27-10-2022 174704](https://user-images.githubusercontent.com/113305087/200484136-9a3dd977-4be6-42c7-bb4e-082b9f2d6d74.jpg)

Директорию работы консоли меняем на директорию проекта Unity:

![Скриншот 27-10-2022 174913](https://user-images.githubusercontent.com/113305087/200484327-189af2b2-7005-4554-86a2-4fa7f7d07fa5.jpg)


4. На сцене созданы соответствующие заданным преподавателем характеристикам плоскость, куб и сфера:

![Скриншот 27-10-2022 175612](https://user-images.githubusercontent.com/113305087/200484696-bf338e1e-cc8e-42de-80b8-aaacdb89c057.jpg)

![Скриншот 27-10-2022 180112](https://user-images.githubusercontent.com/113305087/200484747-5d65cdca-638d-4da8-afb9-40fc25f0fb69.jpg)


5. К сфере подключен C# скрипт-файл:

![Скриншот 27-10-2022 180216](https://user-images.githubusercontent.com/113305087/200484926-0eb069ba-d58b-4d35-8fc0-75abc158396f.jpg)

![Скриншот 27-10-2022 180239](https://user-images.githubusercontent.com/113305087/200484941-7ee278d2-12e0-4e68-90da-8ef2f08eea73.jpg)


6. В скрипт-файл был записан предоставленный преподавателем код:

```
using System.Collections; // добавляем библиотеку System.Collections к файлу
using System.Collections.Generic; // добавляем библиотеку System.Collections.Generic к файлу
using UnityEngine; // добавляем библиотеку UnityEngine к файлу
using Unity.MLAgents; // добавляем библиотеку Unity.MLAgents к файлу
using Unity.MLAgents.Sensors; // добавляем библиотеку Unity.MLAgents.Sensors к файлу (сбор информации)
using Unity.MLAgents.Actuators; // добавляем библиотеку Unity.MLAgents.Actuators к файлу (повторение данных)

public class RollerAgent : Agent //создаём публичный класс RollerAgent, который наследует функционал класса Agent 
{
    Rigidbody rBody; //создаём переменную rBody типа Rigidbody - отвечает за сферу
    // Start is called before the first frame update
    void Start() //стандартный метод для скрипта Unity, первый запуск проекта
    {
        rBody = GetComponent<Rigidbody>(); //считываем Rigigbody в переменную rBody
    }

    public Transform Target; //создаём публичную переменную Target типа Transform - координаты куба
    public override void OnEpisodeBegin() //переопределям метод OnEpisodeBegin - действие в ситуации, когда MLAgent завершил свои действия (начало обучения снова)
    {
        if (this.transform.localPosition.y < 0) //если изначальная позиция сферы, по у меньше 0, то совершится следующее действие
        {
            this.rBody.angularVelocity = Vector3.zero; //угловая скорость сферы = нулевому вектору(x, y, z)
            this.rBody.velocity = Vector3.zero; //скорость сферы = нулевому вектору(x, y, z)
            this.transform.localPosition = new Vector3(0, 0.5f, 0); //изменение изначальной позиции сферы
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4); //рандомное изменение локальной позиции куба по x и z
    }
    public override void CollectObservations(VectorSensor sensor) //переопределяем метод CollectObservations, собирающий параметры во время обучения
    {
        sensor.AddObservation(Target.localPosition); //добавляем к сборам локальную позицию куба
        sensor.AddObservation(this.transform.localPosition); //добавляем к сборам локальную позицию сферы
        sensor.AddObservation(rBody.velocity.x); //добавляем к сборам скорость сферы по x
        sensor.AddObservation(rBody.velocity.z); //добавляем к сборам скорость сферы по z
    }
    public float forceMultiplier = 10; //создаем публичную переменную - изменение силы объекта
    public override void OnActionReceived(ActionBuffers actionBuffers) //переопределяем метод OnActionRecieved - основная функция обучения, принимающая действия
    {
        Vector3 controlSignal = Vector3.zero; //создаём вектор(x, y, z) controlSignal, равный нулевому вектору
        controlSignal.x = actionBuffers.ContinuousActions[0]; // присваеваем вектору по x переданное непрерывное действие с нулевым коэффициентом
        controlSignal.z = actionBuffers.ContinuousActions[1]; // присваеваем вектору по z переданное непрерывное действие с первым коэффициентом
        rBody.AddForce(controlSignal * forceMultiplier); // меняем силу сферы, увеличиваем её

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition); //создаём переменную, узнающую расстояние от сферы до куба

        if(distanceToTarget < 1.42f) //если расстояние меньше определённого результата, то
        {
            SetReward(1.0f); //отмечаются успешные результаты
            EndEpisode(); //конец действия
        }
        else if (this.transform.localPosition.y < 0) // если позиция сферы по y меньше нуля
        {
            EndEpisode(); //конец действия
        }
    }
}
```

Он же был подключен к сфере:

![Скриншот 27-10-2022 181639](https://user-images.githubusercontent.com/113305087/200485475-4b06eb0a-b2e7-4be1-81f0-24e53167472a.jpg)


7. Объекту «сфера» добавлены настроенные по образцу компоненты Rigidbody, Decision Requester, Behavior Parameters:

![image](https://user-images.githubusercontent.com/113305087/200486109-bb7b08e9-3d21-4f23-ae08-1b45212c50f4.png)

![Скриншот 27-10-2022 181839](https://user-images.githubusercontent.com/113305087/200485535-6c2fee5c-6ddd-4950-be03-723d394e4d0b.jpg)


8. В корень проекта добавлен файл конфигурации нейронной сети, полученный из папки с файлами проекта:

![Скриншот 27-10-2022 182036](https://user-images.githubusercontent.com/113305087/200486316-0345b3cb-2834-40c5-97b0-6e5bd6d77414.jpg)

Содержание файла с кодом и его подробный разбор можно увидеть во [втором задании](#задание-2) лабораторной работы


9. Запущена работа ml-агента:

![Скриншот 27-10-2022 210254](https://user-images.githubusercontent.com/113305087/200486480-163dc5d5-7d81-4cbe-8975-bbf9a8272104.jpg)

![Скриншот 27-10-2022 211544](https://user-images.githubusercontent.com/113305087/200486698-0d8c1381-06d3-4f9d-92ca-ed94a6570f99.jpg)


10. Запущена сцена, происходит работа ML-Agent. Сфера учится находить куб:

![Скриншот 27-10-2022 213724](https://user-images.githubusercontent.com/113305087/200486735-e2508be7-a564-443f-9244-0f7873cc9766.jpg)

![Скриншот 27-10-2022 213735](https://user-images.githubusercontent.com/113305087/200486769-5f85aa97-0654-4407-9fad-6b72b9a7f8e3.jpg)


11. Сделаны 3, 9, 27 копий модели «Плоскость-Сфера-Куб», снова запущена симуляция сцены. Заметно, что обучение сферы происходит всё быстрее и быстрее:

![Скриншот 06-11-2022 203655](https://user-images.githubusercontent.com/113305087/200487004-79307d49-a764-40dc-a927-d772952e2b1f.jpg)

![Скриншот 06-11-2022 210237](https://user-images.githubusercontent.com/113305087/200487028-a162e785-271b-4970-8873-a4290a04ffdc.jpg)


![Скриншот 06-11-2022 204812](https://user-images.githubusercontent.com/113305087/200487066-d49cb394-de8b-4d33-af98-01d47abca6bc.jpg)

![Скриншот 06-11-2022 210250](https://user-images.githubusercontent.com/113305087/200487097-6eb4013c-8ad1-4b95-a82d-1bcae3753298.jpg)


![Скриншот 06-11-2022 205555](https://user-images.githubusercontent.com/113305087/200487117-a3075e1b-ca1a-4860-9aad-9daa8811485e.jpg)

![Скриншот 06-11-2022 210300](https://user-images.githubusercontent.com/113305087/200487144-7eb157f5-78d5-4ed5-8fe4-9b85f702f36c.jpg)


12. Работу модели можно проверить при помощи файла, результирующего работу ML-Agent, 'RollerBall.onnx', который мы согласно советам преподавтаеля подключаем к сфере:

![Скриншот 06-11-2022 210838](https://user-images.githubusercontent.com/113305087/200487342-56465987-cd22-4c62-821e-f381dbf3a1ae.jpg)

![Скриншот 06-11-2022 210954](https://user-images.githubusercontent.com/113305087/200487459-f9c92c52-f85a-46cb-8fe7-357d7f205ff0.jpg)


13. Сфера движется, теперь она может относительно хорошо находить куб:

![Скриншот 06-11-2022 211618](https://user-images.githubusercontent.com/113305087/200487669-0ef68c39-3fa6-4390-80b2-ad7e970b3243.jpg)


#### Выводы, касательно работы ML-Agent и обучения сферы:

Работа ML-Agent заключается в том, чтобы обучить объект какому-либо действию. Проследив за работой ML-Agent в задании данной лабораторной работы, можно сделать вывод, что объект действительно успешно обучается - в результате нго работы мы получили сферу, которая может успешно находить и догонять куб на плоскости. Также можно отметить, что чем больше одинаковых объектов проходит обучение одновременно, тем быстрее оно происходит.



## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных к сфере.

#### Файл конфигурации нейронной сети:

```
behaviors: #создаётся секция behaviors, которая будет содержать объект и настройки его обучения
  RollerBall: #объект RollerBall, содержит настройки обучения, которые будут применены к объекту
    trainer_type: ppo #указывает, что тип обучающего алгоритма = ppo, тип по умолчанию, наиболее стабильный, требует небольшое количество гиперпараметров для успешного обучения
    hyperparameters: #параметры обучения
      batch_size: 10 # количество опытов в каждой итерации; 10 - маленькое значение, такие обычно используются для дискретных операций 
      buffer_size: 100 #количество собираемых перед обновлением модели опытов; 100 - значение, в несколько раз больше значения batch_size
      learning_rate: 3.0e-4 #начальная скорость обучения, соответствует силе обновления кажого шага градиентного спуска; значение по умолчанию
      beta: 5.0e-4 #сила энтропийной регуляризации, отвечает за рандомность действий; значение близкое к значению по умолчанию
      epsilon: 0.2 #эпсилон, влияет на силу изменений в процессе обучения - чем меньше, тем стабильнее и медленнее; значение по умолчанию
      lambd: 0.99 #лямбда, параметр регуляризации, используемый при нахождении GAE;
                  #высокие значения соответствуют высокому влиянию наград на обучение; значение выше значения по умолчанию
      num_epoch: 3 #количество проходов опыта для оптимизации градиентного спуска; чем меньше - тем стабильнее результаты и медленнее обучение; 3 - маленько значение
      learning_rate_schedule: linear #определяет изменение скорости обучения; линейное уменьшенение скорости до нуля (есть также постоянная, constant, скорость)
    network_settings: #настройки сети
      normalize: false #применяется ли нормализация ко входным данным векторных наблюдений, вредня для простых задач; false - значение по умолчанию
      hidden_units: 128 #количество единиц в скрытых, полностью соединённых слоях нейронной сети; чем сложнее задача, тем больше число; 128 - значение по умолчанию
      num_layers: 2 #количество скрытых слоёв нейронной сети; для простых задач меньшее количество слоёв - лучше; 2 -значение по умолчанию
    reward_signals: #настройки награждений, каждый reward_signal должен содержать два параметра
      extrinsic: #extrinsic reward signal -> внешний сигнал, основывающийся на окружении
        gamma: 0.99 #"фактор скидки" для будущих вознаграждений; чем скорее будет награда, тем меньше должно быть значение (нов сегда строго меньше 1); 0,99 - значение по умолчанию
        strength: 1.0 #усиление награды; 1.0 - значение по умолчанию
    max_steps: 500000 #максиамальное количество пройденных шагов перед окончанием обучения; значение по умолчанию
    time_horizon: 64 #сколько шагов опыта нужно сделать, чтобы добавить его в буфер опыта; если эпизоды длинные или награды больше, число может быть меньше; значение по умолчанию
    summary_freq: 10000 #необходимое количество опытов, после которого можно вывести статистику обучения на экран; меньше значения по умолчанию
```
#### Decision Requester:
Этот компонент предоставляет удобный и гибкий способ для пробуждения процесса принятия решений у Агента. Этот компонент вызывает функцию RequestDecision() в установленном интервале.

#### Behavior Parameters
Компонент, использующийся для настройки поведения экземпляров Агента и функций "мозга", сответственно указанным через Unity параметрам.



## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости.

Для выполнения этого задания на сцене был создан второй объект-цель - куб голубого цвета, в коде он был обозначен как Target2. В коде были совершены следующие поправки:

```
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Unity.MLAgents; 
using Unity.MLAgents.Sensors; 
using Unity.MLAgents.Actuators; 

public class RollerAgent : Agent  
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start() 
    {
        rBody = GetComponent<Rigidbody>(); 
    }

    public Transform Target;
    public Transform Target2;
    public bool FirstChecked = false;

    public override void OnEpisodeBegin() 
    {
        if (this.transform.localPosition.y < 0) 
        {
            this.rBody.angularVelocity = Vector3.zero; 
            this.rBody.velocity = Vector3.zero; 
            this.transform.localPosition = new Vector3(0, 0.5f, 0); 
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
        Target2.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
        Target.gameObject.SetActive(true);
        Target2.gameObject.SetActive(true);
        FirstChecked = false;
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(Target2.localPosition);
        sensor.AddObservation(this.transform.localPosition); 
        sensor.AddObservation(rBody.velocity.x); 
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers) 
    {
        Vector3 controlSignal = Vector3.zero; 
        controlSignal.x = actionBuffers.ContinuousActions[0]; 
        controlSignal.z = actionBuffers.ContinuousActions[1]; 
        rBody.AddForce(controlSignal * forceMultiplier); 

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);
        float distanceToTarget2 = Vector3.Distance(this.transform.localPosition, Target2.localPosition);
        

        if(distanceToTarget < 1.42f & !FirstChecked)
        {
            FirstChecked = true;
            Target.gameObject.SetActive(false);
        }
        if(distanceToTarget2 < 1.42f & FirstChecked)
        {
            Target2.gameObject.SetActive(false);
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }

        
    }
}
```

Для обучения модели было создано около 60 платформ:

![Скриншот 09-11-2022 231810](https://user-images.githubusercontent.com/113305087/200928936-b776b233-17fa-4b7a-a633-14f1ce0dba68.jpg)

Результат обучения:

![Без названия](https://user-images.githubusercontent.com/113305087/200936712-31755289-051b-41c4-be3a-cb06e55c3892.gif)

В результате мы получили шар, направляющийся сначала к первому, зелёному кубу, а потом ко второму, голубому. Самому шару, несмотря на довольно крупный объем тренируемых данных, точно есть куда стремиться! Ему гораздо тяжелее находить второй, голубой, куб.



## Выводы

**Игровой баланс** - это полученное при создании игры свойство, которое отвечает за логичность и цельность различных механик. Присутствие игрового баланса равно получению игроком полноценного опыта при прохождении игры. Он может проявляться в балансе сложности уровней и боссов, во взаимоотношении между полученной валютой и товарами, которые можно на неё получить, в балансе сил различных персонажей и т.д. Важно понимать, что баланс не равен "одинаковости" - объекты в игре должны быть разными, а игра должна приносить удовольствие. 

Системы машинного обучения - один из отличных способов скорректировать игровой баланс. При машинном обучении, происходит сбор и анализ огромного количества данных, используя которые, алгоритм учится - он перенимает некие особенности полученных данных или же делает выводы о своих действиях, исходя из уведомлений об успехе. Такие системы можжно, например, применить для баланса сложностей битв, происходящих не между игроками, а с "компьютером", - это поднимет интерес игрока. Помимо этого, сбор данных игрока, заинтересованного данной игрой, поможет найти дисбаланс некоторых механик, который можно будет разрешить уже не автоматически, а трудом разработчиков.


Во время выполнения данной лабораторной работы, я научилась тому, как можно совершить простое машинное обучение шарика, преследующего свою цель. В будущем этот навык поможет анализировать и более сложные динамики, помогая реализовывать игровой баланс.


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
