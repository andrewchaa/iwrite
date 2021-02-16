# Auto-increment counter in dynamodb

It's possible even though DynamoDb is a document-based database. You can use `atomic counter`. `atomic counter` is [a numeric attribute that is incremented, unconditionally](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.AtomicCounters), without interfering with other write requests. In my usecase, I was going to use it as view count for a given post. So, undercounting or overcounting doesn't really matter. 

```bash
# cli example
aws dynamodb update-item \
    --table-name ProductCatalog \
    --key '{"Id": { "N": "601" }}' \
    --update-expression "SET Price = Price + :incr" \
    --expression-attribute-values '{":incr":{"N":"5"}}' \
    --return-values UPDATED_NEW
 
```

It's a shame that Cosmos DB doesn't support this yet. I use Auzre at work and AWS for my personal projects. Naturally I tend to compare the app services they provide. 

The below is my C\# code snippet that uses `atomic counter`. 

```csharp
public async Task<(int, Exception)> Save(PostId id)
{
    Console.WriteLine($"Increasing a view count for a post: {id.Value}");

    var getResponse = await _dynamoDbClient.GetItemAsync(
        Tables.ViewCounts,
        new Dictionary<string, AttributeValue> {{Keys.Id, id.Value.ToAttributeValue()}}
    );
    var countExists = getResponse.Item.ContainsKey(Keys.Id);
    
    var key = new Dictionary<string, AttributeValue> {{Columns.Id, id.Value.ToAttributeValue()}};
    var attributeUpdates = new Dictionary<string, AttributeValueUpdate>
    {
        {
            Columns.Count, 
            1.ToAttributeValueUpdate(countExists ? AttributeAction.ADD : AttributeAction.PUT)
        },
    };

    var response = await _dynamoDbClient.UpdateItemAsync(Tables.ViewCounts, key, attributeUpdates);
    
    Console.Write(response.ToJson());

    return (0, null);
}

```

One extra thing I had to do was to pass AttributeAction conditionally. If the count of a post doesn't exist, `AttributeAction.ADD` doesn't work, as there's no number to increase. In that case, I had to pas `AttributeAction.PUT`. 



