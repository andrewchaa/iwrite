# Sql queries I use

For the last 4 years, I haven't used SQL properly. Simply becasue I've used more NoSql Dbs like Dynamo DB and Cosmos DB. Today, I used a simple query. This is my sql notebook I can use for future reference, saving google time.

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

