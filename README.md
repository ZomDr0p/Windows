# Windows
Commands to use in the reconnaissance phase

### System information

**hostname**: Displays the hostname part of the full computer
```
C:\Users\arbel>hostname
DESKTOP-IN9L9R6
```

**systeminfo**: Shows detailed configuration information about a computer and its operating system, including operating system configuration, security information, product identifier and hardware properties such as ram, disk space and network cards.

```
C:\Users\arbel>systeminfo

Host Name:                 DESKTOP-IN9L9R6
OS Name:                   Microsoft Windows 10 Home
OS Version:                10.0.18363 N/A Build 18363
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
Registered Owner:          arbel
Registered Organization:
Product ID:                00326-10000-00000-AA208
Original Install Date:     17/09/2021, 11:55:49
System Boot Time:          17/09/2021, 11:57:15
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 23 Model 113 Stepping 0 AuthenticAMD ~3800 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 27/02/2020
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-gb;English (United Kingdom)
Input Locale:              es;Spanish (Traditional Sort)
Time Zone:                 (UTC+01:00) Brussels, Copenhagen, Madrid, Paris
Total Physical Memory:     8,191 MB
Available Physical Memory: 4,147 MB
Virtual Memory: Max Size:  10,111 MB
Virtual Memory: Available: 5,582 MB
Virtual Memory: In Use:    4,529 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    WORKGROUP
Logon Server:              \\DESKTOP-IN9L9R6
Hotfix(s):                 7 Hotfix(s) Installed.
                           [01]: KB4532938
                           [02]: KB4601556
                           [03]: KB4513661
                           [04]: KB4516115
                           [05]: KB4517245
                           [06]: KB4528759
                           [07]: KB4528760
Network Card(s):           2 NIC(s) Installed.
                           [01]: Intel(R) 82574L Gigabit Network Connection
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    Yes
                                 DHCP Server:     192.168.52.254
                                 IP address(es)
                                 [01]: 192.168.52.160
                                 [02]: fe80::ec93:9b64:3fd7:a2c0
                           [02]: Bluetooth Device (Personal Area Network)
                                 Connection Name: Bluetooth Network Connection
                                 Status:          Media disconnected
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```


### Users and groups information

**net user**: Adds or modifies user accounts, or displays user account information.
```
C:\Users\arbel>net user

User accounts for \\DESKTOP-IN9L9R6

-------------------------------------------------------------------------------
Administrator            arbel                    DefaultAccount
Guest                    WDAGUtilityAccount
```

**net users "UserName"**: Show information related to the user consulted such as account password configuration, 
```
C:\Users\arbel>net user arbel
User name                    arbel
Full Name
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set             17/ 09/ 2021 11:58:38
Password expires             Never
Password changeable           17/ 09/ 2021 11:58:38
Password required            No
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                    17/ 09/ 2021 11:59:09

Logon hours allowed          All

Local Group Memberships      *Administrators
Global Group memberships     *None
```

**net localgroup**: Adds, displays, or modifies local groups. Used without parameters, net localgroup displays the name of the server and the names of local groups on the computer.
```
C:\Users\arbel>net localgroup

Aliases for \\DESKTOP-IN9L9R6

-------------------------------------------------------------------------------
*Administrators
*Device Owners
*Distributed COM Users
*Event Log Readers
*Guests
*Hyper-V Administrators
*IIS_IUSRS
*Performance Log Users
*Performance Monitor Users
*Remote Management Users
*System Managed Accounts Group
*Users
```

**net localgroup "GroupName"**: Shows the users of the consulted group
```
C:\Users\arbel>net localgroup Administrators
Alias name     Administrators
Comment        Administrators have complete and unrestricted access to the computer/domain

Members

-------------------------------------------------------------------------------
Administrator
arbel
```

**net /domain**: Performs the operation on the domain controller in the computer's primary domain. Check users and groups information in the domain.
```
net user Administrator /domain
net group Administrators /domain
```

