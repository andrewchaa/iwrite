# List active \(pending\) Pull Requests on Microsoft Teams chat room

As a pricipal engineer, I move to a new team routinely. In the new team I recently joined, I noticed that Pull Requests stayed pending longer than we liked. There's a out-of-the-box app that shows Pull Requests from Azure Devops but it keeps sending the same PR when anyone push a new commit. So, I wanted to create a simple custom app that lists down all Pull Requets from the team and shows them in our shared chatroom once a day.

## My Acceptance Criteria

* List down all Pull Requests
* Send the message once a day, at 9 AM
* Send the message only from Monday to Friday, not in the weekend
* The message has the list of all pending Pull Requests and associated link to the page where you can review the PR
* Each team can have their own customised list of Pull Requests

## Azure Function

My chosen app service was Azure Function. I used webjobs before but it seemed not relevant any more in .NET Core era. Azure Function supports [CRON](https://en.wikipedia.org/wiki/Cron) expression, so it's easy to execute the function daily. I'm not very familiar with CRON expression, so used this [cheatsheet](https://arminreiter.com/2017/02/azure-functions-time-trigger-cron-cheat-sheet/). 

```csharp
[FunctionName("RetrievePullRequests")]
public static async Task Run([TimerTrigger("0 0 9 * * MON,TUE,WED,THU,FRI")]TimerInfo myTimer, ILogger log)
{
    log.LogInformation($"Monring News function executed at: {DateTime.Now}");

```



