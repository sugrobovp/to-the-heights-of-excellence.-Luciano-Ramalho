# Отличие sort и sorted
```python
>>> t = [1, 3, 2]
>>> t.sort
>>> print(t)
[1, 2, 3]
>>> print(t.sort)
None
```
Метод sort сортирует исходный список на месте, не создавая копию. Это соглашение Python API: функции и методы, изменяющие объект на месте должны возвращать None. В отличие от sort - встроенная функция sorted всегда создает новый список. Так же sorted принимает в качестве аргумента любой итерируемый объект, в том числе и неизменяемые последовательности.

### Пример применения sorted, reverse, key
```python
>>> fruits = ['grape', 'raspberry', 'apple', 'banana']
>>> sorted(fruits)
['apple', 'banana', 'grape', 'raspberry'] 
>>> fruits
['grape', 'raspberry', 'apple', 'banana'] 
>>> sorted(fruits, reverse=True)
['raspberry', 'grape', 'banana', 'apple'] 
>>> sorted(fruits, key=len)
['grape', 'apple', 'banana', 'raspberry'] 
>>> sorted(fruits, key=len, reverse=True)
['raspberry', 'banana', 'grape', 'apple'] 
>>> fruits
['grape', 'raspberry', 'apple', 'banana'] 
>>> fruits.sort() 
>>> fruits
['apple', 'banana', 'grape', 'raspberry'] 
```
key - функция, которая применяется к каждому элементу списка и затем проводится сортировка. Так же из примера видно, что исходный список при sorted не меняется, а создается новый.