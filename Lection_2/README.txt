https://gbcdn.mrgcdn.ru/uploads/asset/4239331/attachment/b63e7ff5e723b10f8eb635f935ce8bc4.html

import pandas as pd
import numpy as np
Series
Она представляет из себя объект, похожий на одномерный массив, но отличительной чертой является наличие индексов. Индекс находится слева, а сам элемент справа.

Синтаксис создания:

pandas.Series(input_data, index, data_type)
input_data: ввод в виде списка, константы, массива NumPy, Dict и т. д.
index: значения индексов.
data_type (опционально): тип данных.
a = pd.Series([4, 7, 6, 3, 9],
              index=['one', 'two', 'three', 'four', 'five'])
a
one      4
two      7
three    6
four     3
five     9
dtype: int64
a = pd.Series([4, 7, 6, 3, 9])
a
0    4
1    7
2    6
3    3
4    9
dtype: int64
a.index
RangeIndex(start=0, stop=5, step=1)
a.values
array([4, 7, 6, 3, 9])
a[0]
4
a[1]
7
DataFrame
Объект DataFrame является табличной структурой данных. В любой таблице всегда присутствуют строки и столбцы. При этом в столбцах можно хранить данные разных типов данных. Столбцами в объекте DataFrame выступают объекты Series, строки которых являются их элементами.

Синтаксис создания:

pandas.DataFrame(input_data, index)
input_data: ввод в виде Dict, 2D массива NumPy, Series и т. д.
index: значения индексов.
df = pd.DataFrame({
    'Age': [46, 37, 44, 42, 42],
    'Country': ['Spain', 'Spain', 'Germany', 'Germany', 'France'],
    'Gender': ['Female', 'Female', 'Male', 'Male', 'Male']
})

df
Age	Country	Gender
0	46	Spain	Female
1	37	Spain	Female
2	44	Germany	Male
3	42	Germany	Male
4	42	France	Male
df['Age']
0    46
1    37
2    44
3    42
4    42
Name: Age, dtype: int64
df.Country
0      Spain
1      Spain
2    Germany
3    Germany
4     France
Name: Country, dtype: object
df[['Country', 'Age']]
Country	Age
0	Spain	46
1	Spain	37
2	Germany	44
3	Germany	42
4	France	42
df.columns
Index(['Age', 'Country', 'Gender'], dtype='object')
df.index
RangeIndex(start=0, stop=5, step=1)
df = pd.DataFrame({
    'Age': [46, 37, 44, 42, 42],
    'Country': ['Spain', 'Spain', 'Germany', 'Germany', 'France'],
    'Gender': ['Female', 'Female', 'Male', 'Male', 'Male']
}, index=[5, 4, 6, 3, 2])

df
Age	Country	Gender
5	46	Spain	Female
4	37	Spain	Female
6	44	Germany	Male
3	42	Germany	Male
2	42	France	Male
df.index = [101, 102, 103, 104, 105]
df
Age	Country	Gender
101	46	Spain	Female
102	37	Spain	Female
103	44	Germany	Male
104	42	Germany	Male
105	42	France	Male
Считывание данных
В целом, pandas поддерживает все самые популярные форматы хранения данных: csv, excel, sql, html и многое другое, но чаще всего приходится работать именно с csv файлами (comma separated values).

Будем работать с датасетом по оттоку клиентов из банка https://www.kaggle.com/datasets/shubh0799/churn-modelling.

Характеристики каждого клиента:

