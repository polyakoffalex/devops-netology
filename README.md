# Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"


###### 1. Работа c HTTP через телнет. Подключитесь утилитой телнет к сайту stackoverflow.com telnet stackoverflow.com 80...
```
HTTP/1.1 301 Moved Permanently  
cache-control: no-cache, no-store, must-revalidate  
location: https://stackoverflow.com/questions  
x-request-guid: 8db25855-ac42-471d-8a5e-2c32acc20eaa  
feature-policy: microphone 'none'; speaker 'none'  
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com  
Accept-Ranges: bytes  
Date: Tue, 15 Feb 2022 13:39:19 GMT  
Via: 1.1 varnish  
Connection: close  
X-Served-By: cache-fra19134-FRA  
X-Cache: MISS  
X-Cache-Hits: 0  
X-Timer: S1644932360.892911,VS0,VE85  
Vary: Fastly-SSL  
X-DNS-Prefetch-Control: off  
Set-Cookie: prov=12d111ff-615b-8c41-9018-6841d91bf043; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly
```
***301 - код состояния HTTP, сообщающий клиенту, что страница, к которой клиент обращается, перемещена по новому адресу и старый адрес следует считать устаревшим.***

###### 2. Повторите задание 1 в браузере, используя консоль разработчика F12.

***Получен код 200***  
***самый долгий запрос `collect` обрабатывался 112ms***  
![Скриншот консоли](https://drive.google.com/file/d/1L_ps3kn8px0Mbls9EL34WMGJ-TMNe8JL/view?usp=sharing)


 
##### 3. Какой IP адрес у вас в интернете?

***89.31.36.69***


##### 4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois


***Провайдер Mobile TeleSystems PJSC***  
***Автономная система AS43148***

***vagrant@vagrant:~$ whois 89.31.36.69***  
```
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '89.31.36.0 - 89.31.36.255'

% Abuse contact for '89.31.36.0 - 89.31.36.255' is 'mailto:abuse@mtu.ru'

inetnum:        89.31.36.0 - 89.31.36.255
netname:        MTS-KURGAN
country:        RU
admin-c:        CCUB1-RIPE
tech-c:         CCUB1-RIPE
status:         ASSIGNED PA
mnt-by:         UTC-MNT
created:        2017-11-29T07:17:11Z
last-modified:  2017-11-29T07:17:11Z
source:         RIPE

role:           Mobile TeleSystems PJSC Ural Branch
address:        Ural Branch of Mobile TeleSystems PJSC
address:        128 Mamina-Sibiryaka
address:        Ekaterinburg 620026
address:        Russia
phone:          +7 343 3652230
admin-c:        AVP24-RIPE
tech-c:         AVP24-RIPE
abuse-mailbox:  mailto:abuse@mtu.ru
nic-hdl:        CCUB1-RIPE
mnt-by:         UTC-MNT
created:        2011-04-16T15:29:55Z
last-modified:  2021-04-07T11:47:09Z
source:         RIPE # Filtered

% Information related to '89.31.32.0/21AS43148'

route:          89.31.32.0/21
descr:          LLC Infocentr
origin:         AS43148
mnt-by:         INFOCENTR-MNT
created:        2010-06-05T11:18:20Z
last-modified:  2010-06-05T11:18:20Z
source:         RIPE

% This query was served by the RIPE Database Query Service version 1.102.2 (HEREFORD)
```



##### 5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute

***root@ubuntu:~# traceroute -An 8.8.8.8***
```
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.88.1 [*]  0.277 ms  0.486 ms  0.462 ms
 2  89.31.36.126 [AS43148]  26.992 ms  26.964 ms  26.945 ms
 3  212.188.2.205 [AS8359]  26.927 ms  26.909 ms  26.891 ms
 4  212.188.42.218 [AS8359]  30.687 ms  30.669 ms  30.652 ms
 5  212.188.42.129 [AS8359]  62.751 ms  62.717 ms  62.690 ms
 6  212.188.29.25 [AS8359]  62.672 ms  63.608 ms  36.238 ms
 7  195.34.50.74 [AS8359]  36.567 ms  36.797 ms  36.535 ms
 8  212.188.29.82 [AS8359]  37.070 ms  37.053 ms  37.040 ms
 9  108.170.250.66 [AS15169]  37.665 ms 108.170.250.34 [AS15169]  37.653 ms 108.170.250.99 [AS15169]  37.001 ms
10  142.250.239.64 [AS15169]  51.827 ms  51.814 ms 142.251.49.24 [AS15169]  51.173 ms
11  74.125.253.109 [AS15169]  51.160 ms 108.170.232.251 [AS15169]  50.759 ms 172.253.65.82 [AS15169]  50.448 ms
12  216.239.56.101 [AS15169]  48.286 ms 172.253.51.249 [AS15169]  51.436 ms 216.239.58.53 [AS15169]  51.139 ms
13    *
14    *
15    *
16    *
17    *
18    *
19    *
20    *
21    *
22  8.8.8.8 [AS15169]  77.299 ms  74.052 ms  73.468 ms
```

##### 6. Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка - delay?

***root@ubuntu:~# mtr -nzw 8.8.8.8***
```
Start: 2022-02-16T09:05:42+0000
HOST: ubuntu                   Loss%   Snt   Last   Avg  Best  Wrst StDev
  1. AS???    192.168.88.1      0.0%    10    0.3   0.4   0.3   1.0   0.2
  2. AS43148  89.31.36.126      0.0%    10   17.5  17.1   0.8  66.0  21.4
  3. AS8359   212.188.2.205     0.0%    10   10.7  14.9   1.1  54.1  17.8
  4. AS8359   212.188.42.218    0.0%    10   20.1  16.5   4.9  33.8  11.8
  5. AS8359   212.188.42.129    0.0%    10   57.8  48.5  36.0  64.9  12.8
  6. AS8359   212.188.29.25     0.0%    10   61.9  49.7  36.4  65.1  11.3
  7. AS8359   195.34.50.74      0.0%    10   60.0  47.3  36.3  62.2  11.6
  8. AS8359   212.188.29.82    10.0%    10   36.8  45.6  36.7  63.1  10.9
  9. AS15169  108.170.250.113  80.0%    10   54.4  56.7  54.4  58.9   3.1
 10. AS15169  142.251.49.158   40.0%    10   80.3  73.3  50.0 101.1  17.3
 11. AS15169  216.239.43.20     0.0%    10   70.8  75.2  50.3 106.8  21.0
 12. AS15169  209.85.251.41     0.0%    10   70.7  63.0  51.2  78.7  11.0
 13. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 14. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 15. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 16. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 17. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 18. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 19. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 20. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 21. AS???    ???              100.0    10    0.0   0.0   0.0   0.0   0.0
 22. AS15169  8.8.8.8          60.0%    10   73.7  61.1  50.2  73.7  12.7
```
***Наибольшая задержка между хопами `216.239.43.20` и `209.85.251.41`***

##### 7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой dig

***vagrant@vagrant:~$ dig +noall +answer dns.google***  
```
dns.google.             333     IN      A       8.8.4.4
dns.google.             333     IN      A       8.8.8.8
```

##### 8. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой dig
***К обоим IP привязано имя `dns.google`***  
***vagrant@vagrant:~$ dig -x 8.8.4.4***
```
; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6328
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   19720   IN      PTR     dns.google.

;; Query time: 92 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Wed Feb 16 09:20:20 UTC 2022
;; MSG SIZE  rcvd: 73
```

***vagrant@vagrant:~$ dig -x 8.8.8.8***
```
; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36296
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   6401    IN      PTR     dns.google.

;; Query time: 4 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Wed Feb 16 09:21:48 UTC 2022
;; MSG SIZE  rcvd: 73
```