Create and add a user to Administrator groups
```
C:\Windows\system32> net user user1 /add
The command completed successfully.

C:\Windows\system32>net user user1 P4ssw0rd.
The command completed successfully.

C:\Windows\system32>net localgroup administrators user1 /add
The command completed successfully.

C:\Windows\system32>net user user1
User name                    user1
Full Name
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set             30/ 09/ 2021 19:17:13
Password expires              11/ 11/ 2021 19:17:13
Password changeable           30/ 09/ 2021 19:17:13
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   Never

Logon hours allowed          All

Local Group Memberships      *Administrators       *Users
Global Group memberships     *None
The command completed successfully.
```

### Process and Services
**tasklist**: Displays a list of currently running processes
**tasklist /svc**: Lists all the service information for each process without truncation
```
C:\Windows\system32>TASKLIST /svc /fi "USERNAME eq desktop-in9l9r6\user" /fi "STATUS eq running"

Image Name                     PID Services
========================= ======== ============================================
sihost.exe                   10672 N/A
svchost.exe                   8312 WpnUserService_4435b76
taskhostw.exe                11184 N/A
explorer.exe                 11188 N/A
svchost.exe                   8500 cbdhsvc_4435b76
StartMenuExperienceHost.e    10960 N/A
GameBar.exe                   2660 N/A
GameBarFTServer.exe          10028 N/A
RuntimeBroker.exe             5444 N/A
SearchUI.exe                  7456 N/A
RuntimeBroker.exe             5136 N/A
ShellExperienceHost.exe       9544 N/A
ApplicationFrameHost.exe      8344 N/A
MicrosoftEdge.exe             4964 N/A
browser_broker.exe            5504 N/A
RuntimeBroker.exe            12264 N/A
MicrosoftEdgeCP.exe          11864 N/A
MicrosoftEdgeSH.exe           3680 N/A
ctfmon.exe                    3932 N/A
cmd.exe                       1556 N/A
conhost.exe                   8588 N/A
SecurityHealthSystray.exe     4660 N/A
vmtoolsd.exe                  5692 N/A
OneDrive.exe                  5144 N/A
WindowsInternal.Composabl     5720 N/A
Microsoft.Photos.exe           764 N/A
RuntimeBroker.exe             6740 N/A
dllhost.exe                   3108 N/A
SystemSettings.exe           10600 N/A
dllhost.exe                   9180 N/A
dllhost.exe                   3744 N/A
MusNotifyIcon.exe             6412 N/A
```

### Network information

**ipconfig**: Displays all current TCP/IP network configuration values and refreshes Dynamic Host Configuration Protocol (DHCP) and Domain Name System (DNS) settings
```
C:\Windows\system32>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : DESKTOP-IN9L9R6
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : localdomain

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : localdomain
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-0C-29-C1-4D-38
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::ec93:9b64:3fd7:a2c0%8(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.52.160(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : 30 September 2021 19:40:12
   Lease Expires . . . . . . . . . . : 30 September 2021 20:10:12
   Default Gateway . . . . . . . . . : 192.168.52.2
   DHCP Server . . . . . . . . . . . : 192.168.52.254
   DHCPv6 IAID . . . . . . . . . . . : 100666409
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-28-D6-1E-3A-00-0C-29-C1-4D-38
   DNS Servers . . . . . . . . . . . : 192.168.52.2
   Primary WINS Server . . . . . . . : 192.168.52.2
   NetBIOS over Tcpip. . . . . . . . : Enabled

Ethernet adapter Bluetooth Network Connection:

   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Bluetooth Device (Personal Area Network)
   Physical Address. . . . . . . . . : DC-FB-48-2A-C1-7C
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
```

**route**: Display the entire contents of the IP routing table
```
C:\Windows\system32>route print
===========================================================================
Interface List
  8...00 0c 29 c1 4d 38 ......Intel(R) 82574L Gigabit Network Connection
 12...dc fb 48 2a c1 7c ......Bluetooth Device (Personal Area Network)
  1...........................Software Loopback Interface 1
===========================================================================

IPv4 Route Table
===========================================================================
Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0     192.168.52.2   192.168.52.160     25
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
     192.168.52.0    255.255.255.0         On-link    192.168.52.160    281
   192.168.52.160  255.255.255.255         On-link    192.168.52.160    281
   192.168.52.255  255.255.255.255         On-link    192.168.52.160    281
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
        224.0.0.0        240.0.0.0         On-link    192.168.52.160    281
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  255.255.255.255  255.255.255.255         On-link    192.168.52.160    281
===========================================================================
Persistent Routes:
  None

IPv6 Route Table
===========================================================================
Active Routes:
 If Metric Network Destination      Gateway
  1    331 ::1/128                  On-link
  8    281 fe80::/64                On-link
  8    281 fe80::ec93:9b64:3fd7:a2c0/128
                                    On-link
  1    331 ff00::/8                 On-link
  8    281 ff00::/8                 On-link
===========================================================================
Persistent Routes:
  None
```

