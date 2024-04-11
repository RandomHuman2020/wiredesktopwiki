***
Wire for Linux has comparable functionality with Wire for Windows and macOS, and calls, video calls, etc. work cross-platform. However, it is an experimental build and we expect to see some issues in day-to-day usage.
We don't offer official support at the moment, but any issues can be reported via  https://github.com/wireapp/wire-desktop. 
***

## Table of Contents

* [Installation on Debian-based distributions](#installation-on-debian-based-distributions)
* [Update Wire on Debian-based distributions](#update-wire-on-debian-based-distributions)
* [Installation with AppImage](#installation-with-appimage)

### Installation on Debian-based distributions

This will work for Debian, Ubuntu and other Ubuntu-based distributions, like Xubuntu, Kubuntu or Mint.

1. Install apt-transport-https to receive the package via HTTPS

        sudo apt-get install apt-transport-https

2. Import our PGP signing key to be able to verify the downloaded package

        wget -q https://wire-app.wire.com/linux/releases.key -O- | sudo apt-key add -

3. Add our repository address to your sources list

        echo "deb [arch=amd64] https://wire-app.wire.com/linux/debian stable main" \
          | sudo tee /etc/apt/sources.list.d/wire-desktop.list

4. Update your local list of available packages

        sudo apt-get update

5. Install wire-desktop

        sudo apt-get install wire-desktop


### Update Wire on Debian-based distributions

1. Run the commands:

        sudo apt-get update
        sudo apt-get upgrade


### Installation with AppImage

1. [Go to our releases page](https://github.com/wireapp/wire-desktop/releases)

2. Scroll to the latest Linux release.

3. Download the assets and verify the signed hashes:

    ```
    wget https://github.com/wireapp/wire-desktop/releases/download/linux%2F3.35.3348/sha256sum.txt.asc
    gpg --verify sha256sum.txt.asc
    wget https://github.com/wireapp/wire-desktop/releases/download/linux%2F3.35.3348/Wire-3.35.3348_x86_64.AppImage
    sha256sum Wire-3.35.3348_x86_64.AppImage ; grep Wire-3.35.3348_x86_64.AppImage sha256sum.txt.asc 
    ```

5. Make AppImage executable

        chmod +x Wire*.AppImage

6. Run AppImage