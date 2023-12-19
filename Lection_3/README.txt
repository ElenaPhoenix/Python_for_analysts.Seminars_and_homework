https://gbcdn.mrgcdn.ru/uploads/asset/4239332/attachment/7d8be3cf1f6192275f44c62047e51fc7.html

import pandas as pd
Будем работать с датасетом по оттоку клиентов из банка https://www.kaggle.com/datasets/shubh0799/churn-modelling, но датасет из себя будет представлять две таблицы:

Личные данные клиента

CustomerId - Уникальный идентификатор клиента
Surname - Фамилия клиента
Geography - Из какой страны клиент
Gender - Пол клиента
Age - Возраст клиента
EstimatedSalary - Предположительная зарплата клиента
Данные по поведению клиента в банке

CustomerId - Уникальный идентификатор клиента
CustomerId - Уникальный идентификатор клиента
Tenure - Сколько лет человек является клиентом банка
Balance - Баланс счета
NumOfProducts - Количество открытых продуктов
HasCrCard - Есть ли у клиента кредитная карта
IsActiveMember - Является ли клиент активные участником
Exited - Уйдет ли человек в отток
users = pd.read_csv('users.csv', sep=';')
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary
0	15634602	Hargrave	France	Female	42	101348.88
1	15647311	Hill	Spain	Female	41	112542.58
2	15619304	Onio	France	Female	42	113931.57
3	15701354	Boni	France	Female	39	93826.63
4	15737888	Mitchell	Spain	Female	43	79084.10
users.shape
(9998, 6)
Создание новых признаков
users['new_feature'] = 0
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	new_feature
0	15634602	Hargrave	France	Female	42	101348.88	0
1	15647311	Hill	Spain	Female	41	112542.58	0
2	15619304	Onio	France	Female	42	113931.57	0
3	15701354	Boni	France	Female	39	93826.63	0
4	15737888	Mitchell	Spain	Female	43	79084.10	0
users['Age (days)'] = users['Age'] * 365
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	new_feature	Age (days)
0	15634602	Hargrave	France	Female	42	101348.88	0	15330
1	15647311	Hill	Spain	Female	41	112542.58	0	14965
2	15619304	Onio	France	Female	42	113931.57	0	15330
3	15701354	Boni	France	Female	39	93826.63	0	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	0	15695
for i, row in users.iloc[:2].iterrows():
    print(row)
    print('__' * 30)
CustomerId          15634602
Surname             Hargrave
Geography             France
Gender                Female
Age                       42
EstimatedSalary    101348.88
new_feature                0
Age (days)             15330
Name: 0, dtype: object
____________________________________________________________
CustomerId          15647311
Surname                 Hill
Geography              Spain
Gender                Female
Age                       41
EstimatedSalary    112542.58
new_feature                0
Age (days)             14965
Name: 1, dtype: object
____________________________________________________________
age_days = []

for i, row in users.iterrows():
    age_days.append(row['Age'] * 365)

age_days[:10]
[15330, 14965, 15330, 14235, 15695, 16060, 18250, 10585, 16060, 9855]
users['Age (days) 2'] = age_days
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	new_feature	Age (days)	Age (days) 2
0	15634602	Hargrave	France	Female	42	101348.88	0	15330	15330
1	15647311	Hill	Spain	Female	41	112542.58	0	14965	14965
2	15619304	Onio	France	Female	42	113931.57	0	15330	15330
3	15701354	Boni	France	Female	39	93826.63	0	14235	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	0	15695	15695
def age_to_days(x):
    return x * 365

users['Age (days) 3'] = users['Age'].apply(age_to_days)
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	new_feature	Age (days)	Age (days) 2	Age (days) 3
0	15634602	Hargrave	France	Female	42	101348.88	0	15330	15330	15330
1	15647311	Hill	Spain	Female	41	112542.58	0	14965	14965	14965
2	15619304	Onio	France	Female	42	113931.57	0	15330	15330	15330
3	15701354	Boni	France	Female	39	93826.63	0	14235	14235	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	0	15695	15695	15695
import time
from tqdm import tqdm
tqdm.pandas()


def age_to_days(x):
    time.sleep(0.001)
    return x * 365

users['Age'].progress_apply(age_to_days)
100%|----------| 9998/9998 [00:11<00:00, 907.22it/s]
0       15330
1       14965
2       15330
3       14235
4       15695
        ...  
