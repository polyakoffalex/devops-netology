# Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"


###### 1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP

```
route-views>sh ip route 89.31.36.69
Routing entry for 89.31.32.0/21
  Known via "bgp 6447", distance 20, metric 0
  Tag 2497, type external
  Last update from 202.232.0.2 5w5d ago
  Routing Descriptor Blocks:
  * 202.232.0.2, from 202.232.0.2, 5w5d ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 2497
      MPLS label: none
route-views>
```

```
route-views>sh bgp 89.31.36.69
BGP routing table entry for 89.31.32.0/21, version 254927
Paths: (23 available, best #18, table default)
  Not advertised to any peer
  Refresh Epoch 1
  101 3356 8359 43148
    209.124.176.223 from 209.124.176.223 (209.124.176.223)
      Origin IGP, localpref 100, valid, external
      Community: 101:20100 101:20110 101:22100 3356:2 3356:100 3356:123 3356:507 3356:903 3356:2111 8359:5500 8359:55545
      Extended Community: RT:101:22100
      path 7FE0BE35A070 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3333 8359 43148
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin IGP, localpref 100, valid, external
      Community: 8359:5500 8359:55545
      path 7FE12C21DCE8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  6939 8359 43148
    64.71.137.241 from 64.71.137.241 (216.218.252.164)
      Origin IGP, localpref 100, valid, external
      path 7FE0338B13F0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 2
  8283 8359 43148
    94.142.247.3 from 94.142.247.3 (94.142.247.3)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 8283:1 8283:101 8359:5500 8359:55545
      unknown transitive attribute: flag 0xE0 type 0x20 length 0x18
        value 0000 205B 0000 0000 0000 0001 0000 205B
              0000 0005 0000 0001
      path 7FE0FA0D22C8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1351 8359 8359 43148
    132.198.255.253 from 132.198.255.253 (132.198.255.253)
      Origin IGP, localpref 100, valid, external
      path 7FE04116CDB8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  57866 3356 8359 43148
    37.139.139.17 from 37.139.139.17 (37.139.139.17)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 3356:2 3356:100 3356:123 3356:507 3356:903 3356:2111 8359:5500 8359:55545
      path 7FE1095C3088 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  852 3356 8359 43148
    154.11.12.212 from 154.11.12.212 (96.1.209.43)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE13C83EB40 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20130 6939 8359 43148
    140.192.8.16 from 140.192.8.16 (140.192.8.16)
      Origin IGP, localpref 100, valid, external
      path 7FE12F7BAA28 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  701 3356 8359 43148
    137.39.3.55 from 137.39.3.55 (137.39.3.55)
      Origin IGP, localpref 100, valid, external
      path 7FE166FDB5E8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3549 3356 8359 43148
    208.51.134.254 from 208.51.134.254 (67.16.168.191)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 3356:2 3356:100 3356:123 3356:507 3356:903 3356:2111 3549:2581 3549:30840 8359:5500 8359:55545
      path 7FE0FC58A070 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  53767 174 174 3356 8359 43148
    162.251.163.2 from 162.251.163.2 (162.251.162.3)
      Origin IGP, localpref 100, valid, external
      Community: 174:21000 174:22013 53767:5000
      path 7FE0D9B036A8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3356 8359 43148
    4.68.4.46 from 4.68.4.46 (4.69.184.201)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 3356:2 3356:100 3356:123 3356:507 3356:903 3356:2111 8359:5500 8359:55545
      path 7FE017BE9ED8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  4901 6079 8359 43148
    162.250.137.254 from 162.250.137.254 (162.250.137.254)
      Origin IGP, localpref 100, valid, external
      Community: 65000:10100 65000:10300 65000:10400
      path 7FE094FA9108 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20912 3257 3356 8359 43148
    212.66.96.126 from 212.66.96.126 (212.66.96.126)
      Origin IGP, localpref 100, valid, external
      Community: 3257:8070 3257:30515 3257:50001 3257:53900 3257:53902 20912:65004
      path 7FE118547950 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3303 8359 43148
    217.192.89.50 from 217.192.89.50 (138.187.128.158)
      Origin IGP, localpref 100, valid, external
      Community: 3303:1004 3303:1006 3303:1030 3303:3054 8359:5500 8359:55545
      path 7FE143F0DB78 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  7018 3356 8359 43148
    12.0.1.63 from 12.0.1.63 (12.0.1.63)
      Origin IGP, localpref 100, valid, external
      Community: 7018:5000 7018:37232
      path 7FE15726F400 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3561 3910 3356 8359 43148
    206.24.210.80 from 206.24.210.80 (206.24.210.80)
      Origin IGP, localpref 100, valid, external
      path 7FE177FE8F30 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 2
  2497 8359 43148
    202.232.0.2 from 202.232.0.2 (58.138.96.254)
      Origin IGP, localpref 100, valid, external, best
      path 7FE18B21E708 RPKI State not found
      rx pathid: 0, tx pathid: 0x0
  Refresh Epoch 1
  7660 2516 1299 8359 43148
    203.181.248.168 from 203.181.248.168 (203.181.248.168)
      Origin IGP, localpref 100, valid, external
      Community: 2516:1030 7660:9003
      path 7FE1141B83B8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3257 3356 8359 43148
    89.149.178.10 from 89.149.178.10 (213.200.83.26)
      Origin IGP, metric 10, localpref 100, valid, external
      Community: 3257:8794 3257:30043 3257:50001 3257:54900 3257:54901
      path 7FE0A5D34CE8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  49788 12552 8359 43148
    91.218.184.60 from 91.218.184.60 (91.218.184.60)
      Origin IGP, localpref 100, valid, external
      Community: 12552:12000 12552:12100 12552:12101 12552:22000
      Extended Community: 0x43:100:1
      path 7FE0A748CC50 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1221 4637 3356 8359 43148
    203.62.252.83 from 203.62.252.83 (203.62.252.83)
      Origin IGP, localpref 100, valid, external
      path 7FE0C9F01588 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  19214 3257 3356 8359 43148
    208.74.64.40 from 208.74.64.40 (208.74.64.40)
      Origin IGP, localpref 100, valid, external
      Community: 3257:8108 3257:30048 3257:50002 3257:51200 3257:51203
      path 7FE113BDBAD0 RPKI State not found
      rx pathid: 0, tx pathid: 0
route-views>
```

