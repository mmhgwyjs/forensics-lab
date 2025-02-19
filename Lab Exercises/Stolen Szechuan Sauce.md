The Case of the Stolen Szechuan Sauce

Scenario: Your bedroom door bursts open, shattering your pleasant dreams. Your mad scientist of a boss begins dragging you out of bed by the ankle. He simultaneously explains between belches that the FBI contacted him. They found his recently-developed Szechuan sauce recipe on the dark web. As you careen past the door frame you are able to grab your incident response “Go-Bag”. Inside is your trusty incident thumb drive and laptop.

Artifacts:
**Domain Controller (DC01) Artifacts:**
1. **[DC01 Memory Dump](https://dfirmadness.com/case001/DC01-memory.zip)**
2. **[DC01 Autoruns](https://dfirmadness.com/case001/DC01-autorunsc.zip)**
3. **[DC01 Protected Files](https://dfirmadness.com/case001/DC01-ProtectedFiles.zip)**

**Network Capture:**
4. **[Case001 PCAP](https://dfirmadness.com/case001/case001-pcap.zip)**

**Desktop Artifacts:**
5. **[Desktop Disk Image (E01)](https://dfirmadness.com/case001/DESKTOP-E01.zip)**
6. **[Desktop Memory Dump](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-memory.zip)**
7. **[Desktop Autoruns](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-autorunsc.zip)**
8. **[Desktop Protected Files](https://dfirmadness.com/case001/DESKTOP-SDN1RPT-Protected%20Files.zip)**


Desktop Protected Files
Reference: [James Smith](https://twitter.com/DFIRmadness) - [The Case of the Stolen Szechuan Sauce](https://dfirmadness.com/the-stolen-szechuan-sauce/) (with explicit permission)



### Questions 

***1. What’s the Operating System of the Server?***  

***2. What’s the Operating System of the Desktop?***  

***3. What was the local time of the Server?***  

***4. Was there a breach?***  

***5. What was the initial entry vector (how did they get in)?***  

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
