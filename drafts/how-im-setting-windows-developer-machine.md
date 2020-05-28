# How I'm setting Windows developer machine

## Installations

### Microsoft Teams for chats

Download from [https://www.microsoft.com/en-gb/microsoft-365/microsoft-teams/group-chat-software](https://www.microsoft.com/en-gb/microsoft-365/microsoft-teams/group-chat-software)

### Google Chrome

Download from [https://www.google.com/chrome/](https://www.google.com/chrome/)

Set Chrome as default browser on Settings &gt; Default apps

### Visual Studio 2019

Download from [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com/)

For Workloads, I choose the below additional options

* ASP.NET and web development
* Azure development
* .NET Core cross-platform development

I didn't choose Node.js as I will use NPM and other tools

Extensions

* Live Share
* SpecFlow for Visual Studio 2019
* Visual Studio IntelliCode
* SlowCheetah: manage App.config, App.debug.config
* ReSharper, of course

#### Resharper

Download from [https://www.jetbrains.com/resharper/](https://www.jetbrains.com/resharper/)

I use Resharer 2.x / Intelli J shortcuts

### Visual Studio Code

Download from [https://code.visualstudio.com/](https://code.visualstudio.com/)

```javascript
# settings.json

{
    "editor.fontFamily": "Fira Code",
    "editor.fontLigatures": true,
    "editor.fontSize": 13,
    "editor.insertSpaces": true
}
```

### ConEmu or Windows Terminal

For reliable terminal window: [https://conemu.github.io/](https://conemu.github.io/)

In case of Windows Terminal, you can get it from Microsoft Store: [https://github.com/Microsoft/Terminal](https://github.com/Microsoft/Terminal)

## Windows

### Mouse

I use inverted scroll direciton to match that on my macbook. I use Logitech Options: [https://www.logitech.com/en-gb/product/options](https://www.logitech.com/en-gb/product/options)

### Theme

The manufacturer's background is crude. Let's install some nice themes. Go to Settings &gt; Personalisation &gt; Themes

### Language

I'm a native Korean speaker, so install Korean language

Settings &gt; Language &gt; Preferred languages: Add a preferred language

## Code

### Chocolatey

Install choco: [https://chocolatey.org/install](https://chocolatey.org/install)

### FiraCode

Install [FiraCode](https://github.com/tonsky/FiraCode). It's free monospaced font with programming ligatures.

### Git

Install by choco

```text
choco install git.install
```

Then install Git Extensions for GUI: [http://gitextensions.github.io/](http://gitextensions.github.io/)

### Service Fabric SDK

As I develop services on Service Fabric at work, I need to install the SDK: [https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-get-started](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-get-started)



