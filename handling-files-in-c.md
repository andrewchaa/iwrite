# Handling files in c\#

So often I have to read and write files, yet I forget how to do it. This is for me to remember.

### search subdirectories  recursively

You can use `Directory.GetFiles` that searches subdirectories for  you.\([https://stackoverflow.com/questions/9830069/searching-for-file-in-directories-recursively/9830116](https://stackoverflow.com/questions/9830069/searching-for-file-in-directories-recursively/9830116)\)

```csharp
string[] files = Directory.GetFiles(sDir, 
  "*.xml", 
  SearchOption.AllDirectories);
```

### get full path from relative path

```csharp
Path.GetFullPath(".\\EventsData\\Events.dll")
```

