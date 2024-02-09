# «SQL. Часть 2»-Абрамов Сергей

---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

## Решение
```
select concat(sotr.first_name , ' ', sotr.last_name) as "Сотрудник",  c2.city as "Город", COUNT(c.customer_id) as "Покупатели"
from staff sotr
join store s2 on s2.store_id = sotr.store_id 
join customer c on c.store_id = s2.store_id
join address a on a.address_id = s2.address_id 
join city c2 on c2.city_id = a.city_id 
group by sotr.staff_id, c2.city_id 
having COUNT(c.customer_id) > 300;
```

![2.1](https://github.com/smabramov/SQL2/blob/604321aeff65fbbfa68477c5177521f123ca5eec/jpg/2.1.jpg)
---


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


## Решение
```
select count(film_id) as "Колличество фильмов" from film 
where length > (select AVG(length) from film);
```

![2.2](https://github.com/smabramov/SQL2/blob/604321aeff65fbbfa68477c5177521f123ca5eec/jpg/2.2.jpg)
---


### Задание 3


Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

## Решение

```
SELECT DATE_FORMAT(p.payment_date, '%M, %Y') AS Месяц, SUM(p.amount) AS Сумма_платежей, COUNT(p.rental_id) AS Колличество_аренд
FROM payment p 
GROUP BY Месяц
ORDER BY Сумма_платежей LIMIT 1;
```

![2.4]()


---