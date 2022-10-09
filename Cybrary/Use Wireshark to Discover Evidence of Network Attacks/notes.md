# Use Wireshark to Discover Evidence of Network Attacks

### Understand the scenario
You are a network and security administrator. You need to locate information from network traffic to discover facts or uncover evidence of attacks. First, you will use Wireshark to capture FTP credentials. Next, you will use Wireshark to determine details from a network traffic capture, such as MAC addresses, DNS server addresses, IP resolutions from FQDNs, and whether HTTP traffic is encrypted. Finally, you will use Wireshark to discover evidence of a password guessing attack.

### Understand your environment
You will be using a Kali Linux virtual machine named Kali Linux 2021 and an Ubuntu virtual machine named Ubuntu 20.4.

## Use Wireshark to capture FTP credentials

* Sign in to Kali Linux 2021 as labuser using Passw0rd! as the password.
* Launch Wireshark, and then maximize the Wireshark window.
* Initiate a network packet capture on eth0 by using a Capture filter to capture only traffic related to FTP ports 20 or 21.
```
Expand this hint for guidance on defining and using a new capture filter.
On the Wireshark menu bar, select Capture, and then select Options.

In the Wireshark – Capture Options window, select eth0.

In the Enter a capture filter… field, enter port 21 or port 20, and then select Start.
```
* Open a Terminal Emulator window, connect to ftp.dlptest.com by using FTP, and then attempt to log on using labuser as the Name and Passw0rd! as the password.
```
Expand this hint for guidance on connecting to FTP.
Open a Terminal Emulator window by selecting it from the top icon menu. The icon looks like a small computer screen showing a black background with a white dollar sign cursor prompt.

Run the following command to access ftp:

ftp ftp.dlptest.com

Verify that the output displays an initial connection to an FTP service and a 220 Welcome to the DLP Test FTP Server statement.

In the Name: ftp.dlptest.com:labuser): prompt, enter labuser, and then press Enter.

In the Password: prompt Enter Passw0rd!, and then press Enter.

After a few moments, verify that a login error message is displayed—these are not valid credentials for this FTP service.
```
* Stop the Wireshark network capture, and then verify that only packets related to the FTP connection process were captured.
```
In the Capturing from eth0 (port 21 or port 20) window, on the toolbar, select the Stop capturing packets icon—it looks like a red square and is the second icon on the toolbar.

Verify that only packets related to the FTP connection process were captured.
```
* Apply a display filter that contains tcp contains USER to find the frame that has a source address of 192.168.10.25 and represents the transmission of the name that was used to attempt to sign in to the FTP server.
```
Select the Apply a display filter field, enter tcp contains USER, and then either press Enter or select the Apply display filter icon on the far right-side of the field—it looks like an arrow.

Select the frame that has a source address of 192.168.10.25—there should only be one or two frames that include USER in the payload.

Review the ASCII interpretation in the bottom pane to verify that the username contained in the packet immediately after USER is labuser—this information is also displayed in the Info column in the top pane.
```
* Remove the existing display filter.
```
Selecting the Clear display filter icon—it is located on the far right of the display filter field and looks like a capital X in a box; it might be grey, but will turn red when your mouse cursor is over it.
```
* Apply a display filter that contains tcp contains PASS to find the frame that that has a source address of 192.168.10.25, and then review the ASCII interpretation in the bottom pane to verify that Passw0rd! was the password used by labuser to authenticate the FTP session.
* Remove the active Capture filter.
```
On the Wireshark menu bar, select Capture, and then select Options.

In the Wireshark-Capture Options window, select the X at the right end of the Capture filter field—this icon functions as a clear capture filter.

Select Close.
```
* Remove the existing display filter.

## Find details in a network traffic capture

