# Sql queries I use

For the last 4 years, I haven't used SQL properly. Simply becasue I've used more NoSql Dbs like Dynamo DB and Cosmos DB. Today, I used a simple query. This is my sql notebook I can use for future reference, saving google time.

#### Handling duplicates

```sql
SELECT DISTINCT Domain FROM Services
```

The above distinct is case-sensitive, especially in sqlite. for case-insensitive, use GROUP BY.

```sql
SELECT Domain Services GROUP BY LOWER(Domain)
```

#### Case-insensitive string comparison

Use `COLLATE NOCASE`

```sql
SELECT DISTINCT Repository 
  FROM ServiceDefinitions 
WHERE Team = @Team COLLATE NOCASE
```

