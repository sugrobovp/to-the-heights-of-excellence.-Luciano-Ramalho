### Применение конструктора dict к итерируемой последовательности 
```python
>>> dial_codes = (
    [880, 'Bangladesh'],
    (55, 'Brazil'),
    (86, 'China'),
    (91, 'India'),
    (62, 'Indonesia'),
    (81, 'Japan'),
    (234, 'Nigeria'),
    (92, 'Pakistan'),
    (7, 'Russia'),
    (1, 'United States')
)
>>> dict(dial_codes)
{880: 'Bangladesh', 55: 'Brazil', 86: 'China', 91: 'India', 62: 'Indonesia', 81: 'Japan', 234: 'Nigeria', 92: 'Pakistan', 7: 'Russia', 1: 'United States'}
```
То есть мы можем применять встроенную функцию dict() к итерируемым последовательностям с подпоследовательностями из двух элементов

### Применение словарных включений
```python
>>> dial_codes = [
... (880, 'Bangladesh'),
... (55, 'Brazil'),
... (86, 'China'),
... (91, 'India'),
... (62, 'Indonesia'),
... (81, 'Japan'),
... (234, 'Nigeria'),
... (92, 'Pakistan'),
... (7, 'Russia'),
... (1, 'United States'),
... ]
>>> country_dial = {country: code for code, country in dial_codes}
>>> country_dial
{'Bangladesh': 880, 'Brazil': 55, 'China': 86, 'India': 91, 'Indonesia': 62,
'Japan': 81, 'Nigeria': 234, 'Pakistan': 92, 'Russia': 7, 'United States': 1}
>>> {code: country.upper()
... for country, code in sorted(country_dial.items())
... if code < 70}
{55: 'BRAZIL', 62: 'INDONESIA', 7: 'RUSSIA', 1: UNITED STATES'}
```
С помощью словарных включений мы смогли перевернуть country, code а затем отсортировать по странам.

# Распаковка отображений

### Пример 1. Оператор **
```python
>>> def dump(**kwargs):
... return kwargs
...
>>> dump(**{'x': 1}, y=2, **{'z': 3})
{'x': 1, 'y': 2, 'z': 3}
```

### Пример 2. Использование ** внутри словаря
```python
>>> {'a': 0, **{'x': 1}, 'y': 2, **{'z': 3, 'x': 4}}
{'a': 0, 'x': 4, 'y': 2, 'z': 3}
```

Ключи словаря должны быть хэшируемыми
### Определение. Объект называется хешируемым, если имеет хеш-код, который не изменяется на протяжении всего времени его жизни (у него должен быть метод __hash__(), и допускает сравнение с другими объектами(у него должен быть метод __eq__()). Если в результате сравнения хэшируемых объектов оказывается, что они равны, то и их хэш-коды тоже должны бьть равны.

### Хэшируемость tuple
```python
>>> tt = (1, 2, (30, 40))
>>> hash(tt)
8027212646858338501
>>> tl = (1, 2, [30, 40])
>>> hash(tl)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> tf = (1, 2, frozenset([30, 40]))
>>> hash(tf)
-4118419923444501110
```
Tuple является хэшируемым тогда и только тогда, когда все его объекты являются хэшируемыми.

### Метод dict.update()
```python
>>> a = {
    'x': 1,
    'y': 2,
    'z': 3
    }
>>> b = {
    'q': 4,
    'w': 5,
    'e': 6
    }
>>> a.update(b)
>>> a
{'x': 1, 'y': 2, 'z': 3, 'q': 4, 'w': 5, 'e': 6}
```
Можно обновлять словарь еще одним. Либо списком из пар других списков(или кортежей):
```python
>>> a = {
    'x': 1,
    'y': 2,
    'z': 3
    }
>>> a.update([['q', 4], ['w', 5]])
>>> a
{'x': 1, 'y': 2, 'z': 3, 'q': 4, 'w': 5}
```

# Применения defaultdict

### Пример 1. List
```python
from collections import defaultdict

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = defaultdict(list)
for k, v in s:
    d[k].append(v)

sorted(d.items())
# [('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]
```

### Пример 2. Создание счетчика букв в слове
```python
from collections import defaultdict

s = 'mississippi'
d = defaultdict(int)
for k in s:
    d[k] += 1

sorted(d.items())
# [('i', 4), ('m', 1), ('p', 2), ('s', 4)]
```
Чтобы обрабатывать отсутствующие ключи - либо используем defaultdict, либо создаем пользовательский dict с методом __missing__ (или как вариант с __getitem__)

### Пример пользовательского словаря с __getitem__, чтобы ключи переделывались в строки
```python
>>> class MyDict(dict):
    def __getitem__(self, __key):
        if not isinstance(__key, str):
            __key = str(__key)
        return super().__getitem__(__key)

>>> test = MyDict([('1', 1), ('2', 2), ('3', 3)])
>>> test[1]
1
```

### Пример с __missing__
```python
class StrKeyDict0(dict):
    def __missing__(self, key):
        if isinstance(key, str):
            raise KeyError(key)
    return self[str(key)]
    def get(self, key, default=None):
        try:
            return self[key]
        except KeyError:
            return default
    def __contains__(self, key):
        return key in self.keys() or str(key) in self.keys()
```