RowNumber - Номер строки
CustomerId - Уникальный идентификатор клиента
Surname - Фамилия клиента
CreditScore - Кредитная оценка клиента
Geography - Из какой страны клиент
Gender - Пол клиента
Age - Возраст клиента
Tenure - Сколько лет человек является клиентом банка
Balance - Баланс счета
NumOfProducts - Количество открытых продуктов
HasCrCard - Есть ли у клиента кредитная карта
IsActiveMember - Является ли клиент активные участником
EstimatedSalary - Предположительная зарплата клиента
Exited - Уйдет ли человек в отток
df = pd.read_csv('./Churn_Modelling.csv')
df
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	1	1	101348.88	1
1	2	15647311	Hill	608	Spain	Female	41	1	83807.86	1	0	1	112542.58	0
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	1	0	113931.57	1
3	4	15701354	Boni	699	France	Female	39	1	0.00	2	0	0	93826.63	0
4	5	15737888	Mitchell	850	Spain	Female	43	2	125510.82	1	1	1	79084.10	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	1	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	1	1	101699.77	0
9997	9998	15584532	Liu	709	France	Female	36	7	0.00	1	0	1	42085.58	1
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	1	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	1	0	38190.78	0
10000 rows ? 14 columns

pd.read_csv('./Churn_Modelling.csv', header=1)
1	15634602	Hargrave	619	France	Female	42	2	0	1.1	1.2	1.3	101348.88	1.4
0	2	15647311	Hill	608	Spain	Female	41	1	83807.86	1	0	1	112542.58	0
1	3	15619304	Onio	502	France	Female	42	8	159660.80	3	1	0	113931.57	1
2	4	15701354	Boni	699	France	Female	39	1	0.00	2	0	0	93826.63	0
3	5	15737888	Mitchell	850	Spain	Female	43	2	125510.82	1	1	1	79084.10	0
4	6	15574012	Chu	645	Spain	Male	44	8	113755.78	2	1	0	149756.71	1
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9994	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	1	0	96270.64	0
9995	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	1	1	101699.77	0
9996	9998	15584532	Liu	709	France	Female	36	7	0.00	1	0	1	42085.58	1
9997	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	1	0	92888.52	1
9998	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	1	0	38190.78	0
9999 rows ? 14 columns

pd.read_csv('./Churn_Modelling.csv', sep=';')
RowNumber,CustomerId,Surname,CreditScore,Geography,Gender,Age,Tenure,Balance,NumOfProducts,HasCrCard,IsActiveMember,EstimatedSalary,Exited
0	1,15634602,Hargrave,619,France,Female,42,2,0,1...
1	2,15647311,Hill,608,Spain,Female,41,1,83807.86...
2	3,15619304,Onio,502,France,Female,42,8,159660....
3	4,15701354,Boni,699,France,Female,39,1,0,2,0,0...
4	5,15737888,Mitchell,850,Spain,Female,43,2,1255...
...	...
9995	9996,15606229,Obijiaku,771,France,Male,39,5,0,...
9996	9997,15569892,Johnstone,516,France,Male,35,10,...
9997	9998,15584532,Liu,709,France,Female,36,7,0,1,0...
9998	9999,15682355,Sabbatini,772,Germany,Male,42,3,...
9999	10000,15628319,Walker,792,France,Female,28,4,1...
10000 rows ? 1 columns

df
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	1	1	101348.88	1
1	2	15647311	Hill	608	Spain	Female	41	1	83807.86	1	0	1	112542.58	0
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	1	0	113931.57	1
3	4	15701354	Boni	699	France	Female	39	1	0.00	2	0	0	93826.63	0
4	5	15737888	Mitchell	850	Spain	Female	43	2	125510.82	1	1	1	79084.10	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	1	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	1	1	101699.77	0
9997	9998	15584532	Liu	709	France	Female	36	7	0.00	1	0	1	42085.58	1
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	1	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	1	0	38190.78	0
10000 rows ? 14 columns