**arp**: Displays current arp cache tables for all interfaces. The ARP cache contains one or more tables that are used to store IP addresses and their resolved Ethernet or Token Ring physical addresses.
```
C:\Windows\system32>arp -A

Interface: 192.168.52.160 --- 0x8
  Internet Address      Physical Address      Type
  192.168.52.2          00-50-56-f2-77-c1     dynamic
  192.168.52.255        ff-ff-ff-ff-ff-ff     static
  224.0.0.22            01-00-5e-00-00-16     static
  224.0.0.251           01-00-5e-00-00-fb     static
  224.0.0.252           01-00-5e-00-00-fc     static
  239.255.255.250       01-00-5e-7f-ff-fa     static
  255.255.255.255       ff-ff-ff-ff-ff-ff     static
```

### Network connections

**netstat -ano**: Displays all active TCP connections and the TCP and UDP ports on which the computer is listening and includes the process ID (PID) for each connection. Addresses and port numbers are expressed numerically and no attempt is made to determine names.
```
C:\Windows\system32>netstat -ano

Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       964
  TCP    0.0.0.0:445            0.0.0.0:0              LISTENING       4
  TCP    0.0.0.0:5040           0.0.0.0:0              LISTENING       4128
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING       11316
  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING       696
  TCP    0.0.0.0:49665          0.0.0.0:0              LISTENING       524
  TCP    0.0.0.0:49666          0.0.0.0:0              LISTENING       1468
  TCP    0.0.0.0:49667          0.0.0.0:0              LISTENING       1444
  TCP    0.0.0.0:49668          0.0.0.0:0              LISTENING       2780
  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       668
  TCP    192.168.52.160:139     0.0.0.0:0              LISTENING       4
  TCP    [::]:135               [::]:0                 LISTENING       964
  TCP    [::]:445               [::]:0                 LISTENING       4
  TCP    [::]:7680              [::]:0                 LISTENING       11316
  TCP    [::]:49664             [::]:0                 LISTENING       696
  TCP    [::]:49665             [::]:0                 LISTENING       524
  TCP    [::]:49666             [::]:0                 LISTENING       1468
  TCP    [::]:49667             [::]:0                 LISTENING       1444
  TCP    [::]:49668             [::]:0                 LISTENING       2780
  TCP    [::]:49669             [::]:0                 LISTENING       668
  UDP    0.0.0.0:123            *:*                                    1716
  UDP    0.0.0.0:5050           *:*                                    4128
  UDP    0.0.0.0:5353           *:*                                    1912
  UDP    0.0.0.0:5355           *:*                                    1912
  UDP    127.0.0.1:1900         *:*                                    6380
  UDP    127.0.0.1:50226        *:*                                    3256
  UDP    127.0.0.1:52218        *:*                                    6380
  UDP    192.168.52.160:137     *:*                                    4
  UDP    192.168.52.160:138     *:*                                    4
  UDP    192.168.52.160:1900    *:*                                    6380
  UDP    192.168.52.160:52217   *:*                                    6380
  UDP    [::]:123               *:*                                    1716
  UDP    [::]:5353              *:*                                    1912
  UDP    [::]:5355              *:*                                    1912
  UDP    [::1]:1900             *:*                                    6380
  UDP    [::1]:52216            *:*                                    6380
```

### User Privileges

