## TL;DR

- `signtool sign /t http://timestamp.digicert.com /a "WireSetup.exe"`

## Requirements
- Extended Validation (EV) Code Signing Certificate
- SafeNet Authentication Client
- SignTool.exe from Visual Studio

## SignTool

SignTool is available as part of the Windows SDK (which comes with [Visual Studio Community 2015](https://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?PId=1927)). Make sure to select the "[ClickOnce Publishing Tools](http://www.benedykt.net/content/repository/2015/08/ClickOnce-Publishing-Tools.png)" from the feature list during the installation of Visual Studio 2015 to get the SignTool.

![](http://i.stack.imgur.com/fEZEX.png)

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