df.head()
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	1	1	101348.88	1
1	2	15647311	Hill	608	Spain	Female	41	1	83807.86	1	0	1	112542.58	0
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	1	0	113931.57	1
3	4	15701354	Boni	699	France	Female	39	1	0.00	2	0	0	93826.63	0
4	5	15737888	Mitchell	850	Spain	Female	43	2	125510.82	1	1	1	79084.10	0
df.tail()
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	1	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	1	1	101699.77	0
9997	9998	15584532	Liu	709	France	Female	36	7	0.00	1	0	1	42085.58	1
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	1	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	1	0	38190.78	0
df.sample()
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
2057	2058	15679550	Chukwualuka	743	France	Male	32	9	0.0	2	1	0	175252.78	0
df.sample(frac=1)
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
4506	4507	15635177	Williamson	597	Spain	Female	66	3	0.00	1	1	1	70532.53	0
6087	6088	15730759	Chukwudi	561	France	Female	27	9	135637.00	1	1	0	153080.40	1
7529	7530	15575430	Robson	579	France	Female	33	1	118392.75	1	1	1	157564.75	0
6273	6274	15576935	Ampt	743	Spain	Male	43	2	161807.18	2	0	1	93228.86	1
838	839	15585888	Nwokezuike	553	Spain	Female	48	3	0.00	1	0	1	30730.95	1
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
439	440	15690134	Hughes	464	Germany	Female	42	3	85679.25	1	1	1	164104.74	0
2314	2315	15756056	Ku	561	Spain	Female	28	3	0.00	2	1	0	191387.76	0
8129	8130	15729246	Hardacre	847	Spain	Male	31	5	0.00	2	1	1	76326.67	0
5459	5460	15617507	Wilson	530	Spain	Female	36	7	0.00	2	1	0	80619.09	0
1677	1678	15801767	Yin	784	Spain	Female	40	8	0.00	2	1	0	108891.30	0
10000 rows ? 14 columns

df.sample(frac=0.5)
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
4510	4511	15657747	Zito	611	Germany	Female	43	9	127216.31	2	0	1	17913.25	0
7244	7245	15670029	Marcelo	445	France	Female	33	7	0.00	2	1	0	122625.68	0
4463	4464	15778975	Nnonso	850	Germany	Female	70	1	96947.58	3	1	0	62282.99	1
8997	8998	15631063	Trentino	710	France	Female	33	2	0.00	2	1	0	72945.32	0
9465	9466	15815259	Fang	835	France	Female	56	2	0.00	2	1	1	39820.13	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
2943	2944	15639277	Lin	678	France	Female	41	9	0.00	1	0	0	13160.03	0
3359	3360	15747878	Aiken	739	Spain	Male	60	4	0.00	1	1	1	51637.67	0
29	30	15656300	Lucciano	411	France	Male	29	0	59697.17	2	1	1	53483.21	0
659	660	15603065	Grubb	751	France	Female	30	6	0.00	2	1	0	15766.10	0
1948	1949	15569187	Fleming	680	Spain	Male	35	9	0.00	2	0	0	143774.06	0
5000 rows ? 14 columns

df.shape
(10000, 14)
Первичный анализ данных
Типы данных:

int: целочисленные значения. Пример: 9, 56, 30
float: вещественные значения (с плавающей точкой). Пример: 7.3, 9.0, 45.334
object/str: строковые значения. Пример: ‘hello, world’, ‘50 000’
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10000 entries, 0 to 9999
Data columns (total 14 columns):
RowNumber          10000 non-null int64
CustomerId         10000 non-null int64
Surname            10000 non-null object
CreditScore        10000 non-null int64
Geography          10000 non-null object
Gender             10000 non-null object
Age                10000 non-null int64
Tenure             10000 non-null int64
Balance            10000 non-null float64
NumOfProducts      10000 non-null int64
HasCrCard          10000 non-null int64
IsActiveMember     10000 non-null int64
EstimatedSalary    10000 non-null float64
Exited             10000 non-null int64
dtypes: float64(2), int64(9), object(3)
memory usage: 1.1+ MB
Выводятся значения:

