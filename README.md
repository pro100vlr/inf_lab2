# Лабораторная работа 2

Условие задачи:

На основе изученного материала лабораторной работы, лекций (2 и 3), дополнительных источников напишите скрипт, который на вход принимает IPv4-адрес в десятичном формате, а на выходе обеспечивает данный IP-адрес в двоичном формате.

Пример входных данных:

```192.168.10.1```

Пример выходныx данных:

```11000000.10101000.00001010.00000001```
Решение:

В скриншотах представлено полное решение задачи

1.<img width="460" alt="Снимок экрана 2024-10-12 в 21 41 52" src="https://github.com/user-attachments/assets/a6c3b15d-fda8-476a-8379-16449c16bd94">

2.<img width="399" alt="Снимок экрана 2024-10-12 в 21 44 23" src="https://github.com/user-attachments/assets/27d52470-d0dd-4600-903a-eda8bcd803bc">

Поэтапно расскажу, как выполнила работу:
1)Создала с помощью консольного текстового редактора файл, который называется ip.sh

sh -это расширение для bash.

2)Затем открылся файл. В нем ввела значимую строчку:#!/bin/bash.Это называется шебанг, он сообщает оболочке, с помощью какой программы интерпретировать скрипт при выполнении.В нашей задаче сценарий должен интерпретироваться и запускаться оболочкой bash.

3)ip_address=$1 - принимаем ip-адрес.В Bash, $ является специальным символом, который используется для доступа к значениям переменных.Когда пишем $ перед именем переменной, Bash заменяет его на значение этой переменной.В конкретном случае ip_address=$1, $1 означает "первый аргумент командной строки".
В Bash, $1, $2, $3 и т.д. являются специальными переменными, которые содержат значения аргументов командной строки.Таким образом, в выражении ip_address=$1, $1 заменяется на значение первого аргумента командной строки, и это значение присваивается переменной ip_address.

4)IFS='.' read o1 o2 o3 o4 <<< "$ip_address"

Эта строка является частью Bash-скрипта и служит для разбиения IP-адреса на отдельные октеты.

Разберу строку по частям:

* IFS='.': Это устанавливает значение внутреннего разделителя полей (Internal Field Separator, IFS) равным точке (.). IFS является специальной переменной в Bash, которая определяет символы, которые используются для разделения полей в строке.
* read  o1 o2 o3 o4: Это команда read, которая читает строку из стандартного ввода и разбивает ее на отдельные поля. o1, o2, o3 и o4 являются именами переменных, в которые будут записаны отдельные поля.
* <<< "$ip_address": Это оператор "here string", который передает строку, содержащую значение переменной ip_address, в качестве стандартного ввода для команды read.
  
5)# Преобразуем каждый октет в двоичный формат с printf и выводим результат printf

printf "%08d." "$(echo "obase=2; $o1" | bc)"

printf "%08d." "$(echo "obase=2; $o2" | bc)"

printf "%08d." "$(echo "obase=2; $o3" | bc)"

printf "%08d\n" "$(echo "obase=2; $o4" | bc)"

Разберу первую строку по частям:
printf "%08d." "$(echo "obase=2; $o1" | bc)"
Эта строка преобразует первый октет IP-адреса ($o1) из десятичного формата в двоичный формат.
* echo "obase=2; $o1": Эта команда выводит строку, содержащую команду obase=2, которая устанавливает основание вывода в двоичном формате, и значение $o1, которое является первым октетом IP-адреса.
* bc: bc является командой, которая запускает калькулятор bc (Basic Calculator). Этот калькулятор позволяет выполнять математические операции и преобразования.
* $( ): Эта конструкция является командной подстановкой, которая выполняет команду внутри скобок и возвращает ее вывод.
* printf "%08d.": Эта команда выводит двоичное представление первого октета IP-адреса в формате %08d, который означает "вывести целое число в двоичном формате, заполнив его нулями до ширины 8 бит". Символ . в конце строки добавляет точку для разделения октетов.Символ % означает начало формата вывода.
Команда bc принимает вывод команды echo и выполняет преобразование значения $o1 в двоичный формат.
Возвращаемое значение команды bc является двоичным представлением значения $o1, которое затем передается команде printf для вывода в формате %08d..

6)Затем ввожу bash ip.sh 192.168.10.1.И получаю ответ, который представлен на скриншоте. В свое время он является верным ответом.

Вывод:В данной лабораторной работе произвела отработку полученной информацией.А именно научилась принимать аргумент из командной строки,присваивать его переменной; разделять в данном случае ip-адрес на октеты; преобразовывать октеты в двоичный формат и выводить результат.
