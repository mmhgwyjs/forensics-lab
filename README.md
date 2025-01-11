# Forensics Lab

> Please note that this project is ongoing and is meant solely for learning purposes. Your feedback would be greatly appreciated, as I am using this opportunity to learn.

## Objective

To create a space for exploring digital forensics and memory analysis, enabling the investigation of digital evidence. This lab emphasizes hands-on experience with memory analysis techniques and understanding the behavior of digital artifacts in real-world scenarios.

## Initial Setup

***1. Installing hypervisor.***
   
- You can use VMware Workstation or VirtualBox, based on your preference. More details [here](https://github.com/mmhgwyjs/homelab?tab=readme-ov-file#hypervisor).

***2. Spinning up a Windows machine.***

- you can check the steps here. https://github.com/mmhgwyjs/windows-lab?tab=readme-ov-file#initial-setup

***3. Enabling Windows Subsystem for Linux (WSL) and Installing Ubuntu.***

for windows server

https://docs.microsoft.com/en-us/windows/wsl/install-on-server

- in powershell, Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
- restart
- download a linux distro: https://learn.microsoft.com/en-us/windows/wsl/install-manual#downloading-distributions
- rename the downloaded .appx then extract it
- run Add-AppxPackage .\app_name.appx
  ![image](https://github.com/user-attachments/assets/4b07aaff-59f3-49d0-bb25-ef2d635077f5)
- run ubuntu, wait for it to be completed
  ![image](https://github.com/user-attachments/assets/245d2e43-02b1-4f60-9e3f-a9e155ec08f7)
- setup username and password

for windows client

- in powershell, dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
- restart
- open microsoft store, search Ubuntu 20.04.6 and Install
  ![image](https://github.com/user-attachments/assets/3b1b59f3-936b-460e-9036-0cad422d34d4)
- Open Ubuntu
  ![image](https://github.com/user-attachments/assets/90390394-1134-4d51-ac4c-69751b29cd5f)
- setup username and password
  ![image](https://github.com/user-attachments/assets/254cfeba-1d2a-470d-87a8-73d2cc5a6841)
- completed
  ![image](https://github.com/user-attachments/assets/53ddfc0c-3cd3-41b3-9295-5756e3f8d38c)

### optional configuration

- set the timezone to UTC
- create custom folders for Tools and artifacts
  ![image](https://github.com/user-attachments/assets/31f6160b-f8eb-442f-9093-08f69f0862c8)
- exclude the created folders in Defender, (Virus & threat protection settings)
  ![image](https://github.com/user-attachments/assets/09f0f6e0-2b5a-48a2-bfb0-a99783f76348)

## Installing Forensic Tools

AIM https://arsenalrecon.com/downloads/
KAPE https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape
EZ Tools https://ericzimmerman.github.io/#!index.md
RegRipper 3.0 https://github.com/keydet89/RegRipper3.0
Event Log Explorer https://eventlogxp.com/
Notepad++ https://notepad-plus-plus.org/

## SIFT Setup (Optional)

We can also use the `SIFT Workstation` from SANS.

> The SIFT Workstation is a collection of free and open-source incident response and forensic tools designed to perform detailed digital forensic examinations in a variety of settings. 

***1. Installing hypervisor.***
   
- You can use VMware Workstation or VirtualBox, based on your preference. More details [here](https://github.com/mmhgwyjs/homelab?tab=readme-ov-file#hypervisor).

***2. Getting SIFT Workstation VM Appliance.***
   
> SIFT Workstation has a prebuilt VM that is readily available for use.

- Go to this [link](https://www.sans.org/tools/sift-workstation/) to download SIFT Workstation.

  > You will need a SANS account to download. Create one if you do not have one yet; it is free.
  
  ![image](https://github.com/user-attachments/assets/8054fb38-024c-4bd1-bb41-4d9a698edc6c)

***3. Installing SIFT Workstation.***

- Open the downloaded OVA file on your hypervisor.

  ![image](https://github.com/user-attachments/assets/487c9a20-aac3-4564-9ce4-999467b4185c)

## Additional Configurations 

***1. Change the default passwords.***

- To update user password, execute the command `passwd`.

***2. Update and upgrade.***

- Use the following commands to update the package list and upgrade installed packages: `sudo apt update` `sudo apt upgrade`.

  > To remove unnecessary packages and free up disk space, use the command `sudo apt autoremove`.
  
***3. Regenerate OpenSSH Host Keys.***

- Delete all the existing files for our SSHD server using the command `sudo /bin/rm -v /etc/ssh/ssh_host_*`.

- Create a new set of keys using the command `sudo dpkg-reconfigure openssh-server`.

- Restart `ssh` service using the command `sudo systemctl restart ssh`.
  
  > Since we are using a prebuilt VM, it is advisable to change the SSH keys for your user. Otherwise, numerous other users might be using the same keys, which could lead to exploitation of your login.

#### ***Great job! We've successfully set up the SIFT Workstation. Now, let us move on to the practical exercises outlined below.***

## Lab Exercises

- Coming soon
