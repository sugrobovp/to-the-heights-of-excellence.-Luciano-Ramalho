# Списковые включения

### Пример 1. Сравнение с map + filter
```python
a = [1,2,3,4,5,6,193,-32]
b = [x for x in a if abs(x) > 7]
c = list(filter(lambda c: abs(c) > 7, a))
print(b)
print(c)
# [193, -32]
# [193, -32]
```
Очевидно, списковое включение легче читается и более того, работает быстрее.
### Пример 2. Декартово произведение
```python
colors = ['black', 'white']
sizes = ['S', 'M', 'L']
tshirts = [(color, size) for color in colors for size in sizes]
thirts
>>>[('black', 'S'), ('black', 'M'), ('black', 'L'), ('white', 'S'), ('white', 'M', ('white', 'L'))]
```
Второй вариант был бы делать цикл for внутри for, что выглядит хуже
```python
for color in colors:
    for size in sizes:
        print((color, size))
```
### Пример 3. Генераторные выражения для инициализации кортежей, массивов
```python
symbols = 'YASDASD'
tuple(ord(symbol) for symbol in symbols)
>>> (65, 83, 68, 65, 83, 68)
import array
array.array('I', (ord(symbol) for symbol in symbols))
>>> array('I', [65, 83, 68, 65, 83, 68])
```
### Пример 4. Генераторное выражение для декартова произведения
```python
colors = ['black', 'white']
sizes = ['S', 'M', 'L']
for tshirt in (f'{c} {s}' for c in colors for s in sizes):
    print(tshirt)
...
black S
black M
black L
white S
white M
white L
```
В отличие от Примера 2, здесь список футболок не находится ни в какой момент в памяти. Генераторное выражение отдает циклу for элементы по одному

