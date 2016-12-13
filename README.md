# Intermediate SQL Queries

Use [Chinook](http://jxs.me/chinook-web/) to complete today's mini-project. You will use the schema provided.

## Setup

### Create Table with Foreign Key

Create a new table called **Movie** with a **MovieId**, **Title** and **MediaTypeId**:

```
CREATE TABLE Movie (
  MovieId INTEGER PRIMARY KEY,
  Title TEXT,
  MediaTypeId INTEGER, 
  FOREIGN KEY(MediaTypeId) REFERENCES MediaType(MediaTypeId)
);
```

Test the table by adding a **Movie** with a **Title** and a **MediaTypeId**.

```
INSERT INTO Movie (Title, MediaTypeId) VALUES ("Aladdin", 3);
```

Now query the table with a `SELECT` statement and you should see your movie.

### Add Foreign Key to Table

Add a foreign key to an existing table. Add **GenreId** to **Movie**:

```
ALTER TABLE Movie ADD COLUMN GenreId INTEGER REFERENCES Genre(GenreId);
```

Query your movie table and see that the same row is now returned with an extra column.

### Update Rows

Don't leave **GenreId** null so add a value using an `UPDATE` statement. Use the `WHERE` clause to avoid overwriting all of the records:

```
UPDATE Movie SET GenreId = 22 WHERE id = 1;
```

## Begin Challenges

### Write a Join

Join the **Artist** and **Album** tables, listing the artist name next to each album name.

### Use Group By

How many albums does each artist have? Use a `GROUP BY` to aggregate the number of albums per artist:

### Having

How about limiting the list to artists with more than one album?

### Subquery

Can you produce the same list using a subquery?
