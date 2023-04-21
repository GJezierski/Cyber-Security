# Deep Blue

A Windows workstation was recently compromised, and evidence suggests it was an attack against internet-facing RDP, then Meterpreter was deployed to conduct 'Actions on Objectives'. Can you verify these findings?

# Questions

## Using DeepBlueCLI, investigate the recovered Security log (Security.evtx). Which user account ran GoogleUpdate.exe? 

```
PS C:\Users\BTLOTest\Desktop\Investigation\DeepBlueCLI-master> .\DeepBlue.ps1 ..\Security.evtx
```
```
Command : "C:\Users\Mike Smith\AppData\Local\Google\Update\GoogleUpdate.exe
```
**Answer:** Mike Smith

## Using DeepBlueCLI investigate the recovered Security.evtx log. At what time is there likely evidence of Meterpreter activity?

Date    : 4/10/2021 10:48:14 AM

**Answer:** 4/10/2021 10:48:14

## Using DeepBlueCLI investigate the recovered System.evtx log. What is the name of the suspicious service created?

Results : Service name: rztbzn
```
PS C:\Users\BTLOTest\Desktop\Investigation\DeepBlueCLI-master> .\DeepBlue.ps1 ..\System.evtx
```

**Answer:** rztbzn

## Investigate the Security.evtx log in Event Viewer. Process creation is being audited (event ID 4688). Identify the malicious executable downloaded that was used to gain a Meterpreter reverse shell, between 10:30 and 10:50 AM on the 10th of April 2021.

``` NewProcessName C:\Users\Mike Smith\Downloads\serviceupdate.exe ```

**Answer:** Mike Smith, serviceupdate.exe

## It's also believed that an additional account was created to ensure persistence between 11:25 AM and 11:40 AM on the 10th April 2021. What was the command line used to create this account? (Make sure you've found the right account!)
```
11:29:15 AM
 CommandLine net user ServiceAct /add 
```
**Answer:** net user ServiceAct /add

## What two local groups was this new account added to?

**Answer:** Remote Desktop users, administrators