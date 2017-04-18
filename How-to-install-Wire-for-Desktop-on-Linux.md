***
Wire for Linux has comparable functionality with Wire for Windows and macOS, and calls, video calls, etc. work cross-platform. However, it is an experimental build and we expect to see some issues arise from day-to-day usage.
We don't offer official support at the moment, and any found issues can be reported by opening an issues on  https://github.com/wireapp/wire-desktop 
***

## Installation on Debian-based distributions (Debian/Ubuntu/Mint)

1. Install apt-transport-https to receive the package via HTTPS

`sudo apt-get install apt-transport-https`

2. Import our PGP signing key to be able to verify the downloaded package

`sudo apt-key adv --fetch-keys http://wire-app.wire.com/linux/releases.key`

3. Add our repository address to your sources list

`echo "deb https://wire-app.wire.com/linux/debian stable main" | sudo tee /etc/apt/sources.list.d/wire-desktop.list`

4. Update your local list of available packages

`sudo apt-get update`

5. Install wire-desktop

`sudo apt-get install wire-desktop`

## Installation with AppImage

1. Download AppImage from https://wire.com/download/

2. Make AppImage executable

`chmod +x wire*.AppImage`

3. Run AppImage