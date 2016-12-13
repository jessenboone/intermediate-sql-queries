# intermediate-sql-queries

Use [Chinook](http://jxs.me/chinook-web/) to complete today's mini-project. You will use the schema provided.

## Setup

### Add foreign key to new table

Create a new table called Movie with a MovieId, Title and MediaTypeId:

```
CREATE TABLE Movie (
  MovieId INTEGER PRIMARY KEY,
  Title TEXT,
  MediaTypeId INTEGER, 
  FOREIGN KEY(MediaTypeId) REFERENCES MediaType(MediaTypeId)
);
```

Test the table by adding a Movie with a Title and a MediaTypeId.

```
insert into Movie (Title, MediaTypeId) values ("Aladdin", 3);
```

Now query the table with a `select` statement and you should see your movie.

## Add foreign key to existing table

We can also add a foreign key to an existing table. Let's add one to our movies table that references genre on genreId

```
ALTER TABLE movies ADD COLUMN genreId INTEGER REFERENCES Genre(GenreId);
```

Query your movies table and you will see that the same row is now returned with an extra column.

## Update Rows

We don't want to leave genre null so let's add a value using the update command.  With an update command you always want to use a where clause (if you don't you will overwrite data on all records).

```
update movies set genreId=22 where id=1
```

## Use a join

Now that we know how to make foreign keys and change data let's do some practice queries.  The simplest way to use a foreign key is via a join statement. 

Join the artist and album tables so we can list the artist name next to each album name.

## Use a nested query/sub-select

The next way to use a primary key is with a nested query/sub-select statement.  By using parenthesis we can do a select inside of a select.  This is really effective when you have a foreign key link between two tables because now we can filter our main query by criteria on a referenced table.

We just got all data from Track where the track was pointing to a record in the genre table that happend to be either Jazz or Blues.

The subquery `(select GenreId from Genre where Name='Jazz' OR Name='Blues')` returns an array of GenreId.

Our parent query then checks for Tracks where the Track Genre is in that array `where GenreId in `


## Group by

How many albums does each artist have?  We could count manually, but no!  Let's use a group by to do some aggregate counts for us.

Select all artist ids, artist names, and a count of how many albums they have.

```
select ar.artistId, ar.name, count(*) from artist ar join album a on ar.ArtistId=a.ArtistId group by ar.artistId
```

#### Challenge
Order this by album count, largest first

## Use Distinct

We have hundreds of customers and want to know which countries our customers come from, but no duplicates!

```
select distinct country from customer
```

## Delete Rows

Always do a select before a delete to make sure you get back exactly what you want and only what you want to delete!

```
select * from customer where fax is not null
```

Then replace the `select *` with a `delete` and you're safely deleting rows.

```
delete from customer where fax is not null
```
