
> 1. How do you find related data held in two separate data tables?

By using a JOIN statement.

> 2. Explain, in your own words, the difference between an INNER JOIN, LEFT OUTER JOIN, and RIGHT OUTER JOIN. Give a real-world example for each.

- __INNER JOIN__: combines information from different tables based on a shared key. The resulting display will only have as many rows as those that have this shared key in both tables. An example might be a join between a table of cars and a table of owners. All cars with owners would be listed. But cars without owners and owners who no longer had cars would not.

- __LEFT OUTER JOIN__: This join combines information from deifferent tables but also lists the records in the 1st table that have no shared key values with the second table. In the above example above cars with owners would be listed and cars without owners would also be listed with a null value in the owner id cell. Owners without cars would not be listed.

- __RIGHT OUTER JOIN__: this is the opposite of the __LEFT OUTER JOIN__. So, in the above example, you would see a list of cars with owners and also the owners without cars lsited. There would be a null value in the car id field for these records. The cars without owners would not be listed.

> 3. Define primary key and foreign key. Give a real-world example for each.

- __Primary Key__: To be able to identify one record uniquely, we need to have an attribute(column), that is guaranteed to be unique for each and every entry (row) in the database. This is called as primary key. An example might be a persons Social Security number in a database.

- __Foriegn Key__: It is a column in one table, that is linked to the primary key of another table. At our company you might have a list of jobs. Each job might be assign to a particular employee who is identified by their SS#. We could designate who was assigned the job in the jobs table by referencing the unique `Primary Key` in the employee table. 


> 4. Define aliasing.

    The use of short variable names, often one letter, in place of the table name in a query.

> 5. Change this query so that you are using aliasing:
```
SELECT professor.name, compensation.salary, compensation.vacation_days FROM professor 
JOIN compensation 
ON professor.id = compensation.professor_id;
```
```
SELECT p.name, c.salary, c.vacation_days FROM professor AS p
JOIN compensation AS c
ON p.id =c.professor_id;

```
> 6. Why would you use a NATURAL JOIN? Give a real-world example.

You would save some typing and possibly using a `NATURAL JOIN`. An example might be if you had a database of employees with address information and wanted to cross reference that with health insurance information to see how many of your employees ahd been using the health care over the last year. If the tables shared fields like SS#, address, first Name, Last name, etc.. you could do a search to form a list consisting of only the column names that appear in both input tables. These columns would appear only once in the output table.

> 7. Using this Employee schema and data, write queries to find the following information:
- List all employees and all shifts.

This is interesting. The `shifts` table and `employees` table do not have shared keys. So, I assume, your looking for two seperate queries?
```
SELECT * FROM  employees;
SELECT * FROM shifts;
```
If, on the other hand, this question mean that I was supposed to get all of the `scheduled_shifts` with `employee` and `shift` information on both, it would look like this.
```
SELECT * FROM  scheduled_shifts
JOIN employees ON employees.id = scheduled_shifts.employee_id
JOIN shifts ON shifts.id = scheduled_shifts.shift_id;
```

> 8. Using this Adoption schema and data, please write queries to retrieve the following information and include the results:

- Create a list of all volunteers. If the volunteer is fostering a dog, include each dog as well.
```
SELECT v.id, v.first_name,v.last_name,v.address, v.phone_number,v.available_to_foster, d.id AS dog_id, d.name AS dog_name,d.breed AS dog_breed
FROM volunteers as v
LEFT OUTER JOIN dogs AS d
ON v.foster_dog_id = d.id

```
- The cat's name, adopter's name, and adopted date for each cat adopted within the past month to be displayed as part of the "Happy Tail" social media promotion which posts recent successful adoptions.
```
SELECT cats.name AS cat_name, adopters.first_name, adopters.last_name, cat_adoptions.date 
FROM cat_adoptions
JOIN adopters ON cat_adoptions.adopter_id = adopters.id
JOIN cats ON cat_adoptions.cat_id = cats.id
WHERE cat_adoptions.date >= (CURRENT_DATE - INTERVAL '30 DAYS');

```
- Create a list of adopters who have not yet chosen a dog to adopt.
```
SELECT adopters.first_name, adopters.last_name, adopters.phone_number
FROM adopters
LEFT OUTER JOIN dog_adoptions
ON adopters.id = dog_adoptions.adopter_id
WHERE dog_adoptions.adopter_id IS NULL;

```
- Lists of all cats and all dogs who have not been adopted.
```
SELECT 'dog' AS type, d.id, d.name, d.gender,d.intake_date
FROM dogs AS d
LEFT JOIN dog_adoptions 
ON d.id = dog_adoptions.dog_id
WHERE dog_adoptions.dog_id IS NULL
UNION ALL
SELECT 'cat', c.id, c.name, c.gender,c.intake_date
FROM cats AS c
LEFT JOIN cat_adoptions
ON c.id = cat_adoptions.cat_id
WHERE cat_adoptions.cat_id IS NULL;
```
- The name of the person who adopted Rosco.
```
SELECT a.first_name, a.last_name
FROM dog_adoptions
JOIN adopters AS a
ON dog_adoptions.adopter_id = a.id
JOIN dogs
ON dog_adoptions.dog_id = dogs.id
WHERE dogs.name = 'Rosco';
```

> 9. Using this Library schema and data, write queries applying the following scenarios and include the results:

- To determine if the library should buy more copies of a given book, please provide the names and position, in order, of all of the patrons with a hold (request for a book with all copies checked out) on "Advanced Potion-Making".
```
    SELECT p.name, h.rank
    FROM holds AS h
    JOIN patrons AS p
    ON h.patron_id = p.id
    JOIN books
    ON h.isbn = books.isbn
    WHERE books.title = 'Advanced Potion-Making'
    ORDER BY h.rank;
```

| name           | rank |
| -------------- | ---- |
| Terry Boot     | 1    |
| Cedric Diggory | 2    |


- List all of the library patrons. If they have one or more books checked out, list the books with the patrons.
```
    SELECT p.id, p.name, b.title, b.isbn
    from patrons AS p
    LEFT JOIN transactions
    ON p.id = transactions.patron_id
    LEFT JOIN books as b
    ON transactions.isbn = b.isbn
    ORDER BY p.name;
```
| id  | name             | title                                   | isbn       |
| --- | ---------------- | --------------------------------------- | ---------- |
| 5   | Cedric Diggory   | Fantastic Beasts and Where to Find Them | 3458400871 |
| 4   | Cho Chang        | Advanced Potion-Making                  | 9136884926 |
| 1   | Hermione Granger | Fantastic Beasts and Where to Find Them | 3458400871 |
| 1   | Hermione Granger | Hogwarts: A History                     | 1840918626 |
| 3   | Padma Patil      | Fantastic Beasts and Where to Find Them | 3458400871 |
| 2   | Terry Boot       | Advanced Potion-Making                  | 9136884926 |
| 2   | Terry Boot       | Fantastic Beasts and Where to Find Them | 3458400871 |
