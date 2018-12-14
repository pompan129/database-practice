>Write out a generic SELECT statement.
```
SELECT <column1, column2, ...>
FROM <table1, table2 ...>
<optional: WHERE <condition>>
```
>Create a fun way to remember the order of operations in a SELECT statement, such as a mnemonic.

    (Select, From, Where): Sing For Waffles!

> Given this dogs table, write queries to select the following pieces of data:
- Display the name, gender, and age of all dogs that are part Labrador.
    ```
    SELECT name, gender, age FROM dogs
    WHERE breed LIKE '%labrador%';
    ```
- Display the ids of all dogs that are under 1 year old.
    ```
    SELECT id FROM dogs
    WHERE age<1;
    ```
- Display the name and age of all dogs that are female and over 35lbs.
    ```
    SELECT name,age FROM dogs 
    WHERE gener = 'F' AND weight > 35;
    ```
- Display all of the information about all dogs that are not Shepherd mixes.
    ```
    SELECT * FROM dogs
    WHERE breed NOT LIKE '%shepherd%';
    ```
- Display the id, age, weight, and breed of all dogs that are either over 60lbs or Great Danes.
    ```
    SELECT id,age,weight,breed FROM dogs
    WHERE weight > 60 OR breed LIKE '%great dane%'
    ```


>Given this cats table, what records are returned from these queries?

- SELECT name, adoption_date FROM cats;

name | adoption_date
---- | ------------
Mushi | 2016-03-22T00:00:00.000Z
Seashell | null
Azul | 2016-04-17T00:00:00.000Z
Victoire | 2016-09-01T00:00:00.000Z
Nala | null


- SELECT name, age FROM cats;

name | age
---- | ---
Mushi | 1
Seashell | 7
Azul | 3
Victoire | 7

>From the cats table, write queries to select the following pieces of data.

- Display all the information about all of the available cats.
    ```
    SELECT * FROM cats;
    ```
- Display the name and sex of all cats who are 7 years old.
    ```
    SELECT name,gender FROM cats
    WHERE age = 7;
    ```
- Find all of the names of the cats, so you don’t choose duplicate names for new cats.
    ```
    SELECT name from cats;
    ```

List each comparison operator and explain when you would use it. Include a real world example for each.

- \> Greater than, used when comparing 2 values. Select all the students  over age 16.
- < Less than, used when comparing 2 values. Select all the people younger than 21.
- = Equal to, used when comparing 2 values. Select the albums where the band is equal to 'The Kinks'.
- <= Less than or equal to, used when comparing 2 values. Select the menu items that cost $5.00 or less.
- \>= Greater than or equal to, used when comparing 2 values. Select the students with a GPA of 3.5 or highr.
- <> Greater than or less than, used when comparing 2 values.  Select people who's age is not equal to mine.
- != Not equal to, used when comparing 2 values. Select all the cows who are not 'sold'.

>From the cats table, what data is returned from these queries?
- SELECT name FROM cats WHERE gender = ‘F’;

name | 
---- | 
Seashell | 
Nala | 

- SELECT name FROM cats WHERE age <> 3;

name | 
---- | 
Mushi | 
Seashell | 
Victoire | 
Nala | 


- SELECT ID FROM cats WHERE name != ‘Mushi’ AND gender = ‘M’;

id |
-- |
3 |
4 |