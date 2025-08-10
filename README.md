# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Лычагин Н.В.`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1. 

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

Ответ

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

docker run --name mysqlhw12 -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:8.0

![alt text](https://github.com/Nikich828/12_2hw/blob/master/1.jpeg)

docker exec -it mysqlhw12 mysql -u root -p

![alt text](https://github.com/Nikich828/12_2hw/blob/master/2.jpeg)

1.2. Создайте учётную запись sys_temp.
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
1.4. Дайте все права для пользователя sys_temp.

CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY '12345';

SELECT user FROM mysql.user;

GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;

![alt text](https://github.com/Nikich828/12_2hw/blob/master/12.jpeg)
![alt text](https://github.com/Nikich828/12_2hw/blob/master/3.jpeg)
![alt text](https://github.com/Nikich828/12_2hw/blob/master/4.jpeg)

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";

![alt text](https://github.com/Nikich828/12_2hw/blob/master/5.jpeg)
![alt text](https://github.com/Nikich828/12_2hw/blob/master/6.jpeg)

1.6. Переподключитесь к базе данных от имени sys_temp.

SYSTEM mysql -u sys_temp -p

SELECT user();

![alt text](https://github.com/Nikich828/12_2hw/blob/master/7.jpeg)

1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

wget https://downloads.mysql.com/docs/sakila-db.zip

unzip sakila-db.zip

![alt text](https://github.com/Nikich828/12_2hw/blob/master/8.jpeg)

1.7. Восстановите дамп в базу данных.

docker exec -i mysqlhw12 mysql -uroot -proot < sakila-db/sakila-schema.sql

docker exec -i mysqlhw12 mysql -uroot -proot < sakila-db/sakila-data.sql

docker exec -it mysqlhw12 mysql -uroot -proot -e "SHOW DATABASES;"

(Написал  -uroot -proot слитно, т.к. при перенаправлении ввода классический синтаксис не работает)

![alt text](https://github.com/Nikich828/12_2hw/blob/master/9.jpeg)

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

USE sakila;

SHOW TABLES;

![alt text](https://github.com/Nikich828/12_2hw/blob/master/10.jpeg)

### Задание 2. 
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа
customer         | customer_id


Ответ

SELECT TABLE_NAME,COLUMN_NAME FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE WHERE TABLE_SCHEMA='sakila' AND CONSTRAINT_NAME='PRIMARY';

![alt text](https://github.com/Nikich828/12_2hw/blob/master/11.jpeg)


