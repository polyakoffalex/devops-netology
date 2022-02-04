# Домашнее задание к занятию "3.3. Операционные системы, лекция 1"


###### 1. Какой системный вызов делает команда cd? В прошлом ДЗ мы выяснили, что cd не является самостоятельной программой, это shell builtin, поэтому запустить strace непосредственно на cd не получится. Тем не менее, вы можете запустить strace на /bin/bash -c 'cd /tmp'. В этом случае вы увидите полный список системных вызовов, которые делает сам bash при старте. Вам нужно найти тот единственный, который относится именно к cd. Обратите внимание, что strace выдаёт результат своей работы в поток stderr, а не в stdout.

***`chdir ("/tmp")`***  


###### 2. Попробуйте использовать команду file на объекты разных типов на файловой системе... Используя strace выясните, где находится база данных file на основании которой она делает свои догадки

***Судя по всему `openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3`***  
***По пути `/etc.magic.mgc` выводится ошибка `openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (No such file or directory)`***

##### 3. Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).

***`vagrant@vagrant:~$ ping 8.8.8.8 > /tmp/ping_log`***  
***`vagrant@vagrant:~$ rm -rf /tmp/ping_log`***  
***`vagrant@vagrant:~$ ps aux | grep ping`***  
***`vagrant@vagrant:~$ lsof -p 3489`***  
***ping    3489 root    1w   REG  253,0    36576 1572881 /tmp/ping_log (deleted)***  
***`vagrant@vagrant:~$ echo '' >/proc/1126/fd/5`***

##### 4. Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?

***Зомби процессы не потребляют ресурсов CPU, RAM. Единственный потребляемый ресурс - запись в таблице процессов ядра***


##### 5. В iovisor BCC есть утилита opensnoop: ...  На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты?

***`root@vagrant:~# /usr/sbin/opensnoop-bpfcc`***

PID    COMM               FD ERR PATH  
***828    vminfo              5   0 /var/run/utmp  
610    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services  
610    dbus-daemon        20   0 /usr/share/dbus-1/system-services  
610    dbus-daemon        -1   2 /lib/dbus-1/system-services  
610    dbus-daemon        20   0 /var/lib/snapd/dbus-1/system-services/  
367    systemd-udevd      14   0 /sys/fs/cgroup/unified/system.slice/systemd-udevd.service/cgroup.procs  
367    systemd-udevd      14   0 /sys/fs/cgroup/unified/system.slice/systemd-udevd.service/cgroup.threads  
828    vminfo              5   0 /var/run/utmp***



##### 6. Какой системный вызов использует uname -a? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в /proc, где можно узнать версию ядра и релиз ОС.

***`uname -a` использует системный вызов `uname()`***

***`Part of the utsname information is also accessible  via  /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.`***



##### 7. Чем отличается последовательность команд через ; и через && в bash? Например:... Есть ли смысл использовать в bash &&, если применить set -e?


***`;` и `&&` в bash - разделитель последовательных команд и условный оператор соответственно***  
***В случае с `root@netology1:~# test -d /tmp/some_dir && echo Hi` вывод на экран получим при успешном завершении работы команды `test`***  
***Использовать в bash `&&`, если применить `set -e` смысла нет. При ошибке выполнение команд остановится***


##### 8. Из каких опций состоит режим bash set -euxo pipefail и почему его хорошо было бы использовать в сценариях?

***`-e` прерывает выполнение исполнения при ошибке любой команды кроме последней в последовательности***  
***`-x` вывод трейса простых команд***  
***`-u` неустановленные/не заданные параметры и переменные считаются как ошибки, с выводом в stderr текста ошибки и выполнит завершение неинтерактивного вызова***  
***`-o` pipefail возвращаемое значение конвейера - это состояние последней команды, которая должна выйти с ненулевым статусом, или ноль, если ни одна команда не вышла с ненулевым статусом***

***Повышение уровня дебага выполняемого сценария. Возможность завершить сценарий при ошибке на любом этапе, кроме последней команды***
##### 9. Используя -o stat для ps, определите, какой наиболее часто встречающийся статус у процессов в системе. В man ps ознакомьтесь (/PROCESS STATE CODES) что значат дополнительные к основной заглавной буквы статуса процессов. Его можно не учитывать при расчете (считать S, Ss или Ssl равнозначными).

***Наиболее частые `S*(S,S+,Ss,Ssl,Ss+)`, `I*(I,I<)`***
***Дополнительные симовлы описывают характеристики процесса: приоритет, многопоточность и пр.***