# Тема 7. Функции и модули
Отчет по Теме #7 выполнил(а):
- Куликов Кирилл Евгеньевич    
- ИНО ЗБ ПОАС 22-1

| Задание | Сам_раб |
| ------ | ------ |
| Задание 1 | + |
| Задание 2 | + |
| Задание 3 | + |
| Задание 4 | + |
| Задание 5 | + |

знак "+" - задание выполнено; знак "-" - задание не выполнено;

Работу проверили:
- к.э.н., доцент Панов М.А.

## Самостоятельная работа №1
Найдите в интернете любую статью (объем статьи не менее 200
слов), скопируйте ее содержимое в файл и напишите программу,
которая считает количество слов в текстовом файле и определит
самое часто встречающееся слово. Результатом выполнения задачи
будет: скриншот файла со статьей, листинг кода, и вывод в консоль,
в котором будет указана вся необходимая информация.
```
with open('D:\Downloads\Новый текстовый документ.txt', 'r', encoding="utf-8") as file:
    text = file.read()

words = text.split()

counter = {}
for word in words:
    if word in counter:
        counter[word] += 1
    else:
        counter[word] = 1

maxCount = max(counter.values())

print("Самые частовстречающиеся слова:",[word for word, count in counter.items() if count == maxCount])
print("Количество слов в тексте:", len(words))

```
![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/e48b1509-0a8c-4d7c-afd6-184430129de9)

![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/cf493a27-4d4a-4263-9197-f27e45bd300f)

  
## Самостоятельная работа №2
У вас появилась потребность в ведении книги расходов, посмотрев
все существующие варианты вы пришли к выводу что вас ничего не
устраивает и нужно все делать самому. Напишите программу для
учета расходов. Программа должна позволять вводить информацию
о расходах, сохранять ее в файл и выводить существующие данные в
консоль. Ввод информации происходит через консоль. Результатом
выполнения задачи будет: скриншот файла с учетом расходов,
листинг кода, и вывод в консоль, с демонстрацией
работоспособности программы.
```
def add_expense():
    expenses = []
    with open('Расходы.txt', 'r') as file:
        for line in file:
            expenses.append({'amount': str(line)})

    expense = {}
    expense['amount'] = float(input('Введите сумму расхода: '))
    expenses.append(expense)
    with open('Расходы.txt', 'w+') as file:
        for expense in expenses:
            file.write(f'{expense["amount"]}\n')
    print('Расход успешно добавлен.')

def view_expenses():
    with open('Расходы.txt', 'r') as file:
        for line in file:
            print(f'- {line}')

def main():
    while True:
        print('1. Добавить расход')
        print('2. Просмотреть расходы')
        print('3. Выйти')
        choice = int(input('Выберите пункт меню: '))
        if choice == 1:
            add_expense()
        elif choice == 2:
            view_expenses()
        elif choice == 3:
            break
        else:
            print('Неверный выбор. Попробуйте снова.')

if __name__ == '__main__':
    main()
```
![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/0cfe6351-5c2b-43e5-ab81-873bdf73dcff)


  
## Самостоятельная работа №3
Имеется файл input.txt с текстом на латинице. Напишите программу,
которая выводит следующую статистику по тексту: количество букв
латинского алфавита; число слов; число строк.
```
def countLetters(text):
    return sum(1 for char in text if char.isalpha())

def countWords(text):
    return len(text.split())

def countLines(text):
    return text.count('\n') + 1

with open('input.txt', 'r') as file:
    text = file.read()

countLetters = countLetters(text)
countWords = countWords(text)
countLines = countLines(text)

print(f'Input file contains:\n{countLetters} letters\n{countWords} words\n{countLines} lines')
```
![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/542d4d82-4f9e-46a1-80e8-63d88a2f2839)


## Самостоятельная работа №4
Напишите программу, которая получает на вход предложение,
выводит его в терминал, заменяя все запрещенные слова
звездочками * (количество звездочек равно количеству букв в
слове). Запрещенные слова, разделенные символом пробела,
хранятся в текстовом файле input.txt. Все слова в этом файле
записаны в нижнем регистре. Программа должна заменить
запрещенные слова, где бы они ни встречались, даже в середине
другого слова. Замена производится независимо от регистра: если
файл input.txt содержит запрещенное слово ехат, то слова ехат,
Ехат, ЕхаМ, ЕХАМ и ехАт должны быть заменены на ****
```
import re

def readForbiddenWords():
    with open('input.txt', 'r', encoding="utf-8") as file:
        return set(file.read().split())

def replaceForbiddenWords(text, forbiddenWords):
    pattern = re.compile(f'({"|".join(forbiddenWords)})', re.IGNORECASE)
    return pattern.sub(lambda match: '*' * len(match.group()), text)

def main():
    forbiddenWords = readForbiddenWords()
    text = input('Введите предложение: ')
    result = replaceForbiddenWords(text, forbiddenWords)
    print(result)

if __name__ == '__main__':
    main()
```
![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/3b6fcd2c-b2ff-4b59-88e1-3b01335a9448)

  
## Самостоятельная работа №5
Программа, которая считывает текст из файла, преобразует все строчные буквы в верхний регистр, а все прописные буквы в нижний регистр, и записывает результат в другой файл.
``` 
def convert_case(filename_in, filename_out):
    with open(filename_in, 'r', encoding="utf-8") as file_in:
        text = file_in.read()
    text = text.swapcase()
    with open(filename_out, 'w', encoding="utf-8") as file_out:
        file_out.write(text)


def main():
    filename_in = 'input.txt'
    filename_out = 'output.txt'
    convert_case(filename_in, filename_out)


if __name__ == '__main__':
    main()
```
![image](https://github.com/4itorKoteykovi4/Software_Engineering/assets/44967696/6842162a-09e2-448a-8542-bf0c77cdd1fb)
