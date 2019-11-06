Wire for Desktop can be started with different arguments to influence the view and behaviour of the app. Here is a list of all known parameters:

## Change wrapped WebApp

```
--env=http://localhost:8888/
```

## Enable Chrome Developer Tools on Startup

```
--devtools
```

Shortcut example on Windows:

![windows](https://cloud.githubusercontent.com/assets/469989/22371754/30759b80-e499-11e6-9e77-2f25ac71bb57.png)

Path to the app: `%APPDATA%\..\Local\wire`

## Start the app minimized

```
--startup
```

## Enable verbose logging

```
--enable-logging
```

## Start production wrapper with devtools

### macOS

```bash
open -a Wire.app --args --devtools
```

Alternative:

```bash
# Navigate to the Wire binary directory
cd "$(mdfind 'kMDItemCFBundleIdentifier="com.wearezeta.zclient.mac"')/Contents/MacOS"

# Start the Wire binary
./Wire --devtools
```

### Windows

```
cd \Users\%username%\AppData\Local\wire\
FOR /F "delims=" %%i IN ('dir /b /ad-h /t:c /od') DO SET a=%%i
cd %a%
Wire.exe --devtools
pause
```

**Disable Web Security**

```
--disable-web-security --user-data-dir="c:/chromedev"
```

**Use Proxy Server**

**Note**: If the proxy requires authentication, a window will appear asking for the credentials.

```
--proxy-server="<protocol>://<ip>:<port>"
```

Example:
```
--proxy-server="http://localhost:8080"
```

**Use Authenticated Proxy Server** (e.g. to pass the credentials automatically to the server once asked)

```
--proxy-server-auth="<protocol>://<username>:<password>@<ip>:<port>"
```

Example:
```
--proxy-server-auth="http://my-user:secretpassword@company-proxy.local:8080"
```

**Furthermore, see [Electron's supported command line switches](https://github.com/electron/electron/blob/v4.2.12/docs/api/chrome-command-line-switches.md).**