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

        echo "deb https://wire-app.wire.com/linux/debian stable main" | sudo tee /etc/apt/sources.list.d/wire-desktop.list

4. Update your local list of available packages

        sudo apt-get update

5. Install wire-desktop

        sudo apt-get install wire-desktop

### Update Wire on Debian-based distributions

1. Run the commands:

        sudo apt-get update
        sudo apt-get upgrade

### Installation with AppImage

1. Download AppImage from https://wire.com/download/

2. Make AppImage executable

        chmod +x wire*.AppImage

3. Run AppImage