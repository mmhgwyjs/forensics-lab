# Forensics Lab

> Please note that this project is ongoing and is meant solely for learning purposes. Your feedback would be greatly appreciated, as I am using this opportunity to learn.

## Objective

To create a space for exploring digital forensics and memory analysis, enabling the investigation of digital evidence. This lab emphasizes hands-on experience with memory analysis techniques and understanding the behavior of digital artifacts in real-world scenarios.

## Initial Setup

For this lab, we will be using the `SIFT Workstation` from SANS.

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
