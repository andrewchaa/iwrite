# Set Powershell Aliases for cross environment development

I use and Mac and Windows laptop for development. I often make mistakes like typing `ll` in powershell prompt instead of `dir`. It's handy to create a few aliases, so that the shell can tolerate my unconscious miakes. 

You can check where the powershell profile is by doing `$profile`. 

```bash
PS C:\> $profile
C:\Users\andrew\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
```

Open or create the profile file by doing `code $profile`. 

```bash
Set-Alias -Name ll -Value Get-ChildItem
Set-Alias -Name open -Value explorer
```

Then I can use `ll` and `open` instead of `dir` and `explorer`. 

