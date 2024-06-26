# Windows Server

### Other Pages
- [Main Page](README.md)
- [Windows 10](Windows_10.md)
- [Ubuntu](Ubuntu.md)
- [Debian](Debian.md)

> :hammer: ~~W.I.P. see [Windows 10](Windows_10.md).~~ This is being worked on now!

>:page_with_curl: This documentation is being swiftly written in preparation for the CyberPatriot Nationals. Basically, it might be a little messy.

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

        Defalut Value: **Allow**
 
    - #### 9.2.4 Ensure 'Windows Firewall: Private: Settings: displat a notification' is set to 'no' (Automated)
        To establish the recommended configuration via GP, set the following UI path to **No:**
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\WindowsDefender Firewall with Advanced Security\Window Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Settings Customize\Display a notification
        ```
        Defalut Value: **Yes**
        ***Recommended Value: **no** ***
    - #### 9.2.5 Ensure 'Windows Firewall: Private: Logging: Name' is set to '%SystemTooy%\System32\logfiles\firewall\Privatefw.log'(Automated)
        To establish the recommended configuration via GP, set the following UI path to ***%SystemRoot%\System32\logfiles\firewall\privatefw.log***:

        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Name
        ```
        Defalut Value: **%SystemRoot%\System32\logfiles\firewall\pfirewall.log** **(Recommended)**

    - #### 9.2.6 Ensure 'Windows Firewall: Private: Logging: Size limit (KB)'' is set to '16,384 KB' or greater (Automated).
        To establish the recommended configuration via GP, set the following UI path to ***16,384 KB or greater***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Size limit (KB)
        ```
        Defalut Value: **4,096 KB**
        ***Recommended Value: **16,384 KB' or greater** ***
    - #### 9.2.7 Ensure 'Windows Firewall: Private: Log dropped packets' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Log dropped packets
        ```
        Defalut Value: **No**
        ***Recommended Value: **Yes** ***
    - #### 9.2.8 Ensure 'Windows Firewall: Private: Log successful connections' is set to 'Yes' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Yes***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Private Profile\Logging Customize\Log successful connections
        ```
        Defalut Value: **No**
        ***Recommended Value: **Yes** ***
- #### 9.3 Public Profile
    - #### 9.3.1 (L1) Ensure 'Windows Firewall: Public: Firewall state' is set to 'On (recommended)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***On(recommended)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Firewall state
        ```
        Defalut Value: **On** **(Recommended)**
    - #### 9.3.2 (L1) Ensure 'Windows Firewall: Public: Inbound connections' is set to 'Block (default)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Block (default)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Inbound connections
        ```
        Defalut Value: **Block** **(Recommended)**
    - #### 9.3.3 (L1) Ensure 'Windows Firewall: Public: Outbound connections' is set to 'Allow (default)' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***Allow (default)***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Outbound connections
        ```
        Defalut Value: **Allow** **(Recommended)**
    - #### 9.3.4 (L1) Ensure 'Windows Firewall: Public: Settings: Display a notification' is set to 'No' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***'No'***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Display a notification
        ```
        Defalut Value: **Yes**
        ***Recommended Value: **No** *** 
    - #### 9.3.5 (L1) Ensure 'Windows Firewall: Public: Settings: Apply local firewall rules' is set to 'No' (Automated)   
        To establish the recommended configuration via GP, set the following UI path to ***No***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Apply local firewall rules
        ```
        Defalut Value: **Yes**
        ***Recommended Value: **No** ***     
    - #### 9.3.6 (L1) Ensure 'Windows Firewall: Public: Settings: Apply local connection security rules' is set to 'No' (Automated)
        To establish the recommended configuration via GP, set the following UI path to ***No***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Settings Customize\Apply local connection security rules
        ```
        Defalut Value: **Yes**
        ***Recommended Value: **No** *** 
    - #### 9.3.7 (L1) Ensure 'Windows Firewall: Public: Logging: Name' is set to '%SystemRoot%\System32\logfiles\firewall\publicfw.log'(Automated)
        To establish the recommended configuration via GP, set the following UI path to ***%SystemRoot%\System32\logfiles\firewall\publicfw.log***:
        ```
        Computer Configuration\Policies\Windows Settings\Security Settings\Windows Defender Firewall with Advanced Security\Windows Defender Firewall with Advanced Security\Windows Firewall Properties\Public Profile\Logging Customize\Name
        ```
        Defalut Value: **%SystemRoot%\System32\logfiles\firewall\pfirewall.log**
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
        

