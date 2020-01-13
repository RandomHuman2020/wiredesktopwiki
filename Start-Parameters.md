## Table of Contents  
* [Known parameters](#known-parameters)
  * [Start the App Minimized](#start-the-app-minimized)
  * [Use Proxy Server](#use-proxy-server)
  * [Use Authenticated Proxy Server](#use-authenticated-proxy-server)
  * [Enable Verbose Logging](#enable-verbose-logging)
  * [Enable Chrome Developer Tools](#enable-chrome-developer-tools)
  * [Disable Web Security](#disable-web-security)
  * [Change Wrapped WebApp](#change-wrapped-webapp)
* [How to Use Start Parameters](#how-to-use-start-parameters)
  * [Windows](#windows)
  * [macOS](#macos)
  * [Linux](#linux)

---

## Known parameters

Wire for Desktop can be started with different arguments to influence the view and behaviour of the app. Here is a list of all known parameters:

#### Start the App Minimized

```
--startup
```

#### Use Proxy Server

**Note**: If the proxy requires authentication, a window will appear asking for the credentials.

```
--proxy-server="<protocol>://<ip>:<port>"
```

Example:
```
--proxy-server="http://localhost:8080"
```

#### Use Authenticated Proxy Server

**Note**: This passes the credentials automatically to the server when asked.

```
--proxy-server-auth="<protocol>://<username>:<password>@<ip>:<port>"
```

Example:
```
--proxy-server-auth="http://my-user:secretpassword@company-proxy.local:8080"
```

#### Enable Verbose Logging

```
--enable-logging
```

#### Enable Chrome Developer Tools

```
--devtools
```

#### Disable Web Security

**Note**: This needs the additional `--user-data-dir` parameter.

```
--disable-web-security
```

Example for Windows:
```
--disable-web-security --user-data-dir="%TEMP%\chromedev"
```

Example for macOS / Linux:
```
--disable-web-security --user-data-dir="/tmp/chromedev"
```

#### Change Wrapped WebApp

```
--env=http://localhost:8888/
```

**Furthermore, see [Electron's supported command line switches](https://github.com/electron/electron/blob/v6.1.7/docs/api/chrome-command-line-switches.md).**

## How to Use Start Parameters

### Windows

#### Option 1: Create a shortcut

The easiest option on Windows is to edit the desktop shortcut.

1. Right-click on the desktop shortcut
2. Select "properties"
3. In the input field for "Target", add a space and one of the parameters
4. Click "OK"
5. Double-click the desktop shortcut

In the following example, `--devtools` was added to the input field:

![shortcut](https://cloud.githubusercontent.com/assets/469989/22371754/30759b80-e499-11e6-9e77-2f25ac71bb57.png)

#### Option 2: Start via command line

1. Click on start
2. Select "Run"
3. Enter "cmd"
4. Click "OK"
3. In the command line, enter `%LOCALAPPDATA%\wire\Wire.exe` following a space and one of the parameters
4. Press enter

In the following example, `--devtools` was entered in the command line:

![cmd](https://user-images.githubusercontent.com/5497598/68288185-39957280-0084-11ea-85d4-53fb92955a62.png)

### macOS

1. Open the Terminal app
2. Enter `open -a Wire.app --args` following a space and one of the parameters
3. Press enter

Alternative:

1. Open the Terminal app
2. Enter the following:
  ```bash
  # Navigate to the Wire binary directory
  cd "$(mdfind 'kMDItemCFBundleIdentifier="com.wearezeta.zclient.mac"')/Contents/MacOS"

  # Start the Wire binary
  ./Wire --devtools
  ```

### Linux

1. Open a terminal
2. Enter `/opt/Wire/wire-desktop` following a space and one of the parameters
3. Press enter