# Windows Server

### Other Pages
- [Main Page](README.md)
- [Windows 10](Windows_10.md)
- [Ubuntu](Ubuntu.md)
- [Debian](Debian.md)

> :hammer: ~~W.I.P. see [Windows 10](Windows_10.md).~~ This is being worked on now!

>:page_with_curl: This documentation is being swiftly written in preparation for the CyberPatriot Nationals. Basically, it might be a little messy.

>:page_with_curl: You will need to install GPMC! Refer to: [Link](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265969(v=ws.11)) and you will need a domain user account: [Link](https://learn.microsoft.com/en-us/microsoft-desktop-optimization-pack/medv-v1/how-to-configure-a-domain-user-or-groupmedvv2)

- ## 1. Account Policies
    - ### 1.1 Password Policies
        - #### 1.1.1 (L1) Ensure 'Enforce password history' is set to '24 or more password(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Enforce password history
        ```
        Setting: 24 or more password(s)
    
        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.1.2 (L1) Ensure 'Maximum password age' is set to '365 or fewer days, but not 0' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Maximum password age
        ```
        Setting: 365 or fewer, but not 0

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.1.3 (L1) Ensure 'Minimum password age' is set to '1 or more day(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Minimum password age
        ```
        Setting: 1 or more day(s)

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.1.4 (L1) Ensure 'Minimum password length' is set to '14 or more character(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Minimum password length
        ```
        Setting: 14 or more character(s)

        Links: [1](https://www.cisecurity.org/insights/white-paperscis-password-policy-guide)

        - #### 1.1.5 (L1) Ensure 'Password must meet complexity requirements' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Password must meet complexity requirements
        ```
        Setting: Enabled

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.1.6 (L1) Ensure 'Store passwords using reversible encryption' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy\Store passwords using reversible encryption
        ```

        Setting: Disabled

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

    - ### 1.2 Account Lockout Policy
        - #### 1.2.1 (L1) Ensure 'Account lockout duration' is set to '15 or more minute(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy\Account lockout duration
        ```

        Setting: 15 or more minute(s)

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.2.2 (L1) Ensure 'Account lockout threshold' is set to '5 or fewer invalid logon attempt(s), but not 0' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy\Account lockout threshold
        ```

        Setting: 5 or fewer invalid login attempt(s), but not 0

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

        - #### 1.2.3 (L1) Ensure 'Allow Administrator account lockout' is set to 'Enabled' (MS only) (Manual)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policies\Allow Administrator account lockout
        ```

        Setting: Enabled

        Links: [1](https://support.microsoft.com/en-us/topic/kb5020282-account-lockout-available-for-built-in-local-administrators-bce45c4d-f28d-43ad-b6fe-70156cb2dc00)

        - #### 1.2.4 (L1) Ensure 'Reset account lockout counter after' is set to '15 or more minute(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy\Reset account lockout counter after
        ```

        Setting: 15 or more minute(s)

        Links: [1](https://www.cisecurity.org/insights/white-papers/cis-password-policy-guide)

---

- ## 2. Local Policies
    - ### 2.2 User Rights Assignment
        - #### 2.2.1 (L1) Ensure 'Access Credential Manager as a trusted caller' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Access Credential Manager as a trusted caller
        ```

        Setting: No One

        - #### 2.2.2 (L1) Ensure 'Access this computer from the network' is set to 'Administrators, Authenticated Users, ENTERPRISE DOMAIN CONTROLLERS' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Access this computer from the network
        ```

        - #### 2.2.3 (L1) Ensure 'Access this computer from the network' is set to 'Administrators, Authenticated Users' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Access this computer from the network
        ```

        - #### 2.2.4 (L1) Ensure 'Act as part of the operating system' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Act as part of the operating system
        ```

        Setting: No One

        - #### 2.2.5 (L1) Ensure 'Add workstations to domain' is set to 'Administrators' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Add workstations to domain
        ```

        Setting: Administrators

        - #### 2.2.6 (L1) Ensure 'Adjust memory quotas for a process' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Adjust memory quotas for a process
        ```

        Setting: Administrators, LOCAL SERVICE, NETWORK SERVICE

        - #### 2.2.7 (L1) Ensure 'Allow log on locally' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Allow log on locally
        ```

        - #### 2.2.8 (L1) Ensure 'Allow log on through Remote Desktop Services' is set to 'Administrators' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Allow log on through Remote Desktop Services
        ```

        - #### 2.2.9 (L1) Ensure 'Allow log on through Remote Desktop Services' is set to 'Administrators, Remote Desktop Users' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Allow log on through Remote Desktop Services
        ```

        - #### 2.2.10 (L1) Ensure 'Back up files and directories' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Back up files and directories
        ```

        - #### 2.2.11 (L1) Ensure 'Change the system time' is set to 'Administrators, LOCAL SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Change the system time
        ```

        - #### 2.2.12 (L1) Ensure 'Change the time zone' is set to 'Administrators, LOCAL SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Change the time zone
        ```

        - #### 2.2.13 (L1) Ensure 'Create a pagefile' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create a pagefile
        ```

        - #### 2.2.14 (L1) Ensure 'Create a token object' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create a token object
        ```

        - #### 2.2.15 (L1) Ensure 'Create global objects' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create global objects
        ```

        - #### 2.2.16 (L1) Ensure 'Create permanent shared objects' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create permanent shared objects
        ```

        - #### 2.2.17 (L1) Ensure 'Create symbolic links' is set to 'Administrators' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create symbolic links
        ```

        - #### 2.2.18 (L1) Ensure 'Create symbolic links' is set to 'Administrators, NT VIRTUAL MACHINE\Virtual Machines' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Create symbolic links
        ```

        - #### 2.2.19 (L1) Ensure 'Debug programs' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Debug programs
        ```

        - #### 2.2.20 (L1) Ensure 'Deny access to this computer from the network' to include 'Guests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access to this computer from the network
        ```

        - #### 2.2.21 (L1) Ensure 'Deny log on as a batch job' to include 'Guests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local 
        Policies\User Rights Assignment\Deny log on as a batch job
        ```

        - #### 2.2.22 (L1) Ensure 'Deny log on as a service' to include 'Guests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on as a service
        ```

        - #### 2.2.23 (L1) Ensure 'Deny log on locally' to include 'Guests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on locally
        ```

        - #### 2.2.24 (L1) Ensure 'Deny log on through Remote Desktop Services' to include 'Guests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services
        ```

        - #### 2.2.25 (L1) Ensure 'Enable computer and user accounts to be trusted for delegation' is set to 'Administrators' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Enable computer and user accounts to be trusted for delegation
        ```

        - #### 2.2.26 (L1) Ensure 'Enable computer and user accounts to be trusted for delegation' is set to 'No One' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Enable computer and user accounts to be trusted for delegation
        ```

        - #### 2.2.27 (L1) Ensure 'Force shutdown from a remote system' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Force shutdown from a remote system
        ```

        - #### 2.2.28 (L1) Ensure 'Generate security audits' is set to 'LOCAL SERVICE, NETWORK SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Generate security audits
        ```

        - #### 2.2.29 (L1) Ensure 'Impersonate a client after authentication' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Impersonate a client after authentication
        ```

        - #### 2.2.30 (L1) Ensure 'Impersonate a client after authentication' is set to 'Administrators, LOCAL SERVICE, NETWORK SERVICE, SERVICE' and (when the Web Server (IIS) Role with Web Services Role Service is installed) 'IIS_IUSRS' (MS only) (Automated)

        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Impersonate a client after authentication
        ```

        - #### 2.2.31 (L1) Ensure 'Increase scheduling priority' is set to 'Administrators, Window Manager\Window Manager Group' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Increase scheduling priority
        ```

        - #### 2.2.32 (L1) Ensure 'Load and unload device drivers' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Load and unload device drivers
        ```

        - #### 2.2.33 (L1) Ensure 'Lock pages in memory' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Lock pages in memory
        ```

        - #### 2.2.34 (L2) Ensure 'Log on as a batch job' is set to 'Administrators' (DC Only) (Automated)
        ```
        Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Log on as a batch job
        ```

        - #### 2.2.35 (L1) Ensure 'Manage auditing and security log' is set to 'Administrators' and (when Exchange is running in the environment) 'Exchange Servers' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Manage auditing and security log
        ```

        - #### 2.2.36 (L1) Ensure 'Manage auditing and security log' is set to 'Administrators' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Manage auditing and security log
        ```

        - #### 2.2.37 (L1) Ensure 'Modify an object label' is set to 'No One' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Modify an object label
        ```

        - #### 2.2.38 (L1) Ensure 'Modify firmware environment values' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Modify firmware environment values
        ```

        - #### 2.2.39 (L1) Ensure 'Perform volume maintenance tasks' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Perform volume maintenance tasks
        ```

        - #### 2.2.40 (L1) Ensure 'Profile single process' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Profile single process
        ```
        
        - #### 2.2.41 (L1) Ensure 'Profile system performance' is set to 'Administrators, NT SERVICE\WdiServiceHost' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Profile system performance
        ```

        - #### 2.2.42 (L1) Ensure 'Replace a process level token' is set to 'LOCAL SERVICE, NETWORK SERVICE' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Replace a process level token
        ```

        - #### 2.2.43 (L1) Ensure 'Restore files and directories' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Restore files and directories
        ```

        - #### 2.2.44 (L1) Ensure 'Shut down the system' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Shut down the system
        ```

        - #### 2.2.45 (L1) Ensure 'Synchronize directory service data' is set to 'No One' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Synchronize directory service data
        ```

        - #### 2.2.46 (L1) Ensure 'Take ownership of files or other objects' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Take ownership of files or other objects
        ```

        - #### 2.2.46 (L1) Ensure 'Take ownership of files or other objects' is set to 'Administrators' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Take ownership of files or other objects
        ```

    - ### 2.3 Security Options
        - #### 2.3.1.1 (L1) Ensure 'Accounts: Block Microsoft accounts' is set to 'Users can't add or log on with Microsoft accounts' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Accounts: Block Microsoft accounts
        ```

        - #### 2.3.1.2 (L1) Ensure 'Accounts: Guest account status' is set to 'Disabled' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Accounts: Guest account status
        ```

        - #### 2.3.1.3 (L1) Ensure 'Accounts: Limit local account use of blank passwords to console logon only' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Accounts: Limit local account use of blank passwords to console logon only
        ```

        - #### 2.3.1.4 (L1) Configure 'Accounts: Rename administrator account' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Accounts: Rename administrator account
        ```

        - #### 2.3.1.5 (L1) Configure 'Accounts: Rename guest account' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Accounts: Rename guest account
        ```

        - #### 2.3.2.1 (L1) Ensure 'Audit: Force audit policy subcategory settings (Windows Vista or later) to override audit policy category settings' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Audit: Force audit policy subcategory settings (Windows Vista or later) to override audit policy category settings
        ```

        - #### 2.3.2.2 (L1) Ensure 'Audit: Shut down system immediately if unable to log security audits' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Audit: Shut down system immediately if unable to log security audits
        ```

        - #### 2.3.2.2 (L1) Ensure 'Audit: Shut down system immediately if unable to log security audits' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Audit: Shut down system immediately if unable to log security audits
        ```

        - #### 2.3.4.1 (L1) Ensure 'Devices: Prevent users from installing printer drivers' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Devices: Prevent users from installing printer drivers
        ```

        - #### 2.3.7.1 (L1) Ensure 'Interactive logon: Do not require CTRL+ALT+DEL' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Do not require CTRL+ALT+DEL
        ```

        - #### 2.3.7.2 (L1) Ensure 'Interactive logon: Don't display last signed-in' is set to 'Enabled' (Automated)        
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Don't display last signed-in
        ```

        - #### 2.3.7.3 (L1) Ensure 'Interactive logon: Machine inactivity limit' is set to '900 or fewer second(s), but not 0' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Machine inactivity limit
        ```

        - #### 2.3.7.4 (L1) Configure 'Interactive logon: Message text for users attempting to log on' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Message text for users attempting to log on
        ```

        - #### 2.3.7.5 (L1) Configure 'Interactive logon: Message title for users attempting to log on' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Message title for users attempting to log on
        ```

        - #### 2.3.7.6 (L1) Ensure 'Interactive logon: Prompt user to change password before expiration' is set to 'between 5 and 14 days' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Prompt user to change password before expiration
        ```

        - #### 2.3.7.7 (L1) Ensure 'Interactive logon: Require Domain Controller Authentication to unlock workstation' is set to 'Enabled' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Require Domain Controller Authentication to unlock workstation
        ```

        - #### 2.3.7.8 (L1) Ensure 'Interactive logon: Smart card removal behavior' is set to 'Lock Workstation' or higher (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Interactive logon: Smart card removal behavior
        ```

        - #### 2.3.8.1 (L1) Ensure 'Microsoft network client: Digitally sign communications (always)' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network client: Digitally sign communications (always)
        ```

        - #### 2.3.8.2 (L1) Ensure 'Microsoft network client: Digitally sign communications (if server agrees)' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network client: Digitally sign communications (if server agrees)
        ```

        - #### 2.3.8.3 (L1) Ensure 'Microsoft network client: Send unencrypted password to third-party SMB servers' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network client: Send unencrypted password to third-party SMB servers
        ```

        - #### 2.3.9.1 (L1) Ensure 'Microsoft network server: Amount of idle time required before suspending session' is set to '15 or fewer minute(s)' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network server: Amount of idle time required before suspending session
        ```

        - #### 2.3.9.2 (L1) Ensure 'Microsoft network server: Digitally sign communications (always)' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network server: Digitally sign communications (always)
        ```

        - #### 2.3.9.3 (L1) Ensure 'Microsoft network server: Digitally sign communications (if client agrees)' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network server: Digitally sign communications (if client agrees)
        ```

        - #### 2.3.9.4 (L1) Ensure 'Microsoft network server: Disconnect clients when logon hours expire' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network server: Disconnect clients when logon hours expire
        ```

        - #### 2.3.9.5 (L1) Ensure 'Microsoft network server: Server SPN target name validation level' is set to 'Accept if provided by client' or higher (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Microsoft network server: Server SPN target name validation level
        ```

        - #### 2.3.10.1 (L1) Ensure 'Network access: Allow anonymous SID/Name translation' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Allow anonymous SID/Name translation
        ```

        - #### 2.3.10.2 (L1) Ensure 'Network access: Do not allow anonymous enumeration of SAM accounts' is set to 'Enabled' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Do not allow anonymous enumeration of SAM accounts
        ```

        - #### 2.3.10.3 (L1) Ensure 'Network access: Do not allow anonymous enumeration of SAM accounts and shares' is set to 'Enabled' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Do not allow anonymous enumeration of SAM accounts and shares
        ```

        - #### 2.3.10.4 (L2) Ensure 'Network access: Do not allow storage of passwords and credentials for network authentication' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Do not allow storage of passwords and credentials for network authentication
        ```

        - #### 2.3.10.5 (L1) Ensure 'Network access: Let Everyone permissions apply to anonymous users' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Let Everyone permissions apply to anonymous users
        ```

        - #### 2.3.10.6 (L1) Configure 'Network access: Named Pipes that can be accessed anonymously' (DC only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Named Pipes that can be accessed anonymously
        ```

        - #### 2.3.10.7 (L1) Configure 'Network access: Named Pipes that can be accessed anonymously' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Named Pipes that can be accessed anonymously
        ```

        - #### 2.3.10.8 (L1) Configure 'Network access: Remotely accessible registry paths' is configured (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Remotely accessible registry paths
        ```

        - #### 2.3.10.9 (L1) Configure 'Network access: Remotely accessible registry paths and sub-paths' is configured (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Remotely accessible registry paths and sub-paths
        ```
        - Set to:
        ```
        System\CurrentControlSet\Control\Print\Printers System\CurrentControlSet\Services\EventlogSoftware\Microsoft\OLAP ServerSoftware\Microsoft\Windows NT\CurrentVersion\PrintSoftware\Microsoft\Windows NT\CurrentVersion\Windows System\CurrentControlSet\Control\ContentIndex System\CurrentControlSet\Control\Terminal Server System\CurrentControlSet\Control\Terminal Server\UserConfig System\CurrentControlSet\Control\Terminal Server\DefaultUserConfiguration Software\Microsoft\Windows NT\CurrentVersion\Perflib System\CurrentControlSet\Services\SysmonLog
        ```

        - #### 2.3.10.10 (L1) Ensure 'Network access: Restrict anonymous access to Named Pipes and Shares' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Restrict anonymous access to Named Pipes and Shares
        ```

        - #### 2.3.10.11 (L1) Ensure 'Network access: Restrict clients allowed to make remote calls to SAM' is set to 'Administrators: Remote Access: Allow' (MS only) (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Restrict clients allowed to make remote calls to SAM
        ```

        - #### 2.3.10.12 (L1) Ensure 'Network access: Shares that can be accessed anonymously' is set to 'None' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Shares that can be accessed anonymously
        ```

        - #### 2.3.10.13 (L1) Ensure 'Network access: Sharing and security model for local accounts' is set to 'Classic - local users authenticate as themselves' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network access: Sharing and security model for local accounts
        ```

        - #### 2.3.11.1 (L1) Ensure 'Network security: Allow Local System to use computer identity for NTLM' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Allow Local System to use computer identity for NTLM
        ```

        - #### 2.3.11.2 (L1) Ensure 'Network security: Allow LocalSystem NULL session fallback' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Allow LocalSystem NULL session fallback
        ```

        - #### 2.3.11.3 (L1) Ensure 'Network Security: Allow PKU2U authentication requests to this computer to use online identities' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network Security: Allow PKU2U authentication requests to this computer to use online identities
        ```

        - #### 2.3.11.4 (L1) Ensure 'Network security: Configure encryption types allowed for Kerberos' is set to 'AES128_HMAC_SHA1, AES256_HMAC_SHA1, Future encryption types' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Configure encryption types allowed for Kerberos
        ```

        - #### 2.3.11.5 (L1) Ensure 'Network security: Do not store LAN Manager hash value on next password change' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Do not store LAN Manager hash value on next password change
        ```

        - #### 2.3.11.6 (L1) Ensure 'Network security: Force logoff when logon hours expire' is set to 'Enabled' (Manual)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Force logoff when logon hours expire
        ```

        - #### 2.3.11.7 (L1) Ensure 'Network security: LAN Manager authentication level' is set to 'Send NTLMv2 response only. Refuse LM & NTLM' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: LAN Manager authentication level
        ```

        - #### 2.3.11.8 (L1) Ensure 'Network security: LDAP client signing requirements' is set to 'Negotiate signing' or higher (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: LDAP client signing requirements
        ```

        - #### 2.3.11.9 (L1) Ensure 'Network security: Minimum session security for NTLM SSP based (including secure RPC) clients' is set to 'Require NTLMv2 session security, Require 128-bit encryption' (Automated)        
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Minimum session security for NTLM SSP based (including secure RPC) clients
        ```

        - #### 2.3.11.10 (L1) Ensure 'Network security: Minimum session security for NTLM SSP based (including secure RPC) servers' is set to 'Require NTLMv2 session security, Require 128-bit encryption' (Automated)    
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Minimum session security for NTLM SSP based (including secure RPC) servers
        ```

        - #### 2.3.11.11 (L1) Ensure 'Network security: Restrict NTLM: Audit Incoming NTLM Traffic' is set to 'Enable auditing for all accounts' (Automated) 
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Network security: Restrict NTLM: Audit Incoming NTLM Traffic
        ```

        - #### 2.3.11.12 (L1) Ensure 'Network security: Restrict NTLM: Outgoing NTLM traffic to remote servers' is set to 'Audit all' or higher (Automated) 
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Restrict NTLM: Outgoing NTLM traffic to remote servers
        ```

        - #### 2.3.13.1 (L1) Ensure 'Shutdown: Allow system to be shut down swithout having to log on' is set to 'Disabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\Shutdown: Allow system to be shut down without having to log on
        ```

        - #### 2.3.15.1 (L1) Ensure 'System objects: Require case insensitivity for non-Windows subsystems' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\System objects: Require case insensitivity for nonWindows subsystems
        ```

        - #### 2.3.15.2 (L1) Ensure 'System objects: Strengthen default permissions of internal system objects (e.g. Symbolic Links)' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\System objects: Strengthen default permissions of internal system objects (e.g. Symbolic Links)
        ```

        - #### 2.3.17.1 (L1) Ensure 'User Account Control: Admin Approval Mode for the Built-in Administrator account' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Admin Approval Mode for the Built-in Administrator account
        ```

        - #### 2.3.17.2 (L1) Ensure 'User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode' is set to 'Prompt for consent on the secure desktop' or higher (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode
        ```

        - #### 2.3.17.3 (L1) Ensure 'User Account Control: Behavior of the elevation prompt for standard users' is set to 'Automatically deny elevation requests' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Behavior of the elevation prompt for standard users
        ```

        - #### 2.3.17.4 (L1) Ensure 'User Account Control: Detect application installations and prompt for elevation' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Detect application installations and prompt for elevation
        ```

        - #### 2.3.17.5 (L1) Ensure 'User Account Control: Only elevate UIAccess applications that are installed in secure locations' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Only elevate UIAccess applications that are installed in secure locations
        ```

        - #### 2.3.17.6 (L1) Ensure 'User Account Control: Run all administrators in Admin Approval Mode' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Run all administrators in Admin Approval Mode
        ```

        - #### 2.3.17.7 (L1) Ensure 'User Account Control: Switch to the secure desktop when prompting for elevation' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Switch to the secure desktop when prompting for elevation
        ```

        - #### 2.3.17.8 (L1) Ensure 'User Account Control: Virtualize file and registry write failures to per-user locations' is set to 'Enabled' (Automated)
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Local Policies\Security Options\User Account Control: Virtualize file and registry write failures to per-user locations
        ```

- ## 5. System Services
    - #### 5.1 (L1) Ensure 'Print Spooler (Spooler)' is set to 'Disabled' (DC only) (Automated)
    ```
    Computer Configuration\Policies\Windows Settings\Security Settings\System Services\Print Spooler
    ```

    - #### 5.2 (L2) Ensure 'Print Spooler (Spooler)' is set to 'Disabled' (MS only) (Automated)
    ```
    Computer Configuration\Policies\Windows Settings\Security Settings\System Services\Print Spooler
    ```




<br><br>

- ## 9. Windows Defender Firewall with Advanced Security
  - ### 9.1 Domain Proflie
  - ### 9.2 Private Profile
    - #### 9.2.1 Ensure 'Windows Firewall: Private: Firewall state' is set to 'On (recommended)'(Automated)
      Navigate to the UI Path articulated in the Remediation section and confirm it is set as
      prescribed. This group policy setting is backed by the following registry location:
    ```
    HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsFirewall\PrivateProfile :EnableFirewall
    ```
    To establish the recommended configuration via GP, set the following UI path to On
    (recommended):

    ```
      Computer Configuration\Policies\Windows Settings\Security Settings\Windows
      Defender Firewall with Advanced Security\Windows Defender Firewall with
      Advanced Security\Windows Firewall Properties\Private Profile\Firewall state
    ```
    Default value: **On** (recommended)
    - #### 9.2.2 Ensure 'Windows Firewall: Private: Inbound connections' is set to 'block (default)'(Automated)
      Navigate to the UI Path articulated in the Remediation section and confirm it is set as
      prescribed. This group policy setting is backed by the following registry location:
      ```
      HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsFirewall\PrivateProfile :DefaultInboundAction
      ```
      To establish the recommended configuration via GP, set the following UI path to Block (default):
      ```
      Computer Configuration\Policies\Windows Settings\Security Settings\Windows
      Defender Firewall with Advanced Security\Windows Defender Firewall with
      Advanced Security\Windows Firewall Properties\Private Profile\Inbound
      connections
      ```
       Default value: **Block** (Default) (recommended)
      - #### 9.2.3 Ensure 'Windows Firewall: Private: Outbound connects is set to 'Allow' (default)(Automated)
      ***Note:** If you set Outbound connections to Block and then deploy the firewall policy by
      using a GPO, computers that receive the GPO settings cannot receive subsequent
      Group Policy updates unless you create and deploy an outbound rule that enables
      Group Policy to work. Predefined rules for Core Networking include outbound rules that
      enable Group Policy to work. Ensure that these outbound rules are active, and
      thoroughly test firewall profiles before deploying.* <br></br>
    Navigate to the UI Path articulated in the Remediation section and confirm it is set as
    prescribed. This group policy setting is backed by the following registry location:

        ```
        HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsFirewall\PrivateProfile
        :DefaultOutboundAction  
        ```
         To establish the recommended configuration via GP, set the following UI path to Allow
        (default):

        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows
        Defender Firewall with Advanced Security\Windows Defender Firewall with
        Advanced Security\Windows Firewall Properties\Private Profile\Outbound
        connections
        ```

        Default Value: **Allow**
 
    - #### 9.2.4 Ensure 'Windows Firewall: Private: Settings: displat a notification' is set to 'no' (Automated)
        To establish the recommended configuration via GP, set the following UI path to **No:**
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\WindowsDefender Firewall with Advanced Security\Window Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Settings Customize\Display a notification
        ```
        Default Value: **Yes**
        ***Recommended Value: **no** ***
    - #### 9.2.5 Ensure 'Windows Firewall: Private: Logging: Name' is set to '%SystemTooy%\System32\logfiles\firewall\Privatefw.log'(Automated)
        To establish the recommended configuration via GP, set the following UI path to ***%SystemRoot%\System32\logfiles\firewall\privatefw.log***:

        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Name
        ```
        Default Value: **%SystemRoot%\System32\logfiles\firewall\pfirewall.log** **(Recommended)**

    - #### 9.2.6 Ensure 'Windows Firewall: Private: Logging: Size limit (KB)'' is set to '16,384 KB' or greater (Automated).
        To establish the recommended configuration via GP, set the following UI path to ***16,384 KB or greater***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Size limit (KB)
        ```
        Default Value: **4,096 KB**
        ***Recommended Value: **16,384 KB' or greater** ***
    - #### 9.2.7 Ensure 'Windows Firewall: Private: Log dropped packets' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Log dropped packets
        ```
        Default Value: **No**
        ***Recommended Value: **Yes** ***
    - #### 9.2.8 Ensure 'Windows Firewall: Private: Log successful connections' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Log successful connections
        ```
        Default Value: **No**
        ***Recommended Value: **Yes** ***
- #### 9.3 Public Profile
 - #### 9.3.1 (L1) Ensure 'Windows Firewall: Public: Firewall state' is set to 'On (recommended)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***On(recommended)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Firewall state
        ```
        Default Value: **On** **(Recommended)**
    - #### 9.3.2 (L1) Ensure 'Windows Firewall: Public: Inbound connections' is set to 'Block (default)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Block (default)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Inbound connections
        ```
        Default Value: **Block** **(Recommended)**
    - #### 9.3.3 (L1) Ensure 'Windows Firewall: Public: Outbound connections' is set to 'Allow (default)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Allow (default)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Outbound connections
        ```
        Default Value: **Allow** **(Recommended)**
    - #### 9.3.4 (L1) Ensure 'Windows Firewall: Public: Settings: Display a notification' is set to 'No' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***'No'***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Display a notification
        ```
        Default Value: **Yes**
        ***Recommended Value: **No** *** 
    - #### 9.3.5 (L1) Ensure 'Windows Firewall: Public: Settings: Apply local firewall rules' is set to 'No' (Automated)   
        To establish the recommended configuration via GP, set the following UI path to ***No***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Apply local firewall rules
        ```
        Default Value: **Yes**
        ***Recommended Value: **No** ***     
    - #### 9.3.6 (L1) Ensure 'Windows Firewall: Public: Settings: Apply local connection security rules' is set to 'No' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***No***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Apply local connection security rules
        ```
        Default Value: **Yes**
        ***Recommended Value: **No** *** 
    - #### 9.3.7 (L1) Ensure 'Windows Firewall: Public: Logging: Name' is set to '%SystemRoot%\System32\logfiles\firewall\publicfw.log'(Automated)
        To establish the recommended configuration via GP, set the following UI path to ***%SystemRoot%\System32\logfiles\firewall\publicfw.log***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Logging Customize\Name
        ```
        Default Value: **%SystemRoot%\System32\logfiles\firewall\pfirewall.log**
    - #### 9.3.8 (L1) Ensure 'Windows Firewall: Public: Logging: Size limit (KB)' is set to ***'16,384 KB or greater'*** (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***16,384 KB or greater***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Logging Customize\Size limit (KB)
        ```
        Default Value: **4,096 KB**
        ***Recommended Value: **16,384 KB or greater** *** 
    - #### 9.3.9 (L1) Ensure 'Windows Firewall: Public: Logging: Log dropped packets' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Public Profile\Logging Customize\Log dropped packets
        ```
        Default Value: **No**
        ***Recommended Value: **Yes** *** 
    - #### 9.3.10 (L1) Ensure 'Windows Firewall: Public: Logging: Log successful connections' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Logging Customize\Log successful connections
        ```
        Default Value: **No**
        ***Recommended Value: **Yes** *** 
- ## 17 Advanced Audit Policy Configuration
    This section contains recommendations for configuring the Windows audit facilities.
    - ### 17.1 Account Logon

<br><br>

## 19. Administrative Templates (User) 
### 19.1 Control Panel
#### 19.1.3 Personalization (formerly Desktop Themes)
##### 19.1.3.1 (L1) Ensure 'Enable screen saver' is set to 'Enabled' (Automated)
``` 
User Configuration\Policies\Administrative Templates\Control 
Panel\Personalization\Enable screen saver
``` 
Setting: Enabled  

<br></br>

##### 19.1.3.2 (L1) Ensure 'Password protect the screen saver' is set to 
'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Control 
Panel\Personalization\Password protect the screen saver
``` 
Setting: Enabled  
<br></br>


##### 19.1.3.3 (L1) Ensure 'Screen saver timeout' is set to 'Enabled: 900 seconds or fewer, but not 0' (Automated)
``` 
User Configuration\Policies\Administrative Templates\Control 
Panel\Personalization\Screen saver timeout
``` 
Setting: Enabled: 900 or fewer, but not 0  

<br></br>

#### 19.5.1 Notifications
##### 19.5.1.1 (L1) Ensure 'Turn off toast notifications on the lock screen' is set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Start Menu and 
Taskbar\Notifications\Turn off toast notifications on the lock screen 
``` 
Setting: Enabled  

<br></br>

#### 19.6.6.1 Internet Communication settings
##### 19.6.6.1.1 (L2) Ensure 'Turn off Help Experience Improvement Program' is set to 'Enabled' (Automated)
``` 
User Configuration\Policies\Administrative Templates\System\Internet 
Communication Management\Internet Communication Settings\Turn off Help 
Experience Improvement Program 
``` 
Setting: Enabled 
<br></br>


#### 19.7.4 Attachment Manager
##### 19.7.4.1 (L1) Ensure 'Do not preserve zone information in file attachments' is set to 'Disabled' (Automated)
``` 
User Configuration\Policies\Administrative Templates\Windows 
Components\Attachment Manager\Do not preserve zone information in file 
attachments
``` 
Setting: Disabled 
<br></br>

##### 19.7.4.2 (L1) Ensure 'Notify antivirus programs when opening attachments' is set to 'Enabled' (Automated)
``` 
User Configuration\Policies\Administrative Templates\Windows 
Components\Attachment Manager\Notify antivirus programs when opening 
attachments
``` 
Setting: Enabled 
<br></br>



#### 19.7.7 Cloud Content
##### 19.7.7.1 (L1) Ensure 'Configure Windows spotlight on lock screen' is set to Disabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows Components\Cloud 
Content\Configure Windows spotlight on lock screen 
``` 
Setting: Disabled 
Links:
[1](https://docs.microsoft.com/en-us/windows/configuration/windows-spotlight#how-do-you-disable-windows-spotlight-for-managed-devices) 
<br></br>

##### 19.7.7.2 (L1) Ensure 'Do not suggest third-party content in Windows spotlight' is set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows Components\Cloud 
Content\Do not suggest third-party content in Windows spotlight
``` 
Setting: Enabled  
<br></br>

##### 19.7.7.3 (L2) Ensure 'Do not use diagnostic data for tailored experiences' is set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows Components\Cloud 
Content\Do not use diagnostic data for tailored experiences
``` 
Setting: Enabled  
<br></br>

##### 19.7.7.4 (L2) Ensure 'Turn off all Windows spotlight features' is set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows Components\Cloud 
Content\Turn off all Windows spotlight features
``` 
Setting: Enabled  
<br></br>

##### 19.7.7.5 (L1) Ensure 'Turn off Spotlight collection on Desktop' is 
set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows Components\Cloud 
Content\Turn off Spotlight collection on Desktop
``` 
Setting: Enabled  
 
Links:  [1](https://docs.microsoft.com/en-us/windows/configuration/windows-spotlight)
<br></br>


#### 19.7.25 Network Sharing
##### 19.7.25.1 (L1) Ensure 'Prevent users from sharing files within their profile.' is set to 'Enabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows 
Components\Network Sharing\Prevent users from sharing files within their 
profile.
``` 
Setting: Enabled  
<br></br>


#### 19.7.40 Windows Installer
##### 19.7.40.1 (L1) Ensure 'Always install with elevated privileges' is set to 'Disabled' (Automated)

``` 
User Configuration\Policies\Administrative Templates\Windows 
Components\Windows Installer\Always install with elevated privileges

``` 
Setting: Disabled:
 
Links:  [1](https://docs.microsoft.com/en-us/windows/win32/msi/alwaysinstallelevated)
<br></br>


#### 19.7.42.2 Playback
##### 19.7.42.2.1 (L2) Ensure 'Prevent Codec Download' is set to 'Enabled' (Automated)
``` 
User Configuration\Policies\Administrative Templates\Windows 
Components\Windows Media Player\Playback\Prevent Codec Download
``` 
Setting: Enabled  

<br></br>

