# Domain Administration

Maxb's notes while he sets up a Windows domain using a Windows Server 2008 R2
and a Windows 7 client machine.

### Things to Note
* Clients must have their DNS server set equal to the domain controller
* Domains by default have a "Guest" user created with them. Fortunately, it's
  disabled.
* ```net user``` will only show local accounts, not domain ones.
* The "Best Practices Analyzer" in the server manager seems like a good way to
  spot misconfigs. There is one for each role the server has.

### Useful PowerShell Commands
* ```import-module ActiveDirectory```: imports the active directory cmdlets.
  Required for most of these. Appears to only be on servers.
* ```get-adcomputer -Filter "name -like '*'"```: Gets all computers in the domain.
* ```get-adgroup -Filter "name -like '*'"```: Gets all groups in the domain.
* ```get-aduser -Filter "name -like '*'"```: Gets all users in the domain.
* ```get-adgroupmember [GROUPNAME]```: Gets all the users in a specified AD group.
* ```remove-adgroupmember -identity [GROUPNAME] -members [MEMBER]```: removes
  specified member from specified group.

### Group Policy
* You can see policies in the Group Policy Management Tool
* Right-click a policy and hit "Edit" to change it. Or, view the overview in the
  "Settings" tab.
* If a new GPO is created, it must be "linked" to the domain. Do this by
  right-clicking the domain in the Group Policy Management tool and selecting
  "Link an Existing GPO"
* Force group policy update ```gpupdate /force```

### Potentially Good Books
* [[Windows Internals, Part 1, 6th Edition|http://shop.oreilly.com/product/0790145305930.do]]
* [[Active Directory, 4th Edition|http://shop.oreilly.com/product/9780596520601.do]]
