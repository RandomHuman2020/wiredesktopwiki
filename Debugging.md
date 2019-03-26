## Developer Console

Our desktop app can be started with a JavaScript developer console from the renderer process. This also works for production applications:

```sh
open -a Wire --args --devtools
```

By default it will show you a console which is assigned to the sidebar of our app (where you can switch your accounts). You will have to inspect the `Webview` DOM element which is of interest for you first and then you need to call `$0.openDevTools()` to get the right one. If you want the webapp (which is rendered inside the webview) to output log statements in production, then you have to start the desktop application with the following parameters:

```sh
open -a Wire --args --devtools --enable-logging
```

## Custom Protocol Links

You can invoke custom protocol links from the terminal:

```sh
open -a WireInternal wire://conversation/62684726-295f-41c8-bc42-a93144158502
```

## Log files

Internal versions of our desktop app generate log files. You can find them here:

- macOS: `open "~/Library/Application Support/WireInternal/logs"`

There will be logs from Electron's main process in the `electron.log` (`electron.old`). Files from webview renderer processes are logged into separate directories which have the name of their webview account ID.