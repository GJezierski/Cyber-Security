# Reading Assignment

## Introduction

Active Directory is a database, which can be used to centrally manage a Microsoft Windows network, users, groups, computers, printers, and other objects and resources. In this lab, you will examine the Active Directory objects and group policies at the domain and organizational unit level. Windows System Administrators commonly use Active Directory in their daily work. Figure 1 is the lab topology for this lab which represents a single Windows Server with Active Directory Domain services.

## Introduction To Active Directory (AD)

Active Directory (AD) is a database and directory service of an organization’s objects and users on a network. AD is a directory service that uses the Lightweight Directory Access Protocol (LDAP). LDAP is an open and cross platform directory services protocol that is used by most directory services. Figure 2 shows the hierarchical nature of Active Directory.

Active Directory manages an organization’s objects which can be servers, clients, computers, hardware, shared files and folders, and users. An AD object can be a container object such as a folder or a leaf such as a file. An AD domain is organized around a collection of objects. A domain can share policy and use an Active Directory database. A tree is organized around multiple AD domains. Domains in a tree share network configuration. A forest is organized around a group of trees that have the same database. Trees in a forest have different namespace; for example, xbox.com and office.com (both owned by a single organization Microsoft). Figure 3 shows what Active Directory looks like on a Windows server.

## Organizational Units (OUs)

Organizational Units (OUs) are AD containers that allow you to place users, printers, groups, computers, and other objects. OUs can be nested inside of each other. You can use OUs to represent an organization’s organizational chart. A good reason to use OUs is to be able to assign a group policy to the OU and all users and computers that are members of that OU will get that policy. In this lab, you will create OUs and users in the OU.

## Group Policies In Active Directory

Group policies can be set at the site, domain, and organizational level of Active Directory as well as on a local machine. Group policies are applied at the site first, domain second, at the OU level third, and then finally at the local machine. If you set a group policy at the Domain level, everything below the domain will get the Group policy first. Best practice is to not set domain level group policies but set organizational unit level group policies is the better option. Microsoft has setup a hierarchy in active directory when applying group policies. They are applied in this order:

* Local policies:
	* Configured on the actual computer itself
* Site policies:
	* Configured in Active Directory. You can configure a site which is a representation of a physical location
* Domain policies
	* Configured in Active Directory and applies to all objects in the domain assigned
* OU policies
	* Configured in Active Directory and applies to all objects in the OU
	
The beauty of group policies is the ability to have greater control over the security of your network as a system administrator.

Here are some ways you can configure group policies in Active Directory:

* Password Policies can be set to establish password length, complexity, and other requirements.
* Systems Management can apply standardized, universal settings across all new users with just a few clicks.
* Health Checking can be used to deploy software updates/patches to ensure your systems are up to date against the latest vulnerabilities.

In this lab, you will set a domain level and organizational unit (OU) group policies.

## Creating an Organization Unit and Users in Active Directory

1. Click on the Windows Server icon in the network topology. After the machine finishes booting, click the  CTRL-ALT-DELETE button in the upper-right corner. 
2. Log on as administrator with the password of P@ssw0rd, then click the arrow.
3. Double-click on the Command Prompt shortcut on the Windows Server 2008 desktop.
4. Type the following command to open the Active Directory Users and Computers interface, then press Enter.
```
C:\>dsa.msc
```
5. Right-click on the campus.edu domain and select New, then select Organizational Unit.
6. Type Minecraft for the Name of the organizational unit and click OK.
7. Expand the campus.edu domain by clicking the + sign beside the icon. Right-click on the Minecraft organizational unit and select New and then select User (bottom option).
8. For the First name, type creeper, and for the User logon name, type creeper. Click Next.
9. Uncheck the box that states “User must change password at next logon.” For the Password, type P@ssw0rd and type P@ssw0rd for the Confirm password. Click Next.
10. Click the Finish button to create the user creeper in the Minecraft organizational unit. 
11. Right-click on the Minecraft organizational unit and select New and then select User.
12. For the First name, type zombie, and for the User logon name, type zombie. Click Next.
13. Uncheck the box that states “User must change password at next logon.” For the Password, type P@ssw0rd and type P@ssw0rd for the Confirm password. Click Next.
14. Click the Finish button to create the user zombie in the Minecraft organizational unit. 
15. Right-click on the Minecraft organizational unit and select New and then select User.
16. For the First name, type steve, and for the User logon name, type steve. Click Next.
17. Uncheck the box that states “User must change password at next logon.” For the Password, type P@ssw0rd and type P@ssw0rd for the Confirm password. Click Next.
18. Click the Finish button to create the user steve in the Minecraft organizational unit.  
19. Click the Minecraft directory, and all three of the users you created in the Minecraft organizational unit will be displayed.
20. Select File from the Active Directory Users and Computers menu and select Exit.