* Start a new Wireshark network traffic capture without saving the captured traffic.
```
On the Wireshark tool bar, select the Start capturing packets icon—it looks like a shark fin and is the left-most icon on the toolbar.

In the Unsaved packets pop-up window, select Continue without Saving.
```
* Open Firefox ESR, and then go to www.space.com.
* Switch to Wireshark, and then stop the network capture.
* Apply ```ip.src == 192.168.10.25``` as a display filter.
* Review the captured traffic to determine the MAC address of the computer that uses 192.168.10.25 as its IP address.
```
In the top Packet List pane, select the first packet that is displayed based on this display filter—be sure to scroll to the top of the capture or press Home on your keyboard to ensure you are at the first packet.

In the middle Packet Details pane, select the arrow next to Ethernet II to expand its contents.

In Ethernet II, locate the Ethernet header value labeled Source:—this is the MAC address of the source of this packet.
```
* Remove the existing display filter.
* Apply http.host=="www.space.com" as a display filter.
* Review the captured traffic to locate and select a packet that displays 192.168.10.25 in the Source column, HTTP in the Protocol column, and Get / HTTP/1.1 in the Info column, and then determine the IP Address value displayed in the Destination column.
* Record the IP address obtained in the previous task in the following Dest IP Addr text box:    Dest IP Addr
* Remove the existing display filter.
* Apply ip.dst == <DestIPAddr> as a display filter.
* Create a new column based on the Transmission Control Protocol Destination Port, and then review the results to determine if encryption was used in the communication between the client and website.
```
In the top Packet List pane, review the displayed packets to determine if there are any TLS labeled packets in the Protocol column—there can be various TLS versions listed, such as TLSv1.3.

In the top Packet List pane, select any packet.

In the middle Packet Details pane, expand Transmission Control Protocol, and then select the Destination Port:.

Right-click Destination Port:, and then select Apply as Column.

In the top Packet List pane between the Length and Info columns, verify that a new column labeled Destination Port is displayed.

Review the contents of the new column.
```

## Discover a password guessing attack

* Switch to Ubuntu 20.4, and then sign in as ubuntu-user using passw0rd! as the password.
* Open a Terminal window by using the Show Applications button.
```
In the bottom left corner of the Ubuntu desktop, select the Show Applications button—it is a square containing nine dots.

In the top Type to search field, enter term, and then select Terminal.
```
* Install an FTP service by using the sudo apt-get install vsftpd command.
```
In the Terminal window, run the following command to install an FTP service:

sudo apt-get install vsftpd

When prompted for a password, enter passw0rd!, and then press Enter.
```
* Start the FTP service by using the service vsftpd start command.
```
Run the following command to start the FTP service:

service vsftpd start

In the Authentication required prompt, enter passw0rd!, and then select Authenticate.
```
* Switch to Kali Linux 2021, and then if needed, sign in as labuser using Passw0rd! as the password.
* Open a Terminal Emulator window, elevate to root by using sudo su and Passw0rd! as the password, and then maximize the Terminal Emulator window.
```
On the Kali Linux toolbar, select the Terminal Emulator icon—it looks like a black computer screen with a white dollar sign cursor.

Run the following command to elevate to root:

sudo su

When prompted for a password, enter Passw0rd!, and then press Enter.

In the Terminal Emulator window, select the Maximize button—it is located to the far right on the header, immediately to the left of the X, and looks like a blank or black circle; once you hover your mouse cursor over it, a white square will be displayed.
```
* Extract the /usr/share/wordlists/rockyou.txt.gz file by using the gunzip command.
``` Run the following command to gunzip a file:

gunzip /usr/share/wordlists/rockyou.txt.gz
```
* Switch to Wireshark, and then remove the existing display filter.
* Initiate a network packet capture on eth0 by using a Capture filter to capture only traffic related to FTP port 21.
```
On the Wireshark menu, select Capture and then select Options.

In the Wireshark – Capture Options window select Ethernet—it may display as Eth0.

In the Enter a capture filter… field, enter port 21, and then select Start.

If prompted by the Unsaved packets pop-up window, select Continue without Saving.
```
* Initiate a password guessing attack on the ubuntu-user account by using Hydra, the /usr/share/wordlists/rockyou.txt wordfile, and the ftp service on 192.168.10.31.
```
Switch to the elevated Terminal window by selecting it from the top taskbar—the Terminal window icon in the taskbar is labeled as root@kali:/home/labuser.

Run the following command to use hydra:

hydra -l ubuntu-user -P /usr/share/wordlists/rockyou.txt ftp://192.168.10.31
```
* Switch to Wireshark, and then apply ftp contains PASS as a display filter.
* Review the captured packets to determine if a password guessing attack is taking place.

## Summary

Congratulations, you have completed the Finding a Needle in a Haystack Challenge Lab.

You have accomplished the following:

* Used Wireshark to capture FTP credentials.

* Evaluated captured packets to discover details from a network traffic capture.

* Detected the occurrence of a password guessing attack.

