# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Нагнибеда Алиса Александровна
- РИ-210941
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * (+-) | 20 |

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
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса.

#### 1. В облачном сервисе google console подключить API для работы с google sheets и google drive.

В Google Cloud Console создан проект, к которому подключены необходимые API:

![Скриншот 11-10-2022 141119](https://user-images.githubusercontent.com/113305087/195166605-dea24294-d8ee-4894-b651-b5528d04227b.jpg)

#### 2. Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

- В Google Cloud Console получен email, который поможет обеспечить связь Google-таблиц с программой:

![Скриншот 10-10-2022 144336](https://user-images.githubusercontent.com/113305087/195166871-b41020d9-97d8-40fd-bd3d-0bc30555d2e7.jpg)

- Полученный email подключен в качестве редактора к созданной в Google-таблицах таблице:

![Скриншот 10-10-2022 144330](https://user-images.githubusercontent.com/113305087/195167333-766f167f-05c2-4934-bc8d-e81bb2a3e237.jpg)

- Создан новый проект в PyCharm, к которому подключены необходимые для выполнения задания библиотеки:

![Скриншот 10-10-2022 144718](https://user-images.githubusercontent.com/113305087/195167513-e98ed28c-7333-4aa1-af14-80578a27a405.jpg)

- К проекту также подключен ключ, полученный из Google Consol, именно при помощи него будет связан код и таблица:
- 
- ![Скриншот 11-10-2022 151124](https://user-images.githubusercontent.com/113305087/195168042-28f0a5ee-9f46-454e-b0d2-0f6217e2c5b7.jpg)

- В файл записан код, предоставленный преподавателем - он выполняет необходимые вычисления и записывает данные в подключенную в первых строках таблицу:

![Скриншот 10-10-2022 144724](https://user-images.githubusercontent.com/113305087/195167620-f1df8b04-25a6-44e1-97c9-b3a62a5e06f5.jpg)
![Скриншот 10-10-2022 151051](https://user-images.githubusercontent.com/113305087/195168254-0060e611-ee63-41b8-b50f-c9efde1118c9.jpg)
![Скриншот 10-10-2022 151101](https://user-images.githubusercontent.com/113305087/195168281-3a624b51-d07a-44d8-a4ec-33729b0d6918.jpg)


#### 3. Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.

- В Unity создан проект:
![Скриншот 10-10-2022 152125](https://user-images.githubusercontent.com/113305087/195168475-3d598ff7-6783-4805-ac1c-c7bdfd6682a5.jpg)

- В Google Cloud создан ключ, при помощи которого будет организована связь Unity с Google-таблицей:

![Скриншот 10-10-2022 151458](https://user-images.githubusercontent.com/113305087/195169058-cc57dbc6-5b5e-4066-ac3d-1b0d1d38e6af.jpg)
![Скриншот 10-10-2022 151632](https://user-images.githubusercontent.com/113305087/195169086-20754fd1-00b2-45f8-8fd2-1a8088d94ff8.jpg)

- В Google-таблице изменены настройки приватности:

![Скриншот 10-10-2022 151728](https://user-images.githubusercontent.com/113305087/195169178-bf709ae6-a34c-4f20-90ed-0c663fdffced.jpg)

- К проекту Unity подключены файлы, предоставленные преподавателями:

![Скриншот 10-10-2022 183352](https://user-images.githubusercontent.com/113305087/195169542-e75d43bc-b87b-4303-aab1-37f27d6ed4e4.jpg)


#### 4. Написать функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы.

- В созданном ранее проекте в Unity мы создаем новый скрипт, в котором будет написан функционал воспроизведения айдио-файла:

![Скриншот 10-10-2022 183341](https://user-images.githubusercontent.com/113305087/195169379-ad955fd6-071f-40ea-8153-9d83bb783052.jpg)

- В файле, открытом в VS-code записан код, представленный преподавателем:

![Скриншот 11-10-2022 155331](https://user-images.githubusercontent.com/113305087/195169875-fbace40d-8894-4b37-b9cd-7a901b9502e7.jpg)

- При выполнении кода, Unity получает и выводит данные из подключенной к файлу таблицы, воспроивзодя при этом звуки, зависимо от значения инфляции:

![Скриншот 11-10-2022 005101](https://user-images.githubusercontent.com/113305087/195170001-3d2867bf-6c19-4ed7-a08a-f4d8dd8abec9.jpg)

- Изменив изначальные данные (посредством запуска кода на Python), мы можем заново воспроизвести решение этой задачи:

![Скриншот 11-10-2022 005246](https://user-images.githubusercontent.com/113305087/195170453-a3e1c96f-f41e-42e5-98e0-0a1970beba4c.jpg)
![Скриншот 11-10-2022 005258](https://user-images.githubusercontent.com/113305087/195170487-568c63c2-f6b7-4059-80ab-e6e4392f47ce.jpg)
![Скриншот 11-10-2022 005241](https://user-images.githubusercontent.com/113305087/195170513-15fb2f06-abc0-4485-8966-c55a396080af.jpg)

В результате мы получили программы в Python и Unity, связанные с Google-Sheets


## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1

Для реализации этого задания был создан новый лист (List2) в той же таблице, с которой я работала ранее, а также был создан новый файл кода в том же проекте, что и ранее, поэтому реализовывать заново подключение между таблицей и проектом не нужно было.

- Код, используемый для задачи с линейной регрессией, был переписан в PyCharm с некоторыми изменениями, заменяющие пойстройку графиков и вывод данных в консоль на передачу их в таблицу:

```
import gspread
import numpy as np
gc = gspread.service_account(filename='unitydatascience-365106-1485a8c29bf8.json')
sh = gc.open("UnitySheets").worksheet("List2")

x = [3, 21, 22, 34, 54, 34, 55, 67, 89, 99]
x = np.array(x)
y = [2, 22, 24, 65, 79, 82, 55, 130, 150, 199]
y = np.array(y)


def model(a, b, x):
  return a*x + b


def loss_function(a, b, x, y):
  num = len(x)
  prediction = model(a,b,x)
  return (0.5 / num) * (np.square(prediction - y)).sum()


def optimize(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  da = (1.0 / num) * ((prediction - y) * x).sum()
  db = (1.0 / num) * ((prediction - y).sum())
  a = a - Lr*da
  b = b - Lr*db
  return a, b


def iterate(a, b, x, y, times):
  for i in range(times):
    a,b = optimize(a, b, x, y)
  return a, b


a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001
amount = 10

iteration = 1
for i in range(1, amount + 1):
    a, b = iterate(a, b, x, y, iteration)
    prediction = model(a, b, x)
    loss = loss_function(a, b, x, y)
    sh.update(('A' + str(i)), str(i))
    sh.update(('B' + str(i)), str(iteration))
    sh.update(('C' + str(i)), str(a))
    sh.update(('D' + str(i)), str(b))
    sh.update(('E' + str(i)), str(loss))
    iteration += 30
```

Результат выполнения программы:

![image](https://user-images.githubusercontent.com/113305087/195172516-7c2fec9f-1b29-4242-a352-4efe0681c79e.png)

Также представляю вариант выполнения программы, в которой были указаны названия столбцов, для лучшего понимания того, какие данные были выведены:

![Скриншот 11-10-2022 194342](https://user-images.githubusercontent.com/113305087/195175702-def28777-75a5-4586-8885-4e3d483bd3ac.jpg)

Такой вариант таблицы был откинут из-за появивишихся позже сложностей с третьим заданием.


## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2

Для выполнения этого задания был создан новый скрипт в том же проекте Unity, что и ранее:

![Скриншот 11-10-2022 191058](https://user-images.githubusercontent.com/113305087/195173410-2dd299b9-9692-40f2-8d2c-f01792ea94f9.jpg)

В этом скрипте был написан следующий код по аналогии с предыдущим заданием:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NumberToSound : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (statusStart == false & dataSet["Mon_" + i.ToString()] <= 250 & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (statusStart == false & dataSet["Mon_" + i.ToString()] > 250 & dataSet["Mon_" + i.ToString()] < 1000 & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (statusStart == false & dataSet["Mon_" + i.ToString()] >= 1000 & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest currentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1srUGeMCRPp9wLdIYumhggFNHAjAHXDanZaQsXTQz6mo/values/List2?key=AIzaSyAvwI4j2DsXTJ1XTYokbD7CxPsFhlPq8Lg");
        yield return currentResp.SendWebRequest();
        string rawResp = currentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[4]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```

Планировалось получать данные по потерям в результате выполнения алгоритма линейной регрессии и выводить их в консоль, также вызывая звуковое сопровождение, однако при выполнении данного кода выводится ошибка, которую мне так и не удалось исправить, несмотря на применение раздичных способов решения этой проблемы (попытка учесть шапку таблицы, о которой я говорила в прошлом пункте, её удаление, создание полностью новой Google-таблицы и др.):

![Скриншот 11-10-2022 214640](https://user-images.githubusercontent.com/113305087/195174244-1ed6314e-9d76-4707-8e1a-9cd3d300c7f1.jpg)

## Выводы

Во время выполнения лабораторной работы, я смогла реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity и поподробнее рассмотреть её на примере задачи с оценкой изменений темпов инфляции. Также на примере задачи о линейной регрессии я смогла реализовать связь Python - Google-Sheets, что помогло мне лучше разобраться в этой теме. Однако к сожалению, работая над связью Google-Sheets – Unity я столкнулась с трудностями, которые не смогла преодолеть.


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