9993    10220
9994    10585
9995    14235
9996    12775
9997    13140
Name: Age, Length: 9998, dtype: int64
Удаление признаков
users.drop(columns='new_feature')
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	new_feature	Age (days)	Age (days) 2	Age (days) 3
0	15634602	Hargrave	France	Female	42	101348.88	0	15330	15330	15330
1	15647311	Hill	Spain	Female	41	112542.58	0	14965	14965	14965
2	15619304	Onio	France	Female	42	113931.57	0	15330	15330	15330
3	15701354	Boni	France	Female	39	93826.63	0	14235	14235	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	0	15695	15695	15695
users = users.drop(columns='new_feature')
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	Age (days)	Age (days) 2	Age (days) 3
0	15634602	Hargrave	France	Female	42	101348.88	15330	15330	15330
1	15647311	Hill	Spain	Female	41	112542.58	14965	14965	14965
2	15619304	Onio	France	Female	42	113931.57	15330	15330	15330
3	15701354	Boni	France	Female	39	93826.63	14235	14235	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	15695	15695	15695
users['new_feature'] = 0
users.drop(columns='new_feature', inplace=True)
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	Age (days)	Age (days) 2	Age (days) 3
0	15634602	Hargrave	France	Female	42	101348.88	15330	15330	15330
1	15647311	Hill	Spain	Female	41	112542.58	14965	14965	14965
2	15619304	Onio	France	Female	42	113931.57	15330	15330	15330
3	15701354	Boni	France	Female	39	93826.63	14235	14235	14235
4	15737888	Mitchell	Spain	Female	43	79084.10	15695	15695	15695
users.drop(columns=['Age (days)', 'Age (days) 2', 'Age (days) 3'], inplace=True)
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary
0	15634602	Hargrave	France	Female	42	101348.88
1	15647311	Hill	Spain	Female	41	112542.58
2	15619304	Onio	France	Female	42	113931.57
3	15701354	Boni	France	Female	39	93826.63
4	15737888	Mitchell	Spain	Female	43	79084.10
Изменение существующих признаков
.loc
users['target'] = 0
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15634602	Hargrave	France	Female	42	101348.88	0
1	15647311	Hill	Spain	Female	41	112542.58	0
2	15619304	Onio	France	Female	42	113931.57	0
3	15701354	Boni	France	Female	39	93826.63	0
4	15737888	Mitchell	Spain	Female	43	79084.10	0
users.loc[users['Geography'] == 'France']
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15634602	Hargrave	France	Female	42	101348.88	0
2	15619304	Onio	France	Female	42	113931.57	0
3	15701354	Boni	France	Female	39	93826.63	0
6	15592531	Bartlett	France	Male	50	10062.80	0
8	15792365	He	France	Male	44	74940.50	0
...	...	...	...	...	...	...	...
9993	15569266	Rahman	France	Male	28	29179.52	0
9994	15719294	Wood	France	Female	29	167773.55	0
9995	15606229	Obijiaku	France	Male	39	96270.64	0
9996	15569892	Johnstone	France	Male	35	101699.77	0
9997	15584532	Liu	France	Female	36	42085.58	0
5013 rows ? 7 columns

users.loc[users['Geography'] == 'France', 'target']
0       0
2       0
3       0
6       0
8       0
       ..
