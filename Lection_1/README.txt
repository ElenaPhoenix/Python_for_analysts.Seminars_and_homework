https://gbcdn.mrgcdn.ru/uploads/asset/4239327/attachment/67ca2d700eae346cc89b98a0d92b1329.html

Горячие клавиши
Edit Mode (press Enter to enable)
Ctrl-A : select all.
Ctrl Home : go to cell start.
Ctrl End : go to cell end.
Ctrl Left : go one word left.
Ctrl Right : go one word right.
Tab : code completion or indent
Shift-Tab : tooltip
pow()
8
?pow
Ctrl-Z : undo
Ctrl-/ : comment
Ctrl-D : delete whole line
value = 3
value += 1
Command Mode (press Esc to enable)
Up : select cell above
Down : select cell below
Shift-Enter : run cell, select below
Ctrl-Enter : run selected cells
Alt-Enter : run cell and insert below
A : insert cell above
B : insert cell below
X : cut selected cells
C : copy selected cells
V : paste cells below
F : find and replace
value = 5
value += 1
value -= 10
Y : change cell to code
M : change cell to markdown
1 : change cell to heading 1
2 : change cell to heading 2
3 : change cell to heading 3
4 : change cell to heading 4
5 : change cell to heading 5
6 : change cell to heading 6
L : toggle line numbers
H : show keyboard shortcuts
I,I : interrupt the kernel
0,0 : restart the kernel (with dialog)
a = 12
3 / 0
b = 3
a + b
---------------------------------------------------------------------------
ZeroDivisionError                         Traceback (most recent call last)
<ipython-input-5-526983b54e29> in <module>
      1 a = 12
----> 2 3 / 0
      3 b = 3
      4 a + b

ZeroDivisionError: division by zero
for i in range(1000000000):
    pass
---------------------------------------------------------------------------
KeyboardInterrupt                         Traceback (most recent call last)
<ipython-input-21-01acf624e1ef> in <module>
----> 1 for i in range(1000000000):
      2     pass

KeyboardInterrupt: 
Markdown - облегчённый язык разметки, созданный с целью обозначения форматирования в простом тексте, с максимальным сохранением его читаемости человеком, и пригодный для машинного преобразования в языки для продвинутых публикаций.

жирный
fdgdfg
курсив
fgfd

список
список
Latex
1
n
?
x
i
j


Тэг HTML - элемент языка разметки. Текст, содержащийся между начальным и конечным тегом, отображается и размещается в соответствии со свойствами, указанными в начальном теге.

 жирный

курсив

текст
а вот и новая строка

первый столбик	второй столбик
первый столбик	второй столбик
Словари
Словарь - неупорядоченная структура данных, которая позволяет хранить пары «ключ — значение».

client_data = {
    'name': 'John',
    'surname': 'Doe',
    'age': 32
}

client_data
{'name': 'John', 'surname': 'Doe', 'age': 32}
client_data['name']
'John'
client_data.keys()
dict_keys(['name', 'surname', 'age'])
client_data.values()
dict_values(['John', 'Doe', 32])
client_data.items()
dict_items([('name', 'John'), ('surname', 'Doe'), ('age', 32)])
for k, v in client_data.items():
    print(f'{k}: {v}')
name: John
surname: Doe
age: 32
client_data['height'] = 186
client_data
{'gender': 'Male', 'age': 14, 'height': 186}
client_data['age'] = 14
client_data
{'gender': 'Male', 'age': 14, 'height': 186}
client_data = {
    'name': 'John',
    'surname': 'Doe',
    'age': 32
}

client_data
{'name': 'John', 'surname': 'Doe', 'age': 32}
client_data.setdefault('age', 14)
32
client_data
{'name': 'John', 'surname': 'Doe', 'age': 32}
client_data.update({
    'age': 14
})
client_data
{'name': 'John', 'surname': 'Doe', 'age': 14}
Вложенный словарь – это словарь, содержащий другие словари.

