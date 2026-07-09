# Домашнє завдання Module 5. Мережа та SSH

**Виконав:** Рустам Майстренко

---

# Завдання 1. Мережева діагностика

### 1. Виведення IP-адрес та інтерфейсів

```bash
ip a
```

### 2. Перевірка доступності мережі Інтернет

```bash
ping -c 4 8.8.8.8
```

### 3. Перевірка listening-портів

```bash
ss -tulpn
```

### Коментар

Локальна IP-адреса мережевого інтерфейсу **eth0**:

```text
172.25.53.24
```

Доступ до Інтернету присутній, оскільки команда `ping` отримала 4 відповіді без втрати пакетів.

Приклад сервісу, який прослуховує порт:

```text
127.0.0.53:53
```

---

# Завдання 2. SSH-доступ з ключами та config

### Генерація SSH-ключа

```bash
ssh-keygen -t ed25519 -C "rustam@homework"
```

### Копіювання ключа

```bash
ssh-copy-id rustam@localhost
```

### Налаштування конфігурації

Файл `~/.ssh/config`:

```text
Host myserver
    HostName localhost
    User rustam
    IdentityFile ~/.ssh/id_ed25519
```

### Підключення

```bash
ssh myserver
```

### Коментар

Host у конфігураційному файлі:

```text
myserver
```

Підключення до сервера виконується без запиту пароля.

---

# Завдання 3. Копіювання файлів між машинами

### Створення тестового файлу

```bash
echo "test" > test.txt
```

### Передача файлу через SCP

```bash
scp test.txt myserver:~/test.txt
```

### Створення директорії на сервері

```bash
ssh myserver "mkdir -p ~/sync_folder"
```

### Синхронізація папки

```bash
mkdir -p local_sync

echo "sync test" > local_sync/sync.txt

rsync -av local_sync/ myserver:~/sync_folder/
```

### Перевірка через SFTP

```bash
sftp myserver
```

Команди в SFTP:

```text
ls
cd sync_folder
ls
exit
```

### Результат

```text
Downloads
dates.txt
homework
lab2
myscript.sh
sync_folder
test.txt

sync.txt
```

### Коментар

Файл `test.txt` був успішно переданий на сервер за допомогою `scp`.

Локальна папка `local_sync` була синхронізована із сервером у директорію:

```text
~/sync_folder/
```

Для перевірки використовувалась команда:

```bash
sftp myserver
```

Після чого були виконані команди `ls` та `cd sync_folder`.