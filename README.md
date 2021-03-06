# network-architecture

ДЗ

    https://github.com/erlong15/otus-linux/tree/network
    (ветка network)

    Vagrantfile с начальным  построением сети

        inetRouter
        centralRouter
        centralServer

    тестировалось на virtualbox
    Планируемая архитектура

    построить следующую архитектуру

    Сеть office1

        192.168.2.0/26 - dev
        192.168.2.64/26 - test servers
        192.168.2.128/26 - managers
        192.168.2.192/26 - office hardware

    Сеть office2

        192.168.1.0/25 - dev
        192.168.1.128/26 - test servers
        192.168.1.192/26 - office hardware

    Сеть central

        192.168.0.0/28 - directors
        192.168.0.32/28 - office hardware
        192.168.0.64/26 - wifi

    Office1 ---\
                    -----> Central --IRouter --> internet
    Office2----/

    Итого должны получится следующие сервера

        inetRouter
        centralRouter
        office1Router
        office2Router
        centralServer
        office1Server
        office2Server

    Практическая часть

        Соединить офисы в сеть согласно схеме и настроить роутинг
        Все сервера и роутеры должны ходить в инет через inetRouter
        Все сервера должны видеть друг друга
        у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
        при нехватке сетевых интерфейсов добавить по несколько адресов на интерфейс

    Формат сдачи ДЗ - vagrant + ansible


---

Теоретическая часть

1. Найти свободные подсети
192.168.0.16/28
192.168.0.48/28
192.168.0.128/25


2. Посчитать сколько узлов в каждой подсети, включая свободные

Сеть office1

192.168.2.0/26      - 62
192.168.2.64/26     - 62
192.168.2.128/26    - 62
192.168.2.192/26    - 62

Сеть office2

192.168.1.0/25      - 126
192.168.1.128/26    - 62
192.168.1.192/26    - 62

Сеть central

192.168.0.0/28      - 14
192.168.0.16/28     - 14
192.168.0.32/28     - 14
192.168.0.48/28     - 14
192.168.0.64/26     - 62
192.168.0.128/25    - 126


3. Указать broadcast адрес для каждой подсети

Сеть office1

192.168.2.0/26      - 192.168.2.63
192.168.2.64/26     - 192.168.2.127
192.168.2.128/26    - 192.168.2.191
192.168.2.192/26    - 192.168.2.255

Сеть office2

192.168.1.0/25      - 192.168.1.127
192.168.1.128/26    - 192.168.1.191
192.168.1.192/26    - 192.168.1.255

Сеть central

192.168.0.0/28      - 192.168.0.15
192.168.0.16/28     - 192.168.0.31
192.168.0.32/28     - 192.168.0.47
192.168.0.48/28     - 192.168.0.63
192.168.0.64/26     - 192.168.0.127
192.168.0.128/25    - 192.168.0.255

4. Проверить нет ли ошибок при разбиении

Ошибок нет.

---

Практическая часть

Запуск стенда

    vagrant up

В папке ansible

    ansible-playbook playbook.yml

Проверка    

Все сервера и роутеры должны ходить в инет через inetRouter     

### centralRouter   
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_230714.png)    
### centralServer   
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_230808.png)    
### office1Router   
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_230737.png)    
### office1Server       
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_230750.png)    

Все сервера должны видеть друг друга    

### centralServer   -->  office1Server      
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_231111.png)    
### centralServer   -->  office2Server      
![](https://github.com/MaxOOOOON/network-architecture/blob/main/pictures/Screenshot_20211031_231054.png)    
