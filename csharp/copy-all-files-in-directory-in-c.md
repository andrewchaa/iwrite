# Copy all files in directory in C\#

C\# doesn't have any command to copy all files. We have to [implement it ourselves](https://stackoverflow.com/questions/7146021/copy-all-files-in-directory) and it's not difficult.

```csharp
void Copy(string sourceDir, string targetDir)
{
    Directory.CreateDirectory(targetDir);

    foreach(var file in Directory.GetFiles(sourceDir))
        File.Copy(file, Path.Combine(targetDir, Path.GetFileName(file)));

    foreach(var directory in Directory.GetDirectories(sourceDir))
        Copy(directory, Path.Combine(targetDir, Path.GetFileName(directory)));
}
```

