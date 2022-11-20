# Домашнее задание №17

> Всем привет! Сначала здесь будет инструкция по настройке БД `Postgres` и `pgAdmin`. После будет несколько задач :)

## Небольшая инструкция по запуску

Необходимо склонить официальный `container` из docker-хаба:
1. https://hub.docker.com/_/postgres (можно выполнить команду `docker pull postgres`).
2. https://hub.docker.com/r/dpage/pgadmin4 (можно выполнить команду `docker pull dpage/pgadmin4`)

После этого на `dashboard` в докере надо просто запустить `postgres` и `pgadmin4`. 

> У некоторых из вас не установился визуализатор `Docker` - ничего страшного. Надо просто руками запустить `PostgreSql`.
> Команда: `docker run -d -p 55000:55000 postgres`

После запуска в терминале надо выполнить команду:
> docker run -p 5050:80 -e 'PGADMIN_DEFAULT_EMAIL=pgadmin4@pgadmin.org' -e 'PGADMIN_DEFAULT_PASSWORD=admin' -d --name pgadmin4 dpage/pgadmin4

Теперь по ссылке доступен pgadmin4: http://localhost:5050. Вас попросят ввести логин и пароль, как только вы попадете на страницу:
- логин: `pgadmin4@pgadmin.org`
- пароль: `admin`

После входа внутри `pgAdmin` необходимо сделать несколько действий:
1. Нажмите `Add New Server` и заполнить данные:
    1. server name -> **pg** (или любой другой по желанию)
2. На вкладке `Connection`:
    1. host -> **host.docker.internal**
    2. port -> **55000**
    3. username -> **postgres**
    4. password -> **admin**
3. Нажмите кнопку `Save`

> Возможно, у вас будут проблемы и `pgAdmin` напишет вам, что не может подключиться к БД. Вся проблема в `host`, 
> потому что на некоторых компьютерах `Docker` требует, чтобы там был написан `IP`, а не 
> `host.docker.internal`. 

**Как найти `IP`, который туда вписать?** Вам нужен IP, на котором работает ваш `Postgres`.
1. Введите команду `docker ps` и скопируйте `CONTAINER ID` вашего `Postgres`. 
2. После этого введите команду: `docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' CONTAINER_ID`, где вместо CONTAINER_ID поставьте то значение, которое вы скопировали.

В выводе будет `ip-адрес`, который нужно вставить вместо `host.docker.internal`.

> Дополнительные инструкции, по которым вам точно станет очень многое ясно. Ссылки ниже:
1. [Инструкция по Docker](Docker.pdf)
2. [Инструкция по Dockerfile](Dockerfile.pdf)
3. [Как собрать свой образ](Как_собрать_и_запустить_свой_образ.pdf)

***

Дополнительная ссылка для ознакомления sql-запросов - [тыкайте сюда](https://tproger.ru/translations/sql-recap/).

## Задача №1
Первое, что нужно сделать, - это, конечно, сфотать работающий `pgAdmin` и прикрепить скрин.

## Задача №2
Теперь необходимо создать новую схему в БД. Назовите ее как хотите :) 

После этого создайте таблицу `User` с некоторыми полями:
1. `id`
2. Имя
3. Фамилия
4. Возраст

И положите туда любое значение. Все команды сохраните и добавьте их в текстовый файл. 
Этот текстовый файл положите как решение второй задачи.

## Задача №3
Положите еще пару значений в эту таблицу. После этого сделайте `select` всей таблицы и отправьте скрин таблицы. 
Это будет решение третьей задачи.