9993    0
9994    0
9995    0
9996    0
9997    0
Name: target, Length: 5013, dtype: int64
users[users['Geography'] == 'France']['target'] = 1
users.head()
<ipython-input-19-b763340dfd50>:1: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  users[users['Geography'] == 'France']['target'] = 1
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15634602	Hargrave	France	Female	42	101348.88	0
1	15647311	Hill	Spain	Female	41	112542.58	0
2	15619304	Onio	France	Female	42	113931.57	0
3	15701354	Boni	France	Female	39	93826.63	0
4	15737888	Mitchell	Spain	Female	43	79084.10	0
users.loc[users['Geography'] == 'France', 'target'] = 1
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15634602	Hargrave	France	Female	42	101348.88	1
1	15647311	Hill	Spain	Female	41	112542.58	0
2	15619304	Onio	France	Female	42	113931.57	1
3	15701354	Boni	France	Female	39	93826.63	1
4	15737888	Mitchell	Spain	Female	43	79084.10	0
.replace
users['Gender'].replace({'Female': 'F', 'Male': 'M'}, inplace=True)
users.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15634602	Hargrave	France	F	42	101348.88	1
1	15647311	Hill	Spain	F	41	112542.58	0
2	15619304	Onio	France	F	42	113931.57	1
3	15701354	Boni	France	F	39	93826.63	1
4	15737888	Mitchell	Spain	F	43	79084.10	0
Методы агрегации
users['Age'].agg(['min', 'max'])
min    18
max    92
Name: Age, dtype: int64
users.agg({
    'Age': ['min', 'max'],
    'EstimatedSalary': 'mean'
})
Age	EstimatedSalary
min	18.0	NaN
max	92.0	NaN
mean	NaN	100097.151381
users.agg(
    min_age=('Age', 'min'),
    max_age=('Age', 'max'),
    mean_salary=('EstimatedSalary', 'mean')
)
Age	EstimatedSalary
min_age	18.0	NaN
max_age	92.0	NaN
mean_salary	NaN	100097.151381
Методы объединения
bank = pd.read_csv('bank.csv', sep=';')
bank.head()
CustomerId	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited
0	15597909	652	7	128135.99	1	1	0	0
1	15687913	501	7	93244.42	1	0	1	0
2	15619087	762	1	102520.37	1	1	1	0
3	15596552	535	5	134542.73	1	1	1	1
4	15741417	624	7	119656.45	2	1	1	0
bank.shape
(9895, 8)
merged = users.merge(bank, left_on='CustomerId', right_on='CustomerId')
merged.head()
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited
0	15634602	Hargrave	France	F	42	101348.88	1	619	2	0.00	1	1	1	1
1	15647311	Hill	Spain	F	41	112542.58	0	608	1	83807.86	1	0	1	0
2	15619304	Onio	France	F	42	113931.57	1	502	8	159660.80	3	1	0	1
3	15701354	Boni	France	F	39	93826.63	1	699	1	0.00	2	0	0	0
4	15737888	Mitchell	Spain	F	43	79084.10	0	850	2	125510.82	1	1	1	0
users_id = users.set_index('CustomerId')
users_id.head()
Surname	Geography	Gender	Age	EstimatedSalary	target
CustomerId						
15634602	Hargrave	France	F	42	101348.88	1
15647311	Hill	Spain	F	41	112542.58	0
15619304	Onio	France	F	42	113931.57	1
15701354	Boni	France	F	39	93826.63	1
15737888	Mitchell	Spain	F	43	79084.10	0
bank_id = bank.set_index('CustomerId')
bank_id.head()
CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited
CustomerId							
15597909	652	7	128135.99	1	1	0	0
15687913	501	7	93244.42	1	0	1	0
15619087	762	1	102520.37	1	1	1	0
15596552	535	5	134542.73	1	1	1	1
15741417	624	7	119656.45	2	1	1	0
bank_id.join(users_id).head()
CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited	Surname	Geography	Gender	Age	EstimatedSalary	target
CustomerId													
15597909	652	7	128135.99	1	1	0	0	Johnstone	Germany	M	33.0	158437.73	0.0
15687913	501	7	93244.42	1	0	1	0	Mai	Germany	F	34.0	199805.63	0.0
15619087	762	1	102520.37	1	1	1	0	Taylor	France	M	53.0	170195.40	1.0
15596552	535	5	134542.73	1	1	1	1	Stephens	Germany	M	48.0	58203.67	0.0
15741417	624	7	119656.45	2	1	1	0	Chibuzo	Spain	F	35.0	4595.05	0.0
bank_id.join(users_id).reset_index().head()
CustomerId	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited	Surname	Geography	Gender	Age	EstimatedSalary	target
0	15597909	652	7	128135.99	1	1	0	0	Johnstone	Germany	M	33.0	158437.73	0.0
1	15687913	501	7	93244.42	1	0	1	0	Mai	Germany	F	34.0	199805.63	0.0
2	15619087	762	1	102520.37	1	1	1	0	Taylor	France	M	53.0	170195.40	1.0
3	15596552	535	5	134542.73	1	1	1	1	Stephens	Germany	M	48.0	58203.67	0.0
4	15741417	624	7	119656.45	2	1	1	0	Chibuzo	Spain	F	35.0	4595.05	0.0
bank.shape
(9895, 8)
Атрибут how


