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







    


        
        