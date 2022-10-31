# Identify Common Cyber Network Attacks with Wireshark

## Analyzing Common Attack Signatures of Suspect Traffic

### The Top Ten Things to Look for When Analyzing Suspect Traffic
1. TCP SYN Scan
2. Unusual Port Numbers
3. GeoIP Location to Suspect Country Codes
4. Domain Calls Including Suspect Countries
5. Unencrypted Web Traffic/File Transfers
6. Outdated TLS / Bad User Agents
7. Large DNS (Or Other) Packets for Sustained Periods – Data Exfiltration
8. Outbound SYN/ACK Replies (SYN Came from Outside Network)
9. Brute Force Password Behavior (FTP, SSH, RDP, HTTP)
10. Reverse Shell Behavior – TCP Port 4444, 1337, 1234, 6001, 8080


### Useful Wireshark Filters
#### Attack Method | Wireshark Filter

* TCP SYN Scan
```
tcp.flags.syn==1 and tcp.flags.ack==0
```
* Unusual Port Numbers
```
!tcp.port in {443 1433 445 995 8000..8005}
```
* Nmap Stealth Scan
```
tcp.flags.syn==1 and tcp.flags.ack==0 and
tcp.window_size <=1024
```
* Suspect GeoIP Country
```
ip.geoip.country == Russia
```
* Country Code
```
ip.geoip.country_iso == CN
```
* Everything but a Country
```
ip and !ip.geoip.country_iso == US
```
* Strange DNS
```
dns.qry.name matches “(us|mx|cr)”
````
* Malware Downloads .bin/.exe/.php
```
http.request.uri matches
"(tar|exe|zip|pdf|bin|php)"
```
* FTP File Transfers
```
ftp.request.command == “RETR”
```
* Unencrypted Strings
```
frame contains torrent
```
* Old TLS Versions
```
tls.handshake.extensions.supported_version in
{0x0300 0x0301 0x0302}
```
* DNS Exfiltration
```
DNS and ip.len > 200
```
* Outbound SYN/ACK
```
tcp.flags.syn==1 and tcp.flags.ack==1 and
(!ip.dst==10.0.0.0/8) (insert local IP range)
```
* Brute Force Attacks
```
frame contains admin
```
* Reverse Shell Behavior
```
tcp.port in {1234 4444 1337 6001}
```
