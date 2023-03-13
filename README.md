# 12.3. «SQL. Часть 1» - НиконоровДА FOPS-6

## Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```SQL
SELECT DISTINCT district FROM address WHERE district like 'K%a' and district not like '% %';
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/1.png)

## Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```SQL
SELECT payment_id, payment_date, amount FROM payment WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18' AND amount > 10.00 ORDER BY payment_date DESC;
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/2.png)


Доработка:

```SQL
SELECT payment_id, payment_date, amount FROM payment WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59' AND amount > 10.00 ORDER BY payment_date DESC;
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/2.1.png)

## Задание 3

Получите последние пять аренд фильмов.

```SQL
SELECT rental_id, payment_id, payment_date, amount FROM payment ORDER BY payment_date DESC LIMIT 5;
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/3.png)

## Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.

```SQL
SELECT LOWER(first_name), REPLACE(first_name, 'LL','pp') FROM customer WHERE first_name = 'Kelly' OR first_name = 'Willie';
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/4.png)

## Задание 5

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

```SQL
SELECT SUBSTRING_INDEX(email,'@',1) AS email_name, SUBSTRING_INDEX(email,'@',-1) AS domain_name FROM customer;
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/5.png)

## Задание 6

```SQL
SELECT SUBSTRING_INDEX(email  , '@', 1) as up_email_name,  CONCAT(LEFT(UPPER(SUBSTRING_INDEX(email  , '@', 1)), 1), LOWER(SUBSTR((SUBSTRING_INDEX(email , '@',1)),2))) as email_name ,   SUBSTRING_INDEX(email  , '@', -1) as dw_domain_name , CONCAT(LEFT(UPPER(SUBSTRING_INDEX(email  , '@', -1)), 1), LOWER(SUBSTR((SUBSTRING_INDX(email , '@',-1)),2))) as domain_name FROM customer;
```

![alt text](https://github.com/mxssclxck/hw-12.03/blob/main/img/6.png)

