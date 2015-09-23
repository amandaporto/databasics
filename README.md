## Databasics

Fork this repository into your own github profile.

Before closing the homework assignment issue:

- Update this README as follows:
  - [ ] For each question (just after or below the question itself) include the SQL you wrote to generate the answer
  - [ ] For each question (just after or below the question itself) include the *answer* to the question asked.

- Also:
  - [ ] Commit the updated `store.sqlite3` database file
  - [ ] Include a link to your forked repo in the comments when closing the issue.


NOTE: To run sqlite with this database: `sqlite3 store.sqlite3`

NOTE: You may want to keep a backup of the `store.sqlite3` file in case you damage the file. *OR* you can use the command `git checkout store.sqlite3` to undo any changes to the database file since the fork or your last commit.

## Explorer Mode

- [√] How many users are there?
select * from users;
*50*

- [√] What are the 5 most expensive items?
select title, price from items order by price desc limit 5;
* Small Cotton Gloves  9984      
Small Wooden Comput  9859      
Awesome Granite Pan  9790      
Sleek Wooden Hat     9390      
Ergonomic Steel Car  9341 *

- [√] What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
select title, min(price) from items where category="Books";
*Ergonomic Granite Chair  1496*

Result does not change when searching in all categories containing Books .
select title, min(price) from items where category like "Books%";
*Ergonomic Granite Chair  1496*  

- [√] Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
SELECT first_name, last_name, street, city, state FROM users JOIN addresses ON users.id = addresses.user_id WHERE street like "6439%";
*Corrine     Little      6439 Zetta Hills  Willmouth   WY*

SELECT first_name, last_name, street, city, state FROM users JOIN addresses ON users.id = addresses.user_id WHERE first_name like "Corrine%";
*Corrine     Little      6439 Zetta Hills  Willmouth   WY        
Corrine     Little      54369 Wolff Forg  Lake Bryon  CA *

- [√] Correct Virginie Mitchell's address to "New York, NY, 10108".
UPDATE addresses SET city="New York", zip="10108" WHERE user_id=(SELECT id FROM users WHERE first_name = "Virginie");
*Virginie    Mitchell    12263 Jake Crossing  New York    10108     
Virginie    Mitchell    83221 Mafalda Canyo  New York    10108    *

- [√] How much would it cost to buy one of each tool?
select sum(price) from items where category like "Tools%";
*24605*

- [√] How many total items did we sell?
select sum(quantity) from orders;
*2125*

- [√] How much was spent on books?
SELECT category, sum(price*quantity) FROM items JOIN orders ON items.id = orders.item_id WHERE category="Books";
*420566*

- [√] Simulate buying an item by inserting a User for yourself and an Order for that User.
INSERT INTO users (first_name, last_name, email) VALUES ("Amanda", "Porto", "amandaporto@blablabla.com");
INSERT INTO orders (item_id, quantity, user_id, created_at) VALUES ("78", "2", "51", datetime());

*378         51          78          2           2015-09-23 13:05:54 *

## Adventure Mode

- [ ] What item was ordered most often? Grossed the most money?


- [ ] What user spent the most?


- [ ] What were the top 3 highest grossing categories?
