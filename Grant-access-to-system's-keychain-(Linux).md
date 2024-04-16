# How to solve "Wire could not access your system safe storage" on Linux

With the introduction of Electron's [safeStorage](https://www.electronjs.org/docs/latest/api/safe-storage), the Wire app now requires access to your system's keychain.

This should happen transparently, but we identified an issue with the community maintained [Snap package](https://snapcraft.io/wire), and with users that do not use a full desktop environment (usually users who prefer a tiling window manager).

## If you are using the Snap package:
- There is currently no workaround as we do not maintain that package, we have identified a potential fix and contacted the maintainer, you can follow the progress [here](https://github.com/wireapp/wire-desktop/issues/7764), we recommend using the app in a browser in the mean time.

## If you are not using a full desktop environment:
- Install one of the supported keychain on your system
- Start the Wire app with a flag to grant Electron access to the library

### Install a supported keychain
Electron supports either the Gnome or KDE keychain to store information, you would need to install either a version of `gnome-libsecret` or `kwallet` on your system, the process differs depending on distribution, we will provide examples for Debian/libsecret and Arch/kwallet5

- getting libsecret on a Debian based distribution:
```
sudo apt install libsecret-tools
```
- getting kwallet5 on an Arch based distribution:
```
sudo pacman -S kwallet5
```

### Launch Wire with the `--password-store` flag:
If chromium does not find a supported desktop environment, you will need to start the app with the relevant flag, list [here](https://www.electronjs.org/docs/latest/api/safe-storage#safestoragegetselectedstoragebackend-linux)
- Launching the app on Debian/libsecret:
```
wire-desktop --password-store="gnome-libsecret"
```
- Launching the app on Arch/kwallet5:
```
wire-desktop --password-store="kwallet5"
```