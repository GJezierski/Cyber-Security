# AZ300.3-000v2: Getting Started with Azure Active Directory [Getting Started]

## Create a new Azure Active Directory tenant

1. In this task, you will create a new Azure AD tenant, and then you will connect to the new tenant.

	Sign in to DC1 as ```Contoso\Administrator``` using ```Passw0rd!``` as the password.

2. Open a browser, go to ``` http://portal.azure.com ```, and then sign in as ```Admin-26183351@LODSPRODMCA.onmicrosoft.com``` using ```J!2j+aF6Mp``` as the password.

3. Create a new Azure Active Directory tenant by using the following settings:
```
Setting	Value
Directory type	Azure Active Directory
Organization name	Contoso26183351
Initial domain name	MyAD26183351
Country/Region	United States
```
4. Display the ContosoLab26183351 tenant by using the Click here to navigate to your new directory: Contoso26183351 link.

## Configure an Azure global administrator account

1. Create a new user by using the following settings (leave others with their defaults):
```
Setting	Value
User name	SyncAdmin
Name	SyncAdmin
First name	Sync
Last name	Admin
Let me create the password	Enabled
Initial password	InitialPwd26183351
Role	Global Administrator
Usage location	United States
```

2. In a new InPrivate or incognito browser window, sign in to https://portal.azure.com as SyncAdmin@myad26183351.onmicrosoft.com using InitialPwd26183351 as the password, change the password to NewPwd26183351, and then close the InPrivate or incognito browser window.

## Configure Azure AD Connect

1. On the DC1 desktop, open Azure AD Connect, and then configure an express settings installation by using the following settings (leave others with their defaults):
```
Setting	Value
Azure AD USERNAME	SyncAdmin@myad26183351.onmicrosoft.com
Azure AD PASSWORD	NewPwd26183351
AD DS USERNAME	Contoso\Administrator
AD DS PASSWORD	Passw0rd!
Continue without matching all UPN suffixes to verified domains	Checked
```
2. Verify that the AD DS accounts are displayed in the Contoso26183351 Azure tenant.

## Implement self-service password reset

In this exercise, you will implement self-service password reset (SSPR) for selected users in the new Azure AD tenant. First, you will configure a group of users who will be permitted to use SSPR. Next, you will implement SSPR for the Azure AD group. Finally, you will test SSPR.

## Create an Azure AD group for self-service password reset

n this task, you will create a new Azure AD user account, and then you will configure the account to use your personal email address during multifactor authentication and SSPR. Next, you will create a new Azure AD group. Finally, you will add the user to the group.

1. Create a new user by using the following settings (leave others with their defaults):
```
Setting	Value
User name	TestUser
Name	TestUser
First name	Test
Last name	User
Let me create the password	Enabled
Initial password	InitialPwd26183351
```

2. Configure your personal email address as the TestUser authentication method contact.

3. Create a new group by using the following settings:
```
Setting	Value
Group name	SSPR
Group description	SSPR
Members	TestUser
```

## Implement self-service password reset for an Azure AD group

In this task, you will implement SSPR. First, you will upgrade Azure AD to a Premium P2 trial. Next, you will configure a group of users who will be permitted to use SSPR. Finally, you will implement SSPR for the Azure AD group.

1. Activate an Azure AD Premium P2 trial for Contoso26183351.
2. Assign an Azure Active Directory P2 license to the SSPR group.
3. Enable password reset for the SSPR group.
4. Configure the password reset Authentication method as email only.
5. Configure password reset registration to not require user to register when signing in.
6. Configure password reset notifications to Notify users on password resets and to Notify all admins when other admins reset their password.


## Create role-based access control custom roles

In this exercise, you will create custom role-based access control (RBAC) roles. First, you will create a custom role by using Azure PowerShell, and then you will create a custom role by using the Azure portal.

## Create a custom role by using Azure PowerShell

In this task, you will create a custom role by using Azure PowerShell. First, you will retrieve the resource ID of the AZ300-RG resource group, and then you will identify the operations associated with virtual machines. Next, you will retrieve the Virtual Machine Contributor role definition, and then you will edit the role definition. Finally, you will save the role definition in a .json file, and then you will use the .json file to create a new custom role.