## Setting a Domain Level Policy in Active Directory

1. ​​​Type the following command and press Enter to add the user terrance with the password of P@ssw0rd,
```
C:\>net user terrance P@ssw0rd /add
```
2. Type the following command and press Enter to get information about the user terrance you just created.
```
C:\>net user terrance
```
3. There is another account on the system called superman. View the information about the superman account by typing the following command:
```
C:\>net user superman
```
... Challenge 1 - 4
8. Type the following command and press Enter to delete the user terrance.
```
C:\>net user terrance /del
```
9. Type the following command and press Enter to verify that the user terrance has been deleted.
```
C:\>net user terrance 
```
10. Type the following command and press Enter to exit the command prompt, then press Enter.
```
C:\>exit
```
11. Click on Start, select Administrative Tools and then select Group Policy Management.
12. Click the + button to expand Forest: campus.edu. Click the + button to expand Domains and then click the + button to expand campus.edu. Right-click Default Domain Policy and select Edit.
13. Click the + button to expand Computer Configuration.
Click the + button to expand Policies.
Click the + button to expand Windows Settings.
Click the + button to expand Security Settings.
Click the + button to expand Account Policies.
Click on Password Policy.
14. Double-click Minimum password length. Change the default value of the policy setting Password must be at least: from 7 characters to 10 characters. Click OK to apply this setting to the campus.edu domain.
15. Verify that the minimum password length is now 10 characters. Select File and choose Exit.
16. Double-click on the Command Prompt shortcut on the Windows Server 2008 desktop.
17. Type the following command and press Enter to refresh the Group Policy Settings on the machine.
```
C:\>gpupdate /force
```
18. Type the following command and press Enter to attempt to add the user peaches with the password of P@ssw0rd. 
```
C:\>net user peaches P@ssw0rd /add
```
19. Type the following command and press Enter to add the user peaches with the password of P@ssw0rd12.
```
C:\>net user peaches P@ssw0rd12 /add
```
20. Type the following command and press Enter to delete the user peaches.
```
C:\>net user peaches /del
```
21. Type the following command and press Enter to attempt to change the password of the creeper account to P@ssw0rd1.
```
C:\>net user creeper P@ssw0rd1 
```
22. Type the following command and press Enter to change the password of the creeper account to P@ssw0rd12.
```
C:\>net user creeper P@ssw0rd12
```
23. Type the following command and press Enter to exit the command prompt.
```
C:\>exit
```

## Setting an Organizational Level Policy in Active Directory

1. Click on Start, select Administrative Tools, and then select Group Policy Management.
2. Click the + button to expand Forest:campus.edu. Click the + button to expand Domains and then click the + button to expand campus.edu. Right-click on the Minecraft organizational unit and select Create a GPO in this domain, and Link it here…
3. In the New GPO box, type Minecraft Policy. Leave the Source Starter GPO set to (none) and click the OK button to create the new group policy for the Minecraft OU. 
4. Click the + button to expand Minecraft. Right-click on the Minecraft Policy and choose Edit.
5. Click the + button to expand User Configuration. Click the + button to expand Policies. Click the + button to expand Administrative Templates. Then double-click on Control Panel.
6. Double-click Prohibit access to the Control Panel. Click the Enabled button. Click OK.
7. Verify that Prohibit access to the Control Panel is enabled. Select File and choose Exit.
8. Double-click on the Command Prompt shortcut on the Windows Server 2008 desktop.
9. Type the following command to refresh the group policy settings on the machine, then press Enter.
```
C:\>gpupdate /force
```
10. ype the following command to add the user zombie to the backup operators group, then press Enter.
```
C:\>net localgroup “backup operators” zombie /add
```
11. Type the following command to view the user zombie in the backup operators group, then press Enter.
```
C:\>net localgroup “backup operators”
```
*** Challenge 5-6

12. Type the following command to close the administrator’s session on Windows Server, then press Enter. 
```
C:\>logoff
```
13. After the machine reboots, click the CTRL-ALT-DELETE button. Then log in as zombie with the password of P@ssw0rd, and click the arrow.
14. Click on Start and type control in the Start search box. Click the Control Panel link.
15. You will receive a message that “This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator.” Click the OK button.

Note: Press the STOP button to complete the lab.