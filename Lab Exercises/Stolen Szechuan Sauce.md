The Case of the Stolen Szechuan Sauce

Scenario: Your bedroom door bursts open, shattering your pleasant dreams. Your mad scientist of a boss begins dragging you out of bed by the ankle. He simultaneously explains between belches that the FBI contacted him. They found his recently-developed Szechuan sauce recipe on the dark web. As you careen past the door frame you are able to grab your incident response “Go-Bag”. Inside is your trusty incident thumb drive and laptop.

Artifacts:
**Domain Controller (DC01) Artifacts:**

1. **[DC01 Memory Dump](https://dfirmadness.com/case001/DC01-memory.zip)**
   
3. **[DC01 Autoruns](https://dfirmadness.com/case001/DC01-autorunsc.zip)**
   
5. **[DC01 Protected Files](https://dfirmadness.com/case001/DC01-ProtectedFiles.zip)**

**Network Capture:**

4. **[Case001 PCAP](https://dfirmadness.com/case001/case001-pcap.zip)**

**Desktop Artifacts:**

5. **[Desktop Disk Image (E01)](https://dfirmadness.com/case001/DESKTOP-E01.zip)**

6. **[Desktop Memory Dump](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-memory.zip)**
   
8. **[Desktop Autoruns](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-autorunsc.zip)**
   
10. **[Desktop Protected Files](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-Protected%20Files.zip)**


Desktop Protected Files
Reference: [James Smith](https://twitter.com/DFIRmadness) - [The Case of the Stolen Szechuan Sauce](https://dfirmadness.com/the-stolen-szechuan-sauce/) (with explicit permission)

### Questions 

> **If you are reading this, it means I have not yet finished this exercise. Please note that I will be including my thought process throughout the questions, which may lead to incorrect analysis or processes, but this is how I want to document them for now. I will also dump all artifacts I find, whether they are suspicious, malicious, or not. This will serve as my draft document.**

***1. What’s the Operating System of the Server?***  

**Answer: `Windows Server 2012 R2 (x64), Build 9600`**

citadeldc01.mem

using volatility, `vol -f citadeldc01.mem windows.info`

![image](https://github.com/user-attachments/assets/4f53e4ce-f8a2-481f-853c-c98688a70b7f)

Key Registry & Memory Values  
| Key                             | Value                  | Meaning |
|---------------------------------|------------------------|---------|
| `NtMajorVersion`               | `6`                    | Major Windows version |
| `NtMinorVersion`               | `3`                    | Minor Windows version |
| `PE MajorOperatingSystemVersion` | `6`                  | PE file OS major version |
| `PE MinorOperatingSystemVersion` | `3`                  | PE file OS minor version |
| `Major/Minor`                   | `15.9600`              | Windows build version |
| `NtProductType`                 | `NtProductLanManNt`    | Indicates a Server OS |

Windows Version Mapping  
Windows versions are identified by **(Major.Minor) version mapping**:

| Major.Minor | Windows Version |
|------------|----------------|
| 6.0        | Windows Vista / Server 2008 |
| 6.1        | Windows 7 / Server 2008 R2 |
| 6.2        | Windows 8 / Server 2012 |
| **6.3**    | **Windows 8.1 / Server 2012 R2** |

Since `NtProductType = NtProductLanManNt`, it confirms this is a **Windows Server** version, specifically **Windows Server 2012 R2**.

***2. What’s the Operating System of the Desktop?***  

**Answer: Windows 10 Enterprise Evaluation**

using FTK imager, extract the software reg hive, then use registry explorer to view

![image](https://github.com/user-attachments/assets/a6a20e0d-3b92-4552-8ff3-2e884b1d3b7e)

SOFTWARE\Microsoft\Windows NT\CurrentVersion

20200918_0417_DESKTOP-SDN1RPT.E01

***3. What was the local time of the Server?***  

**Answer: `Pacific Standard Time`**

![image](https://github.com/user-attachments/assets/86b2ec78-0fbf-4efd-9984-baf6e69338a6)

vol -f citadeldc01.mem windows.registry.printkey --key 'ControlSet001\Control\TimeZoneInformation'

***4. Was there a breach?***  

Yes, for initial analysis from the mem dump

vol -f citadeldc01.mem windows.psscan > psscan.txt

vol -f citadeldc01.mem windows.netscan > netscan.txt

found this IP: 203.78.103.109

![image](https://github.com/user-attachments/assets/832f29c9-a0b2-468e-b0f9-d610f8463b9c)

![image](https://github.com/user-attachments/assets/ed7e9c06-8a7e-481c-8a90-1edf49246d03)

cat netscan.txt | grep -Eiv "dns|0.0.0.0|::" > to remove the noise `-E regex, -i case insensitive, -v invert the match, like do not match

location, vol -f citadeldc01.mem windows.pstree --pid 3644

![image](https://github.com/user-attachments/assets/5b9a7c72-603e-4d05-8177-157542595fb0)

\Windows\System32\coreupdater.exe

i got error on dumping the file

![image](https://github.com/user-attachments/assets/4b8de77c-c510-4e98-afd1-81f1e55b2825)

i cannot find the process with 2244 PID

I use malfind but did not see the 3644 and 2244 process, though I am not fully sure how read the results

vol -f citadeldc01.mem windows.malfind

> research how to read malfind results


***5. What was the initial entry vector (how did they get in)?***  

i am thinking extracting the winevent logs from the disk image or use the pcap provided, lets check the packet capture first

![image](https://github.com/user-attachments/assets/461c9012-4ce4-4472-ac80-7d4ea808e33f)

protocol hier
![image](https://github.com/user-attachments/assets/a3d8ba4e-44a7-4321-a483-40e1a226735d)

top talkers
![image](https://github.com/user-attachments/assets/446a3fbd-2fdb-4dbc-9aff-cec59ef8f54a)

194.61.24.102 > it is from Russia, lets note this. as we know the endpoint is in pacific time - US
![image](https://github.com/user-attachments/assets/e6ba81aa-dba6-402d-9fba-662d12dc741a)

uses port 3389 - rdp

![image](https://github.com/user-attachments/assets/e5674688-11fe-4dd9-beb9-c58bd9aefdc6)

1st packet = ping
![image](https://github.com/user-attachments/assets/309c41d0-06e7-4b3e-b7ea-69f235793f9a)

***6. Was malware used? If so what was it?***  

***7. What process was malicious?***  

***8. Identify the IP Address that delivered the payload.***  

***9. What IP Address is the malware calling to?***  

***10. Where is this malware on disk?***  

***11. When did it first appear?***  

***12. Did someone move it?***  

***13. What were the capabilities of this malware?***  

***14. Is this malware easily obtained?***  

***15. Was this malware installed with persistence on any machine?***  

***16. When?***  

***17. Where?***  

***18. What malicious IP Addresses were involved?***  

***19. Were any IP Addresses from known adversary infrastructure?***  

***20. Are these pieces of adversary infrastructure involved in other attacks around the time of the attack?***  

***21. Did the attacker access any other systems?***  

***22. How?***  

***23. When?***  

***24. Did the attacker steal or access any data?***  

***25. When?***  

***26. What was the network layout of the victim network?***  

***27. What architecture changes should be made immediately?***  

***28. Did the attacker steal the Szechuan sauce? If so, what time?***  

***29. Did the attacker steal or access any other sensitive files? If so, what times?***  

***30. Finally, when was the last known contact with the adversary?***  

### Advanced and Bonus Questions  

***31. What CIS Top 20 or SANS Top 20 Controls would have directly prevented this breach?***  

***32. What major architecture improvement could be made that would have prevented this breach?***  

***33. Can you identify policy improvements or controls that should be implemented to secure this environment?***  

***34. Which users have actually logged onto the DC?***  

***35. Which users have actually logged onto the Desktop machine?***  

***36. What are the passwords for the users in the domain?***  

***37. Can you recover the original file about Beth’s Secrets?***  

***38. What was the original name?***  

***39. Original Contents?***  

***40. Finally, what file was time stomped?***  
