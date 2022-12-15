Use case специальных методов на примере азбуки Морзе

```python
# Алфавит
morse_alphabet = {
    "А" : ".-",
    "Б" : "-...",
    "В" : ".--",
    "Г" : "--.",
    "Д" : "-..",
    "Е" : ".",
    "Ж" : "...-",
    "З" : "--..",
    "И" : "..",
    "Й" : ".---",
    "К" : "-.-",
    "Л" : ".-..",
    "М" : "--",
    "Н" : "-.",
    "О" : "---",
    "П" : ".--.",
    "Р" : ".-.",
    "С" : "...",
    "Т" : "-",
    "У" : "..-",
    "Ф" : "..-.",
    "Х" : "....",
    "Ц" : "-.-.",
    "Ч" : "---.",
    "Ш" : "----",
    "Щ" : "--.-",
    "Ъ" : "--.--",
    "Ы" : "-.--",
    "Ь" : "-..-",
    "Э" : "..-..",
    "Ю" : "..--",
    "Я" : ".-.-",
    "1" : ".----",
    "2" : "..---",
    "3" : "...--",
    "4" : "....-",
    "5" : ".....",
    "6" : "-....",
    "7" : "--...",
    "8" : "---..",
    "9" : "----.",
    "0" : "-----",
    "." : "......",
    "," : ".-.-.-",
    ":" : "---...",
    ";" : "-.-.-.",
    "(" : "-.--.-",
    ")" : "-.--.-",
    "'" : ".----.",
    "\"": ".-..-.",
    "-" : "-....-",
    "/" : "-..-.",
    "?" : "..--..",
    "!" : "--..--",
    "@" : ".--.-.",
    "=" : "-...-",
}

# Перевернем словарь по компрехеншену
inverse_morse_alphabet = {v: k for k, v in morse_alphabet.items()}

class Morse(object):
    
    # В буффер будем складывать унарные плюс и минус методами __neg__ и __pos__ 
    def __init__(self, buffer=""):
        self.buffer = buffer

    def __neg__(self):
        return Morse("-" + self.buffer)

    def __pos__(self):
        return Morse("." + self.buffer)

    # По буфферу получим букву
    def __str__(self):
        return inverse_morse_alphabet[self.buffer]

    def __add__(self, other):
        return str(self) + str(+other)

    # Правое сложение когда нужно сложить строку с Morse object
    def __radd__(self, s):
        return s + str(+self)

    def __sub__(self, other):
        return str(self) + str(-other)

    # Правое вычитание когда нужно вычитаем из строки Morse object
    def __rsub__(self, s):
        return s + str(-self)


class MorseWithSpace(Morse):
    def __str__(self):
        return super().__str__() + " "

    def __neg__(self):
        return MorseWithSpace(super().__neg__().buffer)

    def __pos__(self):
        return MorseWithSpace(super().__pos__().buffer)


_ = Morse()
___ = MorseWithSpace()
print(+--+_+-+_++_+--_+_-_+-+-+-___++++_+-_-+++_+-+_--++--_)
```
Получим 
```python
Привет Хабр!
```