1. Switch to the original Create a tenant browser tab.
2. Configure an Azure Cloud Shell PowerShell session by using the existing AZ300-RG resource group, a new storage account named cloudshell26183351 in the East US region, and a new file share named shell.
3. Run the following command to obtain the resource ID of the AZ300-RG resource group:
```
Get-AzureRmResource -ResourceGroupName AZ300-RG
```
4. In the Resource ID text box, enter /subscriptions/xx/resourceGroups/AZ300-RG and then replace xx with the ResourceId displayed in the results of the previous command.
5. Run the following command to identify the operations associated with virtual machines:
```
Get-AzProviderOperation "Microsoft.Compute/virtualmachines/*" | FT Operation, Description -AutoSize
```
6. Run the following command to retrieve the Virtual Machine Contributor role definition:
```
Get-AzRoleDefinition -Name "Virtual Machine Contributor" | ConvertTo-Json | Out-File $home\clouddrive\VMOperatorRole.json
```
7. Run the following command to change directories:
```
cd $home\clouddrive
```
8. Run the following command to open the VMOperatorRole.json file in the Azure Cloud Shell code editor:
```
code VMOperatorRole.json
```
9. In the code editor window, locate the Name property, and then change the value to "Virtual Machine Operator".
10. Locate the Id property, and then delete the entire line.
11. Locate the IsCustom property, and then change the value to true.
12. Locate the Description property, and then change the value to "Lets you view, start, and stop virtual machines."
13. Locate the AssignableScopes property, and then change the value to "<RGID>".
14. Locate the Actions property, and then edit it to contain only the
```
"Microsoft.Compute/*/read", 
"Microsoft.Compute/virtualMachines/start/action",
"Microsoft.Compute/virtualMachines/deallocate/action" actions.
```
15. Save the VMOperatorRole.json file, and then close the editor.
16. In the Cloud Shell window, run the following command to create a custom role, and then close the Cloud Shell window.:
```
New-AzRoleDefinition -InputFile "VMOperatorRole.json"
```

## Create a custom role by using the Azure portal
In this task, you will create a custom role by using the Azure portal. First, you will retrieve the Storage Account Contributor built-in role. Next, you will review the permissions granted by the Storage Account Contributor role. Finally, you will create a new custom role based on the Storage Account Contributor role.

1. View the roles that can be assigned to the AZ300-RG resource group.
2. View the providers and permissions associated with the Storage Account Contributor role.
3. Create a custom role named Storage Account Contributor (No Support) in the AZ300-RG resource group that is based on the Storage Account Contributor role, that does not include the permissions associated with the Microsoft.Support provider, and that is scoped only to the AZ300-RG resource group.
4. Verify that the Microsoft.Support provider permmissions are not associated with the Storage Account Contributor (No Support) role.

## Implement managed identities for Azure virtual machines

In this exercise, you will implement managed identities. First, you will enable a system-assigned managed identity, and then you will disable the identity. Next, you will create a user-assigned managed identity, and then you will assign a role to the managed identity. Finally, you will add the user-assigned managed identity to a virtual machine.

### Manage a system-assigned identity
In this task, you will enable a system-assigned managed identity, and then you will disable the identity.

1. Enable a system assigned managed identity for the MyVM virtual machine.
2. Remove the system assigned managed identity for the MyVM virtual machine.

## Create a user-assigned identity
In this task, you will create a user-assigned managed identity. Next, you will assign a role to the managed identity. Finally, you will add the user-assigned managed identity to a virtual machine.

1. Create a user assigned managed identity named MyManagedID26183351 in the AZ300-RG resource group that is located in (US) East US 2.
2. Assign the MyManagedID26183351 user assigned managed identity to the MyVM virtual machine.
3. Add a Reader role assignment to the MyVM virtual machine that is assigned to the MyManagedID26183351 managed identity.

## Implement multi-factor authentication for an Azure AD user

In this task, you will enable per-user multi-factor authentication (MFA) for the TestUser account

1. Switch to the Contoso26183351 browser tab. Do not close the original browser tab.
2. Enable Multi-Factor Authentication for TestUser.
3. Open an InPrivate or incognito browser window, sign in to http://portal.azure.com as Testuser@myad26183351.onmicrosoft.com using NewPwd26183351 as the password, complete the verification process by using your personal phone, complete the sign in process, and then close the InPrivate or incognito browser window.
4. Disable Multi-Factor Authentication for TestUser.

## Implement an Azure conditional access policy that requires multi-factor authentication

In this task, you will implement an Azure conditional access policy that requires MFA. First, you will disable MFA for TestUser. Next, you will implement an Azure conditional access policy that requires MFA when TestUser connects to the Azure portal. Finally, you will test the conditional access policy.

1. Disable security defaults for Contoso26183351.
2. Create an Azure AD Conditional Access policy by using the following settings (leave others with their defaults):
3. Open an InPrivate or incognito browser window, sign in to http://portal.azure.com as Testuser@myad26183351.onmicrosoft.com using NewPwd26183351, verify the account, and then close the browser window.

## Implement Azure Policy
In this task, you will implement Azure Policy. First, you will review a policy definition. Next, you will assign a policy. Finally, you will test the policy.

1. Switch to the original browser tab.
2. Review the Allowed locations Azure policy definition, and then assign the policy to the AZ300-RG resource group to permit resources deployment in East US 2.
3. Create an Azure virtual network named VNet1 in the AZ300-RG resource group that is located in (US) East US.
4. Create an Azure virtual network named VNet1 in the AZ300-RG resource group that is located in (US) East US 2.

## Summary

Congratulations, you have completed the Getting Started with Azure Active Directory lab.

You have accomplished the following:

Installed and configured Azure AD Connect.
Implemented SSPR.
Created RBAC custom roles.
Implemented managed identities for Azure virtual machines.
Implemented MFA for an Azure AD user.
Implemented an Azure conditional access policy that requires MFA.
Implemented Azure Policy.

