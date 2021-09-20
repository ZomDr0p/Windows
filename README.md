# Windows
Commands to use in the reconnaissance phase

### Systeminfo
```
systeminfo
hostname 
```

### What users/localgroups are on the machine?
```
net users
net localgroups
net localgroup Administrators
net user Administrator
```

### Crosscheck local and domain too
```
net user Administrator /domain
net group Administrators /domain
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
