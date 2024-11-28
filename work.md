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