###### 2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

`ip link add dummy0 type dummy`  
`ip address add 192.168.100.10/24 dev dummy0`  
`ip link set dummy0 up`

`ip route add 192.168.100.0/24 via 192.168.88.1`  
`ip route add 192.168.110.0/24 dev ens160`  
`netstat -rn`
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.88.1    0.0.0.0         UG        0 0          0 ens160
169.254.0.0     0.0.0.0         255.255.0.0     U         0 0          0 ens160
192.168.0.0     0.0.0.0         255.255.255.0   U         0 0          0 dummy0
192.168.88.0    0.0.0.0         255.255.255.0   U         0 0          0 ens160
192.168.100.0   192.168.88.1    255.255.255.0   UG        0 0          0 ens160
192.168.110.0   0.0.0.0         255.255.255.0   U         0 0          0 ens160
```


##### 3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

`ss -lnpt`  


```
State   Recv-Q   Send-Q      Local Address:Port        Peer Address:Port                                                
LISTEN  0        4096            127.0.0.1:8125             0.0.0.0:*       users:(("netdata",pid=5088,fd=8))           
LISTEN  0        4096            127.0.0.1:19999            0.0.0.0:*       users:(("netdata",pid=5088,fd=3))           
LISTEN  0        128         127.0.0.53%lo:53               0.0.0.0:*       users:(("systemd-resolve",pid=804,fd=13))   
LISTEN  0        5               127.0.0.1:631              0.0.0.0:*       users:(("cupsd",pid=18720,fd=7))            
LISTEN  0        4096                    *:9100                   *:*       users:(("node_exporter",pid=2569,fd=3))     
LISTEN  0        5                   [::1]:631                 [::]:*       users:(("cupsd",pid=18720,fd=6))    
```
***Порты 8125 и 19999 слушает программа netdata***  
***Порт 53 слушает резолвер dns***  
***Порт 9100 слушает node_exporter***



##### 4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

`ss -lnpu`  

```
State   Recv-Q   Send-Q      Local Address:Port        Peer Address:Port                                                
UNCONN  0        0                 0.0.0.0:57893            0.0.0.0:*       users:(("avahi-daemon",pid=866,fd=14))      
UNCONN  0        0                 0.0.0.0:631              0.0.0.0:*       users:(("cups-browsed",pid=18722,fd=7))     
UNCONN  0        0                 0.0.0.0:5353             0.0.0.0:*       users:(("avahi-daemon",pid=866,fd=12))      
UNCONN  0        0               127.0.0.1:8125             0.0.0.0:*       users:(("netdata",pid=5088,fd=7))           
UNCONN  0        0           127.0.0.53%lo:53               0.0.0.0:*       users:(("systemd-resolve",pid=804,fd=12))   
UNCONN  0        0                 0.0.0.0:68               0.0.0.0:*       users:(("dhclient",pid=967,fd=6))           
UNCONN  0        0                    [::]:5353                [::]:*       users:(("avahi-daemon",pid=866,fd=13))      
UNCONN  0        0                    [::]:41234               [::]:*       users:(("avahi-daemon",pid=866,fd=15)) 
```

***Порт 68 слушает dhcp клиент***  
***Порт 5353 слушает avahi-daemon, некий лайтовый dns клиент***  



##### 5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали.



![Схема](https://img001.prntscr.com/file/img001/V0LvudsCS5u0h1U3TgcrXg.png)















