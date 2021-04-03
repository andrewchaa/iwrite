# Uploading a file to S3 using PreSignedUrl with HttpClient

S3 PreSignedUrl expects PUT request with file stream. I had a little trouble to find an example. This is a note for myself for future reference.

```csharp
private static async Task UploadToS3(string filename, string preSignedUrl)
{
    await using var fileStream = File.OpenRead(filename);
    var fileStreamResponse = await new HttpClient().PutAsync(
        new Uri(preSignedUrl),
        new StreamContent(fileStream));
    fileStreamResponse.EnsureSuccessStatusCode();
}

```



