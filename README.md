# Домашнее задание к занятию "3.4. Операционные системы, лекция 2"


###### 1. На лекции мы познакомились с node_exporter...  


**# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.**  
**# TYPE go_gc_duration_seconds summary**  
**go_gc_duration_seconds{quantile="0"} 0**   
**go_gc_duration_seconds{quantile="0.25"} 0**  
**go_gc_duration_seconds{quantile="0.5"} 0**  
**go_gc_duration_seconds{quantile="0.75"} 0**  
**go_gc_duration_seconds{quantile="1"} 0**  
**go_gc_duration_seconds_sum 0**  
**go_gc_duration_seconds_count 0**  
**# HELP go_goroutines Number of goroutines that currently exist.**  
**# TYPE go_goroutines gauge**  
**go_goroutines 9**  
.....
 - поместите его в автозагрузку
 - предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на systemctl cat cron)  
 - удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

`cat nano /etc/systemd/system/node_exporter.service`

**[Unit]**  
***Description=Prometheus Node Exporter***  
***Wants=network-online.target***  
***After=network-online.target***

**[Service]**  
***User=node_exporter***  
***Group=node_exporter***  
***Type=simple***  
***EnvironmentFile=/etc/default/node_exporter***  
***ExecStart=/usr/local/bin/node_exporter $NE_OPT***

**[Install]**  
***WantedBy=multi-user.target***

`cat /etc/default/node_exporter`  
***NE_OPT="--log.level=info"***


`sudo systemctl enable --now node_exporter`  
`systemctl status node_exporter`

***Active: active  (running)***
###### 2. Ознакомьтесь с опциями node_exporter и выводом /metrics по-умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.
***# TYPE node_cpu_seconds_total counter***  
**node_cpu_seconds_total{cpu="0",mode="idle"} 5199.8**  
**node_cpu_seconds_total{cpu="0",mode="system"} 82.21**  
**node_cpu_seconds_total{cpu="0",mode="user"} 243.12**

***# TYPE node_memory_MemAvailable_bytes gauge***  
**node_memory_MemAvailable_bytes 2.256326656e+09**  
***# TYPE node_memory_MemFree_bytes gauge***  
**node_memory_MemFree_bytes 9.45836032e+08**  
***# TYPE node_memory_MemTotal_bytes gauge***  
**node_memory_MemTotal_bytes 4.122759168e+09**  

***# TYPE node_disk_io_time_seconds_total counter***  
**node_disk_io_time_seconds_total{device="sda"} 58.92**  
***# TYPE node_disk_read_bytes_total counter***  
**node_disk_read_bytes_total{device="sda"} 1.203106816e+09**

***# TYPE node_network_receive_errs_total counter***  
**node_network_receive_errs_total{device="ens160"} 0**  
***# TYPE node_network_receive_bytes_total counter***  
**node_network_receive_bytes_total{device="ens160"} 3.3009215e+07**  
***# TYPE node_network_transmit_bytes_total counter***  
**node_network_transmit_bytes_total{device="ens160"} 2.117522e+06**  
***# TYPE node_network_transmit_errs_total counter***  
**node_network_transmit_errs_total{device="ens160"} 0**

 
##### 3. Установите в свою виртуальную машину Netdata. Воспользуйтесь готовыми пакетами для установки (sudo apt install -y netdata)....

***Netdata установлена `sudo apt install -y netdata`***  
***`/etc/netdata/netdata.conf` отредактирован согласно задания***  
***В Vagrantfile порт проброшен***  
***Был приятно удивлён с количества и детализации снимаемых метрик :)***


##### 4. Можно ли по выводу dmesg понять, осознает ли ОС, что загружена не на настоящем оборудовании, а на системе виртуализации?

`vagrant@vagrant:$` **dmesg | grep virt**  
[    0.009380] CPU MTRRs all blank - virtualized system.  
[    0.075777] Booting paravirtualized kernel on KVM  
[   15.651411] systemd[1]: Detected virtualization oracle.  

***Согласно выводу `dmesg` мы можем судить о том, что ОС "осознаёт", что она загружена в виртуальной среде***


##### 5. Как настроен sysctl fs.nr_open на системе по-умолчанию? Узнайте, что означает этот параметр. Какой другой существующий лимит не позволит достичь такого числа (ulimit --help)?

`fs.nr_open` ***по умолчанию настроен на 1048576***  
***Этот параметр задёт жесткий лимит на открытые дескрипторы в ОС***  
`ulimit -Hn` ***покажет нам это же значение***


##### 6. Запустите любой долгоживущий процесс (не ls, который отработает мгновенно, а, например, sleep 1h) в отдельном неймспейсе процессов; покажите, что ваш процесс работает под PID 1 через nsenter. Для простоты работайте в данном задании под root (sudo -i). Под обычным пользователем требуются дополнительные опции (--map-root-user) и т.д

`root@vagrant:~#` ***unshare -f --pid --mount-proc sleep 1h***  
`^Z`   
`[2]+  Stopped                 unshare -f --pid --mount-proc sleep 1h`  
`root@vagrant:~#` ***ps***  
    PID TTY          TIME CMD  
  38301 pts/1    00:00:00 sudo  
  38302 pts/1    00:00:00 bash  
  38313 pts/1    00:00:00 sleep  
  45646 pts/1    00:00:00 unshare  
  45647 pts/1    00:00:00 sleep  
  45652 pts/1    00:00:00 ps  
`root@vagrant:~#` ***nsenter -t 45647 -p -m***  
`root@vagrant:/#` ***ps***  
    PID TTY          TIME CMD  
      1 pts/1    00:00:00 sleep  
      2 pts/1    00:00:00 bash  
     13 pts/1    00:00:00 ps  
`root@vagrant:/#`


##### 7. Найдите информацию о том, что такое :(){ :|:& };:. Запустите эту команду в своей виртуальной машине Vagrant с Ubuntu 20.04 (это важно, поведение в других ОС не проверялось). Некоторое время все будет "плохо", после чего (минуты) – ОС должна стабилизироваться. Вызов dmesg расскажет, какой механизм помог автоматической стабилизации. Как настроен этот механизм по-умолчанию, и как изменить число процессов, которое можно создать в сессии?

`:(){ :|:& };:` ***по своей сути является fork бомбой. По сути функция, которая параллельно запускает себя дважды, потом каждая ещё по два экземпляра и так в геометрической прогрессии, пока не исчерпается память.***  
***Решается заданием параметра `ulimit -u` двузначным числом, чтобы ограничить максимально допустимое количество процессов для пользователя***
