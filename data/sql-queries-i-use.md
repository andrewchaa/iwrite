# Sql queries I use for SQLite

For the last 4 years, I haven't used SQL properly. Simply becasue I've used more NoSql Dbs like Dynamo DB and Cosmos DB. Today, I used a simple query. This is my sql notebook I can use for future reference, saving google time.

#### Case insensitivity in SQLite

This was an issue when I did lots of string comparision. There are two ways. First, you can use `COLLATE NOCASE` in the where clause, each time. The other option is you create the column to be case-insensitive. The second option is much faster in performance

```sql
SELECT DISTINCT Repository 
  FROM ServiceDefinitions 
WHERE Team = @Team COLLATE NOCASE
```

```sql
CREATE TABLE "DomainEvents" (
	"Name"	Text NOT NULL COLLATE NOCASE,
	"Obsolete"	INTEGER,
	"Description"	Text,
	"Domain"	BLOB,
	"SubDomain"	Text,
	"Team"	Text,
	"TeamLead"	Text,
	"SubscriberCount"	INTEGER,
	PRIMARY KEY("Name")
);
```

#### Case-insensitive string comparison with Sqlite

Use `COLLATE NOCASE`

```sql
SELECT DISTINCT Repository 
  FROM ServiceDefinitions 
WHERE Team = @Team COLLATE NOCASE
```

#### Create a table

```sql
CREATE TABLE IF NOT EXISTS ServiceDefinitions (
    Name Text NOT NULL PRIMARY KEY,
    Team Text,
    Repository Text,
    Tier Text,
    Domain Text,
    SubDomain Text
)

```

#### Handling duplicates

```sql
SELECT DISTINCT Domain FROM Services
```

The above distinct is case-sensitive, especially in sqlite. for case-insensitive, use GROUP BY.

```sql
SELECT Domain Services GROUP BY LOWER(Domain)
```

#### Wild-card match

```sql
LIKE '%.rtf'
```

