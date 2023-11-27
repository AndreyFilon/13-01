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

---
