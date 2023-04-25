# Follina 

``` https://ethical.blue/textz/pl/32 ```

On a Friday evening when you were in a mood to celebrate your weekend, your team was alerted with a new RCE vulnerability actively being exploited in the wild. You have been tasked with analyzing and researching the sample to collect information for the weekend team.

# Questions

## Question 1) What is the SHA1 hash value of the sample? (Format: SHA1Hash)

``` sha1sum sample.doc ```

**Answer:** 06727ffda60359236a8029e0b3e8a0fd11c23313

## Question 2) According to VirusTotal, what is the full filetype of the provided sample? (Format: X X X X) 

https://www.virustotal.com/gui/file/4a24048f81afbe9fb62e7a6a49adbd1faf41f266b5f9feecdceb567aec096784/details

**Answer:** Office Open XML Document

## Question 3) Extract the URL that is used within the sample and submit it (Format: https://x.domain.tld/path/to/something)

``` unzip sample.doc ``` ```document.xml.rels```
**Answer:** https://www.xmlformats.com/office/word/2022/wordprocessingDrawing/RDF842l.html

## Question 4) What is the name of the XML file that is storing the extracted URL? (Format: file.name.ext) 

**Answer:** document.xml.rels

## Question 5) The extracted URL accesses a HTML file that triggers the vulnerability to execute a malicious payload. According to the HTML processing functions, any files with fewer than <Number> bytes would not invoke the payload. Submit the <Number> (Format: Number of Bytes)	

**Answer:** 4096

## Question 6) After execution, the sample will try to kill a process if it is already running. What is the name of this process? (Format: filename.ext) 

**Answer:** msdt.exe

## Question 7) You were asked to write a process-based detection rule using Windows Event ID 4688. What would be the ProcessName and ParentProcessname used in this detection rule? [Hint: OSINT time!] (Format: ProcessName, ParentProcessName) 

**Answer:** msdt.exe, WINWORD.exe

## Question 8) Submit the MITRE technique ID used by the sample for Execution [Hint: Online sandbox platforms can help!] (Format: TXXXX) 

``` https://attack.mitre.org/tactics/TA0002/ ```

**Answer:** T1059

## Question 9) Submit the CVE associated with the vulnerability that is being exploited (Format: CVE-XXXX-XXXXX)

**Answer:** CVE-2022–30190