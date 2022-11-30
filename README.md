# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Научиться простейшему обучению перцептрона на примере логических операций

## Задание 1
### Реализовать в проекте Unity перцептрон, который умеет производить данные вычесления: OR, AND, NAND, XOR

**Ход работы:**

#### 1. Создаём новый проект Unity - я создала 3D проект. В нём создаём пустой объект StudyObject, к которому прекрепляем скрипт, содержащий реализацию перцептрона.

Проект Unity:

![image](https://user-images.githubusercontent.com/113305087/204632835-823cd224-ab33-48a3-a84d-afc139b1d98f.png)

Скрипт с реализацией перцептрона, предоставленный преподавателем:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}
```

#### 2. Реализуем обучение перцептрона проведению вычеслений, задав необходимые входные и выходные параметры

##### а) Вычисления OR:

Для успешного обучения зададим правильные входные и выходные значения, на которые будет равняться перцептрон:

![image](https://user-images.githubusercontent.com/113305087/204634022-c99debd0-dc50-4ed5-bff9-eb20d1661fbb.png)

Проведём обучение при помощи 8, заданных изначально операций:

```
...
Train(8);
...
```

Обучение я провела дважды, во время первой итерации полное обучение произошло на шестой операции, во время второй - на четвертой:

![image](https://user-images.githubusercontent.com/113305087/204635579-b5bc6b13-6506-4a73-920a-d206c9755912.png)

![image](https://user-images.githubusercontent.com/113305087/204636322-65f0636e-7444-4ef7-82b8-e169d781e97f.png)

Результат обеих:

![image](https://user-images.githubusercontent.com/113305087/204635871-24b18b45-9da0-42b4-b765-13b34e414b00.png)
![image](https://user-images.githubusercontent.com/113305087/204638557-b1555ba2-3fea-4907-9210-defa0022b57a.png)


Вывод: Перцептрон довольно быстро обучается вычислениям, касающимся этой логической операции. В итоге получены правильные результаты.


##### б) Обучение AND
Для проведения этого обучения так же зададим правильные входные и выходные значения, на которые будет равняться перцептрон:

![image](https://user-images.githubusercontent.com/113305087/204638974-1e871f31-86cc-4b00-85c0-4f882429907f.png)

И снова проведём обучение при помощи 8, заданных изначально операций.

Обучение я так же провела дважды, во время первой итерации полное обучение произошло на шестой операции, во время второй - тоже на шестой:

![image](https://user-images.githubusercontent.com/113305087/204639582-b66cadc0-1aa4-4431-aade-093c57a32bbc.png)

![image](https://user-images.githubusercontent.com/113305087/204639820-3cd8d175-c071-48f0-9202-d8c7fd63980c.png)

Результат обеих:

![image](https://user-images.githubusercontent.com/113305087/204639665-23f49689-c050-4d4f-b28f-577cfa0d2388.png)
![image](https://user-images.githubusercontent.com/113305087/204639850-592f9b94-3a85-48ad-a144-1dbc7451d44c.png)


Вывод: Перцептрон быстро обучается "сложению", и в итоге были получены правильные результаты. Помимо этого, можно заметить, что максимальное количество операций, необходимых для обучения перцептрона этой и предыдущей операции, равно всего лишь шести.


##### в) Обучение NAND
Данная операция полностью противоположна сложению. Прогнозируя, основываясь на прошлых выводах, можно сказать, что количество проведённых операций не должно превысить число 6. Для проведения этого обучения зададим правильные входные и выходные значения, на которые будет равняться перцептрон:

![image](https://user-images.githubusercontent.com/113305087/204640594-b631955c-00af-4412-b57a-da33f53f779b.png)

И проведём обучение при помощи 8, заданных изначально операций.

Обучение было проведено дважды, во время первой итерации полное обучение в этот раз произошло уже на седьмой операции, во время второй - на шестой:

![image](https://user-images.githubusercontent.com/113305087/204640729-fdd4bb4e-32b3-45cf-a202-66be06522376.png)

![image](https://user-images.githubusercontent.com/113305087/204641017-d324f486-3870-4629-afe4-fb45ce868256.png)

Результат обеих:

![image](https://user-images.githubusercontent.com/113305087/204640880-3a703851-dbd9-4bec-a22f-41f7aecb478f.png)
![image](https://user-images.githubusercontent.com/113305087/204641060-ad976b79-a5b1-4454-9fa0-688549f796ef.png)

Проведён был также третий опыт - полное обучение заняло всего четыре итерации:

![image](https://user-images.githubusercontent.com/113305087/204641204-62b716f5-bf5f-423e-8fdf-aadbb13a9e5d.png)

![image](https://user-images.githubusercontent.com/113305087/204641232-c3dac107-c8cf-4277-98bd-29988b76b971.png)

Вывод: Перцептрон почти так же быстро, относительно предыдущих операций, обучается "отрицанию сложения (конъюнкции)" - максимальное количество итераций равно семи; в итоге были получены правильные результаты. Чем больше операций проводится, тем меньше итераций требуется для обучения перцептрона - но это просто совпадение.


##### г) Обучение XOR
Заранее известно, что обучение данной логической операции не принесёт желаемых результатов. Но для проведения этого обучения зададим правильные входные и выходные значения, на которые будет равняться перцептрон:

![image](https://user-images.githubusercontent.com/113305087/204642995-71185d3b-3e2f-45ea-9c79-c078bb3c3069.png)

Изначально проведём обучение при помощи 8, заданных изначально операций. Обучение, как и ожидалось, прошло неудачно:

![image](https://user-images.githubusercontent.com/113305087/204643105-e2d7bb32-af81-4a63-82cd-78a6aed298af.png)

Поробуем увеличить количество операций до 100:

```
...
Train(100);
...
```

![image](https://user-images.githubusercontent.com/113305087/204643594-483a0402-45e4-44ab-87e5-e48a35b9648b.png)

Результаты не изменились - значение ошибки всё ещё велико, а итог неправильный

Вывод: Перцептрону тяжело обучиться "исключающему ИЛИ" при помощи простых, линейных операций, как итог он получает неправильные результаты.


## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать, от чего зависит необходимое количество эпох обучения.

**Ход работы:**

Построим графики зависимости количества эпох от ошибки обучения в Google Sheets, взяв за основные данные результаты, полученные в результате некоторых повторно проведенных операций обучения:

Таблица результатов:

![image](https://user-images.githubusercontent.com/113305087/204752714-4beeeaec-931e-42d4-a4f1-9ef3a7dc76eb.png)

Получившийся график:

![image](https://user-images.githubusercontent.com/113305087/204752614-9ee6713b-a48e-43b9-a6bf-e5b6720223ef.png)


Для того, чтобы понять, от чего зависит необходимое количество эпох обучения, рассмотрим некоторые из получившихся во время операций значения весов и смещения:

```
W1: -0,817158937454224 W2: 0,931469917297363 B: -0,277249574661255
W1: -0,817158937454224 W2: -0,0685300827026367 B: -1,27724957466125
W1: -0,817158937454224 W2: -0,0685300827026367 B: -1,27724957466125
W1: 0,182841062545776 W2: 0,931469917297363 B: -0,277249574661255
TOTAL ERROR: 3
``` 
```
W1: 0,182841062545776 W2: 0,931469917297363 B: -0,277249574661255
W1: 0,182841062545776 W2: -0,0685300827026367 B: -1,27724957466125
W1: 0,182841062545776 W2: -0,0685300827026367 B: -1,27724957466125
W1: 1,18284106254578 W2: 0,931469917297363 B: -0,277249574661255
TOTAL ERROR: 2
```

Между двумя верхними операциями значения весов увеличились, а значения смещений не изменились, но в результате количество ошибок уменьшилось.

```
W1: 1,18284106254578 W2: 0,931469917297363 B: -0,277249574661255
W1: 1,18284106254578 W2: -0,0685300827026367 B: -1,27724957466125
W1: 1,18284106254578 W2: -0,0685300827026367 B: -1,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -0,277249574661255
TOTAL ERROR: 2
```
```
W1: 2,18284106254578 W2: 0,931469917297363 B: -0,277249574661255
W1: 2,18284106254578 W2: -0,0685300827026367 B: -1,27724957466125
W1: 1,18284106254578 W2: -0,0685300827026367 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -1,27724957466125
TOTAL ERROR: 3
```
Между двумя верхними операциями значения весов, а также значения смещений (по модулю) увеличились - количество ошибок увеличилось.

```
W1: 2,18284106254578 W2: 1,93146991729736 B: -1,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
TOTAL ERROR: 1
```
```
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
W1: 2,18284106254578 W2: 0,931469917297363 B: -2,27724957466125
TOTAL ERROR: 0
```
Между двумя верхними операциями значения весов уменьшились, значения смещений по модулю - увеличились => количество ошибок свелось к нулю.

Единственное, что изменялось на протяжении всех итераций - это значения весов и смещений (w1 = weight1, w2 = weight2, b = bias). Соответственно, можно сделать вывод, что необходимое количество операций для завершения обучения перцептрона линейным операциям зависит именно от изменения этих значений.



## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity

**Ход работы:**

В третьем задании я реализовала смену цветов раздичных шаров в соответствии с результатами логических операций.

1. Для выполнения третьего задания я создаю новое окружение:

![image](https://user-images.githubusercontent.com/113305087/204813658-636568f1-cec1-4e31-95dc-aabdc2b3590d.png)

Это окружение состоит из 8 элементов:

- Платформа, с которой стартуют шары
- Ровная наклонная поверхность, играющая роль горки
- Платформа, на которую приземляются шары
- Вытянутый цилиндр, который будет играть роль триггера:

![image](https://user-images.githubusercontent.com/113305087/204815756-94214e36-de48-4545-81af-9d566b70a248.png)

- 4 шара двух цветов - два из них, дальние жёлтый и розовый, будут следовать по принципу, изученному перцептроном по "ИЛИ", а два других будут действовать по принципу "И". Все шары обладают компонентом RigidBody, в настройках которого указано, что они подвержены гравитации:

![image](https://user-images.githubusercontent.com/113305087/204815141-3fa96695-11c4-4977-a620-3faeb4fcf03e.png)

2. Пишем скрипт, который мы прикрепим к каждому из шаров. Этот скрипт будет отвечать за смену цвета:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sphere : Perceptron
{
     private void OnTriggerEnter(Collider triggerBody)
    {
        int triggerBodyValue = triggerBody.gameObject.GetComponent<Renderer>().material.color == Color.magenta ? 0 : 1;
        int movingBodyValue = this.gameObject.GetComponent<Renderer>().material.color == Color.magenta ? 0 : 1;

        if (CalcOutput((double)movingBodyValue, (double)triggerBodyValue) == 0)
            this.gameObject.GetComponent<Renderer>().material.color = Color.yellow;
        else
            this.gameObject.GetComponent<Renderer>().material.color = Color.magenta;
    }
}
```

В скрипте мы указываем цифровые значения для двух цветов, которыми мы обозначаем шары и триггер: 

- Розовый цвет = 0
- Желтый цвет = 1

В соответствии с этими значениями и будут производиться логические операции, влияющие на изменение цвета шаров.

3. Привязываем данный шрифт к каждому из шаров, указывая необходимые стартовые значения в компоненте:

![image](https://user-images.githubusercontent.com/113305087/204816625-2b346468-e42e-46e1-9df7-a9d6cf3bef9f.png)
![image](https://user-images.githubusercontent.com/113305087/204816685-9284dcc2-8884-48b2-8dfd-64c7362bbe85.png)

4. Запускаем программу и смотрим на изменение цвета:

5. Запускаем программу повторно, заменив цвет цилиндра на розовый:

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
