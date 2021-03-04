# Powershell tips

### list environment variables

```text
gci env:* | sort-object name
```

#### update powershell \(in admin shell\)

```text
iex "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"
```

