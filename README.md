# PrintDemon
This is an bind shell PoC using [PrintDemon](https://github.com/ionescu007/PrintDemon). This script is using the latest bypass for CVE-2020-1337, which is [CVE-2020-17001](https://bugs.chromium.org/p/project-zero/issues/detail?id=2075) for privilege escalation. The vulnerability allows an unprivileged user to gain system-level privileges and is based on @ionescu007 PoC.

__Note__: This is a proof of concept. We have encountered some issues with printing to C:\Windows\System32\Ualapi.dll on some machines. We have not yet isolated what is causing this.

## Code Borrowed from
https://github.com/ionescu007/PrintDemon
https://github.com/BC-SECURITY/Invoke-PrintDemon
https://bugs.chromium.org/p/project-zero/issues/detail?id=2075
https://stackoverflow.com/questions/4442122/send-raw-zpl-to-zebra-printer-via-usb
https://stackoverflow.com/questions/29759854/how-to-connect-to-tcp-socket-with-powershell-to-send-and-receive-data
