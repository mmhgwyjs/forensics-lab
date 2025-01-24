# Forensics Lab

> Please note that this project is ongoing and is meant solely for learning purposes. Your feedback would be greatly appreciated, as I am using this opportunity to learn.

## Objective

To create a space for exploring digital forensics and memory analysis, enabling the investigation of digital evidence. This lab emphasizes hands-on experience with memory analysis techniques and understanding the behavior of digital artifacts in real-world scenarios.

## Initial Setup

***1. Installing hypervisor.***
   
- You can use VMware Workstation or VirtualBox, based on your preference. More details [here](https://github.com/mmhgwyjs/homelab?tab=readme-ov-file#hypervisor).

***2. Setting Up a Windows Machine***

- Follow the steps outlined here: [Windows Lab Setup Guide](https://github.com/mmhgwyjs/windows-lab?tab=readme-ov-file#initial-setup)

***3. Enabling Windows Subsystem for Linux (WSL) and Installing Ubuntu***

#### For Windows Server:
> For detailed instructions, refer to the official Microsoft guide:  
[Install WSL on Windows Server](https://docs.microsoft.com/en-us/windows/wsl/install-on-server)

- Open PowerShell and run the following command to enable WSL:  
   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
   ```
- Restart the server.

- Download a Linux distribution from the Microsoft Store: [WSL Distro Download](https://learn.microsoft.com/en-us/windows/wsl/install-manual#downloading-distributions)

- Rename the downloaded `.appx` file and extract it.

- Install the extracted package by running:  
   ```powershell
   Add-AppxPackage .\app_name.appx
   ```
   ![image](https://github.com/user-attachments/assets/4b07aaff-59f3-49d0-bb25-ef2d635077f5)

- Run the Ubuntu distribution. Wait for the installation to complete.  
   ![image](https://github.com/user-attachments/assets/245d2e43-02b1-4f60-9e3f-a9e155ec08f7)

- Set up a username and password for Ubuntu.

#### For Windows Client:
- Open PowerShell and run the following command to enable WSL:  
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```
- Restart the machine.

- Open the Microsoft Store, search for **Ubuntu 20.04.6**, and click **Install**:  
   ![image](https://github.com/user-attachments/assets/3b1b59f3-936b-460e-9036-0cad422d34d4)

- Open Ubuntu after installation:  
   ![image](https://github.com/user-attachments/assets/90390394-1134-4d51-ac4c-69751b29cd5f)

- Set up a username and password for Ubuntu:  
   ![image](https://github.com/user-attachments/assets/254cfeba-1d2a-470d-87a8-73d2cc5a6841)

- You’re all set! The installation is complete:  
   ![image](https://github.com/user-attachments/assets/53ddfc0c-3cd3-41b3-9295-5756e3f8d38c)

## Addtional Configurations

***1. Set the Timezone to UTC***  
- Change the system timezone to UTC for consistency and compatibility across environments.

***2. Create Custom Folders for Tools and Artifacts***
- Organize your system by creating dedicated folders for tools and artifacts:
  
  ![image](https://github.com/user-attachments/assets/31f6160b-f8eb-442f-9093-08f69f0862c8)

***3. Exclude the Created Folders in Windows Defender***  
- To prevent Defender from scanning your custom folders, exclude them in the **Virus & Threat Protection settings**:
  
  ![image](https://github.com/user-attachments/assets/09f0f6e0-2b5a-48a2-bfb0-a99783f76348)

## Installing Forensic Tools

- **AIM (Arsenal Image Mounter)**: A tool for mounting forensic images.  
  [Download AIM](https://arsenalrecon.com/downloads/)

- **KAPE (Kroll Artifact Parser and Extractor)**: A powerful tool for rapid collection and parsing of forensic artifacts.  
  [Download KAPE](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape)

- **EZ Tools (Eric Zimmerman's Tools)**: A collection of tools for digital forensics analysis, including extraction and parsing utilities.  
  [Access EZ Tools](https://ericzimmerman.github.io/#!index.md)

- **RegRipper 3.0**: A tool for extracting and analyzing registry data in forensic investigations.  
  [Download RegRipper 3.0](https://github.com/keydet89/RegRipper3.0)

- **Event Log Explorer**: A tool for exploring and analyzing Windows event logs.  
  [Download Event Log Explorer](https://eventlogxp.com/)

- **Notepad++**: A text editor widely used for viewing and editing log files and scripts.  
  [Download Notepad++](https://notepad-plus-plus.org/)

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

## Additional Configurations (SIFT)

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

| Exercise                          | Description                                                                                     | Link                                                                                       | Status       |
|-----------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------|
| Installing Volatility3            | Install and set up Volatility3 for memory forensics, including dependencies and usage basics.    | [View Exercise](https://github.com/mmhgwyjs/forensics-lab/blob/main/Lab%20Exercises/Volatility.md)                                                                         | In Progress  |
