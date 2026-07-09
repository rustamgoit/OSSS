# Домашнє завдання №2. Файлова система і права доступу

**Виконав:** Рустам Майстренко

---

## Завдання 1. Ієрархія каталогів Linux

### 1. Перейди в кореневий каталог / і покажи вміст

```bash
cd /
ls
```

Результат:

```bash
bin                dev   init               lib64       mnt   root  sbin.usr-is-merged  sys  var
bin.usr-is-merged  etc   lib                lost+found  opt   run   snap                tmp
boot               home  lib.usr-is-merged  media       proc  sbin  srv                 usr
```

### 2. Перейди в /etc і покажи вміст

```bash
cd /etc
ls
```

### 3. Створити порожній файл (без `touch`)

```bash
> test.txt
```

### 4. Переглянути вміст файлу

```bash
cat test.txt
```

### 5. Перейти у домашній каталог абсолютним шляхом

```bash
cd /home/rustam
pwd
```

Результат:

```text
/home/rustam
```

### 6. Перейти у домашній каталог відносним шляхом

```bash
cd ~/Downloads
pwd

cd ..
pwd
```

Результат:

```text
/home/rustam/Downloads
/home/rustam
```

---

## Завдання 2. Робота з документацією

### Виконані команди

```bash
man ls
help cd
man cat
man man
cp --help
mv --help
```

### Відповіді на питання

**1. Який ключ `ls` показує приховані файли?**

`-a` (`--all`)

**2. Який ключ у `cat` нумерує рядки?**

`-n` (`--number`)

**3. Чим відрізняються `man` і `--help`?**

`man` відкриває повну документацію команди з детальним описом, параметрами та прикладами використання. `--help` виводить коротку довідку безпосередньо в терміналі з основними параметрами команди.

---

## Завдання 3. Міні-сценарій

```bash
cd ~/Downloads
> homework.txt
ls
cd ..
cd Downloads
man ls
```

Після перегляду документації для виходу використовується клавіша `q`.
