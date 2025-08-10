# Домашнее задание к занятию "`Расширенные возможности SQL`" - `Лычагин Н.В.`


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

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.

Ответ

```sql
SELECT 
    s.first_name AS "Фамилия сотрудника",
    s.last_name AS "Имя сотрудника",
    c.city AS "Город магазина",
    COUNT(cu.customer_id) AS "Количество клиентов"
FROM 
    store st
JOIN 
    staff s ON st.manager_staff_id = s.staff_id
JOIN 
    address a ON st.address_id = a.address_id
JOIN 
    city c ON a.city_id = c.city_id
JOIN 
    customer cu ON st.store_id = cu.store_id
GROUP BY 
    st.store_id, s.first_name, s.last_name, c.city
HAVING 
    COUNT(cu.customer_id) > 300;
```
![alt text](https://github.com/Nikich828/12_4hw/blob/master/1.jpeg)


### Задание 2. 

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

Ответ

```sql
SELECT 
    COUNT(*) AS "Количество длинных фильмов"
FROM 
    film
WHERE 
    length > (SELECT AVG(length) FROM film);
```
![alt text](https://github.com/Nikich828/12_4hw/blob/master/2.jpeg)

### Задание 3.

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

Ответ

```sql
SELECT 
    DATE_FORMAT(p.payment_date, '%Y-%m-01') AS "Месяц",
    SUM(p.amount) AS "Сумма платежей",
    COUNT(r.rental_id) AS "Количество аренд"
FROM 
    payment p
JOIN
    rental r ON p.rental_id = r.rental_id
GROUP BY 
    DATE_FORMAT(p.payment_date, '%Y-%m-01')
ORDER BY 
    SUM(p.amount) DESC
LIMIT 1;
```
![alt text](https://github.com/Nikich828/12_4hw/blob/master/3.jpeg)
