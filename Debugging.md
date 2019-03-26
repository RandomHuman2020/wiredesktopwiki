## Custom Protocol Links

You can invoke custom protocol links from the terminal:

```sh
open -a WireInternal wire://conversation/62684726-295f-41c8-bc42-a93144158502
```

## Log files

Internal versions of our desktop app generate log files. You can find them here:

- macOS: `open "~/Library/Application Support/WireInternal/logs"`

There will be logs from Electron's main process in the `electron.log` (`electron.old`). Files from webview renderer processes are logged into separate directories which have the name of their webview account ID.