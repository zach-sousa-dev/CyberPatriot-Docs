# STEAM Academy CyberPatriot Documentation

## Contents

- [Virtual Machines](#virtual-machines)
	- [Getting Started with the VMs](#getting-started-with-the-vms)
  - [Windows 10](#windows-10)
	  - [General Security](#general-security)
	  - [User Management](#managing-users-in-windows)
    - [Security Policies](#security-policies)
  - [Windows Server](#windows-server)
  - [Ubuntu 22](#ubuntu-22)
	  - [User Management](#managing-users-in-ubuntu)
	  - [Firewall](#uncomplicated-firewall-\(ufw\))
    - [Services](#services-in-ubuntu)
    - [General Maintenance](#general-maintenance-in-ubuntu)
  - [Debian](#debian)
- [Packet Tracer](#packet-tracer)
	- [Getting Started with PT](#getting-started-with-pt)
- [Net Academy Quiz](#net-academy-quiz)
	- [How to Complete the Quiz](#how-to-complete-the-quiz)


# Virtual Machines

### Getting Started with the VMs

1. Where to download VM images
2. Loading the images into VMware
>:warning: **DO NOT HAVE TWO INSTANCES OF ONE IMAGE OPEN SIMULTANEOUSLY** :warning:
3. Entering the UID
4. Understanding the README, scoring sheet, and forensics questions
5. Stop scoring
>:warning: **DELETE THE IMAGE WHEN YOU ARE DONE** :warning:

## Windows 10

### General Security

- Open Control Panel
- Enable Firewall
- Update Windows

### Managing Users in Windows

- **Open User Manager**
	1. Win + R 
	2. Type `lusrmgr.msc`
  ![Open User Manager](images/lusrmgr.png "lusrmgr.msc")
  4. Press enter
	5. Open Users
  ![User Manager](images/usermanager.png "User Manager")
	![Users](images/usermanagerusers.png "Users")

- **Add User**
- **Delete User**
- **Create Group**
- **Add User to Group**
- **Remove User from Group**
- **Open Control Panel**
- **Change User Password**

### Security Policies

- **Open Security Policy Manager**
- **Set Secure Password Settings**
- **Set Password Lockout**
- **Limit Local Use of Blank Passwords to Console**
- **Disable Anonymous Enumeration of SAM Accounts**

## Windows Server
> WIP

## Ubuntu 22

> :trollface:

### Managing Users in Ubuntu
- **Removing a User**
	1. In the terminal, run: `sudo deluser -- remove-home <username>`
- **Removing a User and Backing Up Their Files**
  1. In the terminal, run: `sudo mkdir /oldusers-data`
  2. In the terminal, run: `sudo chown root:root /oldusers-data`
  3. In the terminal, run: `sudo chmod 0700 /oldusers-data`
  4. In the terminal, run: `sudo deluser -remove-home -backup-to /oldusers-data`
- **Make User an Administrator**
- **Remove Administrator Privilege**
- **Change Another User's Password**
- **Add User to Group**

### Uncomplicated Firewall \(ufw\)
- **Check status of ufw**
- **Enable ufw \(ufw\)**
- **Allow ssh through ufw**

### Services in Ubuntu
- **List Running Services**
- **Stop a Service**

### General Maintenance in Ubuntu
- **Automatically Check for Updates**
- **Update Software**
- **Remove Files of Type**
- **Remove Unwanted Software**




## Debian

> Uses the same commands as [Ubuntu](#ubuntu-22) but the GUI is much more limited.

---

# Packet Tracer

### Getting Started with PT

1. Logging into Net Academy
2. Downloading the project
3. Opening the project
4. Brief tour
5. Saving and submitting the project

# Net Academy Quiz

### How to Complete the Quiz

1. Logging into Net Academy
2. Opening the quiz
3. Answering the questions
4. Submitting the quiz