client_data.update({
    'age': 15,
    'body': {
        'weight': 80,
        'height': 186
    }
})

client_data
{'name': 'John',
 'surname': 'Doe',
 'age': 15,
 'body': {'weight': 80, 'height': 186}}
client_data['body']
{'weight': 80, 'height': 186}
client_data['body']['height']
186
Модуль Random
Модуль random предоставляет функции для генерации случайных чисел или к примеру, для случайного выбора элементов последовательности. Посмотрим на самые полезные функции.

import random
random.randint(0, 10)
9
random.seed(9)
random.randint(0, 10)
7
random.random()
0.9772194595909891
random.uniform(0, 10)
7.835047467372638
a = ['black', 'red', 'yellow', 'green']
random.sample(a, 2)
['yellow', 'red']
random.shuffle(a)
a
['green', 'yellow', 'black', 'red']
random.choice(a)
'black'
Функции
Функция в python - объект, который принимает аргументы, производит с ними желаемые действия и возвращает значение. Также функция — это фрагмент программного кода, который решает какую-либо задачу. Его можно вызывать в любом месте основной программы. Функции помогают избегать дублирования кода при многократном его использовании.

Аргумент функции — значение, которое передается в функцию при её вызове.

def func(arg1, arg2):
    # make magic
    result = arg1 + arg2
    return result
Аргументы по позиции и имени
Позиционный аргумент - это аргумент, передаваемый в функцию в определенной последовательности (на определенных позициях), без указания их имен

def calc_sum(a, b):
    print(f'a is {a}')
    print(f'b is {b}')
    result = a + b 
    return result
calc_sum(3, 5)
a is 3
b is 5
8
Именованный аргумент - это аргумент, передаваемые в функцию при помощи имени.

calc_sum(a=3, b=5)
a is 3
b is 5
8
calc_sum(b=5, a=3)
a is 3
b is 5
8
calc_sum(b=5, 3)
  File "<ipython-input-53-93aa6c5cb30e>", line 1
    calc_sum(b=5, 3)
                  ^
SyntaxError: positional argument follows keyword argument
calc_sum(3, b=5)
a is 3
b is 5
8
Аргументы по умолчанию
В функцию можно передавать аргументы по умолчанию, это те аргументы, значения которых будут использованы, если не передали им явное значение при вызове.

def say_hi(greeting='Hello', name='World'):
    return f'{greeting}, {name}'
say_hi()
'Hello, World'
def say_hi(greeting, name='World'):
    return f'{greeting}, {name}'
say_hi()
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-60-6acd93c5568f> in <module>
----> 1 say_hi()

TypeError: say_hi() missing 1 required positional argument: 'greeting'
def say_hi(greeting='Hello', name='World'):
    return f'{greeting}, {name}'
say_hi(greeting='Hey', name='Apple')
'Hey, Apple'
Аргумент *args
*args — это сокращение от «arguments» (аргументы).

def calc_sum(a, b, c):
    result = a + b + c
    return result
def calc_sum(a, b, c, d, e):
    result = a + b + c + d + e
    return result
def calc_sum(*args):
    result = sum(args)
    return result
calc_sum(1)
1
calc_sum(10, 0, 5)
15
def calc_sum(*args):
    print(args)
    print(type(args))
    result = sum(args)
    return result
calc_sum(1, 2, 3)
(1, 2, 3)
<class 'tuple'>
6
def printer(*args):
    print(type(args))
    print(args)
    print()
    for i in args:
        print(i)
printer(1, 'text', {'key': 'value'})
<class 'tuple'>
(1, 'text', {'key': 'value'})

1
text
{'key': 'value'}
names = ['John', 'Nick', 'Bill']
printer(names)
<class 'tuple'>
(['John', 'Nick', 'Bill'],)

['John', 'Nick', 'Bill']
printer(*names)
<class 'tuple'>
('John', 'Nick', 'Bill')

John
Nick
Bill
Атрибут **kwargs
**kwargs — сокращение от «keyword arguments» (именованные аргументы).