toy_df1 = pd.DataFrame({
    'col_1': [1, 2, 3],
    'col_2': [9, 9, 9]
})

toy_df2 = pd.DataFrame({
    'col_1': [3, 4],
    'col_3': [0, 0]
})

display(toy_df1, toy_df2)
col_1	col_2
0	1	9
1	2	9
2	3	9
col_1	col_3
0	3	0
1	4	0
toy_df1.merge(toy_df2, how='left')
col_1	col_2	col_3
0	1	9	NaN
1	2	9	NaN
2	3	9	0.0
toy_df1.merge(toy_df2, how='right')
col_1	col_2	col_3
0	3	9.0	0
1	4	NaN	0
toy_df1.merge(toy_df2, how='inner')
col_1	col_2	col_3
0	3	9	0
toy_df1.merge(toy_df2, how='outer')
col_1	col_2	col_3
0	1	9.0	NaN
1	2	9.0	NaN
2	3	9.0	0.0
3	4	NaN	0.0
left
merged_left = bank.merge(users, on='CustomerId', how='left')
merged_left.shape
(9895, 14)
merged_left.isna().sum()
CustomerId         0
CreditScore        0
Tenure             0
Balance            0
NumOfProducts      0
HasCrCard          0
IsActiveMember     0
Exited             0
Surname            2
Geography          2
Gender             2
Age                2
EstimatedSalary    2
target             2
dtype: int64
merged_left[merged_left['Age'].isna()]
CustomerId	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited	Surname	Geography	Gender	Age	EstimatedSalary	target
6922	15682355	772	3	75075.31	2	1	0	1	NaN	NaN	NaN	NaN	NaN	NaN
7360	15628319	792	4	130142.79	1	1	0	0	NaN	NaN	NaN	NaN	NaN	NaN
users[users['CustomerId'] == 15682355]
CustomerId	Surname	Geography	Gender	Age	EstimatedSalary	target
right
merged_right = bank.merge(users, on='CustomerId', how='right')
merged_right.shape
(9998, 14)
merged_right.isna().sum()
CustomerId           0
CreditScore        105
Tenure             105
Balance            105
NumOfProducts      105
HasCrCard          105
IsActiveMember     105
Exited             105
Surname              0
Geography            0
Gender               0
Age                  0
EstimatedSalary      0
target               0
dtype: int64
merged_right[merged_right['CreditScore'].isna()]
CustomerId	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited	Surname	Geography	Gender	Age	EstimatedSalary	target
169	15611325	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Wood	Germany	M	24	53134.30	0
342	15681081	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Marrero	Spain	F	47	38970.14	0
371	15774696	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Cole	Germany	F	75	113428.77	0
609	15586585	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Duncan	Germany	F	51	86410.28	0
629	15692463	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Rahman	Spain	F	28	45042.56	0
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
9367	15785024	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Warner	France	F	40	175877.70	1
9515	15792922	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Tu	Spain	M	38	81861.10	0
9561	15810010	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Dahlenburg	Germany	M	36	53172.02	0
9691	15754599	NaN	NaN	NaN	NaN	NaN	NaN	NaN	K'ung	France	M	42	82868.34	1
9766	15795511	NaN	NaN	NaN	NaN	NaN	NaN	NaN	Vasiliev	Germany	M	39	13906.34	0
105 rows ? 14 columns

bank[bank['CustomerId'] == 15611325]
CustomerId	CreditScore	Tenure	Balance	NumOfProducts	HasCrCard	IsActiveMember	Exited
inner
merged_inner = bank.merge(users, on='CustomerId', how='inner')
merged_inner.shape
(9893, 14)
merged_inner.isna().sum()
CustomerId         0
CreditScore        0
Tenure             0
Balance            0
NumOfProducts      0
HasCrCard          0
IsActiveMember     0
Exited             0
Surname            0
Geography          0
Gender             0
Age                0
EstimatedSalary    0
target             0
dtype: int64
outer
merged_outer = bank.merge(users, on='CustomerId', how='outer')
merged_outer.shape
(10000, 14)
merged_outer.isna().sum()
CustomerId           0
CreditScore        105
Tenure             105
Balance            105
NumOfProducts      105
HasCrCard          105
IsActiveMember     105
Exited             105
Surname              2
Geography            2
Gender               2
Age                  2
EstimatedSalary      2
target               2
dtype: int64
Методы группировок
groupby


