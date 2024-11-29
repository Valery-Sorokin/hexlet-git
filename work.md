---
date: 2024-11-29T14:51:00Z  # Дата - время последнего изменения


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

## Классный тренажер по git - Learn Git Branching

[Learn Git Branching](https://learngitbranching.js.org/?locale=ru_RU)

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
# Use VS Code as git default diff tool and merge tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

## Просмотр и редактирование глобальных переменных

```bash
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

Она показывает список всех выполненных коммитов, отсортированных по дате добавления.

Если добавить имя файла в конец команды `git log` в формате `-- <имя_файла>`, то можно увидеть, в каких коммитах он изменялся

```bash
git log
```

У команды `git log` есть полезный флаг `-p`, который сразу выводит диф для каждого коммита:

```bash
git log -p
# Тут все коммиты с полным дифом
# Промотать вперед — кнопка f, промотать назад — b
# Выйти из режима просмотра — q
git log --oneline # Однострочная история
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
git log --oneline   # Однострочная история
# Однострочная история - из нее берем первые 7 символов
git show 5120bea    # Показать коммит 5120bea
git show HEAD~2     # Показать коммит 2 до HEAD
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

## Индекс в Git

Стандартный способ работы с индексом — это добавление или изменение файлов и последующий коммит:

```bash
git add somefile
git commit -m 'add somefile'
```

Если речь идет про один-два файла, которые нужно закоммитить прямо 
сейчас, то можно сделать проще. Этот подход работает только с уже 
отслеживаемыми файлами:

```bash
echo 'new data' >> INFO.md
# Не нужно явно вызывать команду `git add`
git commit INFO.md -m 'update INFO.md'
```

Иногда бывает наоборот — мы исправили много файлов и хотим добавить их в коммит сразу все. Тогда поможет точка:

```bash
# Добавляет абсолютно все изменения рабочей директории в индекс
git add .
```

Команда выше очень опасна. С ее помощью крайне легко закоммитить много лишнего, особенно если перед коммитом не посмотреть `git diff --staged`.

Ну и совсем страшная, но полезная команда — это коммит с одновременным добавлением всего в индекс:

```bash
# Флаг -a автоматически добавляет все изменения рабочей директории в индекс
git commit -am 'do something'
```

С другой стороны, нередко разные изменения делаются в одних и тех же 
файлах. То есть изменения в этих файлах по-хорошему должны находиться в 
разных коммитах.

И даже такое можно сделать с помощью Git. Для этого подходит команда `git add -i`, которая показывает измененные куски файлов и спрашивает, что с ними сделать

### Решение Задания

```bash
# При выполнении задачи состояние репозитория могло измениться.
# Перед набором команд из списка, обновите упражнение с помощью кнопки Сброс

cd code-user/ # Переходим в директорию code-user
git add -i
patch
1
# Подтверждаем выбор нажатием Enter
s
y
n
status
quit
git commit -m '+2/-0'
```

## Перемещение по истории

как перемещаться по истории с помощью команды `git checkout`: 

Для начала воспользуемся командой `git log`:

```bash
# Показывает сокращенный вывод
git log --oneline

fc74e2d update README.md
65a8ef7 Revert "remove PEOPLE.md"
5120bea add new content
e6f625c add INFO.md
273f81c remove NEW.md
aa600a4 remove PEOPLE.md
fe9893b add NEW.md
3ce3c02 add PEOPLE.md
3c5d976 add README.md
```

Переключимся на момент, когда был выполнен коммит с сообщением *add INFO.md*. Для этого используем команду `git checkout <хеш коммита>`:

```bash
git checkout e6f625c

Note: switching to 'e6f625c'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

Or undo this operation with:

  git switch -
```

Выполните команду выше и изучите рабочую директорию. Обратите 
внимание, что хеш вашего коммита может отличаться. Вы увидите, что 
пропала часть изменений из-за возврата в прошлое. Сами изменения никуда 
не делись, и мы снова можем вернуться на последний коммит следующей 
командой:

```bash
# Позже мы поговорим, что такое main
git checkout main
```

Самый простой способ узнать место нахождения — вызвать команду `git branch`. В обычной ситуации, когда мы находимся на последнем коммите, Git покажет такой вывод:

```bash
git branch

# Позже мы поговорим, что такое main
* main
```

Но если прямо сейчас загружен коммит из прошлого, то вывод станет таким:

```bash
* (HEAD detached at e6f625c)
  main
```

Если добавить имя файла в конец команды `git log` в формате `-- <имя_файла>`, то можно увидеть, в каких коммитах он изменялся

## Игнорирование файлов

Git позволяет гибко настраивать игнорирование определенных файлов и директорий. Делается это с помощью файла *.gitignore*, который нужно создать в корне проекта. В этот файл с помощью текстового  редактора добавляются имена файлов и директорий, которые надо игнорировать:

Git поддерживает игнорирование файлов, но сам его не настраивает. Для 
игнорирования файлов и директорий, программист должен создать файл *.gitignore* в корне проекта и добавить его в репозиторий.

```bash
touch .gitignore
# Добавляем в файл правила игнорирования по примеру выше
git add .gitignore
git commit -m 'update gitignore'
```

Как только *.gitignore* создан и в него добавлен какой-то файл  или директория, игнорирование заработает автоматически. Все новые файлы, попадающие под игнорирование, не отобразятся в выводе команды `git status`.

Иногда  бывает такое, что программист случайно уже добавил в репозиторий файл, 
который нужно проигнорировать. В этой ситуации недостаточно обновить правила игнорирования. Дополнительно придется удалить файл или директорию из Git с помощью `git rm` и закоммитить.

### Пример .gitignore

```bash
# В этом файле можно оставлять комментарии
# Имя файла .gitignore
# Файл нужно создать самостоятельно

# Каждая строчка — это шаблон, по которому происходит игнорирование

# Игнорируем файл в любой директории проекта
access.log

# Игнорируем директорию в любой директории проекта
node_modules/

# Игнорируем каталог в корне рабочей директории
/coverage/

# Игнорируем все файлы с расширением sqlite3 в директории db
# При этом не игнорируются такие же файлы внутри любого вложенного каталога в db
# Например, /db/something/lala.sqlite3
/db/*.sqlite3

# Игнорировать все .txt файлы в каталоге doc/ на всех уровнях вложенности
doc/**/*.txt

# Исключение временных и вторичных файлов и директорий
#	*.log
#	build/
#	temp-*
```
