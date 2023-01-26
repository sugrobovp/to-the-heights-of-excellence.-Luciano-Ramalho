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
С помощью словарных включений мы смогли перевернуть country, code

