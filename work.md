updated: **20241127** - <mark>20.20</mark>
key: value

### Testing your SSH connection

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

### Установка глобальных переменных

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
```

### Как добавить репозиторий

```bash
git remote add origin git@github.com:Valery-Sorokin/hexlet-git.git
git branch -M main
git push -u origin main
```

### Как клонировать репозиторий

```bash
git clone git@github.com:Valery-Sorokin/hexlet-git.git
cd hexlet-git
ls -la
```

### Как получить изменения с GitHub

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

### git pull/push требует логин и пароль

Распространенной ошибкой является клонирование с использованием **HTTPS** вместо **SSH**. Вы можете исправить это, перейдя в свой репозиторий, нажав "Clone" и скопировав поле "Clone with SSH" (пример интерфейса GiLab).
Обновить URL-адрес удаленного источника можно, например, так:

```bash
git remote set-url origin git remote set-url origin git@github.com:Valery-Sorokin/hexlet-git.git
```
