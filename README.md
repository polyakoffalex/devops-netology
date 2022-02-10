# Домашнее задание к занятию "3.5. Файловые системы"


###### 1. Узнайте о sparse (разряженных) файлах.

***Прочитал статью. Думаю имеет право на существование в случаях передачи больших фалов в пиринговых сетях, хранении большого объёма информации, и, может быть для архивации данных***

###### 2. Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

***Права будут идентичные. Создав произвольный файл и ссылку на него, мы увидим одинаковый набор прав. `chmod` на файл изменит и права на жесткую ссылку, т.к. оба объекта имеют общний `inode`***


 
##### 3. Сделайте vagrant destroy на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:...

***`vagrant destroy` удалил первую VM. Vagrantfile изменён согласно задания. `vagrant up` установил новую VM согласно конфигурации***


##### 4. Используя fdisk, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.

`sudo fdisk /dev/sdb`  
 ***Создано 2 раздела 2Gb и 500Mb***



##### 5. Используя sfdisk, перенесите данную таблицу разделов на второй диск.

`sfdisk -d /dev/sdb | sfdisk /dev/sdc`  
***Перенос таблицы разделов на второй диск***

##### 6. Соберите mdadm RAID1 на паре разделов 2 Гб.

`root@vagrant:~# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b1,c1}`  
***Собрали RAID1 из двухгигабайтных разделов*** 


##### 7. Соберите mdadm RAID0 на второй паре маленьких разделов.

`root@vagrant:~# mdadm --create --verbose /dev/md1 -l 0 -n 2 /dev/sd{b2,c2}`  
***Собрали RAID1 из двухгигабайтных разделов***

##### 8. Создайте 2 независимых PV на получившихся md-устройствах.

`root@vagrant:~# pvcreate /dev/md0 /dev/md1`  
***Создали 2 независимых PV***

##### 9. Создайте общую volume-group на этих двух PV.

`root@vagrant:~# vgcreate vg0 /dev/md0 /dev/md1`  
***Volume group "vg0" successfully created***

##### 10. Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

`lvcreate -L 100M vg0 /dev/md1`  
***Logical volume "lvol0" created.***

##### 11. Создайте mkfs.ext4 ФС на получившемся LV.

`mkfs.ext4 /dev/vg0/lvol0`  
***mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes  
Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done***

##### 12. Смонтируйте этот раздел в любую директорию, например, /tmp/new.

`root@vagrant:~# mkdir /tmp/new`  
`root@vagrant:~# mount /dev/vg0/lvol0 /tmp/new`  
***ФС примонтирована в /tmp/new***

##### 13. Поместите туда тестовый файл, например wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz.

***Файл `ls-lR.gz` помещён в директорию /tmp/new как `test.gz`***

##### 14. Прикрепите вывод lsblk

`root@vagrant:~# lsblk`
***NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55.4M  1 loop  /snap/core18/2128
loop1                       7:1    0 70.3M  1 loop  /snap/lxd/21029
loop2                       7:2    0 32.3M  1 loop  /snap/snapd/12704
loop3                       7:3    0 55.5M  1 loop  /snap/core18/2284
loop4                       7:4    0 43.4M  1 loop  /snap/snapd/14549
loop5                       7:5    0 61.9M  1 loop  /snap/core20/1328
loop6                       7:6    0 67.2M  1 loop  /snap/lxd/21835
sda                         8:0    0   64G  0 disk
├─sda1                      8:1    0    1M  0 part
├─sda2                      8:2    0    1G  0 part  /boot
└─sda3                      8:3    0   63G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk
├─sdb1                      8:17   0    2G  0 part
│ └─md0                     9:0    0    2G  0 raid1
└─sdb2                      8:18   0  500M  0 part
  └─md1                     9:1    0  996M  0 raid0
    └─vg0-lvol0           253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2.5G  0 disk
├─sdc1                      8:33   0    2G  0 part
│ └─md0                     9:0    0    2G  0 raid1
└─sdc2                      8:34   0  500M  0 part
  └─md1                     9:1    0  996M  0 raid0
    └─vg0-lvol0           253:1    0  100M  0 lvm   /tmp/new***
	
	
##### 15. Протестируйте целостность файла:

`root@vagrant:~# gzip -t /tmp/new/test.gz && echo $?`  
***0***

##### 16. Используя pvmove, переместите содержимое PV с RAID0 на RAID1.

`root@vagrant:~# pvmove /dev/md1`  
***/dev/md0: Moved: 80.00%  
/dev/md0: Moved: 100.00%***

##### 17. Сделайте --fail на устройство в вашем RAID1 md.

`mdadm /dev/md0 --fail /dev/sdb1`  
***mdadm: set /dev/sdb1 faulty in /dev/md0***

##### 18. Подтвердите выводом dmesg, что RAID1 работает в деградированном состоянии.

`root@vagrant:~# dmesg | grep md0`  
***[ 4288.213432] md/raid1:md0: not clean -- starting background reconstruction
[ 4288.213434] md/raid1:md0: active with 2 out of 2 mirrors
[ 4288.213456] md0: detected capacity change from 0 to 2144337920
[ 4288.215830] md: resync of RAID array md0
[ 4298.794516] md: md0: resync done.
[ 7385.381063] md/raid1:md0: Disk failure on sdb1, disabling device.
               md/raid1:md0: Operation continuing on 1 devices.***
			   
##### 19. Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:...

`root@vagrant:~# gzip -t /tmp/new/test.gz && echo $?`  
***0***

##### 20. Погасите тестовый хост, vagrant destroy.

`vagrant destroy`