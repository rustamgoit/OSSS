# Домашнє завдання Module 6. Bash-скрипти

**Виконав:** Рустам Майстренко

---

# Варіант A — Скрипт бекапу логів

## Код скрипта `backup.sh`

```bash
#!/bin/bash

# Check that exactly 2 arguments were provided
if [ "$#" -ne 2 ]; then
    echo "Usage: ./backup.sh <log_dir> <backup_dir>"
    exit 1
fi

LOG_DIR="$1"
BACKUP_DIR="$2"
LOCK_FILE="/tmp/backup.lock"

# Check that both arguments are existing directories
if [ ! -d "$LOG_DIR" ] || [ ! -d "$BACKUP_DIR" ]; then
    echo "Usage: ./backup.sh <log_dir> <backup_dir>"
    exit 1
fi

# Protection against parallel execution
if [ -e "$LOCK_FILE" ]; then
    echo "Backup already running"
    exit 1
fi

# Create lock file
touch "$LOCK_FILE"

# Remove lock file automatically on script exit
trap 'rm -f "$LOCK_FILE"' EXIT

# Create archive name with date and time
DATE=$(date +"%Y-%m-%d_%H-%M")
ARCHIVE="$BACKUP_DIR/logs_backup_$DATE.tar.gz"

# Create archive
tar -czf "$ARCHIVE" -C "$LOG_DIR" .

# Check result
if [ "$?" -ne 0 ]; then
    echo "Backup failed"
    exit 2
fi

echo "Backup created: $ARCHIVE"
```

---

# Перевірка роботи

### Створення тестових каталогів

```bash
mkdir -p ~/test_logs ~/test_backup
echo "log test" > ~/test_logs/app.log
```

### Надання прав на виконання

```bash
chmod +x ~/backup.sh
```

### Запуск скрипта

```bash
./backup.sh ~/test_logs ~/test_backup
```

Результат:

```text
Backup created: /home/rustam/test_backup/logs_backup_2026-07-09_01-57.tar.gz
```

### Перевірка створеного архіву

```bash
ls ~/test_backup
```

Результат:

```text
logs_backup_2026-07-09_01-57.tar.gz
```

### Перевірка неправильного запуску

```bash
./backup.sh
```

Результат:

```text
Usage: ./backup.sh <log_dir> <backup_dir>
```

---

# Короткий опис

Скрипт `backup.sh` приймає два аргументи: каталог із логами та каталог для збереження резервної копії. Перед виконанням він перевіряє правильність аргументів, захищається від паралельного запуску за допомогою lock-файлу `/tmp/backup.lock`, створює архів логів із поточною датою та часом у назві й повідомляє про успішне створення резервної копії або про помилку.