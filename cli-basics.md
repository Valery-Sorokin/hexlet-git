# cli-basics

## Как проверить, в какой директории мы находимся

Проверить, в какой директории мы сейчас находимся, можно командой `pwd`:

```bash
pwd

/Users/guest
```

название команды `pwd` — это сокращение, которое расшифровывается как *print working directory*. Похожим образом устроены имена многих команд, что позволяет легче и быстрее их запомнить

## Как посмотреть список файлов

Изучим команду `ls` (сокращение от *list*). Она выводит список файлов и директорий в текущей рабочей директории:

```bash
ls

Desktop  Documents Downloads Library  Movies  Music  Pictures Public
```

## Как переместиться в другую директорию

Еще одна полезная команда — `cd` (сокращение от *change directory*). С помощью нее мы перемещаемся по файловой структуре. Для этого ей нужно передать **аргумент** — директорию, в которую необходимо переместиться:

```bash
# Входим в директорию
cd Music
# Смотрим ее содержимое
ls

iTunes
```

```bash
# Смотрим текущую рабочую директорию
pwd

/Users/guest/Music
```

```bash
# Если имя директории содержит пробел, 
# то его нужно экранировать с помощью `\`
cd Best\ music
```

Выше мы указали относительный путь. Отличить их друг от друга очень легко:

- Абсолютный — первым символом в пути идет `/`
- Относительный — во всех остальных случаях

Команда `cd` понимает и абсолютные, и относительные пути. Поэтому передавать ей можно что угодно:

```bash
# Неважно, в каком месте
cd /Users/guest/Music # Абсолютный путь
```

и перейти на директорию уровнем выше:

```bash
# В директории /Users/guest/Music
cd ..
pwd

/Users/guest
```

с помощью этого заполнителя можно выходить на любое количество уровней, указывая `..` через разделитель:

```bash
# В директории /Users/guest/Music
# Выходим на два уровня вверх
cd ../..
pwd

/Users
```

```bash
# Из любого места
cd
pwd

/Users/guest
```

```bash
# Из любого места
cd ~/Music
pwd

/Users/guest/Music
```

Команда `ls` также может принимать на вход **аргумент** — директорию, которую нужно проанализировать:

```bash
ls Music

iTunes
```

# Интерфейс командной строки

## Аргументы и опции

вы часто будете пользоваться программой `ls`, которая выводит на экран список файлов и директорий.

```bash
ls

Desktop Documents Downloads Library Movies Music Pictures Public
```

Еще мы можем посмотреть скрытые файлы и директории. В *nix-системах они начинаются с точки: `.profile`.

Тогда необходимо набрать `ls -a`:

```bash
ls -a

.  .CFUserTextEncoding Desktop   Downloads Movies Pictures
.. .localized          Documents Library   Music  Public
```

А если захотим посмотреть содержимое каталога Public? Тогда мы воспользуемся командой `ls` с аргументом:

```bash
ls Public

Drop Box
```

Практически любую команду можно дополнить двумя способами:

+ Способ 1 — это **аргументы**. Для примера рассмотрим команду `ls Music`, которая содержит аргумент `Music`

+ Способ 2 — это **опции**, еще их иногда называют флагами. Например, команда `ls -a` содержит в себе опцию `-a`

## Опции

Опции можно комбинировать. Представим, что мы хотим увидеть список 
всех файлов, включая скрытые, причем с подробным описанием. В таком 
случае нужно набрать команду `ls -a -l`. Можно объединить эти опции и записать ту же команду вот так:

- `ls -al`
- `ls -la`

При работе с опциями не забывайте ставить `-`. Без него вы получите команду `ls la` в которой `la` — это аргумент, а не опция. В таком случае командная оболочка покажет содержимое директории `la`.

Еще мы можем использовать опции и аргументы одновременно, хотя все зависит от программы. В случае с `ls` можно использовать одновременно и то, и другое. Чтобы просмотреть полное содержимое директории `Music` с информацией о каждом файле, можно набрать команду `ls -la Music`:

```bash
ls -la Music

total 0
drwx------+  4 Guest  _guest   128 Nov 21  2017 .
drwxr-xr-x+ 89 Guest  _guest  2848 Aug 24 14:06 ..
-rw-r--r--   1 Guest  _guest     0 Nov 21  2017 .localized
drwxr-xr-x   9 Guest  _guest   288 Aug 26 17:25 iTunes
```

Иногда сложно понять подобные записи: `-tupa`. Не совсем понятно, что это:

- Одна опция `tupa`
- Четыре опции `t`, `u`, `p` и `a`, объединенные в одну цепочку

В таких ситуациях нужно смотреть документацию соответствующей программы. Это можно сделать с помощью команды `man` (сокращение от *manual*). Достаточно набрать `man <имя команды>` — и мы попадем в режим чтения документации.

В мануале содержится описание утилиты в целом, формат ее вызова, все 
возможные опции, примеры вызовов и много другой полезной информации:

Попробуйте прямо сейчас посмотреть мануал программы `ls`, набрав в терминале `man ls`. Перемещаться внутри мануала можно так:

- Промотать вперед — **f (forward)**
- Промотать назад — **b (backward)**
- Выход из режима просмотра — **q (quit)**

## Варианты опций

У большинства утилит есть два варианта одной и той же опции — длинная и короткая версия. Например, в PHP есть `-v` и `--version`:

```bash
php -v

PHP 7.2.7 (cli) (built: Jun 22 2018 06:27:50) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies

php --version

PHP 7.2.7 (cli) (built: Jun 22 2018 06:27:50) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
```

Если значение опции содержит в себе специальные или пробельные символы, 
то его нужно оборачивать в кавычки, двойные или одинарные:

```bash
say -o 'hi.aac' 'Hello, World.'
```

Такое подробное описание есть практически у любой утилиты. Описания построены по одному и тому же принципу:

- Квадратные скобки `[]` обозначают необязательность. Например, опция `-v` необязательна, то же самое касается и любых других опций этой программы
- Вертикальная черта `|` обозначает операцию «исключающее или». Посмотрите на последний блок `[-f file | string ...]`. Он означает, что `say` может либо произносить текст из файла, либо произносить строчку, 
  переданную как аргумент. Сделать оба варианта одновременно не получится

### Новые изменения !