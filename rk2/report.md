# Постановка задачи

Отсортировать слова в каждой строке файла по алфавиту.
Результат решения сохранить в новый файл.

## Допущения

- Длина строки не превышает 256 символов
- Слов в строке не больше 100
- Слова разделяются произвольным количеством пробелов
- Количество слов не указывается

## Пример работы ("черный ящик")

Для тестирования программы выделяется четыре класса эквивалентности:
пустой/несуществующий файл;
файл со слишком длинными строками;
файл со строками, содержащими слишком много слов;
файл с нормальными строками.

| Произвольная строка исходного файла                                        | Соответствующая строка выходного файла     |
|----------------------------------------------------------------------------|--------------------------------------------|
| Несуществующий файл                                                        | Сообщение «Файл не существует»             |
| Пустой файл                                                                | Сообщение «Файл пуст»                      |
| a a a a a a a a … a a a a (больше 100 слов)                                | Сообщение «В файле слишком много слов»     |
| tree flavour module … exam test word (длина строки превышает 256 символов) | Сообщение «В файле слишком длинные строки» |
| a c e b d z                                                                | a b c d e z                                |

# Декомпозиция

## Диаграммы IDEF0

*... изображения с диаграммами ...*

[//]: # (TODO: add IDEF0 png files here)

## Спецификации модулей (выделенных подзадач)

### Спецификация модуля А1

| Имя               | read_file                                                         |
|-------------------|-------------------------------------------------------------------|
| Функция           | Считывание слов из строки файла в массив с последующей обработкой |
| Список параметров | Файловая переменная на вход, файловая переменная на выход         |
| Входные данные    | Файловая переменная на вход                                       |
| Выходные данные   | Файловая переменная на выход                                      |
| Внешние эффекты   | Нет                                                               |
| Допущение модуля  | Входной файл существует и содержит непустые строки                |

### Спецификация модуля A23

| Имя               | greater_than                                                                          |
|-------------------|---------------------------------------------------------------------------------------|
| Функция           | Определяет, больше ли первое переданное слов, чем второе (лексикографический порядок) |
| Список параметров | Первое слово, второе слово, признак                                                   |
| Входные данные    | Первое слово, второе слово                                                            |
| Выходные данные   | Признак                                                                               |
| Внешние эффекты   | Нет                                                                                   |

## Тесты («черный ящик»)

### Тестовые данные модуля A1

Для тестирования данного модуля выделяется два класса эквивалентности: пустой входной файл и не пустой. При этом для непустого
файла рассматриваются случаи, когда слово одно, и когда их несколько.

| Содержимое входного файла                   | Результат                                  |
|---------------------------------------------|--------------------------------------------|
| Ничего                                      | Ненулевой код возврата                     |
| word                                        | \[word\], количество: 1                    |
| word1 word2<br/> word3                      | \[word1, word2\], \[word3\], количество: 2 |
| a a a a a a a a … a a a a (больше 100 слов) | Ненулевой код возврата                     |

### Тестовые данные модуля A23

Для тестирования данного модуля выделяется два класса эквивалентности:
первое переданное слово больше второго;
первое переданное слово не больше второго.

| Число | Результат (1 - TRUE; 0 - FALSE) |
|-------|---------------------------------|
| a b   | 0                               |
| b a   | 1                               |
| 1 2   | 0                               |
| 10 1  | 1                               |