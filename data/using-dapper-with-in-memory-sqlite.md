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



