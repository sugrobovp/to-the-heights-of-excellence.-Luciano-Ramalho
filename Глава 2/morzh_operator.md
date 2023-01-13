# Оператор := на примерах

### Пример 1
```python
x = [1, 2, 3]
quadrs = [last := c for c in x]
print(last)
# 3
```

### Пример 2
Пользователь вводит текст пока есть возможность.
```python
value = input('Please enter something: ')
while value != '':
    print('Nice!')
    value = input('Please enter something: ')
```
Который можно записать вот так с помощью оператора присваивания.
```python
while(value:=input('Please enter something') != ''):
    print('Nice')
```

### Пример 3
```python
def cube(num):
    return num**3

num_list = [1,2,3,4,5]
[cube(x) for x in num_list if cube(x) < 20]
```
Здесь cube(x) вызывается дважды. С помощью оператора присваивания упростим
```python
[y for x in num_list if (y := cube(x)) < 20]
```
cube(x) вызывается только один раз, что повышает эффективность и читаемость кода

### Пример 4
```python
a = [1,-23,4,5,-6,123]
b = [y for x in a if (y := abs(x)) > 7]
print(b)
# 23, 123
```