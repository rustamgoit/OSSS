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

Результат:

```bash
PackageKit              dhcp           ldap                 passwd-        subgid
X11                     dhcpcd.conf    legal                perl           subgid-
adduser.conf            dpkg           libaudit.conf        pm             subuid
alternatives            e2scrub.conf   locale.alias         polkit-1       subuid-
apparmor                environment    locale.conf          profile        sudo.conf
apparmor.d              environment.d  locale.gen           profile.d      sudo_logsrvd.conf
apport                  ethertypes     localtime            protocols      sudoers
apt                     fonts          logcheck             python3        sudoers.d
bash.bashrc             fstab          login.defs           python3.12     supercat
bash_completion         fuse.conf      logrotate.conf       rc0.d          sysctl.conf
bash_completion.d       gai.conf       logrotate.d          rc1.d          sysctl.d
bindresvport.blacklist  glvnd          lsb-release          rc2.d          systemd
binfmt.d                gnutls         machine-id           rc3.d          terminfo
byobu                   gprofng.rc     magic                rc4.d          timezone
ca-certificates         groff          magic.mime           rc5.d          tmpfiles.d
ca-certificates.conf    group          manpath.config       rc6.d          ubuntu-advantage
cloud                   group-         mime.types           rcS.d          ucf.conf
console-setup           gshadow        mke2fs.conf          resolv.conf    udev
credstore               gshadow-       modprobe.d           rmt            update-manager
credstore.encrypted     gss            modules              rpc            update-motd.d
cron.d                  gtk-3.0        modules-load.d       rsyslog.conf   vconsole.conf
cron.daily              host.conf      mtab                 rsyslog.d      vim
cron.hourly             hostname       nanorc               security       vtrgb
cron.monthly            hosts          netconfig            selinux        vulkan
cron.weekly             init.d         netplan              sensors.d      wgetrc
cron.yearly             inputrc        networkd-dispatcher  sensors3.conf  wsl.conf
crontab                 iproute2       networks             services       xattr.conf
dbus-1                  issue          newt                 sgml           xdg
dconf                   issue.net      nsswitch.conf        shadow         xml
debconf.conf            kernel         opt                  shadow-        zsh_command_not_found
debian_version          landscape      os-release           shells
default                 ld.so.cache    pam.conf             skel
deluser.conf            ld.so.conf     pam.d                ssh
depmod.d                ld.so.conf.d   passwd               ssl
```

### 3. Перейди у каталог /home і покажи список користувачів

```bash
cd /home
ls
```

Результат:

```bash
rustam
```


## Завдання 2. Файли, каталоги та посилання

### 1. Створи новий каталог у домашньому каталозі

```bash
cd ~
mkdir lab2
```

### 2. Створи всередині файл

```bash
cd lab2
> file.txt
```

### 3. Скопіюй файл у нове ім’я

```bash
cp file.txt copy.txt
```

### 4. Перейменуй копію

```bash
mv copy.txt renamed.txt
```

### 5. Створи жорстке посилання

```bash
ln file.txt hardlink.txt
```

### 6. Створи символічне посилання

```bash
ln -s file.txt symlink.txt
```

### 7. Знайди файл по імені

```bash
find ~ -name file.txt
```

### Результат:

```bash
/home/rustam/lab2/file.txt
```

---

## Завдання 3. Права доступу

### 1. Переглянь права файлу, який ти створив

```bash
ls -l file.txt
```

Результат:

```bash
-rw-r--r-- 2 rustam rustam 0 Jul  9 00:06 file.txt
```

### 2. Надай файлу права тільки на читання

```bash
chmod 444 file.txt
```

### 3. Надай власнику право на запис

```bash
chmod u+w file.txt
```

### 4. Переглянь значення umask

```bash
umask
```

Результат:

```bash
0022
```

### 5. Встанови нове значення

```bash
umask 023
```

## Завдання 4. Користувачі

### 1. Створи нового користувача

```bash
sudo useradd -m trainee
```

### 2. Додай його до sudo-групи

```bash
sudo usermod -aG sudo trainee
```

### 3. Перевір, що користувач існує

```bash
grep trainee /etc/passwd
```

Результат:

```bash
trainee:x:1001:1001::/home/trainee:/bin/sh
```