Count - количество непропущенных объектов (там, где нет nan значений)
mean - арифметическое среднее
std - стандартное отклонение
min - минимальное значение
25% - квантиль 25 процентов
50% - квантиль 50 процентов или же медиана
75% - квантиль 75 процентов
max - максимальное значение
df.describe()
RowNumber	CustomerId	CreditScore	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
count	10000.00000	1.000000e+04	10000.000000	10000.000000	10000.000000	10000.000000	10000.000000	10000.00000	10000.000000	10000.000000	10000.000000
mean	5000.50000	1.569094e+07	650.528800	38.921800	5.012800	76485.889288	1.530200	0.70550	0.515100	100090.239881	0.203700
std	2886.89568	7.193619e+04	96.653299	10.487806	2.892174	62397.405202	0.581654	0.45584	0.499797	57510.492818	0.402769
min	1.00000	1.556570e+07	350.000000	18.000000	0.000000	0.000000	1.000000	0.00000	0.000000	11.580000	0.000000
25%	2500.75000	1.562853e+07	584.000000	32.000000	3.000000	0.000000	1.000000	0.00000	0.000000	51002.110000	0.000000
50%	5000.50000	1.569074e+07	652.000000	37.000000	5.000000	97198.540000	1.000000	1.00000	1.000000	100193.915000	0.000000
75%	7500.25000	1.575323e+07	718.000000	44.000000	7.000000	127644.240000	2.000000	1.00000	1.000000	149388.247500	0.000000
max	10000.00000	1.581569e+07	850.000000	92.000000	10.000000	250898.090000	4.000000	1.00000	1.000000	199992.480000	1.000000
df['Age'].min()
18
df['Balance'].max()
250898.09
df[['CreditScore', 'Age', 'Tenure']].mean()
CreditScore    650.5288
Age             38.9218
Tenure           5.0128
dtype: float64
Получаем 4 значения:

count - количество непропущенных объектов
unique - количество уникальных значений
top - самое частотное значение (мода)
freq - частота появления самого частотного значения
df.describe(include=['object'])
Surname	Geography	Gender
count	10000	10000	10000
unique	2932	3	2
top	Smith	France	Male
freq	32	5014	5457
df.dtypes
RowNumber            int64
CustomerId           int64
Surname             object
CreditScore          int64
Geography           object
Gender              object
Age                  int64
Tenure               int64
Balance            float64
NumOfProducts        int64
HasCrCard            int64
IsActiveMember       int64
EstimatedSalary    float64
Exited               int64
dtype: object
df['Age'].dtype
dtype('int64')
df['HasCrCard'].astype('bool')
0        True
1       False
2        True
3       False
4        True
        ...  
9995     True
9996     True
9997    False
9998     True
9999     True
Name: HasCrCard, Length: 10000, dtype: bool
df['HasCrCard'].dtype
dtype('int64')
df['HasCrCard'] = df['HasCrCard'].astype('bool')
df['HasCrCard'].dtype
dtype('bool')
df['Geography'].unique()
array(['France', 'Spain', 'Germany'], dtype=object)
df['Geography'].nunique()
3
df['Geography'].value_counts()
France     5014
Germany    2509
Spain      2477
Name: Geography, dtype: int64
df['Geography'].value_counts(normalize=True)
France     0.5014
Germany    0.2509
Spain      0.2477
Name: Geography, dtype: float64
Фильтрация
Фильтрация в pandas основывается на булевых масках.

Булевая маска — бинарные данные, которые используются для выбора определенных объектов из структуры данных.

df['Gender'] == 'Male'
0       False
1       False
2       False
3       False
4       False
        ...  
9995     True
9996     True
9997    False
9998     True
9999    False
Name: Gender, Length: 10000, dtype: bool
male = df[df['Gender'] == 'Male']
male
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
5	6	15574012	Chu	645	Spain	Male	44	8	113755.78	2	True	0	149756.71	1
6	7	15592531	Bartlett	822	France	Male	50	7	0.00	2	True	1	10062.80	0
8	9	15792365	He	501	France	Male	44	4	142051.07	2	False	1	74940.50	0
9	10	15592389	H?	684	France	Male	27	2	134603.88	1	True	1	71725.73	0
10	11	15767821	Bearce	528	France	Male	31	6	102016.72	2	False	0	80181.12	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9992	9993	15657105	Chukwualuka	726	Spain	Male	36	2	0.00	1	True	0	195192.40	0
9993	9994	15569266	Rahman	644	France	Male	28	7	155060.41	1	True	0	29179.52	0
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	True	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	True	1	101699.77	0
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	True	0	92888.52	1
5457 rows ? 14 columns

