## Find and Review Nextcloud Logs
[![How To: Find and Review Nextcloud Logs](./_files/_previews/view-logs.gif)](./_files/videos/view-logs.webm)

Nextcloud logs are helpful to get percise information about what happened when an error occured.
The logs can be viewed from the admin area.
Go to "Settings" > "Logging" to view the logs.

You can use the log level filter to exclude irrelevant events from the list and find the relevant events faster.
Errors created logged by the passwords app can usually be identified by checking the app column.
But there are some cases where the app could be listed as "index", "no app in context" or "PHP" instead.

If you have found the correct log entry, click on the "copy" icon and select "copy raw" to copy the log entry.


## Find the system information
#### Nextcloud Version
The Nextcloud version can be found in the "Overview" section in the admin area.
Go to "Settings" > "Overview" and thake a look at the section "Version".

#### Environment
If the "Monitoring" app has not been disabled, it will help to gather system information quickly.
Go to "Settings" > "System" in the admin area to check the PHP and database information.


## Check the browser log
In most browsers you can open the developer tools with "F12".
In Opera you need to click "Ctrl+Shift+C" to do so.

Make sure that you are in the "Console" tab.
Most of the information there is not necessary, so it might be good to filter the log.
In any Chromium based browser (Chrome, Edge, Vivaldi, Opera) click on "Default levels" and uncheck "Info".
In any Firefox based browser uncheck "Log", "Information" and "Debug" in the top right corner.

Now there should only be warnings and errors.