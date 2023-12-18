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
	  - [Firewall](#uncomplicated-firewall)
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

- Update Windows
- Open Control Panel
- Enable Firewall
- Disable Remote Assistance
- Remove Unwanted Software
	> Examples of unwanted software are PC Cleaner, Wireshark, Net Stumbler, and Ophcrack
  1. Navigate to `Control Panel>Programs>Programs and Features`

	![Uninstaller Menu](images/uninstall_menu.png "Uninstall Menu")

  2. Right click on the unwanted software and select "Uninstall"
  3. Follow the steps of the uninstaller and remove everything

### Managing Users in Windows

- **Open User Manager**
	1. Win + R 
	2. Type `lusrmgr.msc`

  ![Open User Manager](images/lusrmgr.png "lusrmgr.msc")

  3. Press enter
	4. Open Users

  ![User Manager](images/usermanager.png "User Manager")
	![Users](images/usermanagerusers.png "Users")

- **Add User**
	1. Right click in the middle of the window
  2. Select new user

  ![User Selection](images/select_new.png "Select New User")

  4. Give a username and password
  5. Ensure the "User must change password at next logon" box is checked
  
	![User Creation](images/user_create.png "Create User")

- **Delete User**
	1. Right click on an existing user
  2. Select delete

	![User Deletion](images/select_delete.png "Delete User")

	3. Select "yes" on the dialogue box

	![Confirm Deletion](images/placehold.png "Confirm Delete")

- **Change User Password**
	1. Right click on existing user
  2. Select set password

	![Set Password](images/)

- **Create Group**
	> Nearly identical to user creation
	1. Open the "Groups" tab of the user manager

	![Group Manager](images/usermanagergroup.png "Manage Groups")

	2. Right click in the middle of the window
  3. Select new group

	![Group Selection](images/select_new_group.png "Select New Group")

	4. Add group name

  ![Group Creation](images/group_create.png "Create Group")

	5. To add users right away follow the steps in **Add User to Group**
  6. Select "Create" to create the group

- **Add User to Group**  
	> :bulb: Can be used to add user to group "Administrators"
- **Remove User from Group**
	> :bulb: Can be used to remove user from group "Administrators"

### Security Policies

- **Open Security Policy Manager**
	1. Win + R 
	2. Type `secpol.msc`
	
	![Open Security Policy Manager](images/secpol.png "secpol.msc")
	
	3. Press enter

- **Set Secure Password Settings**
- **Set Password Lockout**
- **Limit Local Use of Blank Passwords to Console**
- **Disable Anonymous Enumeration of SAM Accounts**

## Windows Server
> :page_with_curl: WIP

## Ubuntu 22

> :page_with_curl: Currently, not *every* action that we need to perform in Ubuntu is documented using terminal commands (GUI is used instead). If you discover a command alternative please take note of it so it can be added to the documentation.

> :page_with_curl: Make sure to replace anything wrapped in `<these angle brackets>` with what you need. Ex. `<username>` change to `linda`. 

> :page_with_curl: Any time you use `sudo` you will be prompted for a password. Your password can be found in the README. Remember, Linux doesn't show passwords as you type them!


### Managing Users in Ubuntu
- **Removing a User**
	1. In the terminal, run: `sudo deluser --remove-home <username>`
- **Removing a User and Backing Up Their Files**
  1. In the terminal, run: `sudo mkdir /oldusers-data`
  2. In the terminal, run: `sudo chown root:root /oldusers-data`
  3. In the terminal, run: `sudo chmod 0700 /oldusers-data`
  4. In the terminal, run: `sudo deluser -remove-home -backup-to /oldusers-data`
- **Disable a User**
  1. In the terminal, run: `sudo usermod -L <username>`
- **Make User an Administrator**
  1. In the terminal, run: `sudo usermod –aG sudo <username>`
- **Remove Administrator Privilege**
  1. In the terminal, run: `sudo deluser <username> sudo`
- **Change Another User's Password**
  1. In the terminal, run: `sudo passwd <username>`
  2. Follow the prompts
> :page_with_curl: Remember, Linux does **not** display passwords as you type them.
- **Add User to Group**
  1. In the terminal, run: `sudo gpasswd –a <username> <group-name>`

### Passwords
- **Defining Minimum Password Requirements**
	1. In the terminal, run: `sudo nano /etc/pam.d/common-password`
  2. In the file, look for the line that contains `password requisite`
  3. Replace that line with `password requisite pam_cracklib.so retry=3 minlen=10 difok=3 ucredit=-1 lcredit=-1 dcredit=-1  ocredit=-1`
  4. Press CRTL + X to save and exit
- **Change Password Age Rules**
  1. In the terminal, run: `sudo nano /etc/login.defs`
  2. Look for the lines `PASS_MAX_DAYS`, `PASS_MIN_DAYS`, and `PASS_WARN_AGE`
  3. Edit the values to be something like the following: `PASS_MAX_DAYS   99999`, `PASS_MIN_DAYS   0`, and `PASS_WARN_AGE   7`
  4. Press CRTL + X to save and exit
- **Remember 5 Previous Passwords**
  1. In the terminal, run: `sudo nano /etc/pam.d/common-password`
  2. Look for the line that contains `password required`
  3. Replace the end of the line with `pam_unix.so remember=5` 

### Uncomplicated Firewall
- **Check status of ufw**
  1. In the terminal, run: `sudo ufw status`
  > :bulb: You can use this to verify whether ufw is installed, based on if the command is recognized.
- **Enable ufw \(ufw\)**
  1. In the terminal, run: `sudo ufw enable`
- **Allow ssh through ufw**
  1. In the terminal, run: `sudo ufw allow ssh`
  > :page_with_curl: Only do this if ssh is a critical service in the specifications and that it is written explicity that you should allow ssh through ufw.

### Services in Ubuntu
- **List Running Services**
	1. In the terminal, run: `systemctl list-units --type=service --state=active`
  > :bulb: You can use this to search for any suspect services or services you *thought* you turned off.
- **Stop a Service**
  1. In the terminal, run: `sudo systemctl stop <service-name>`
- **Start a Service**
1. In the terminal, run: `sudo systemctl start <service-name>`
- **Restart a Service**
1. In the terminal, run: `sudo systemctl restart <service-name>`
- **Disable a Service**
1. In the terminal, run: `sudo systemctl disable <service-name>`

### Locking Down
- **Fix Disabled sudo Authentication**
	> :bulb: If you've been running sudo commands, but you aren't being prompted for a password, sudo authentication is *probably* disabled. :smiley:
  1. In the terminal, run: `sudo nano /etc/sudoers`
  2. Search for the line `Defaults !authenticate`
  3. Remove the `!`
  4. Press CRTL + X to save and exit
- **Disable Root Login From ssh**
  1. In the terminal, run: `sudo nano /etc/ssh/shhd_config`
  2. Look for `PermitRootLogin`
  3. Change `yes` to `no`
  4. Press CRTL + X to save and exit
- **Disable ipv4 Port Forwarding**
  1. In the terminal, run: `sudo nano /etc/sysctl.conf`
  2. Change the line `net.ipv4.ip_forward=1` to `net.ipv4.ip_forward=0`
  3. Press CRTL + X to save and exit
- **Fix Insecure Permissions on Shadow File**
  1. In the terminal, run: `sudo chmod 0640 /etc/shadow`
- **Turn Off Remote Desktop**
  > Need photos here!

### General Maintenance in Ubuntu
- **Automatically Check for Updates**
	> Need photos here!
- **Update Software**
  1. In the terminal, run: `sudo apt update`
- **Find Directory Containing Files of Type**
  1. In the terminal, run: `locate *<file-extenstion>`, for example: `locate *.mp3`
- **Delete Individual Files of Type**
  1. In the terminal, run: `sudo find . -type f -name "*<file-extension>" -exec rm -i {} \;`
  2. You will be prompted to delete each file that is found, type `y` to delete or `n` to keep it
- **Delete All Files of Type From a Directory**
  1. In the terminal, run: `sudo rm /home/<directory>/*.mp3`
- **Remove Unwanted Software**
  1. In the terminal, run: `sudo apt remove <package-name>`




## Debian

> :page_with_curl: Uses the same commands as [Ubuntu](#ubuntu-22) but the GUI is much more limited.

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

