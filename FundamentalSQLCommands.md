>1. List the commands for adding, updating, and deleting data.
  - __adding__: INSERT INTO
  - __updating__: UPDATE 
  - __deleting__: DELETE 

>2. Explain the structure for each type of command.
- __INSERT INTO__: This is followed by the table name and a schema for the insert. `VALUES` next and then the data (in correct order) for each record.
    ```
    INSERT INTO products (id, name, price)
    VALUES
    (11773, 'South Face Jacket', 174.99),
    (11774, 'Big Mountain 2-Person Tent', 219.99);
     ```
- __UPDATE__: This comand is followed by the table name and then the `SET` command. After designating the fields and value to update and a `WHERE` command to select specific record(s)

    `UPDATE products SET price=159.99 WHERE id=11773;`
- __DELETE__: This command is followed by the `FROM` command and table name. Then the `WHERE` command use used to designate which records to delete. Be careful, this is not reversible.
    `DELETE FROM products WHERE id=11776;`

>3. What are some of the data types that can be used in tables? Give a real-world example of each type.
- __integer__: Whole numbers. Could be used to store the enrollment in a class or inventory numbers for a small business.
- __decimal__: A floating point number with a precision specified by the user. Could be used to store dollar amounts or say temperature data to a needed dprecision.
- __varchar__: character data. could be used to store a person's name or maybe a job title.
-__timestamp__: Both date and time. You could record flight times for an airport.

>4. Decide how to create a new table to hold a list of people invited to a wedding dinner. The table needs to have first and last names, whether they sent in their RSVP, the number of guests they are bringing, and the number of meals (1 for adults and 1/2 for children).

- Which data type would you use to store each of the following pieces of information?
    - First and last name. - __varchar__
    - Whether they sent in their RSVP. __boolean__
    - Number of guests. __smallint__
    - Number of meals. __numeric__

- Write a command that creates the table to track the wedding dinner.
    ```
    CREATE TABLE wedding (
      id integer,
      first_name varchar(10),
      last_name varchar(20),
      rsvp boolean,
      guests smallint,
      meals numeric(3,1)
  );
  ```
- Write a command that adds a column to track whether the guest sent a thank you card.
    ```
     ALTER TABLE wedding ADD COLUMN thankyou boolean;
    ```
- You have decided to move the data about the meals to another table, so write a command to remove the column storing the number meals from the wedding table.
    ```
    ALTER TABLE wedding DROP COLUMN meals;
    ```

- The guests will need a place to sit at the reception, so write a command that adds a column for table number.
    ```
    ALTER TABLE wedding ADD COLUMN table_number smallint;
    ```
- The wedding is over and we do not need to keep this information, so write a command that deletes the table numbers from the database.
     ```
    ALTER TABLE wedding DROP COLUMN table_number;
    ```
>5. Write a command to create a new table to hold the books in a library with the columns ISBN, title, author, genre, publishing date, number of copies, and available copies.
    ```
    CREATE TABLE library (
     ISBN smallint, 
     title varchar(40), 
     author varchar(20), 
     genre varchar(20), 
     publishing_date date, 
     number_copies smallint, 
     available_copies smallint
    )
    ```

- Find three books and add their information to the table.
    ```
    INSERT INTO library (ISBN, title, author, genre, publishing_date, number_copies, available_copies)
    VALUES
    (0143039431, 'The Grapes of Wrath', 'John Steinbeck', 'Literature & Fiction', 'March 28, 2006', 12, 6),
    (1451626657, 'Catch-22: 50th Anniversary Edition ', 'Joseph Heller', 'Literature & Fiction', 'April 5, 2011', 10, 2),
    (0553106635, 'A Storm of Swords (A Song of Ice and Fire, Book 3) ', 'George R. R. Martin', 'Fantasy', 'October 31, 2000', 20, 1),

    ```
- Someone has just checked out one of the books. Change the number of available copies to 1 fewer.
    ```
    UPDATE laibrary SET available_copies = available_copies + 1 
    WHERE ISBN=0143039431;
    ```
- Now one of the books has been added to the banned books list. Remove it from the table.
    ```
    DELETE FROM library WHERE ISBN=0143039431;
    ```

> 6. Write a command to make a new table to hold spacecrafts. Information should include id, name, year launched, country of origin, a brief description of the mission, orbiting body, if it is currently operating, and its approximate miles from Earth. In addition to the table creation, provide commands that perform the following operations:
- Add three non-Earth-orbiting satellites to the table.
- Remove one of the satellites from the table since it has just crashed into the planet.
- Edit another satellite because it is no longer operating and change the value to reflect that.
    ```
    CREATE TABLE spacecraft (
     id smallint,
     name varchar(30),
     launch_year smallint,
     country character(3),
     mission_description text,
     orbiting_body varchar(20),
     in_operation boolean
    );

    INSERT INTO spacecraft (id, name, launch_year, country, mission_description, orbiting_body, in_operation)
    VALUES
    (1, 'Mangalyaan', 2013, 'IND', 
    'The mission is a "technology demonstrator" project to develop the technologies for designing, planning, management, and operations of an interplanetary mission.', 'Mars', true),
    (2, 'Luna 22', 1974, 'RUS', 
    'Luna 22 was a lunar orbiter mission. The spacecraft carried imaging cameras and also had the objectives of studying the Moon's magnetic field, surface gamma ray emissions and composition of lunar surface rocks, and the gravitational field, as well as micrometeorites and cosmic rays.', 'Moon', false),
    (3, 'Deep Impact', 2005, 'USA', 
    'It was designed to study the interior composition of the comet Tempel 1 (9P/Tempel), by releasing an impactor into the comet.', 'Sun', false);
        
    DELETE FROM spacecraft WHERE ID=2;

    UPDATE spacecraft SET in_operation = flase
    WHERE id=1;   
    ```


> 7. Write a command to create a new table to hold the emails in your inbox. This table should include an id, the subject line, the sender, any additional recipients, the body of the email, the timestamp, whether or not you have read the email, and the id of the email chain it's in. Also provide commands that perform the following operations:

- Add three new emails to the inbox.
- You deleted one of the emails, so write a command to remove the row from the inbox table.
- You started reading an email but just heard a crash in another room. Mark the email as unread before investigating the crash, so you can come back and read it later.
```
CREATE TABLE emails (
     id integer,
     subject varchar(256),
     sender varchar(100),
     other_recipients varchar(100)[],
     read boolean,
     chain_id smallint,
     time temestamp,
     body text
    );

INSERT INTO emails (id, subject, sender, other_recipients, read, chain_id, time, body)
    VALUES
    (1, 'saying hello', 'bob@bob.com', null, false, 123, '1999-01-08 04:05:06',  'Hello mary! From Bob.'),
    (2, 'What time', 'jeff@jeff.com', ['wert23@gmail.com'], false, 888, '2015-01-18 01:05:06',  'what time should we meet?'),
    (3, 'I quit', 'coolguy@business.com', [lex@business.com, boss@business.com], true, 666, '2018-10-21 01:15:16',  'take this job and shove it!');


    UPDATE emails SET read = false
        WHERE id=3;   
```