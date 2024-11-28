---
date: 2024-11-28T13:55:00Z  # Дата - время последнего изменения


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
# --global   использовать глобальный файл конфигурации
# --system   использовать системный файл конфигурации
# --local    использовать файл конфигурации репозитоgit config --global user.name "John Doe"
git config --global user.name "Valery Sorokin"
git config --global user.email johndoe@example.com
git config --global init.defaultBranch main
# Глобальные параметры для окончаний строк
# git config --global core.autocrlf true # Для Windows параметр true
git config --global core.autocrlf input # Для Linux input
git config --global core.editor "code --wait" # Visual Studio Code
git config --global -e # Открыть .gitconfig в редакторе по умолчанию
git config --global --list --show-origin #S how Git Config in the Command Line/
# --show-origin    показать источник настройки
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

## Отмена коммитов

- [Git revert](https://ru.hexlet.io/courses/intro_to_git/lessons/commits-cancelation/theory_unit#git-revert)
- [Команда git reset](https://ru.hexlet.io/courses/intro_to_git/lessons/commits-cancelation/theory_unit#komanda-git-reset)

### Команда `git revert`

Самая простая ситуация — отмена 
изменений. Фактически она сводится к созданию еще одного коммита, 
который выполняет изменения, противоположные тому коммиту, который 
отменяется:

```bash
# Этой команде нужен идентификатор коммита
# Это коммит, которым мы удалили файл PEOPLE.md
git revert aa600a43cb164408e4ad87d216bc679d097f1a6c
# После этой команды откроется редактор, ожидающий ввода описания коммита
# Обычно сообщение revert не меняют, поэтому достаточно просто закрыть редактор
[main 65a8ef7] Revert "remove PEOPLE.md"
 1 file changed, 1 insertion(+)
 create mode 100644 PEOPLE.md
# В проект вернулся файл PEOPLE.md

git log -p

commit 65a8ef7fd56c7356dcee35c2d05b4400f4467ca8
Author: tirion <tirion@got.com>
Date:   Sat Sep 26 15:32:46 2020 -0400

    Revert "remove PEOPLE.md"

    This reverts commit aa600a43cb164408e4ad87d216bc679d097f1a6c.

diff --git a/PEOPLE.md b/PEOPLE.md
new file mode 100644
index 0000000..4b34ba8
--- /dev/null
+++ b/PEOPLE.md
@@ -0,0 +1 @@
+Haskell Curry
```

### Команда `git reset`

Git позволяет удалять коммиты. Это опасная операция, которую нужно 
делать только в том случае, если речь идет про новые коммиты, которых 
нет ни у кого, кроме вас.

Если коммит был отправлен во внешний 
репозиторий, например, на GitHub, то менять историю ни в коем случае 
нельзя. Это сломает работу у тех, кто работает с вами над проектом.

Для удаления коммита используется команда `git reset`:

```bash
# Добавляем новый коммит, который мы сразу же удалим
echo 'test' >> INFO.md
git add INFO.md
git commit -m 'update INFO.md'

[main 17a77cb] update INFO.md
 1 file changed, 1 insertion(+)
 # Важно, что мы не делаем git push

git reset --hard HEAD~1

HEAD is now at 65a8ef7 Revert "remove PEOPLE.md"

# Если посмотреть `git log`, то последнего коммита там больше нет
```

Флаг `--hard` означает полное удаление. Без него `git reset` отменит коммит, но не удалит его, а поместит все изменения этого коммита в рабочую директорию, так что с ними можно будет продолжить работать.

Флаг `HEAD~` означает «один коммит от последнего коммита». Обратите внимание, что здесь используется знак `~` — тильда. Его легко перепутать с дефисом `-`. Если бы мы хотели удалить два последних коммита, то могли бы написать `HEAD~2`:

## Изменение последнего коммита

Крайне часто разработчики делают коммит и сразу понимают, что забыли добавить часть файлов через `git add`. Оставшуюся часть изменений можно дослать следующим коммитом.

Есть  еще один способ. Если изменения еще не были отправлены во внешнюю 
систему, можно добавить изменения в текущий коммит. Для этого во время 
коммита добавляется флаг `--amend`:

```bash
echo 'experiment with amend' >> INFO.md
echo 'experiment with amend' >> README.md
git add INFO.md
# Забыли сделать подготовку README.md к коммиту
git commit -m 'add content to INFO.md and README.md'

[main 256de25] add content to INFO.md and README.md
 1 file changed, 1 insertion(+)

git status

On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   README.md

# Увидели, что забыли добавить файл
# Добавляем

git add README.md
git commit --amend
# После этой команды откроется редактор, ожидающий ввода описания коммита
# Здесь можно поменять сообщение или выйти из редактора, оставив старое

[main d96151a] add content to INFO.md and README.md
 Date: Sat Sep 26 16:02:07 2020 -0400
 2 files changed, 2 insertions(+)

git status

On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

В реальности `--amend` не добавляет изменения в существующий коммит. Этот флаг приводит к откату коммита через `git reset` и выполнению нового коммита с новыми данными. Поэтому мы и видим ровно один коммит, хотя команда `git commit` выполнялась два раза (первый раз — когда сделали ошибочный коммит).

Чтобы не открывался редактор для ввода описания коммита к команде `git commit --amend` можно добавить опцию `--no-edit`. В этом случае описание коммита не изменится

```bash
git commit --amend --no-edit
```
