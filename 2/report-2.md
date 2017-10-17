### Номер 1

`ls -lRa /dev/disk | grep ^l | cut -f 3 -d/ | sort | uniq`

### Номер 2

`ls -lRa /run 2> /dev/null | grep ^s | wc -l`

### Номер 3

Не горжусь этим решением, можно было решить в одну строку. Но слишком много времени убил на это, чтобы в итоге использовать что-то другое

```
cd ~/radio
find . -amin -60 -type f | grep -e mp3 -e ogg | grep incomplete | sort | uniq > /tmp/modified-last-hour
find . -type f | grep -e mp3 -e ogg | grep incomplete | sort | uniq > /tmp/all-files
diff /tmp/all-files /tmp/modified-last-hour
diff /tmp/all-files /tmp/modified-last-hour | grep \< | cut -d ' ' -f 2 | xargs rm
```

### Номер 4

```
alias vim=nvim
alias gco='git checkout'
alias rs='rails server'
alias RET='RAILS_ENV=test'
alias g=git
```

### Номер 5

`sudo grep -lr /etc -e ^#$(whoami) 2> /dev/null`

### Номер 6

`sudo find / -type d 2> /dev/null | awk '{print gsub("/","/"), $0}' | sort -r | cut -d ' ' -f 2`

### Номер 7

Сохранить код ниже в какой-нибудь скрипт

```
#! /bin/bash

MY_NAME=$(who | grep $(whoami) | head -n 1 | cut -d ' ' -f 1)

MY_TERMINAL=$(who | grep $(whoami) | head -n 1 | cut -d ' ' -f 4)

if [ ! -f /tmp/last-visit ]; then
  who | cut -d ' ' -f 1 | sort | uniq > /tmp/last-visit
  exit
fi

who | cut -d ' ' -f 1 | sort | uniq > /tmp/current-visit

echo ${MY_NAME}
echo ${MY_TERMINAL}

diff /tmp/last-visit /tmp/current-visit | grep \> | who | cut -d ' ' -f 1 | sort | uniq | write $MY_NAME $MY_TERMINAL

mv /tmp/current-visit /tmp/last-visit
```

И в crontab задать что-нибудь вроде `*/5 * * * * bash %путь до скрипта%`

### Номер 8

`ls -lRa | find -perm /000 -writable`

### Номер 9

```
sudo groupadd test
sudo usermode -g test
sudo chown poctek:test %somewhere%
```
 
 ### Номер 10
 
 `sudo ls -lRSa | sudo find -atime -30 -type f | head —n 9 | cut -d \/ -f 2`