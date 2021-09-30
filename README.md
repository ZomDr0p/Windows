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

### Network information
```
ipconfig /all
route print
arp -A
```

### Network connections
```
netstat -ano
```

### To see what access token do the current user have
```
whoami /priv
```

### Recursive string scan
```
findstr /spin "password" *.*
```

### Running processes
```
tasklist /SVC
```

### Especially good with hotfix info
```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

## Run AS Empire

**runas**: Allows a user to run specific tools and programs with different permissions than the user's current logon provides. /savecred Indicates if the credentials have been previously saved by this user
```
C:\Windows\system32>runas /user:user1 /savecreds "cmd.exe /k whoami"
Attempting to start cmd.exe /k whoami as user "DESKTOP-IN9L9R6\user1" ...
desktop-in9l9r6\user1
```