Логические И
При операторе & нужно, чтобы выполнялось два условия одновременно:

df[(df['Gender'] == 'Female') & (df['NumOfProducts'] >= 3)]
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	True	0	113931.57	1
7	8	15656148	Obinna	376	Germany	Female	29	4	115046.74	4	True	0	119346.88	1
30	31	15589475	Azikiwe	591	Spain	Female	39	3	0.00	3	True	0	140469.38	1
88	89	15622897	Sharpe	646	France	Female	46	4	0.00	3	True	0	93251.42	1
90	91	15757535	Heap	647	Spain	Female	44	5	0.00	3	True	1	174205.22	1
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9565	9566	15752294	Long	582	France	Female	38	9	135979.01	4	True	1	76582.95	1
9747	9748	15775761	Iweobiegbunam	610	Germany	Female	69	5	86038.21	3	False	0	192743.06	1
9800	9801	15640507	Li	762	Spain	Female	35	3	119349.69	3	True	1	47114.18	1
9877	9878	15572182	Onwuamaeze	505	Germany	Female	33	3	106506.77	3	True	0	45445.78	1
9895	9896	15796764	Bruno	684	Germany	Female	56	3	127585.98	3	True	1	80593.49	1
187 rows ? 14 columns

Логические ИЛИ
При операторе | нужно, чтобы выполнялось хотя бы одно условие:

df[(df['HasCrCard']) | (df['NumOfProducts'] >= 3)]
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	True	1	101348.88	1
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	True	0	113931.57	1
4	5	15737888	Mitchell	850	Spain	Female	43	2	125510.82	1	True	1	79084.10	0
5	6	15574012	Chu	645	Spain	Male	44	8	113755.78	2	True	0	149756.71	1
6	7	15592531	Bartlett	822	France	Male	50	7	0.00	2	True	1	10062.80	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9993	9994	15569266	Rahman	644	France	Male	28	7	155060.41	1	True	0	29179.52	0
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	True	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	True	1	101699.77	0
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	True	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	True	0	38190.78	0
7150 rows ? 14 columns

Логические НЕ
При операторе ~ булевая маска обращается: True меняется на False и наоборот:

df[~(df['Geography'] == 'Spain')]
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	True	1	101348.88	1
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	True	0	113931.57	1
3	4	15701354	Boni	699	France	Female	39	1	0.00	2	False	0	93826.63	0
6	7	15592531	Bartlett	822	France	Male	50	7	0.00	2	True	1	10062.80	0
7	8	15656148	Obinna	376	Germany	Female	29	4	115046.74	4	True	0	119346.88	1
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	True	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	True	1	101699.77	0
9997	9998	15584532	Liu	709	France	Female	36	7	0.00	1	False	1	42085.58	1
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	True	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	True	0	38190.78	0
7523 rows ? 14 columns

df[df['Geography'].isin(['France', 'Germany'])]
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
0	1	15634602	Hargrave	619	France	Female	42	2	0.00	1	True	1	101348.88	1
2	3	15619304	Onio	502	France	Female	42	8	159660.80	3	True	0	113931.57	1
3	4	15701354	Boni	699	France	Female	39	1	0.00	2	False	0	93826.63	0
6	7	15592531	Bartlett	822	France	Male	50	7	0.00	2	True	1	10062.80	0
7	8	15656148	Obinna	376	Germany	Female	29	4	115046.74	4	True	0	119346.88	1
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9995	9996	15606229	Obijiaku	771	France	Male	39	5	0.00	2	True	0	96270.64	0
9996	9997	15569892	Johnstone	516	France	Male	35	10	57369.61	1	True	1	101699.77	0
9997	9998	15584532	Liu	709	France	Female	36	7	0.00	1	False	1	42085.58	1
9998	9999	15682355	Sabbatini	772	Germany	Male	42	3	75075.31	2	True	0	92888.52	1
9999	10000	15628319	Walker	792	France	Female	28	4	130142.79	1	True	0	38190.78	0
7523 rows ? 14 columns

