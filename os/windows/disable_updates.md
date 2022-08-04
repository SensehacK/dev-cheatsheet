# Disable Windows 10 Updates


## Disable notification



```text

To disable the "Updates are available" popup in Windows 10, do the following.

    Open an elevated command prompt.
    Ensure that the console is opened in the folder C:\Windows\System32. If not, then type the following command to change the directory:

    cd /d "%Windir%\System32"

    Type or copy-paste the following command:

    takeown /f musnotification.exe

    This command will take NTFS ownership of the executable file that produces the popup.
    The next command will prevent the operating system from accessing the file.

    icacls musnotification.exe /deny Everyone:(X)

    Now, repeat the same for the MusNotificationUx file.

    takeown /f musnotificationux.exe
    icacls musnotificationux.exe /deny Everyone:(X)

This should be enough to stop Windows 10 from showing these annoying notifications.

To undo the changes you made, run the following commands one by one.

cd /d "%Windir%\System32"
icacls musnotification.exe /remove:d Everyone
icacls musnotification.exe /grant Everyone:F
icacls musnotification.exe /setowner "NT SERVICE\TrustedInstaller"
icacls musnotification.exe /remove:g Everyone
icacls musnotificationux.exe /remove:d Everyone
icacls musnotificationux.exe /grant Everyone:F
icacls musnotificationux.exe /setowner "NT SERVICE\TrustedInstaller"
icacls musnotificationux.exe /remove:g Everyone

That's it. Credits go to jingyu9575 of superuser.
```


https://winaero.com/disable-updates-available-windows-10/