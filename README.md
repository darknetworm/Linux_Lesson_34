# Linux_Lesson_34
## Bridges, tunnels, VPN

### Описание репозитория

Лабораторный стенд для тестирования различных режимов VPN соединений между сервером и клиентом, настраиваемые с использованием Vagrant и Ansible. Все файлы и структуру директорий temрlates и client необходимо скопировать в общую директорию.

**Vagrantfile** - в зависимости от использования файла Ansible playbook создаются VPN-сервер с подключающимся к нему клиентом (в режимах tap или tun) или VPN-сервер для подключения к нему с хост-машины (создаваемая виртуальная машина client при этом не используется и создаётся для универсальности файла настройки vagrant). Настройка функциональности хостов производится с помощью Ansible playbook.  
**hosts** - файл с настройками компьютеров для быстрого доступа к ним из playbook.  
**tap.yml** - файл Ansible playbook для установки и настройки виртуальных машин для соединения в режиме tap.  
**tun.yml** - файл Ansible playbook для установки и настройки виртуальных машин для соединения в режиме tun.  
**ras.yml** - файл Ansible playbook для установки и настройки сервера для соединения с хост-машиной в режиме RAS с обменом клиентскими сертификатами.  
Директория **/templates** содержит файлы для конфигурирования режимов работы VPN соединений, а также сервис, отвечающий за работу OpenVPN.  
Директория **/client** содержит файл конфигурирования подключения к VPN-серверу с хост-машины. Также в эту директорию загружается ключевая информация для постороения клиент-серверного VPN-соединения. После копирования необходимых сертификатов и ключей в директорию, её можно переместить в другое место.

---

### Проверка работоспособности стенда

Для проверки работоспособности VPN-соединения в режиме tap и tun использовалась утилита ping и для проверки пропускной спопосбности канала - iperf3.
![tap](https://github.com/darknetworm/Linux_Lesson_34/assets/82410807/1343cd31-010e-481c-acad-c1dd990e8148)  
Режим tap.
![tun](https://github.com/darknetworm/Linux_Lesson_34/assets/82410807/42aa130f-6e39-4606-9c85-dc0dd0004fa9)  
Режим tun.  

Из-за "слабой" конфигурации ПК, на котором снимались скриншоты, разница между двумя режимами практически не различима. На более мощном ПК результаты iperf в режиме tap значительнот превосходили результаты в режиме tun, т.к. tap работает на канальном уровне, а tun - на сетевом.

Для проверки работоспособности клиент-серверного VPN-соединения на основе обмена клиентскими сертификатами необходимо из директории /client запуститьЖ
    sudo openvpn --config client.conf
и проверить созданное соединение с помощью утилиты ping
![rsa](https://github.com/darknetworm/Linux_Lesson_34/assets/82410807/f150bdf6-280f-406e-bad5-c7f371f6a4a8)