Индексация
df_small = df[(df['Geography'] == 'Spain')][['Geography', 'Gender', 'Age']]
df_small.head()
Geography	Gender	Age
1	Spain	Female	41
4	Spain	Female	43
5	Spain	Male	44
11	Spain	Male	24
14	Spain	Female	35
loc
df_small.loc[1]
Geography     Spain
Gender       Female
Age              41
Name: 1, dtype: object
df_small.loc[3]
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
   2896             try:
-> 2897                 return self._engine.get_loc(key)
   2898             except KeyError:

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.Int64HashTable.get_item()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.Int64HashTable.get_item()

KeyError: 3

During handling of the above exception, another exception occurred:

KeyError                                  Traceback (most recent call last)
<ipython-input-114-826e5ec6c72e> in <module>
----> 1 df_small.loc[3]

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in __getitem__(self, key)
   1422 
   1423             maybe_callable = com.apply_if_callable(key, self.obj)
-> 1424             return self._getitem_axis(maybe_callable, axis=axis)
   1425 
   1426     def _is_scalar_access(self, key: Tuple):

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in _getitem_axis(self, key, axis)
   1848         # fall thru to straight lookup
   1849         self._validate_key(key, axis)
-> 1850         return self._get_label(key, axis=axis)
   1851 
   1852 

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in _get_label(self, label, axis)
    158             raise IndexingError("no slices here, handle elsewhere")
    159 
--> 160         return self.obj._xs(label, axis=axis)
    161 
    162     def _get_loc(self, key: int, axis: int):

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/generic.py in xs(self, key, axis, level, drop_level)
   3735             loc, new_index = self.index.get_loc_level(key, drop_level=drop_level)
   3736         else:
-> 3737             loc = self.index.get_loc(key)
   3738 
   3739             if isinstance(loc, np.ndarray):

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
   2897                 return self._engine.get_loc(key)
   2898             except KeyError:
-> 2899                 return self._engine.get_loc(self._maybe_cast_indexer(key))
   2900         indexer = self.get_indexer([key], method=method, tolerance=tolerance)
   2901         if indexer.ndim > 1 or indexer.size > 1:

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.Int64HashTable.get_item()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.Int64HashTable.get_item()

KeyError: 3
df_small.loc[[1, 4, 5], ['Gender', 'Age']]
Gender	Age
1	Female	41
4	Female	43
5	Male	44
iloc
df_small.head()
Geography	Gender	Age
1	Spain	Female	41
4	Spain	Female	43
5	Spain	Male	44
11	Spain	Male	24
14	Spain	Female	35
df_small.iloc[[0, 1, 2]]
Geography	Gender	Age
1	Spain	Female	41
4	Spain	Female	43
5	Spain	Male	44
df_small.iloc[2500]
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-125-fdbc3008acb9> in <module>
----> 1 df_small.iloc[2500]

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in __getitem__(self, key)
   1422 
   1423             maybe_callable = com.apply_if_callable(key, self.obj)
-> 1424             return self._getitem_axis(maybe_callable, axis=axis)
   1425 
   1426     def _is_scalar_access(self, key: Tuple):

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in _getitem_axis(self, key, axis)
   2155 
   2156             # validate the location
-> 2157             self._validate_integer(key, axis)
   2158 
   2159             return self._get_loc(key, axis=axis)

~/teacher_geekbrains/venv/lib/python3.8/site-packages/pandas/core/indexing.py in _validate_integer(self, key, axis)
   2086         len_axis = len(self.obj._get_axis(axis))
   2087         if key >= len_axis or key < -len_axis:
-> 2088             raise IndexError("single positional indexer is out-of-bounds")
   2089 
   2090     def _getitem_tuple(self, tup):

