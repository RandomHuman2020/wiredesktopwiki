## Wrapper Logfiles
- Windows: Logfiles are located in: `%APPDATA%\Wire`

## Chrome Cache

Wire for Web saves app cache on Windows in `%APPDATA%\Wire\Cache`. It can be viewed with a tool like [ChromeCacheView](http://www.nirsoft.net/utils/chrome_cache_view.html).

## Windows Error logs

When the whole app crashed, it obviously can not write errors into log files, but Windows itself is tracking the crash. On Windows 7 you see a dialog, but on Windows 8.1 and 10 you need to check the computer management console for the error. Do the following steps:

1. Try "compmgmt.msc" in the search box of Windows task bar to open the Computer Management
2. Go to **System Tools | Event Viewer | Windows Logs**
3. Open **Application** item (it will take some time because it is collecting the logs)
4. You can search for "Errors" or you can clean the log and make the app crash again