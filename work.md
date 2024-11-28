---
date: 2024-11-27T22:57:00Z  # Дата - время последнего изменения
key: value  

---

# hexlet-git.git

## Testing your SSH connection

1. Open Terminal

2. Enter the following:

```bash
   ssh -T git@github.com
   # Attempts to ssh to GitHub
```

3. You may see a warning like this:
   
   > The authenticity of host 'github.com (IP ADDRESS)' can't be established.
   > ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
   > Are you sure you want to continue connecting (yes/no)?

***

## Установка глобальных переменных

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
```

## Как добавить репозиторий

```bash
git remote add origin git@github.com:Valery-Sorokin/hexlet-git.git
git branch -M main
git push -u origin main
```

## Как клонировать репозиторий

```bash
git clone git@github.com:Valery-Sorokin/hexlet-git.git
cd hexlet-git
ls -la
```

## Как получить изменения с GitHub

```bash
git pull --rebase
```

***

SSH - `git@github.com:Valery-Sorokin/hexlet-git.git`

***

<master@oraclelinux9gui.local>

***

<vsorokin@tut.by>

***

## git pull/push требует логин и пароль

Распространенной ошибкой является клонирование с использованием **HTTPS** вместо **SSH**. Вы можете исправить это, перейдя в свой репозиторий, нажав "Clone" и скопировав поле "Clone with SSH" (пример интерфейса GiLab).
Обновить URL-адрес удаленного источника можно, например, так:

```bash
git remote set-url origin git remote set-url origin git@github.com:Valery-Sorokin/hexlet-git.git
```

## Анализ истории изменений

- [Команда git log](#komanda-git-log)
- [Команда git show](#komanda-git-show)
- [Команда git blame](#komanda-git-blame)
- [Команда git grep](#komanda-git-grep)
- [GitHub](#github)

### Команда `git log`

Она показывает список всех выполненных коммитов, отсортированных по дате добавления

```bash
git log
```

У команды `git log` есть полезный флаг `-p`, который сразу выводит диф для каждого коммита:

```bash
git log -p
# Тут все коммиты с полным дифом
# Промотать вперед — кнопка f, промотать назад — b
# Выйти из режима просмотра — q
```

### Команда `git show`

У каждого коммита есть уникальный набор символов — **идентификатор** (еще говорят «хеш»). С помощью хеша можно посмотреть все изменения, сделанные в рамках одного коммита:

```bash
git show 5120bea3e5528c29f8d1da43731cbe895892eb6d
# Тут выводится диф между этим коммитом и предыдущим
```

Хеши коммитов в Git очень длинные, и ими бывает неудобно пользоваться. 
Поэтому разработчики Git добавили возможность указывать только часть 
хеша. Достаточно взять первые семь символов и подставить их в ту 
команду, которая работает с коммитами:

```bash
git show 5120bea
```

### Команда `git blame`

Для этого подойдет команда `git blame <путь до файла>`. Эта команда выводит файл и рядом с каждой строчкой показывает того, кто ее менял и в каком коммите:

```bash
git blame INFO.md
```

### Команда `git grep`

Команда `git grep` ищет совпадение с указанной строкой во 
всех файлах проекта. Это очень удобная команда для быстрого анализа из 
терминала. Она удобнее обычного `grep`, потому что знает про игнорирование и не смотрит в директорию *.git*, а еще умеет искать по истории:

```bash
git grep line

INFO.md:new line

# Флаг `i` позволяет искать без учета регистра
git grep -i hexlet

README.md:Hello, Hexlet! How are you?

# Поиск в конкретном коммите
git grep Hexlet 5120bea

# Поиск по всей истории
# Возвращаем список хешей коммитов `rev-list`
git grep Hexlet $(git rev-list --all)
```

### GitHub

В простых ситуациях анализировать проект 
можно прямо на GitHub. Он позволяет просматривать историю коммитов, 
изменения в конкретном коммите и многое другое.

# Отмена изменений в рабочей директории

- [Неотслеживаемые файлы](https://ru.hexlet.io/courses/intro_to_git/lessons/changes-cancelation/theory_unit#neotslezhivaemye-fayly)
- [Измененные файлы в рабочей директории](https://ru.hexlet.io/courses/intro_to_git/lessons/changes-cancelation/theory_unit#izmenennye-fayly-v-rabochey-direktorii)
- [Изменения, подготовленные к коммиту](https://ru.hexlet.io/courses/intro_to_git/lessons/changes-cancelation/theory_unit#izmeneniya-podgotovlennye-k-kommitu)

### Неотслеживаемые файлы

Это самая простая ситуация. Представьте, что вы добавили новые файлы в репозиторий и поняли, что они вам не нужны.

В этом случае можно выполнить очистку:

```bash
mkdir one
touch two

git status

On branch main
Your branch is up to date with 'origin/main'.

# Пустые директории в Git не добавляются в принципе
# Физически директория one находится в рабочей директории,
# но при этом ее нет в Git, поэтому Git игнорирует ее
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    two

# Выполняем очистку. Команда удалит все неотслеживаемые файлы
# -f – force, -d – directory
git clean -fd

Removing one/
Removing two
```

### Измененные файлы в рабочей директории

Для отмены изменений в таких файлах используется команда `git restore`. Причем Git сам напоминает об этом при проверке статуса:

```bash
echo 'new text' > INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  # Ниже написано, как отменить изменение
  (use "git restore <file>..." to discard changes in working directory)
    modified:   INFO.md

# Отменяем
git restore INFO.md
```

## Изменения, подготовленные к коммиту

С файлами, подготовленными к коммиту, можно поступить по-разному. Первый
 вариант — отменить изменения совсем, второй — отменить только 
индексацию, не изменяя файлы в рабочей директории. Второе полезно в том 
случае, если изменения нужны, но мы не хотим их коммитить сейчас:

```bash
echo 'new text' > INFO.md
git add INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   INFO.md
```

И здесь снова помогает Git. При выводе статуса он показывает нужную команду для перевода изменений в рабочую директорию:

```bash
git restore --staged INFO.md
git status

On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   INFO.md
```