IndexError: single positional indexer is out-of-bounds
df_small.iloc[0, [0, 2]]
Geography    Spain
Age             41
Name: 1, dtype: object
Сортировки
df.sort_values('Age')
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
3512	3513	15657779	Boylan	806	Spain	Male	18	3	0.00	2	True	1	86994.54	0
1678	1679	15569178	Kharlamov	570	France	Female	18	4	82767.42	1	True	0	71811.90	0
3517	3518	15757821	Burgess	771	Spain	Male	18	1	0.00	2	False	0	41542.95	0
9520	9521	15673180	Onyekaozulu	727	Germany	Female	18	2	93816.70	2	True	0	126172.11	0
2021	2022	15795519	Vasiliev	716	Germany	Female	18	3	128743.80	1	False	0	197322.13	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
3387	3388	15798024	Lori	537	Germany	Male	84	8	92242.34	1	True	1	186235.98	0
3033	3034	15578006	Yao	787	France	Female	85	10	0.00	2	True	1	116537.96	0
2458	2459	15813303	Rearick	513	Spain	Male	88	10	0.00	2	True	1	52952.24	0
6759	6760	15660878	T'ien	705	France	Male	92	1	126076.24	2	True	1	34436.83	0
6443	6444	15764927	Rogova	753	France	Male	92	3	121513.31	1	False	1	195563.99	0
10000 rows ? 14 columns

df.sort_values('Age', ascending=False)
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
6443	6444	15764927	Rogova	753	France	Male	92	3	121513.31	1	False	1	195563.99	0
6759	6760	15660878	T'ien	705	France	Male	92	1	126076.24	2	True	1	34436.83	0
2458	2459	15813303	Rearick	513	Spain	Male	88	10	0.00	2	True	1	52952.24	0
3033	3034	15578006	Yao	787	France	Female	85	10	0.00	2	True	1	116537.96	0
3387	3388	15798024	Lori	537	Germany	Male	84	8	92242.34	1	True	1	186235.98	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9782	9783	15728829	Weigel	509	France	Male	18	7	102983.91	1	True	0	171770.58	0
2141	2142	15758372	Wallace	674	France	Male	18	7	0.00	2	True	1	55753.12	1
9501	9502	15634146	Hou	835	Germany	Male	18	2	142872.36	1	True	1	117632.63	0
9520	9521	15673180	Onyekaozulu	727	Germany	Female	18	2	93816.70	2	True	0	126172.11	0
1619	1620	15770309	McDonald	656	France	Male	18	10	151762.74	1	False	1	127014.32	0
10000 rows ? 14 columns

df.sort_values(['Age', 'CreditScore'])
RowNumber	CustomerId	Surname	CreditScore	Geography	Gender	Age	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	EstimatedSalary	Exited
9782	9783	15728829	Weigel	509	France	Male	18	7	102983.91	1	True	0	171770.58	0
1678	1679	15569178	Kharlamov	570	France	Female	18	4	82767.42	1	True	0	71811.90	0
9029	9030	15722701	Bruno	594	Germany	Male	18	1	132694.73	1	True	0	167689.56	0
7334	7335	15759133	Vaguine	616	France	Male	18	6	0.00	2	True	1	27308.58	0
9526	9527	15665521	Chiazagomekpele	642	Germany	Male	18	5	111183.53	2	False	1	10063.75	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
3387	3388	15798024	Lori	537	Germany	Male	84	8	92242.34	1	True	1	186235.98	0
3033	3034	15578006	Yao	787	France	Female	85	10	0.00	2	True	1	116537.96	0
2458	2459	15813303	Rearick	513	Spain	Male	88	10	0.00	2	True	1	52952.24	0
6759	6760	15660878	T'ien	705	France	Male	92	1	126076.24	2	True	1	34436.83	0
6443	6444	15764927	Rogova	753	France	Male	92	3	121513.31	1	False	1	195563.99	0
10000 rows ? 14 columns