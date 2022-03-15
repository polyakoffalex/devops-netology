# Домашнее задание к занятию "4.1. Командная оболочка Bash: Практические навыки"

## Обязательная задача 1

Есть скрипт:
```bash
a=1
b=2
c=a+b
d=$a+$b
e=$(($a+$b))
```

Какие значения переменным c,d,e будут присвоены? Почему?

| Переменная  | Значение | Обоснование |
| ------------- | ------------- | ------------- |
| `c`  | a+b  | строковое выражение, т.к. переменные не обозначены $ |
| `d`  | 1+2  | переменные преобразованы в числовые значение, но арифметическое действие не выполнено, т.к. `+` строковый символ |
| `e`  | 3  | валидное выражение, преобразование переменных в число и арифметическое действие |


## Обязательная задача 2
На нашем локальном сервере упал сервис и мы написали скрипт, который постоянно проверяет его доступность, записывая дату проверок до тех пор, пока сервис не станет доступным (после чего скрипт должен завершиться). В скрипте допущена ошибка, из-за которой выполнение не может завершиться, при этом место на Жёстком Диске постоянно уменьшается. Что необходимо сделать, чтобы его исправить:
```bash
while ((1==1)
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	fi
done
```

### Ваш скрипт:
```bash
while ((1==1))
do
	curl https://localhost:4757
	if (($? != 0))
	then
		date >> curl.log
	else exit 
	fi
	sleep 90
done
```
В исходном скрипте не хватало закрывающий скобки в цикле `while`. Добавлено условие завершения работы скрипта, если хост доступе. Во избежание заполнения дискового пространства добавлено условие старта через 90 секунд

## Обязательная задача 3
Необходимо написать скрипт, который проверяет доступность трёх IP: `192.168.0.1`, `173.194.222.113`, `87.250.250.242` по `80` порту и записывает результат в файл `log`. Проверять доступность необходимо пять раз для каждого узла.

### Ваш скрипт:
```bash
#!/bin/bash

IPS="172.217.169.163 87.250.250.242 192.168.1.1"

rm -f ./ipcheck.log

for IP in $IPS 
do
	echo "Checking $IP..."

    STATUS=0
    for i in {1..5}
    do
        netcat -w 3 -vz $IP 80 2> /dev/null
        if [ $? -ne 0 ]
        then
            STATUS=1
            break
        fi
    done

    if [ $STATUS -eq 0 ]
    then
        echo "[`date '+%Y/%m/%d %H:%M:%S'`] $IP is available" >> ipcheck.log
    else 
        echo "[`date '+%Y/%m/%d %H:%M:%S'`] $IP is NOT available" >> ipcheck.log
    fi
done

echo " "
echo "Print reulsts:"
cat ipcheck.log
```

## Обязательная задача 4
Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается.

### Ваш скрипт:
```bash
#!/bin/bash

IPS="172.217.169.163 87.250.250.242 192.168.1.1"

rm -f ./ipcheck.log

while true
do
    for IP in $IPS 
    do
    	echo "Checking $IP..."
    
        STATUS=0
        for i in {1..5}
        do
            netcat -w 3 -vz $IP 80 2> /dev/null
            if [ $? -ne 0 ]
            then
                STATUS=1
                break
            fi
        done
    
        if [ $STATUS -ne 0 ]
        then
            echo "[`date '+%Y/%m/%d %H:%M:%S'`] $IP is NOT available" >> ipcheck.log
            break 2
        fi
    done

    echo "Wait for 5 sec..."
    sleep 5
done

echo " "
echo "Print reulsts:"
cat ipcheck.log
```