toy_df = pd.DataFrame({
    'client_id': [1, 2, 2, 3, 1, 1],
    'item': ['chocolate', 'cheese', 'ham', 'candy', 'chair', 'book'],
    'price': [68, 280, 302, 39, 2099, 1089]
})

toy_df
client_id	item	price
0	1	chocolate	68
1	2	cheese	280
2	2	ham	302
3	3	candy	39
4	1	chair	2099
5	1	book	1089
grouped = toy_df.groupby('client_id')
grouped
<pandas.core.groupby.generic.DataFrameGroupBy object at 0x7f871b370610>
grouped.groups
{1: [0, 4, 5], 2: [1, 2], 3: [3]}
grouped.sum()
price
client_id	
1	3256
2	582
3	39
grouped.agg({'price': ['sum', 'min', 'max']})
price
sum	min	max
client_id			
1	3256	68	2099
2	582	280	302
3	39	39	39
users.groupby('Geography').agg({'Age': ['mean'], 'EstimatedSalary': ['min']})
Age	EstimatedSalary
mean	min
Geography		
France	38.513864	90.07
Germany	39.770734	11.58
Spain	38.890997	417.41
pivot_table
toy_df
client_id	item	price
0	1	chocolate	68
1	2	cheese	280
2	2	ham	302
3	3	candy	39
4	1	chair	2099
5	1	book	1089
toy_df.pivot_table(index='client_id',
                   values='price',
                   aggfunc='sum')
price
client_id	
1	3256
2	582
3	39
users.pivot_table(index='Geography',
                  aggfunc={'Age': ['mean'], 'EstimatedSalary': 'min'})
Age	EstimatedSalary
mean	min
Geography		
France	38.513864	90.07
Germany	39.770734	11.58
Spain	38.890997	417.41
users.pivot_table(index='Geography',
                  columns='Gender', 
                  values='EstimatedSalary',
                  aggfunc='mean',
                  margins=True,
                  margins_name='Total')
Gender	F	M	Total
Geography			
France	99591.409159	100174.252495	99911.490489
Germany	102446.424124	99910.369711	101116.714573
Spain	100734.107475	98425.687680	99440.572281
Total	100615.282193	99665.818876	100097.151381
crosstab
pd.crosstab(index=users['Geography'],
            columns=users['Gender'])
Gender	F	M
Geography		
France	2260	2753
Germany	1193	1315
Spain	1089	1388
pd.crosstab(index=users['Geography'],
            columns=users['Gender'],
            values=users['EstimatedSalary'],
            aggfunc='mean')
Gender	F	M
Geography		
France	99591.409159	100174.252495
Germany	102446.424124	99910.369711
Spain	100734.107475	98425.687680
pd.crosstab(index=users['Geography'],
            columns=users['Gender'],
            normalize='all')
Gender	F	M
Geography		
France	0.226045	0.275355
Germany	0.119324	0.131526
Spain	0.108922	0.138828
pd.crosstab(index=users['Geography'],
            columns=users['Gender'],
            normalize='index')
Gender	F	M
Geography		
France	0.450828	0.549172
Germany	0.475678	0.524322
Spain	0.439645	0.560355
pd.crosstab(index=users['Geography'],
            columns=users['Gender'],
            normalize='columns')
Gender	F	M
Geography		
France	0.497578	0.504582
Germany	0.262660	0.241019
Spain	0.239762	0.254399
Встроенные визуализации
users['Age'].hist();

data = users.groupby('Gender').count()['Age']
data.name = 'Gender'
data
Gender
F    4542
M    5456
Name: Gender, dtype: int64
data.plot.pie(y='Gender');

users.iloc[:100].plot.scatter(x='Age', y='EstimatedSalary');

data = bank.groupby('Tenure').count()['Balance']
data.name = 'num_clients'
data
Tenure
0      411
1     1027
2     1036
3      994
4      978
5     1000
6      957
7     1020
8     1014
9      971
10     487
Name: num_clients, dtype: int64
data.plot.bar(width=0.8);
