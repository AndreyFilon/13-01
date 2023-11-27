# Домашнее задание к занятию 13-1 "«Уязвимости и атаки на информационные системы»" - `Филон Андрей`  

---

### Задание 1. 

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

<ins>**Ответ:**</ins>

![1](https://github.com/AndreyFilon/13-01/blob/main/ports-services.jpg)  

##### Найденные уязвимости:  
Port/Title  

21/tcp  
Exploit Title: vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)  
https://www.exploit-db.com/exploits/17491  

53/tcp  
Exploit: BIND 9.4.2 - Remote DNS Cache Poisoning (Metasploit)  
https://www.exploit-db.com/exploits/6122  

80/tcp  
Apache 1.4/2.2.x - APR 'apr_fnmatch()' Denial of Service  
Apache 2.2.4 - 413 Error HTTP Request Method Cross-Site Scripting  

111/tcp  
RPCBind / libtirpc - Denial of Service  
https://www.exploit-db.com/exploits/41974  

139/tcp  
445/tcp  
Samba < 3.0.20 - Remote Heap Overflow  
https://www.exploit-db.com/exploits/7701  

2121/tcp    
ProFTPd IAC 1.3.x - Remote Command Execution  
'mod_tls' Remote Buffer Overflow  
https://www.exploit-db.com/exploits/15449  
https://www.exploit-db.com/exploits/4312    

3306/tcp   
MySQL 5.0.x - Single Row SubSelect Remote Denial of Service  
MySQL 5.0.x - IF Query Handling Remote Denial of Service  

5432/tcp  
PostgreSQL 8.3.6 - Conversion Encoding Remote Denial of Service   
PostgreSQL 8.3.6 - Low Cost Function Information Disclosure   
PostgreSQL 8.2/8.3/8.4 - UDF for Command Execution   

5900/tcp  
VNC Keyboard - Remote Code Execution (Metasploit)  

---

### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

<ins>**Ответ:**</ins>  

Режим SYN (-sS) - хост пытается инициировать TCP-соединение с целевой машиной, используя флаг SYN. Если порт закрыт, машина отвечает с флагами RST и ACK, то есть, разрывает соединение. С открытых же портов приходит пакет с флагами SYN и ACK. Таким образом, сервер подтверждает, что готов установить TCP-соединение.  


      
    Режим FIN, Xmas, NULL (-sF,-sX,-sN). Эти методы используются в случае, если SYN-сканирование по каким-либо причинам оказалось неработоспособным. Хост посылает на целевую машину TCP-пакет с флагом FIN. Если порт закрыт, в ответ приходит пакет с флагами RST и ACK (разрыв соединения). Если же порт открыт, в ответ не придет ничего (так как в запросе не установлены флаги SYN, ACK или RST). В этом случае nmap посылает еще один FIN-пакет в тот же порт, но с другого порта хоста, для проверки, что ответный пакет не потерялся. В этом режиме невозможно определить, открыт ли порт или фильтруется фаерволлом, только если в ответ не приходит ICMP-пакет "Destination Unreachable". В Xmas Tree используется пакет с набором флагов FIN, URG, PSH, а NULL-сканирование использует пакет без флагов. Согласно рекомендации RFC 973 п. 64, ОС сканируемого хоста должна ответить на такой пакет, прибывший на закрытый порт, пакетом RST, в то время как открытый порт должен игнорировать эти пакеты.   
    UDP-режим (-sU) предназначен для сканирования портов, принимающих UDP-соединения. На каждый порт сканируемой машины отправляется UDP-пакет без данных. Если в ответ было получено ICMP-сообщение "порт недоступен", это означает, что порт закрыт. В противном случае предполагается, что сканируемый порт открыт. Большой проблемой при UDP сканировании является его медленная скорость работы. Открытые и фильтруемые порты редко посылают какие-либо ответы, заставляя Nmap отправлять повторные запросы, на случай если пакеты были утеряны.  
    
---
