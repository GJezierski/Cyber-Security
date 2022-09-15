## Identify Aspects of Intrusion

## Scenario
Your corporate network has been hacked. Your job is to participate in the attack analysis and incident response to identify vulnerabilities that were exploited, attack vectors, and methods of attack.

### Initial Response
You now have access to one of the corporate computers that was hacked. A trusted toolset has been mapped to the local command prompt for use. First begin with using the trusted toolset to identify any anomalous behavior or log entries. Various Windows command line tools will be used to gather the data.

Open the Trusted Tool Set by right clicking on the shortcut on the desktop and select Run as Administrator.

In the next step, we will identify all the current OS variables.

### System Date & Time
Now see if the system date and time match what the desktop toolbar application is showing us. This will also help to document a timeline of our response. First, enter the following command in the prompt:
```
C:\Windows\system32> echo > c:\ ir_file.txt
```

### Environmental Variables
Capture a list of the current environmental variables. these can be looked at later for any anomalies in the variables. Issue the following command:
```
C:\Windows\system32> set >> c:\ir_file.txt
```

### Task List
In the same trusted toolset command terminal issue the following command to gather information about the current tasks.
```
C:\Windows\system32> tasklist >> c:\ir_file.txt
```

### Network Connections
In the same command terminal, issue the following command:
```
C:\Windows\System32> **netstat -nao >> C:\ir_file.txt**We are telling netstat to append its output to our existing Incident Response text file and show us all process IDs, network connections and not resolve FQDNs.
```

### Victim Network Settings
Information about the victim's network interfaces needs to be captured. Use the trusted version of ipconfig to gain this information. In the same terminal window type the following:
```
C:\Windows\system32> ipconfig /all >> c:\ir_file.txt
```

### Security Logs

A variety of logs need to be pulled and saved to file for later analysis. For this, stay in the trusted toolset shell but move into the SysinternalsSuite directory and use a tool called psloglist. To do this, type the following commands:
```
C:\Windows\system32> cd C:\Program Files\SysinternalsSuite\
C:\Program Files\SysinternalsSuite> psloglist.exe -s -x security > C:\ir_securitylogs.txt
```

### Windows Event Utility (wevtutil)

Use wevtutil from the trusted toolset to query a specific event ID from a specific type of event log. Query the Security event log for all instance of Event ID 4616 which shows that the system time was changed. An attacker might do this to make the Incident Responder's job more difficult. From the trusted toolset shell type the following command:
```
C:\Program Files\SysinternalsSuite\> wevtutil qe Security /q:"*[System/EventID=4616]" > c:\ ir_timechange.txt
```

### PowerShell - Enumerate Processes

In the same trusted toolset shell, now drop into a PowerShell prompt by typing the following command:
```
C:\Program Files\SysinternalsSuite> powershell.exe
You should now see a PS at the beginning of your terminal prompt. This change in the prompt is how you know you are a PowerShell vice in normal DOS terminal.
```

### PowerShell - Enumerate Processes

Now enter the following PowerShell command to enumerate the list of running processes:
```
PS C:\Program Files\SysinternalsSuite> Get-Process | Out-File c:\ ir_processes.txt
```

### PowerShell - Security Logs

You can also use PowerShell to retrieve the security logs and search for specific event IDs. Continuing in the same trusted toolset PowerShell prompt, type the following command:
```
PS C:\Program Files\SysinternalsSuite> Get-EventLog Security | ?{$_.EventID -eq 4688} | Out-File C:\ ir_processcreated.txt
```

### Attack Analysis

Open the Windows Explorer window by clicking on the icon from the bottom toolbar. Click on the C:\ drive icon, you should see all the text files you created.

### Attack Analysis - IR File

Open the file named ir_file.txt

Review the various data you recovered and saved into this file. We normally look for things that look out of place or strange. Unfortunately, there is no list that we can give for you to use so browse through and look at the users, the network connections, network configuration, etc.

### Attack Analysis - IR Processes

Now open the ir_processes.txt file.

When reviewing processes on a box that has been attacked you would look for strange processes that are not normally running on this type of computer. For example, the system administrator should have a baseline list of approved software and have a good idea of what processes should be running on one of his networked computers.

You would compare your list to his list and also do research on whatever processes you don't recognize. Keep in mind though, that if a rootkit has been installed on the victim computer it can hide processes from you. However, we are using a trusted toolset so hopefully our tools are getting accurate system information.

### Attack Analysis - Processes Created

Looking at various processes that were created and logged based on your organization's auditing and logging policy may provide useful information to your attack analysis.

Open the ir_processcreated.txt file.

### Attack Analysis - IR Security Logs

Open the file you created called ir_securitylogs.txt. Based on other information we found while responding to this incident two unauthorized accounts were added to this computer, bad_use**r and **Sysadmin. The file will be large so it will take a moment to open.

### Attack Analysis - IR Security Logs

Let's search for hits on the following keywords:

bad_user
Sysadmin
password
create
delete
S-1-5-7 (this is the SID associated with an anonymous logon)
500 (associated with all Admin level users, which lets us see security events triggered by an Admin)


In this lab we have participated in the collection of information to be used in an attack analysis. We collected a variety of system information to be archived and to be further investigated and correlated with other network activity from IDS devices, and other network activity from other users. Congratulations