def printer(**kwargs):
    print(type(kwargs))
    print()
    for key, value in kwargs.items():
        print(f'{key} - {value}')
printer(a=10, b='20')
<class 'dict'>

a - 10
b - 20
def say_hi(**kwargs):
    greeting = kwargs.get('greeting', 'Hello')
    name = kwargs.get('name', 'World')
    return f'{greeting}, {name}'
say_hi()
'Hello, World'
say_hi(greeting='Hey', name='John')
'Hey, John'
say_hi(greeting='Hey', name='John', extra=5)
'Hey, John'
data = {'greeting': 'Hey',
        'name': 'John',
        'extra':5}

say_hi(**data)
'Hey, John'
Аннотирование типов
def calc_sum(a: int, b: int) -> int:
    return a + b
calc_sum(1, 2)
3
calc_sum(1.1, 2.2)
3.3000000000000003
calc_sum('abc', 'dce')
'abcdce'
Генераторы
Допустим, у вас есть файл, который весит десяток гигабайт. Из него нужно выбрать и обработать строки, подходящие под какое-то условие. Что в такой ситуации делать? А можно обрабатывать такие объемы данных небольшими порциями, чтобы не вызывать переполнения памяти. В Python на этот случай есть специальный инструмент — генераторы.

Генератор - это объект, который сразу при создании не вычисляет значения всех своих элементов.

Генератор хранит в памяти:

последний вычисленный элемент
правило перехода к следующему
условие, при котором выполнение прерывается
Вычисление следующего значения происходит лишь при выполнении метода next(). Предыдущее значение при этом теряется. Этим генераторы отличаются от списков, ведь списки хранят в памяти все свои элементы, и удалить их можно только программно. Вычисления с помощью генераторов экономят память.

def my_range(start, end):
    current = start
    while current < end:
        yield current
        current += 1
Оператор yield приостанавливает функцию и сохраняет локальное состояние, чтобы его можно было возобновить с того места, где оно было остановлено.

ranger = my_range(0, 2)
ranger
<generator object my_range at 0x7f137c05c580>
next(ranger)
0
next(ranger)
1
next(ranger)
---------------------------------------------------------------------------
StopIteration                             Traceback (most recent call last)
<ipython-input-10-c186e1cb4ee7> in <module>
----> 1 next(ranger)

StopIteration: 
gen_a = my_range(2, 5)
for i in gen_a:
    print(i)
2
3
4
for i in gen_a:
    print(i)
list comprehensions
squares = []
for i in range(5):
    squares.append(i * i)
squares
[0, 1, 4, 9, 16]
squares = [i * i for i in range(5)]
squares
[0, 1, 4, 9, 16]
# new_list = [expression for member in iterable]
even_nums = []
for i in range(10):
    if i % 2 == 0:
        even_nums.append(i)

even_nums
[0, 2, 4, 6, 8]
even_nums = [i for i in range(10) if i % 2 == 0]
even_nums
[0, 2, 4, 6, 8]
orig_prices = [125, -9, 103, 38, -5, 116]
prices = [i if i > 0 else 0 for i in orig_prices]
prices
[125, 0, 103, 38, 0, 116]
def get_price(price):
    return price if price > 0 else 0


prices = [get_price(i) for i in orig_prices]
prices
[125, 0, 103, 38, 0, 116]
set comprehensions
numbers = ['black', 'red', 'green', 'green', 'red', 'green']
{i for i in numbers}
{'black', 'green', 'red'}
dict comprehensions
squares_dict = {i: i * i for i in range(5)}
squares_dict
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
%%time

even_nums = []
for i in range(100_000_000):
    if i % 2 == 0:
        even_nums.append(i)
CPU times: user 10.6 s, sys: 373 ms, total: 11 s
Wall time: 11 s
%%time
even_nums = [i for i in range(100_000_000) if i % 2 == 0]
CPU times: user 3.74 s, sys: 441 ms, total: 4.18 s
Wall time: 4.18 s