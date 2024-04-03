# Windows 10

## Contents

### Other Pages
- [Main Page](README.md)
- [Windows Server](Server.md)
- [Ubuntu](Ubuntu.md)
- [Debian](Debian.md)

### Sub Headings
- [General Security](#general-security)
	- [Update Windows](#update-windows)
  - [Set Security Settings](#set-security-settings)
  - [Open Control Panel](#open-control-panel)
  - [Enable Firewall](#enable-firewall)
  - [Disable Remote Assistance](#disable-remote-assistance)
  - [Remove Unwanted Software](#remove-unwanted-software)
- [User Management](#managing-users)
	- [Open User Manager](#open-user-manager)
  - [Add User](#add-user)
  - [Delete User](#delete-user)
  - [Change Password](#change-user-password)
  - [Create Group](#create-group)
  - [Add User to Group](#add-user-to-group)
  - [Remove User from Group](#remove-user-from-group)
  - [Delete Group](#delete-group)
- [Security Policies](#security-policies)
	- [Open Security Policy Manager](#open-security-policy-manager)
  - [Secure Password Settings](#set-secure-password-settings)
  - [Set Password Lockout](#set-password-lockout)
  - [Limit Blank Passwords](#limit-local-use-of-blank-passwords-to-console-only)
  - [Disable Anonymous Enumeration of SAM Accounts](#disable-anonymous-enumeration-of-sam-accounts)

## 1. Account wPolicies 
### 1.1 Password Policies
#### 1.1.1 (L1) Ensure 'Enforce password history' is set to '24 or more password(s)' (Automated)
``` 
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Enforce password history 
``` 
Setting: 24  
Links:  [1](https://www.cisecurity.org/white-papers/cis-password-policy-guide/),
[2](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/password-policy)
<br></br>



#### 1.1.2 (L1) Ensure 'Maximum password age' is set to '365 or fewer days, but not 0' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Maximum password age
```

Setting: 42  
Links:  [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide), 
[2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br></br>

#### 1.1.3 (L1) Ensure 'Minimum password age' is set to '1 or more day(s)' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Minimum password age
```
Setting: 1      
Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide),
[2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br></br>


#### 1.1.4 (L1) Ensure 'Minimum password length' is set to '14 or more character(s)' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Minimum password length
```
Setting: 7  
Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide),
[2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br></br>


#### 1.1.5 (L1) Ensure 'Password must meet complexity requirements' is set to 'Enabled' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Password must meet complexity requirements
```
Setting: Not contain the user's account name, have at least six characters in length, contain characters that are uppercase, lowercase, base 10 digits (0 through 9), non-alphabetic characters(i.e. !,$,#,%)  
Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide),
[2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br><br>
## 17. Advanced Audit Policy Configuration
### 17.1. Account Logon
#### 17.1.1.  Ensure 'Audit Credential Validation' is set to 'Success 
and Failure' (Automated)

<br></br>
  



---

## Windows Defender Firewall with Advanced Security

### Private Profile

### (L1) Ensure 'Windows Firewall: Private: Firewall state' is set to 'On (recommended)' (Automated)
<br></br>
It's reccomended that Windows Defender Firewall is on. Simply type "Windows defender firewall with advanced security" Then turn it on.

To turn the Windows Defender Firewall With Advanced Security on search up group policy, Computer configuration , then Windows Settings, Security Settings, Windows Defender Firewall, click the drop down arrow go into Windows Defender Firewall With Advanced Security, Windows Firewall Properties, Private Profile, Firewall state.

<br></br>

### How to turn on firewall in enterprise version of windows


 Computer Configuration\Policies\Windows Settings\Security Settings\Windows 
Defender Firewall with Advanced Security\Windows Defender Firewall with 
Advanced Security\Windows Firewall Properties\Private Profile\Firewall state

### Ensure 'Windows Firewall: Private: Inbound connections' is set to 'Block (default)' (Automated)

<br></br>

Computer Configuration\Policies\Windows Settings\Security Settings\Windows 
Defender Firewall with Advanced Security\Windows Defender Firewall with 
Advanced Security\Windows Firewall Properties\Private Profile\Inbound 
connections


Set it to ***Block(Default)***


### (L1) Ensure 'Windows Firewall: Private: Outbound connections' is set to 'Allow (default)' (Automated)
<br></br>

Computer Configuration\Policies\Windows Settings\Security Settings\Windows 
Defender Firewall with Advanced Security\Windows Defender Firewall with 
Advanced Security\Windows Firewall Properties\Private Profile\Outbound 
connections

This should be set to ***Allow(Defautlt)***

###  Ensure 'Windows Firewall: Private: Settings: Display a notification' is set to 'No' (Automated)

Computer Configuration\Policies\Windows Settings\Security Settings\Windows 
Defender Firewall with Advanced Security\Windows Defender Firewall with 
Advanced Security\Windows Firewall Properties\Private Profile\Settings 
Customize\Display a notification

This setting should be set to ***No***


#### 1.1.6 (L1) Ensure 'Relax minimum password length limits' is set to 'Enabled' (Automated)
```
Audit: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SAM:RelaxMinimumPasswordL
engthLimits

Remediation: Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Relax minimum password length limits
```
Setting: minimum password length can be configured to a max of 14 chars

Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide), 
[2](https://support.microsoft.com/en-us/topic/minimum-password-length-auditing-and-enforcement-on-certain-versions-of-windows-5ef7fecf-3325-f56b-cc10-4fd565aacc59),  [3](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br></br>

#### 1.1.7 (L1) Ensure 'Store passwords using reversible encryption' is set to 'Disabled' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Password Policy\Store passwords using reversible encryption
```
Setting: Disabled     
Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide), [2](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-policy)
<br></br>

## 1.2 Account Lockout Policy
#### 1.2.1 (L1) Ensure 'Account lockout duration' is set to '15 or more minute(s)' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Account Lockout Policy\Account lockout duration
```
Setting: None, because this policy setting only has meaning if the account lockout threshold is specified    
Link: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)
<br></br>

#### 1.2.2 (L1) Ensure 'Account lockout threshold' is set to '5 or fewer invalid logon attempt(s), but not 0' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Account Lockout Policy\Account lockout threshold
```
Setting: 0 failed logon attempts    
Link: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)
<br></br>

#### 1.2.3 (L1) Ensure 'Allow Administrator account lockout' is set to 'Enabled' (Manual)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Account Lockout Policies\Allow Administrator account lockout
```
Setting: Disabled   
Link: [1](https://support.microsoft.com/en-us/topic/kb5020282-account-lockout-available-for-built-in-local-administrators-bce45c4d-f28d-43ad-b6fe-70156cb2dc00)
<br></br>

#### 1.2.4 (L1) Ensure 'Reset account lockout counter after' is set to '15 or more minute(s)' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Account 
Policies\Account Lockout Policy\Reset account lockout counter after
```
Setting: None, because this policy setting only has meaning if the account lockout threshold is specified   
Link: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)
<br></br>

## 2. Local Policies
### 2.1 Audit Policy (this is left blank and exists to ensure the structure of Windows benchmarks is consistent.)
#### 2.2.1 (L1) Ensure 'Access Credential Manager as a trusted caller' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Access Credential Manager as a trusted caller
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/access-credential-manager-as-a-trusted-caller)
<br></br>

#### 2.2.2 (L1) Ensure 'Access this computer from the network' is set to 'Administrators, Remote Desktop Users' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Access this computer from the network
```
Setting: Administrators, backup operators, everyone, users    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/access-credential-manager-as-a-trusted-caller)
<br></br>

#### 2.2.3 (L1) Ensure 'Act as part of the operating system' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Act as part of the operating system
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/act-as-part-of-the-operating-system)
<br></br>

#### 2.2.4 (L1) Ensure 'Adjust memory quotas for a process' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Adjust memory quotas for a process
```
Setting: Administrators, LOCAL SERVICE, NETWORK SERVICE   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process)
<br></br>

#### 2.2.5 (L1) Ensure 'Allow log on locally' is set to 'Administrators, Users' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Allow log on locally
```
Setting: Administrators, backup operators, guest, users   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/allow-log-on-locally)
<br></br>

#### 2.2.6 (L1) Ensure 'Allow log on through Remote Desktop Services' is set to 'Administrators, Remote Desktop Users' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Allow log on through Remote Desktop Services
```
Setting: Administrators, remote desktop users   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/allow-log-on-through-remote-desktop-services)
<br></br>

#### 2.2.7 (L1) Ensure 'Back up files and directories' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Back up files and directories
```
Setting: Administrators, backup operators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/back-up-files-and-directories)
<br></br>

#### 2.2.8 (L1) Ensure 'Change the system time' is set to 'Administrators, LOCAL SERVICE' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Change the system time
```
Setting: Administrators, LOCAL SERVICE    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/change-the-system-time)
<br></br>

#### 2.2.9 (L1) Ensure 'Change the time zone' is set to 'Administrators, LOCAL SERVICE, Users' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Change the time zone
```
Setting: Administrators, LOCAL SERVICE, users   
Link: [1](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/change-the-time-zone)
<br></br>

#### 2.2.10 (L1) Ensure 'Create a pagefile' is set to 'Administrators' (Automated)
```
2.2.10 (L1) Ensure 'Create a pagefile' is set to 'Administrators' 
(Automated
```
Setting: Administrators   
Link: [1](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-a-pagefile)
<br></br>

#### 2.2.11 (L1) Ensure 'Create a token object' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Create a token object
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/create-a-token-object)
<br></br>

#### 2.2.12 (L1) Ensure 'Create global objects' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE' (Automated)
```
2.2.12 (L1) Ensure 'Create global objects' is set to 'Administrators, 
LOCAL SERVICE, NETWORK SERVICE, SERVICE' (Automated
```
Setting: Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/create-global-objects)
<br></br>

#### 2.2.13 (L1) Ensure 'Create permanent shared objects' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Create permanent shared objects
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/create-permanent-shared-objects)
<br></br>

#### 2.2.14 (L1) Configure 'Create symbolic links' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Create symbolic links
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/create-symbolic-links)
<br></br>

#### 2.2.15 (L1) Ensure 'Debug programs' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Debug programs
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/debug-programs)
<br></br>

#### 2.2.16 (L1) Ensure 'Deny access to this computer from the network' to include 'Guests' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Deny access to this computer from the network
```
Setting: Guest    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/deny-access-to-this-computer-from-the-network)
<br></br>

#### 2.2.17 (L1) Ensure 'Deny log on as a batch job' to include 'Guests' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Deny log on as a batch job
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/deny-log-on-as-a-batch-job)
<br></br>

#### 2.2.18 (L1) Ensure 'Deny log on as a service' to include 'Guests' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Deny log on as a service
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/deny-log-on-as-a-service)
<br></br>

#### 2.2.19 (L1) Ensure 'Deny log on locally' to include 'Guests' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Deny log on locally
```
Setting: Guest    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/deny-log-on-locally)
<br></br>

#### 2.2.20 (L1) Ensure 'Deny log on through Remote Desktop Services' to include 'Guests' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Deny log on through Remote Desktop Services
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/deny-log-on-through-remote-desktop-services)
<br></br>

#### 2.2.21 (L1) Ensure 'Enable computer and user accounts to be trusted for delegation' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Enable computer and user accounts to be trusted for delegation
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/enable-computer-and-user-accounts-to-be-trusted-for-delegation)
<br></br>

#### 2.2.22 (L1) Ensure 'Force shutdown from a remote system' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Force shutdown from a remote system
```
Setting: Administrators   
Link: [1](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/force-shutdown-from-a-remote-system)
<br></br>

#### 2.2.23 (L1) Ensure 'Generate security audits' is set to 'LOCAL SERVICE, NETWORK SERVICE' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Generate security audits
```
Setting: LOCAL SERVICE, NETWORK SERVICE   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/generate-security-audits)
<br></br>

#### 2.2.24 (L1) Ensure 'Impersonate a client after authentication' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Impersonate a client after authentication
```
Setting: Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/impersonate-a-client-after-authentication)
<br></br>

#### 2.2.25 (L1) Ensure 'Increase scheduling priority' is set to 'Administrators, Window Manager\Window Manager Group' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Increase scheduling priority
```
Setting: On Windows 10 R1607 or older: Administrators
On Windows 10 R1703 or newer: Administators, Window Manager/Window Manager Group    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/increase-scheduling-priority)
<br></br>

#### 2.2.26 (L1) Ensure 'Load and unload device drivers' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Load and unload device drivers
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/load-and-unload-device-drivers)
<br></br>

#### 2.2.27 (L1) Ensure 'Lock pages in memory' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Lock pages in memory
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/lock-pages-in-memory)
<br></br>

#### 2.2.28 (L2) Ensure 'Log on as a batch job' is set to 'Administrators' (Automated)
```
Computer Configuration\Windows Settings\Security Settings\Local Policies\User 
Rights Assignment\Log on as a batch job
```
Setting: Administrators, backup operators, performance log users    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/log-on-as-a-batch-job)
<br></br>

#### 2.2.29 (L2) Configure 'Log on as a service' (Automated)
```
Computer Configuration\Windows Settings\Security Settings\Local Policies\User 
Rights Assignment\Log on as a service
```
Setting: NT SERVICE\ALL SERVICES    
Link:[1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/log-on-as-a-batch-job), [2](https://learn.microsoft.com/en-us/windows/security/application-security/application-isolation/microsoft-defender-application-guard/faq-md-app-guard#what-is-the-wdagutilityaccount-local-account-)
<br></br>

#### 2.2.30 (L1) Ensure 'Manage auditing and security log' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Manage auditing and security log
``` 
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/manage-auditing-and-security-log)
<br></br>

#### 2.2.31 (L1) Ensure 'Modify an object label' is set to 'No One' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Modify an object label
```
Setting: No one   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/modify-an-object-label)
<br></br>

#### 2.2.32 (L1) Ensure 'Modify firmware environment values' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Modify firmware environment values
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/modify-firmware-environment-values)
<br></br>

#### 2.2.33 (L1) Ensure 'Perform volume maintenance tasks' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Perform volume maintenance tasks
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/perform-volume-maintenance-tasks)
<br></br>

#### 2.2.34 (L1) Ensure 'Profile single process' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Profile single process
```
Setting: Administrators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/profile-single-process)
<br></br>

#### 2.2.35 (L1) Ensure 'Profile system performance' is set to 'Administrators, NT SERVICE\WdiServiceHost' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Profile system performance
```
Setting: Windows 7 or newer, NT SERVICE\WdiServiceHost
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/profile-system-performance)
<br></br>

#### 2.2.36 (L1) Ensure 'Replace a process level token' is set to 'LOCAL SERVICE, NETWORK SERVICE' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Replace a process level token
```
Setting: LOCAL SERVICE, NETWORK SERVICE   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/replace-a-process-level-token)
<br></br>

#### 2.2.37 (L1) Ensure 'Restore files and directories' is set to 'Administrators' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Restore files and directories
```
Setting: Administrators, backup operators   
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/restore-files-and-directories)
<br></br>

#### 2.2.38 (L1) Ensure 'Shut down the system' is set to 'Administrators, Users' (Automated)
```
Computer Configuration\Policies\Windows Settings\Security Settings\Local 
Policies\User Rights Assignment\Shut down the system
```
Setting: Administrators, backup operators, users    
Link: [1](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/shut-down-the-system)
<br></br>


## General Security

#### Update Windows

1. Open Windows settings
2. Navigate to update and security

![Windows Settings](images/windows/windows_settings.png "Windows Settings")
![Windows Update](images/windows/windows_update.png "Windows Update")

4. Check for updates
5. Select "Install now"

![Install Updates](images/windows/install_updates.png "Install Updates")

6. When prompted restart the computer

#### Set Security Settings

1. Open Windows settings
2. Navigate to update and security

![Windows Settings](images/windows/windows_settings.png "Windows Settings")

3. Select Windows Security

![Windows Update](images/windows/windows_security.png "Windows Security")

4. If any red exclaimation marks appear select the section and resolve the issue

> The section requiring a Microsoft Login is unnecessary

![Security Menu](images/windows/security_menu.png "Security Menu")

#### Open Control Panel

1. Win + R
2. Type `control`

![Open Control Panel](images/windows/control.png "Open Control Panel")

3. Press Enter

#### Enable Firewall

1. Navigate to `Control Panel>System and Security>Windows Defender Firewall`
2. Select `Turn Windows Defender on or off`

![Open Firewall Settings](images/windows/firewall_control.png "Open Firewall Settings")

3. Turn both firewalls on

![Enable Firewall](images/windows/firewall_final.png "Enable Firewall")

#### Disable Remote Assistance

1. Navigate to `Control Panel>System and Security`
2. Select `Allow remote access` under `System`

![System Settings](images/windows/system.png "System Settings")

3. Uncheck "Allow Remote Assistance connections to this computer"

![Disable Remote](images/windows/disable_remote.png "Disable Remote Connections")

4. Select "Apply"

#### Remove Unwanted Software

> :bulb: Examples of unwanted software are PC Cleaner, Wireshark, Net Stumbler, and Ophcrack
1. Navigate to `Control Panel>Programs>Programs and Features`

![Uninstaller Menu](images/windows/uninstall_menu.png "Uninstall Menu")

2. Right click on the unwanted software and select "Uninstall"
3. Follow the steps of the uninstaller and remove everything

## Managing Users

#### Open User Manager

1. Win + R 
2. Type `lusrmgr.msc`

![Open User Manager](images/windows/lusrmgr.png "lusrmgr.msc")

3. Press enter
4. Open Users

![User Manager](images/windows/usermanager.png "User Manager")
![Users](images/windows/usermanagerusers.png "Users")

#### Add User

1. Right click in the middle of the window
2. Select new user

![User Selection](images/windows/select_new.png "Select New User")

4. Give a username and password
5. Ensure the "User must change password at next logon" box is checked

![User Creation](images/windows/user_create.png "Create User")

#### Delete User

1. Right click on an existing user
2. Select delete

![User Deletion](images/windows/select_delete.png "Delete User")

3. Select "yes" on the dialogue box

![Confirm Deletion](images/windows/confirm_delete.png "Confirm Delete")

#### Change User Password

1. Right click on existing user
2. Select set password

![Set Password](images/windows/set_password.png "Set Password")

3. Select "Proceed" on the popup

![Proceed to Password](images/windows/confirm_change.png "Proceed")

4. Enter a new password and select "OK"

![New Password](images/windows/change_password.png "Enter New Password")

#### Create Group
 
> :page_with_curl: Nearly identical to user creation
1. Open the "Groups" tab of the user manager

![Group Manager](images/windows/usermanagergroup.png "Manage Groups")

2. Right click in the middle of the window
3. Select new group

![Group Selection](images/windows/select_new_group.png "Select New Group")

4. Add group name

![Group Creation](images/windows/group_create.png "Create Group")

5. To add users right away follow the steps in **Add User to Group**
6. Select "Create" to create the group

#### Add User to Group

> :bulb: Can be used to add user to group "Administrators"

1. Double click on the group to open it
2. Select "Add"

![Group Edit Menu](images/windows/group_menu.png "Group Edit Menu")

3. Type the username in the text field
4. select "OK"

![Add User](images/windows/add_user.png "Add User To Group")

5. The Group should now populate with the created user

![Updated Group Menu](images/windows/add_group_menu.png "Updated Group Menu")

#### Remove User from Group

> :bulb: Can be used to remove user from group "Administrators"

1. Double click on the group to open it
2. Select the user you want to remove
3. Select "Remove"

![Remove User From Group](images/windows/remove_group_menu.png "Select The User")

#### Delete Group

1. Right click on the desired group
2. Select "Delete"

![Delete Group](images/windows/delete_group.png "Select Delete")

3. Select "Yes" on the popup

![Confirm Delete](images/windows/confirm_delete_group.png "Confirm Deletion")

## Security Policies

#### Open Security Policy Manager
	
1. Win + R 
2. Type `secpol.msc`

![Open Security Policy Manager](images/windows/secpol.png "secpol.msc")

3. Press enter

#### Set Secure Password Settings

1. Navigate to `Security Settings>Account Policies>Password Policy`

![Password Policy](images/windows/password_policy.png "Password Policy")

2. Set the password settings to be more secure
3. Set the settings by double clicking, entering the value, then selecting "Apply"

> Examples of secure settings are in the below image.
The amount of time for most things are subject to change

![Secure Password Settings](images/windows/secure_password.png "Secure Password Settings")

#### Set Password Lockout

1. Navigate to `Security Settings>Account Policies>Account Lockout Policy`

![Lockout Policy](images/windows/lockout_policy.png "Lockout Policy")

2. Select "Account lockout threshold"

![Lockout Threshold](images/windows/lockout_threshold.png "Lockout Threshold")

3. Set the value to a secure number \(somewhere around 5\)

![Secure Lockout Threshold](images/windows/secure_lockout.png "Secure Lockout Threshold")

4. Changing the threshold will propmt with suggested changes
5. Select "OK"

![Suggested Lockout Changes](images/windows/suggested_lockout.png "Suggested Lockout Changes")

> :page_with_curl: The lockout timer can be changed based on preference

#### Limit Local Use of Blank Passwords to Console Logon Only

1. Navigate to `Security Settings>Local Policies>Security Options`

![Security Options](images/windows/security_options.png "Security Options")

2. Find "Accounts: Limit local account use of blank password to console logon only"

![Limit Blank Passwords](images/windows/limit_blank_passwords.png "Limit Blank Passwords")

3. Select "Enabled"

#### Disable Anonymous Enumeration of SAM Accounts
1. Navigate to `Security Settings>Local Policies>Security Options`

![Security Options](images/windows/security_options.png "Security Options")

2. Find "Network access: Do not allow anonymous enumeration of SAM accounts"

![Limit SAM Enum](images/windows/SAM_enum.png "Limit SAM Enumeration")

3. Select "Enabled"