## Week-4/Day-2
-------------------------------------------------------------
## Explorer Mode

1. How many users are there?
 - `SQL:` SELECT count (*) from users

 - `ANSWER:`
+---------+
|   count |
|---------|
|      50 |
+---------+

-------------------------------------------------------------

2. What are the titles of the 5 most expensive items?
- `SQL:` SELECT title,price from items ORDER BY price DESC LIMIT 5


- `ANSWER:`
+-----------------------+---------+
| title                 |   price |
|-----------------------+---------|
| Small Cotton Gloves   |    9984 |
| Small Wooden Computer |    9859 |
| Awesome Granite Pants |    9790 |
| Sleek Wooden Hat      |    9390 |
| Ergonomic Steel Car   |    9341 |
+-----------------------+---------+

-------------------------------------------------------------

3. What is the cheapest item in the Books category?
- `SQL:` SELECT * from items where category='Books' ORDER BY price ASC LIMIT 1


- `ANSWER:`
+------+-------------------------+------------+-------------------------------------+---------+
|   id | title                   | category   | description                         |   price |
|------+-------------------------+------------+-------------------------------------+---------|
|   76 | Ergonomic Granite Chair | Books      | De-engineered bi-directional portal |    1496 |
+------+-------------------------+------------+-------------------------------------+---------+
-------------------------------------------------------------

4. Who lives at 6439 Zetta Hills, Willmouth, WY?
- `SQL:` SELECT * from addresses where street='6439 Zetta Hills' AND city = 'Willmouth' AND state = 'WY'


- `ANSWER:`
+------+-----------+------------------+-----------+---------+-------+
|   id |   user_id | street           | city      | state   |   zip |
|------+-----------+------------------+-----------+---------+-------|
|   43 |        40 | 6439 Zetta Hills | Willmouth | WY      | 15029 |
+------+-----------+------------------+-----------+---------+-------+

-------------------------------------------------------------

5. Correct Virginie Mitchell's address to "New York, NY, 10108".
- `SQL:` SELECT id FROM users where first_name = 'Virginie' AND last_name = 'Mitchell'
- `SQL:` UPDATE addresses SET city = 'New York' , state = 'NY' , zip = '10108' WHERE user_id = 39


- `ANSWER:`



(Super Answer: `SQL:` UPDATE addresses SET city = 'New York' , state = 'NY' , zip = '10108' WHERE user_id = (SELECT id FROM users where first_name = 'Virginie' AND last_name = 'Mitchell')
-------------------------------------------------------------

6. How much would it cost to buy one of each item in the Tools category?
- `SQL:` SELECT SUM(price) FROM items WHERE category = 'Tools'


- `ANSWER:`
+-------+
|   sum |
|-------|
|  7383 |
+-------+

-------------------------------------------------------------

7. How many total items did we sell?
- `SQL:` SELECT SUM(quantity) from orders


- `ANSWER:`
+-------+
|   sum |
|-------|
|  2126 |
+-------+

-------------------------------------------------------------

8. How much was spent on Books?
- `SQL:` SELECT sum(quantity * items.price) as total FROM orders, items WHERE items.id = orders.item_id AND items.category = 'Books'


- `ANSWER:`
+---------+
|   total |
|---------|
|  420566 |
+---------+

-------------------------------------------------------------

9. Simulate buying an item by inserting a User for yourself and an Order for yourself.

- `SQL:` INSERT INTO users VALUES(51,'Hamilton', 'Clark', 'dhclark2@ncsu.edu')
- `SQL:` INSERT INTO addresses VALUES(55,51,'221 46th Avenue S.', 'St. Petersburg', 'FL', 33705)
- `SQL:` INSERT INTO orders VALUES(378,51,27,1,'2016-02-09 00:40:31.307668')

- `ANSWER:`


-------------------------------------------------------------
## Adventure Mode


1. What item was ordered the most?
- `SQL:` SELECT item_id, COUNT(*) as count FROM orders GROUP BY item_id ORDER BY count DESC

... take highest counted (three have 9 counts)

- `SQL:` SELECT * from items WHERE id = 65 OR id = 10 OR id = 46


- `ANSWER:`
+------+---------------------------+--------------------------+--------------------------------------+---------+
|   id | title                     | category                 | description                          |   price |
|------+---------------------------+--------------------------+--------------------------------------+---------|
|   10 | Ergonomic Concrete Gloves | Baby & Electronics       | Diverse client-driven hardware       |    6114 |
|   46 | Practical Rubber Computer | Jewelery & Health        | Synchronised foreground service-desk |    7534 |
|   65 | Incredible Granite Car    | Music, Sports & Clothing | Virtual bi-directional alliance      |    7295 |
+------+---------------------------+--------------------------+--------------------------------------+---------+

-------------------------------------------------------------

2. What user spent the most?
- `SQL:`


- `ANSWER:`


-------------------------------------------------------------

3. What were the top 3 highest grossing categories?
- `SQL:`


- `ANSWER:`


-------------------------------------------------------------

4. Who made the most expensive single order?
- `SQL:` SELECT orders.user_id, users.first_name, users.last_name, orders.item_id, items.category, orders.quantity, items.price, (items.price * orders.quantity) as sale from users,orders,items WHERE orders.item_id = items.id AND orders.user_id = users.id ORDER BY sale DESC LIMIT 1


- `ANSWER:`
+-----------+--------------+-------------+-----------+------------+------------+---------+--------+
|   user_id | first_name   | last_name   |   item_id | category   |   quantity |   price |   sale |
|-----------+--------------+-------------+-----------+------------+------------+---------+--------|
|         2 | Missouri     | Carroll     |       100 | Toys       |         10 |    9790 |  97900 |
+-----------+--------------+-------------+-----------+------------+------------+---------+--------+


