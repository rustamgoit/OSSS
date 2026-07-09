# Домашнє завдання №4. Пакети, сервіси та журнали

**Виконав:** Рустам Майстренко

---

## Завдання 1. Менеджери пакетів

```bash
sudo apt update
sudo apt install tree -y
dpkg -l | grep tree
tree --version
sudo apt remove tree -y
```

Результат: пакет `tree` був встановлений, перевірений та видалений.

---

## Завдання 2. Керування сервісами через systemctl

```bash
sudo systemctl status cron
sudo systemctl stop cron
sudo systemctl status cron
sudo systemctl start cron
sudo systemctl enable cron
```

Результат: сервіс `cron` був перевірений, зупинений, повторно запущений та доданий в автозавантаження.

---

## Завдання 3. Робота з логами

```bash
cd /var/log
tail -n 10 syslog
journalctl -p err
journalctl | grep cron
```

Результат: були переглянуті останні записи файлу `syslog`, помилки системи через `journalctl`, а також записи про запуск і зупинку сервісу `cron`.

---

## Завдання 4. Створення власного сервісу

### 1. Створення bash-скрипта

```bash
cat > ~/myscript.sh << 'EOF'
#!/bin/bash
while true
do
    date >> /home/rustam/dates.txt
    sleep 1
done
EOF

chmod +x ~/myscript.sh
```

### 2. Створення systemd-сервісу

```bash
sudo tee /etc/systemd/system/myscript.service > /dev/null << 'EOF'
[Unit]
Description=My Script Service

[Service]
ExecStart=/home/rustam/myscript.sh
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```

### 3. Запуск сервісу

```bash
sudo systemctl daemon-reload
sudo systemctl enable myscript.service
sudo systemctl start myscript.service
sudo systemctl status myscript.service
```

### 4. Перевірка запису даних у файл

```bash
tail /home/rustam/dates.txt
```

Результат:

```text
Thu Jul  9 01:03:40 UTC 2026
Thu Jul  9 01:03:41 UTC 2026
Thu Jul  9 01:03:42 UTC 2026
```

Висновок: сервіс `myscript.service` успішно запущений і щосекунди записує поточну дату у файл `/home/rustam/dates.txt`.