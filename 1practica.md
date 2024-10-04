# Практическое занятие №1. Введение, основы работы в командной строке

Пошибайлов И.С. , РТУ МИРЭА

Научиться выполнять простые действия с файлами и каталогами в Linux из командной строки. Сравнить работу в командной строке Windows и Linux.

## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).
grep '.*' /etc/passwd | cut -d: -f1 | sort
![image](https://github.com/user-attachments/assets/851884fa-055b-4da7-a1f7-8c20d2392c1d)


## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

```
awk '{print $2, $1}' /etc/protocols | sort -nr | head -n 5
```
![image](https://github.com/user-attachments/assets/26ab43fe-abbf-432f-a174-50ad49f2bc8e)


## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

```
#!/bin/bash

text=$*
length=${#text}

for i in $(seq 1 $((length + 2))); do
    line+="-"
done

echo "+${line}+"
echo "| ${text} |"
echo "+${line}+"
```
![image](https://github.com/user-attachments/assets/3a160e86-01b0-4816-8754-dfc7f04f4460)
Перед отправкой решения проверьте его в ShellCheck на предупреждения.

## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

```
#!/bin/bash

file="$1"

id=$(grep -o -E '\b[a-zA-Z]*\b' "$file" | sort -u)
_________________________________

grep -oE '\b[a-zA-Z_][a-zA-Z0-9_]*\b' hello.c | grep -vE '\b(int|void|return|if|else|for|while|include|stdio)\b' | sort | uniq

```

![image](https://github.com/user-attachments/assets/7db65420-cb37-40d8-9837-e68dd4cd8273)

## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

Например, пусть программа называется reg:

```
#!/bin/bash

file=$1

chmod 755 "./$file"

sudo cp "$file" /usr/local/bin/
```

В результате для banner задаются правильные права доступа и сам banner копируется в /usr/local/bin.
![image](https://github.com/user-attachments/assets/6575f783-0c8c-4bb3-966b-40fba621c5cc)

Общие сведения

https://ru.wikipedia.org/wiki/Интерфейс_командной_строки
https://nullprogram.com/blog/2020/08/01/
https://habr.com/ru/post/150950/

Стандарты

https://www.gnu.org/prep/standards/standards.html#Command_002dLine-Interfaces
https://www.gnu.org/software/libc/manual/html_node/Argument-Syntax.html
https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html

Реализация разбора опций

Питон

https://docs.python.org/3/library/argparse.html#module-argparse
https://click.palletsprojects.com/en/7.x/
