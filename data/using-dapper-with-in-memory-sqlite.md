# Using dapper with in-memory sqlite

[Dapper](https://github.com/StackExchange/Dapper) makes it really easy to store and to query data from relational database.

By setting Mode to memory, you can create an in-memory sqlite database. `Mode=Memory;Cache=Shared` will make the database shared across connections.

```csharp
var masterSqliteConnection = new SqliteConnection("Data Source=Scriveners;Mode=Memory;Cache=Shared");
            _masterSqliteConnection.Open();
var createCommand = connection.CreateCommand();
createCommand.CommandText =
    @"
    CREATE TABLE ServiceDefinitions (
        Name Text NOT NULL PRIMARY KEY,
        Release Text,
        Build Text,
        Team Text,
        Repository Text,
        Tier Text,
        Domain Text,
        SubDomain Text
    )";

createCommand.ExecuteNonQuery();
```

Btw, Sqlite query is case-sensitive by default. To do case-insensitive comparison, use `COLLATE NOCASE` 

```csharp
public async Task<HiveTeam> GetTeam(string name)
{
    await using var connection = new SqliteConnection(ScrivenerDatabase.ConnectionString);
    return await connection.QueryFirstOrDefaultAsync<HiveTeam>(
        $"SELECT * FROM {Tables.Teams} WHERE Name = @name COLLATE NOCASE",
        new {name});
}

```

