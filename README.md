# Домашнее задание к занятию «Система мониторинга Zabbix» Дружинин Д.А.
В практике есть 2 основных и 1 дополнительное (со звездочкой) задания. Первые два нужно выполнять обязательно, третье - по желанию и его решение никак не повлияет на получение вами зачета по этому домашнему заданию, при этом вы сможете глубже и/или шире разобраться в материале.
Пожалуйста, присылайте на проверку всю задачу сразу. Любые вопросы по решению задач задавайте в чате учебной группы.
### Цели задания
1.	Научиться устанавливать Zabbix Server c веб-интерфейсом
2.	Научиться устанавливать Zabbix Agent на хосты
3.	Научиться устанавливать Zabbix Agent на компьютер и подключать его к серверу Zabbix
### Чеклист готовности к домашнему заданию
•	  Просмотрите в личном кабинете занятие "Система мониторинга Zabbix"
### Инструкция по выполнению домашнего задания
1.	Сделайте fork репозитория c шаблоном решения к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2.	Выполните клонирование этого репозитория к себе на ПК с помощью команды git clone.
3.	Выполните домашнее задание и заполните у себя локально этот файл README.md:
o	впишите вверху название занятия и ваши фамилию и имя;
o	в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
o	для корректного добавления скриншотов воспользуйтесь инструкцией «Как вставить скриншот в шаблон с решением»;
o	при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в инструкции по MarkDown.
4.	После завершения работы над домашним заданием сделайте коммит (git commit -m "comment") и отправьте его на Github (git push origin).
5.	Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6.	Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.
________________________________________
### Задание 1
Установите Zabbix Server с веб-интерфейсом.
### Процесс выполнения
1.	Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2.	Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3.	Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4.	Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
### Требования к результаты
1.	Прикрепите в файл README.md скриншот авторизации в админке.
2.	Приложите в файл README.md текст использованных команд в GitHub

### Решение 1
![alt text](https://github.com/Daark46/Zabbix/blob/main/Zabbix/Картинка%20zabbix%201.png)

```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb

dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb

apt update

apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts

su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'

su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf

sudo systemctl restart zabbix-server apache2 # zabbix-agent

sudo systemctl enable zabbix-server apache2 # zabbix-agent  
```

### Задание 2
Установите Zabbix Agent на два хоста.
### Процесс выполнения
1.	Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2.	Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3.	Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4.	Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5.	Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.
### Требования к результаты
1.	Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2.	Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3.	Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4.	Приложите в файл README.md текст использованных команд в GitHub

### Решение 2
![alt text](https://github.com/Daark46/Zabbix/blob/main/Zabbix/zabbix2.png)
![alt text](https://github.com/Daark46/Zabbix/blob/main/Zabbix/zabbix2.1.png)
![alt text](https://github.com/Daark46/Zabbix/blob/main/Zabbix/zabbix3.png)

```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb

dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb

apt update

apt install zabbix-agent

sudo systemctl restart zabbix-agent

sudo systemctl enable zabbix-agent
```
