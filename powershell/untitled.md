# Powershell tips

### list environment variables

```csharp
// list all environment variables
gci env:* | sort-object name

// set environment variable
$env:CYPRESS_INSTALL_BINARY="C:\Users\andrew.chaa\Downloads\cypress.zip"

// update powershell. run this in priviledged powershell
iex "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"
```



