
## 6 System Maintenance
### 1 
1. Ensure permissions on /etc/passwd are configured (Automated) 
 #### Description: 
Run the following command and verify Uid and Gid are both 0/root and Access is 644:
```
# stat /etc/passwd
```
```
Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```
#### Remediation:  

Run the following command to set permissions on /etc/passwd:
```
# chown root:root /etc/passwd
# chmod u-x,go-wx /etc/passwd
```

2. Ensure permissions on /etc/passwd- are configured (Automated)   

#### Description:   
The /etc/passwd- file contains backup user account information.   
#### Rationale:   
It is critical to ensure that the /etc/passwd- file is protected from unauthorized access.    
Although it is protected by default, the file permissions could be changed either 
inadvertently or through malicious actions.   
#### Audit:
Run the following command and verify Uid and Gid are both 0/root and Access is 644 or more restrictive:
```
# stat /etc/passwdAccess: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```
Remediation:  
Run the following command to set permissions on /etc/passwd- :
```
# chown root:root /etc/passwd-
# chmod u-x,go-wx /etc/passwd-
```

3. Ensure permissions on /etc/group are configured 
(Automated)   
#### Description:
The /etc/group file contains a list of all the valid groups defined in the system.   
The command below allows read/write access for root and read access for everyone else.   
#### Rationale:
The /etc/group file needs to be protected from unauthorized changes by non-privileged 
users, but needs to be readable as this information is used with many non-privileged 
programs.
#### Audit:
Run the following command and verify Uid and Gid are both 0/root and Access is 644 :
```
# stat /etc/group
Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```
#### Remediation:
Run the following command to set permissions on /etc/group :
```
# chown root:root /etc/group
# chmod u-x,go-wx /etc/group
```
4. Ensure permissions on /etc/group- are configured 
(Automated)  
#### Description:
The /etc/group- file contains a backup list of all the valid groups defined in the system.
#### Rationale:
It is critical to ensure that the /etc/group- file is protected from unauthorized access.   
Although it is protected by default, the file permissions could be changed either 
inadvertently or through malicious actions.
#### Audit:
Run the following command and verify Uid and Gid are both 0/root and Access is 644 or 
more restrictive:
```
# stat /etc/groupAccess: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```
#### Remediation:
Run the following command to set permissions on /etc/group- :
```
# chown root:root /etc/group-
# chmod u-x,go-wx /etc/group-
```

5. Ensure permissions on /etc/shadow are configured 
(Automated)  
#### Description:
The /etc/shadow file is used to store the information about user accounts that is critical 
to the security of those accounts, such as the hashed password and other security 
information.  
#### Rationale:
If attackers can gain read access to the /etc/shadow file, they can easily run a 
password cracking program against the hashed password to break it.   Other security 
information that is stored in the /etc/shadow file (such as expiration) could also be 
useful to subvert the user accounts.
#### Audit:
Run the following command and verify verify Uid is 0/root, Gid is 0/root or 
\<gid>/shadow, and Access is 640 or more restrictive:
```
# stat /etc/shadow

Access: (0640/-rw-r-----) Uid: ( 0/ root) Gid: ( 0/ root)
```
#### Remediation:
Run one of the following commands to set ownership of /etc/shadow to root and group 
to either root or shadow:
```
# chown root:root /etc/shadow
# chown root:shadow /etc/shadow
```
Run the following command to remove excess permissions form /etc/shadow:
```
# chmod u-x,g-wx,o-rwx /etc/shadow
```

### 2

### 3
 