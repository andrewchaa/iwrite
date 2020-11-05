# Building a simple CLI

CLI, command-line interface, provides a very handy command interface that serves your face. If restful APIs are for machine, CLI is for human, especially developers.

### Install package

commandlineparser: [https://github.com/commandlineparser/commandline](https://github.com/commandlineparser/commandline)

```text
CommandLineParser
```

### Quick start example

```csharp
using System;
using CommandLine;

namespace QuickStart
{
    class Program
    {
        public class Options
        {
            [Option('c', "cmd", Required = false, HelpText = "Your choice of command")]
            public string Command { get; set; }
        }

        static async Task Main(string[] args)
        {
            await Parser.Default.ParseArguments<Options>(args)
                .WithParsedAsync<Options>(async o =>
            {
                if (string.IsNullOrEmpty(o.Command))
                {
                    Console.WriteLine("Examples: \n");
                    Console.WriteLine("dotnet run --cmd add-domains");
                    Console.WriteLine("");
                }
            });
        }
    }
}
```

### show examples

```bash
dotnet run

Examples:

dotnet run --cmd download
dotnet run --cmd detect-events
dotnet run --cmd document-event
dotnet run --cmd publish-to-wiki
dotnet run --cmd demo
```