**whoami /priv**: Displays the security privileges of the current user.
```
C:\Windows\system32>whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                            Description                                                        State
========================================= ================================================================== ========
SeIncreaseQuotaPrivilege                  Adjust memory quotas for a process                                 Disabled
SeSecurityPrivilege                       Manage auditing and security log                                   Disabled
SeTakeOwnershipPrivilege                  Take ownership of files or other objects                           Disabled
SeLoadDriverPrivilege                     Load and unload device drivers                                     Disabled
SeSystemProfilePrivilege                  Profile system performance                                         Disabled
SeSystemtimePrivilege                     Change the system time                                             Disabled
SeProfileSingleProcessPrivilege           Profile single process                                             Disabled
SeIncreaseBasePriorityPrivilege           Increase scheduling priority                                       Disabled
SeCreatePagefilePrivilege                 Create a pagefile                                                  Disabled
SeBackupPrivilege                         Back up files and directories                                      Disabled
SeRestorePrivilege                        Restore files and directories                                      Disabled
SeShutdownPrivilege                       Shut down the system                                               Disabled
SeDebugPrivilege                          Debug programs                                                     Disabled
SeSystemEnvironmentPrivilege              Modify firmware environment values                                 Disabled
SeChangeNotifyPrivilege                   Bypass traverse checking                                           Enabled
SeRemoteShutdownPrivilege                 Force shutdown from a remote system                                Disabled
SeUndockPrivilege                         Remove computer from docking station                               Disabled
SeManageVolumePrivilege                   Perform volume maintenance tasks                                   Disabled
SeImpersonatePrivilege                    Impersonate a client after authentication                          Enabled
SeCreateGlobalPrivilege                   Create global objects                                              Enabled
SeIncreaseWorkingSetPrivilege             Increase a process working set                                     Disabled
SeTimeZonePrivilege                       Change the time zone                                               Disabled
SeCreateSymbolicLinkPrivilege             Create symbolic links                                              Disabled
SeDelegateSessionUserImpersonatePrivilege Obtain an impersonation token for another user in the same session Disabled
```

### Files/Directory reconnaissance

**findstr**: Recursive string scan looking for passwords
```
findstr /spin "password" *.*
```

**tree**: Display Users folders
```
C:\Windows\system32>tree /f /a C:\Users
Folder PATH listing
Volume serial number is 1685-81A0
C:\USERS
+---arbel
|   +---3D Objects
|   +---Contacts
|   +---Desktop
|   |   |   Microsoft Edge.lnk
|   |   |
|   |   \---lab
|   |           Empire-master.zip
|   |           sysmon-config-master.zip
|   |           Sysmon.zip
|   |
|   +---Documents
|   |       hello_there.txt
|   |
|   +---Downloads
|   |       7z1900-x64.exe
```


### Windows Management Instrumentation

**WMI** provides information about the status of local or remote computer systems used for management of devices and applications in a same network. WMIC utility provides a command-line interface for WMI. 

Hotfix info:
```
C:\Windows\system32>wmic qfe get Caption,Description,HotFixID,InstalledOn
Caption                                     Description      HotFixID   InstalledOn
http://support.microsoft.com/?kbid=4532938  Update           KB4532938  1/9/2020
http://support.microsoft.com/?kbid=4601556  Update           KB4601556
http://support.microsoft.com/?kbid=4513661  Update           KB4513661  1/9/2020
http://support.microsoft.com/?kbid=4516115  Security Update  KB4516115  1/9/2020
http://support.microsoft.com/?kbid=4517245  Update           KB4517245  1/9/2020
http://support.microsoft.com/?kbid=4528759  Security Update  KB4528759  1/9/2020
http://support.microsoft.com/?kbid=4528760  Update           KB4528760  1/9/2020
```

## Run AS 

**runas**: Allows a user to run specific tools and programs with different permissions than the user's current logon provides. /savecred Indicates if the credentials have been previously saved by this user
```
C:\Windows\system32>runas /user:user1 /savecreds "cmd.exe /k whoami"
Attempting to start cmd.exe /k whoami as user "DESKTOP-IN9L9R6\user1" ...

desktop-in9l9r6\user1
```



## References

 - https://github.com/morph3/Windows-Red-Team-Cheat-Sheet
 - https://www.ired.team/offensive-security/enumeration-and-discovery/enumerating-com-objects-and-their-methods
 - https://casvancooten.com/posts/2020/11/windows-active-directory-exploitation-cheat-sheet-and-command-reference/
