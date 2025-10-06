# Домашнее задание к занятию "`SQL. Часть 2`" - `Кудряшов Андрей`



---

### Задание 1

```
sudo mysql -u root
USE sakila;
```

```
SELECT 
CONCAT(staff.first_name, ' ', staff.last_name) AS manager,
city.city AS city_name,
COUNT(customer.customer_id) AS total_customers
FROM store
JOIN staff ON store.manager_staff_id = staff.staff_id
JOIN address ON store.address_id = address.address_id
JOIN city ON address.city_id = city.city_id
JOIN customer ON store.store_id = customer.store_id
-- JOIN customer ON customer.store_id = store.store_id  -- закомментил, потому что уже есть
GROUP BY store.store_id, staff.first_name, staff.last_name, city.city
HAVING COUNT(customer.customer_id) > 300;
```

<img width="643" height="337" alt="1" src="https://github.com/user-attachments/assets/cd5722d5-4c21-4a63-a988-ec4d569ac648" />


---

### Задание 2

```
SELECT COUNT(film_id) 
FROM film 
WHERE length > (SELECT AVG(length) FROM film);
```

<img width="558" height="199" alt="2" src="https://github.com/user-attachments/assets/7063daea-0431-44fa-abcb-8c31acd248c5" />

---

### Задание 3

```
SELECT 
DATE_FORMAT(payment.payment_date, '%Y-%m') as pay_month,
SUM(payment.amount) as total,
COUNT(rental.rental_id) as rent_count
FROM payment
JOIN rental ON payment.rental_id = rental.rental_id
GROUP BY pay_month
ORDER BY total DESC
LIMIT 1;
```

<img width="531" height="306" alt="3" src="https://github.com/user-attachments/assets/281de18c-a2ec-40c9-a830-dd6cd05111c7" />


---


### Задание 4

```
SELECT 
CONCAT(staff.first_name, ' ', staff.last_name) as staff_full,
COUNT(payment.payment_id) as num_sales,
IF(COUNT(payment.payment_id) > 8000, 'Да', 'Нет') as Преммя
FROM staff
JOIN payment ON staff.staff_id = payment.staff_id
GROUP BY staff.staff_id, staff.first_name, staff.last_name;
```

<img width="604" height="292" alt="4" src="https://github.com/user-attachments/assets/3215cc58-498e-46f4-93b4-5d68810e3a4e" />


---


### Задание 5

```
SELECT film.film_id, film.title
FROM film
LEFT JOIN inventory ON film.film_id = inventory.film_id
LEFT JOIN rental ON inventory.inventory_id = rental.inventory_id
WHERE rental.rental_id IS NULL;
```

<img width="717" height="952" alt="5" src="https://github.com/user-attachments/assets/85b798a9-ad35-42cb-aca4-3a291f85a182" />

---
