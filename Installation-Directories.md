## Chrome directory

### Windows

- Production:
  ```
  %APPDATA%\Wire
  ```
- Internal:
  ```
  %APPDATA%\WireInternal
  ```

### macOS

- Production:
  ```
  ~/Library/Containers/com.wearezeta.zclient.mac/Data/Library/Application Support/Wire/
  ```
- Internal:
  ```
  ~/Library/Application Support/WireInternal/
  ```

## EXE files

- Production:
  ```
  %LOCALAPPDATA%\wire\app-<version>\Wire.exe
  ```
- Internal:
  ```
  %LOCALAPPDATA%\wireinternal\app-<version>\Wire.exe
  ```

## Logfiles

### Windows

- Production:
  ```
  %APPDATA%\Wire\logs\
  ```
- Internal:
  ```
  %APPDATA%\WireInternal\logs\
  ```

### Windows Error logs
When the whole app crashed, it obviously can not write errors into log files, but Windows itself is tracking the crash. On Windows 7 you see a dialog, but on Windows 8.1 and 10 you need to check the computer management console for the error. Do the following steps:

1. Try "compmgmt.msc" in the search box of Windows task bar to open the Computer Management
2. Go to **System Tools > Event Viewer > Windows Logs**
3. Open **Application** item (it will take some time because it is collecting the logs)
4. You can search for "Errors" or you can clean the log and make the app crash again

### macOS

- Production:
  ```
  ~/Library/Containers/com.wearezeta.zclient.mac/Data/Library/Application Support/Wire/logs/
  ```
- Internal:
  ```
  ~/Library/Application Support/WireInternal/logs/
  ```

### Linux

- Production:
  ```
  ~/.config/Wire/logs/
  ```
- Internal:
  ```
  ~/.config/WireInternal/logs/
  ```

## App Settings

Settings for the size of the Wire app window and its position on the screen are stored in:

### Windows

- Production:
  ```
  %APPDATA%\Wire\config\
  ```
- Internal:
  ```
  %APPDATA%\WireInternal\config\
  ```

### macOS

- Production:
  ```
  ~/Library/Containers/com.wearezeta.zclient.mac/Data/Library/Application Support/Wire/config/
  ```
- Internal:
  ```
  ~/Library/Application Support/WireInternal/config/
  ```

### Linux

- Production:
  ```
  ~/.config/Wire/config/
  ```
- Internal:
  ```
  ~/.config/WireInternal/config/
  ```

## Chrome Cache
Wire for Web saves app cache on Windows in `%APPDATA%\Wire\Cache`. It can be viewed with a tool like [ChromeCacheView](http://www.nirsoft.net/utils/chrome_cache_view.html).