Wire's wrapper can be started with different arguments to influence the view & behaviour of the wrapper. Here is a list of all known parameters:

**Change wrapped webapp**

```
--env=http://localhost:8888/
```

**Enable Chrome Developer Tools on Startup**

```
--devtools
```

**Start the app minimized**

```
--startup
```

**Start production wrapper with devtools**

```bash
# Navigate to the Electron binary directory
cd /Applications/(Wire.app | Wire.localized/Wire.app)/Contents/MacOS

# Start the Electron binary
./Electron --devtools
```

Alternative:

```bash
open /Applications/(Wire.app | Wire.localized/Wire.app) --args --devtools
```