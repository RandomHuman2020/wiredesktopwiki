## Signing on Windows

- `signtool sign /t http://timestamp.digicert.com /a "WireSetup.exe"`

## Requirements
- Extended Validation (EV) Code Signing Certificate
- SafeNet Authentication Client
- SignTool.exe from Visual Studio

## SignTool

SignTool is available as part of the Windows SDK (which comes with [Visual Studio Community 2015](https://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?PId=1927)). Make sure to select the "[ClickOnce Publishing Tools](http://www.benedykt.net/content/repository/2015/08/ClickOnce-Publishing-Tools.png)" from the feature list during the installation of Visual Studio 2015 to get the SignTool.

![Visual Studio](http://i.stack.imgur.com/fEZEX.png)

Once Visual Studio is installed you can run the `signtool` command from the [Visual Studio Command Prompt](https://msdn.microsoft.com/en-us/library/ms229859(v=vs.110).aspx). 

By default (on Windows 10) the SignTool will be installed at `C:\Program Files (x86)\Windows Kits\10\bin\x86\signtool.exe`.

## Code Signing
1. Install [SafeNet hardware token drivers](https://www.digicert.com/custsupport/fetch-safenet-driver.php?order_id=00770529)
1. Insert digicert USB hardware token into USB port
1. Execute `signtool sign /t http://timestamp.digicert.com /a "WireSetup.exe"` from the [Visual Studio Command Prompt](https://msdn.microsoft.com/en-us/library/ms229859(v=vs.110).aspx)
1. Enter Code Signing Token when requested (can be received from Wolfram or the webapp Team)
1. Open SafeNet Authentication Client, change to Advanced View, click on Client Settings, select Advanced register and check **Enable single logon** so you don't have to enter it again every time

## Further Reading
- [Signing Windows Programs with SignTool | digicert](https://www.digicert.com/code-signing/signcode-signtool-command-line.htm)
- [Sign Setup Files with SignTool.exe (Windows Installer) | Microsoft](https://msdn.microsoft.com/en-us/library/vstudio/ee290833(v=vs.100).aspx)
- [Sign your installer or else bad things will happen | grunt-electron-installer](https://github.com/atom/grunt-electron-installer#sign-your-installer-or-else-bad-things-will-happen)

## Creating a notarized Electron build

### Libraries

1. [electron-packager](https://github.com/electron/electron-packager)

Config:

```ts
{
    appBundleId: macOSConfig.bundleId,
    appCategoryType: 'public.app-category.social-networking',
    appCopyright: commonConfig.copyright,
    appVersion: commonConfig.version,
    asar: commonConfig.enableAsar,
    buildVersion: commonConfig.buildNumber,
    darwinDarkModeSupport: true,
    dir: '.',
    extendInfo: plistEntries,
    helperBundleId: `${macOSConfig.bundleId}.helper`,
    icon: 'resources/macos/logo.icns',
    ignore: /electron\/renderer\/src/,
    name: commonConfig.name,
    osxNotarize: {
      appleId: macOSConfig.notarizeAppleId!,
      appleIdPassword: macOSConfig.notarizeApplePassword!,
      ascProvider: macOSConfig.ascProvider!,
    },
    osxSign: {
      entitlements: 'resources/macos/entitlements/parent-notarization.plist',
      'entitlements-inherit': 'resources/macos/entitlements/parent-notarization.plist',
      hardenedRuntime: true,
      identity: macOSConfig.certNameNotarization,
      type: 'distribution',
    },
    out: commonConfig.buildDir,
    overwrite: true,
    platform: 'darwin',
    protocols: [{name: `${commonConfig.name} Core Protocol`, schemes: [commonConfig.customProtocolName]}],
    prune: true,
    quiet: false,
  };
```

**Problem: app is correctly notarized, but doesn't start.**

2. [electron-builder](https://github.com/electron-userland/electron-builder)

Config:

```ts
{
    afterSign: async (context: electronBuilder.AfterPackContext) => {
      if (context.targets[0].name === 'dmg' && macOSConfig.enableNotarization) {
        // manually notarize the .app file
        const appName = context.packager.appInfo.productFilename;
        const appFile = path.join(context.appOutDir, `${appName}.app`);
        await manualNotarize(appFile, macOSConfig);
      }
    },
    appId: macOSConfig.bundleId,
    artifactName: '${productName}.${ext}',
    buildVersion: commonConfig.version,
    copyright: commonConfig.copyright,
    directories: {
      output: commonConfig.distDir,
    },
    dmg: {
      icon: path.resolve('resources/macos/logo.icns'),
      title: commonConfig.name,
    },
    extraMetadata: {
      homepage: commonConfig.websiteUrl,
    },
    mac: {
      asar: commonConfig.enableAsar,
      category: 'public.app-category.social-networking',
      darkModeSupport: true,
      entitlements: path.resolve('resources/macos/entitlements/parent-notarization.plist'),
      entitlementsInherit: path.resolve('resources/macos/entitlements/parent-notarization.plist'),
      extendInfo: plistEntries,
      forceCodeSigning: true,
      gatekeeperAssess: false,
      hardenedRuntime: true,
      icon: path.resolve('resources/macos/logo.icns'),
      identity: macOSConfig.certNameNotarization,
      strictVerify: 'all',
      target: 'dmg',
    },
    productName: commonConfig.name,
    protocols: [{name: `${commonConfig.name} Core Protocol`, schemes: [commonConfig.customProtocolName]}],
    publish: null,
    removePackageScripts: true,
    ...(macOSConfig.electronMirror && {
      electronDownload: {
        mirror: macOSConfig.electronMirror,
      },
    }),
  };
```

**Problem: app is correctly notarized, but doesn't start.**

### Entitlements

Tried both libraries with the following entitlements:

1.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
    <true/>
  </dict>
</plist>
```

2.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
    <true/>
    <key>com.apple.security.network.client</key>
    <true/>
    <key>com.apple.security.device.camera</key>
    <true/>
    <key>com.apple.security.device.microphone</key>
    <true/>
    <key>com.apple.security.network.server</key>
    <true/>
    <key>com.apple.security.cs.allow-dyld-environment-variables</key>
    <true/>
    <key>com.apple.security.cs.allow-jit</key>
    <true/>
    <key>com.apple.security.cs.disable-library-validation</key>
    <true/>
    <key>com.apple.security.files.user-selected.read-write</key>
    <true/>
  </dict>
</plist>
```

3. (default entitlements)


Both libraries are using `electron-notarize` and this is probably the same bug:
https://github.com/electron/electron-notarize/issues/26