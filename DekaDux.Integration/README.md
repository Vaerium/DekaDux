# DekaDux.Integration

A distributable library providing integrations for DekaDux to third parties.\
https://github.com/Vaerium/DekaDux

## Example Implementation

```csharp
public class DekaDuxExampleImplementation
{
    public async Task ExampleMethod()
    {
        string userAgent = "vaerium"; // your server name
        string dekaDuxPath = "C:\\binary\\dekadux_install_directory"; // path to dekadux directory
        string serverDataSet = "A9_Generic_12Class"; // your server data set within dekadux
        string serverProtocolVersion = "A9"; // your server protocol version within dekadux

        DekaDuxController dekaDuxController = new DekaDuxController(userAgent, dekaDuxPath); // initialize controller with your server parameters

        string? versionString = dekaDuxController.GetInstalledVersion(); // if you want the current version from the update check

        UpdateCheckResult updateCheckResult = await dekaDuxController.CheckForUpdatesAsync(); // check for updates

        if (updateCheckResult.IsUpdateAvailable || updateCheckResult.CurrentVersion is null)
        {
            var progress = new Progress<DownloadProgressReport>(report =>
            {
                // update your UI or log progress here
                Console.WriteLine($"{report.Status}: {report.Percentage}%");
            });

            await dekaDuxController.UpdateAsync(progress); // can also call this directly, checks version itself update
        }

        dekaDuxController.Launch(serverDataSet, serverProtocolVersion); // launch dekadux with your server parameters
    }
}
```