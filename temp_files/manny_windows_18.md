###  18.10.3.1 (L2) Ensure 'Allow a Windows app to share application data between users' is set to 'Disabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\App Package Deployment\Allow a Windows app to share application 
data between users
```

**REMIDIATION:** To establish the recommended configuration via GP, set the following UI path to Disabled

---

### 18.10.3.2 (L1) Ensure 'Prevent non-admin users from installing 
packaged Windows apps' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\App Package Deployment\Prevent non-admin users from installing 
packaged Windows apps
```

To establish the recommended configuration via GP, set the following UI path to 
Enabled

---
### 18.10.4.1 (L1) Ensure 'Let Windows apps activate with voice 
while the system is locked' is set to 'Enabled: Force Deny' 
(Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\App Privacy\Let Windows apps activate with voice while the system 
is locked
```

To establish the recommended configuration via GP, set the following UI path to 
Enabled: Force Deny


---
### 18.10.5.1 (L1) Ensure 'Allow Microsoft accounts to be optional' is 
set to 'Enabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\App runtime\Allow Microsoft accounts to be optional
```

To establish the recommended configuration via GP, set the following UI path to 
Enabled

---
### 18.10.5.2 (L2) Ensure 'Block launching Universal Windows apps with Windows Runtime API access from hosted content.' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\App runtime\Block launching Universal Windows apps with Windows 
Runtime API access from hosted content.
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled:
---
### 18.10.7.1 (L1) Ensure 'Disallow Autoplay for non-volume devices' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\AutoPlay Policies\Disallow Autoplay for non-volume devices
```

**REMIDIATION:** To establish the recommended configuration via GP, set the following UI path to Enabled:
---

### 18.10.7.2 (L1) Ensure 'Set the default behavior for AutoRun' is set to 'Enabled: Do not execute any autorun commands' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\AutoPlay Policies\Set the default behavior for AutoRun

```

**REMIDIATION:** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not execute any autorun commands
---

### 18.10.7.3 (L1) Ensure 'Turn off Autoplay' is set to 'Enabled: All drives' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\AutoPlay Policies\Turn off Autoplay
```

**REMIDATION:**  To establish the recommended configuration via GP, set the following UI path to Enabled: All drives

---
### 18.10.8.1.1 (L1) Ensure 'Configure enhanced anti-spoofing' is set to 'Enabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\Biometrics\Facial Features\Configure enhanced anti-spoofing
```


**REMIDATION:**  To establish the recommended configuration via GP, set the following UI path to Enabled
---

### 18.10.9.1.1 (BL) Ensure 'Allow access to BitLocker-protected fixed data drives from earlier versions of Windows' is set to 'Disabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Allow access to 
BitLocker-protected fixed data drives from earlier versions of Windows
```

**REMIDIATION:** To establish the recommended configuration via GP, set the following UI path to Disabled:

---
### 18.10.9.1.2 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled

---
### 18.10.9.1.3 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Allow data recovery agent' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Allow data recovery agent
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)
---

### 18.10.9.1.4 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Recovery Password' is set to 'Enabled: Allow 48-digit recovery password' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Recovery Password
```

**REMIDATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: Allow 48-digit recovery password:

---
### 18.10.9.1.5 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Recovery Key' is set to 'Enabled: Allow 256-bit recovery key' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Recovery Key
```

**REMIDATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Allow 256-bit recovery key:

---
### 18.10.9.1.6 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Omit recovery options from the BitLocker setup wizard' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Omit recovery options from the 
BitLocker setup wizard
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)

---
### 18.10.9.1.7 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Save BitLocker recovery information to AD DS for fixed data drives' is set to 'Enabled: False' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Save BitLocker recovery information 
to AD DS for fixed data drives
```
**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: False (unchecked)
---
### 18.10.9.1.8 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Configure storage of BitLocker recovery information to AD DS' is set to 'Enabled: Backup recovery passwords and key packages' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Configure storage of BitLocker 
recovery information to AD DS:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: Backup recovery passwords and key packages

---
### 18.10.9.1.9 (BL) Ensure 'Choose how BitLocker-protected fixed drives can be recovered: Do not enable BitLocker until recovery information is stored to AD DS for fixed data drives' is set to 'Enabled: False' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Choose how BitLockerprotected fixed drives can be recovered: Do not enable BitLocker until 
recovery information is stored to AD DS for fixed data drives
```

**To establish the recommended configuration via GP, set the following UI path to 
Enabled: False (unchecked):**


### 18.10.9.1.10 (BL) Ensure 'Configure use of hardware-based encryption for fixed data drives' is set to 'Disabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Configure use of 
hardware-based encryption for fixed data drives
```

**To establish the recommended configuration via GP, set the following UI path to 
Disabled**

---
### 18.10.9.1.11 (BL) Ensure 'Configure use of passwords for fixed data drives' is set to 'Disabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Configure use of 
passwords for fixed data drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Disabled:

---

### 18.10.9.1.12 (BL) Ensure 'Configure use of smart cards on fixed data drives' is set to 'Enabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Configure use of 
smart cards on fixed data drives
```

**REMIDIATION** **To establish the recommended configuration via GP, set the following UI path to Enabled:** 


### 18.10.9.1.13 (BL) Ensure 'Configure use of smart cards on fixed data drives: Require use of smart cards on fixed data drives' is set to 'Enabled: True' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Fixed Data Drives\Configure use of 
smart cards on fixed data drives: Require use of smart cards on fixed data 
drives
```


**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)


### 18.10.9.2.1 (BL) Ensure 'Allow enhanced PINs for startup' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Allow enhanced 
PINs for startup
```

**REMIDIATION* **To establish the recommended configuration via GP, set the following UI path to 
Enabled**

---

### 18.10.9.2.2 (BL) Ensure 'Allow Secure Boot for integrity validation' is set to 'Enabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Allow Secure 
Boot for integrity validation
```

**Remidiation** To establish the recommended configuration via GP, set the following UI path to Enabled:


---

### To establish the recommended configuration via GP, set the following UI path to Enabled:

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled:

---

### 18.10.9.2.4 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Allow data recovery agent' is set to 'Enabled: False' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Allow data 
recovery agent
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: False (unchecked)

---

### 18.10.9.2.5 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Recovery Password' is set to 'Enabled: Require 48-digit recovery password' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Recovery 
Password
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: Require 48-digit recovery password

---

### 18.10.9.2.6 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Recovery Key' is set to 'Enabled: Do not allow 256-bit recovery key' (Automated

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Recovery Key
```

**REMIDATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not allow 256-bit recovery key

---

### 18.10.9.2.7 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Omit recovery options from the BitLocker setup wizard' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Omit recovery 
options from the BitLocker setup wizard
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked):

---

### 18.10.9.2.8 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Save BitLocker recovery information to AD DS for operating system drives' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Save BitLocker 
recovery information to AD DS for operating system drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: True (checked):

---

### 18.10.9.2.9 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Configure storage of BitLocker recovery information to AD DS:' is set to 'Enabled: Store recovery passwords and key packages' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Configure 
storage of BitLocker recovery information to AD DS:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: Store recovery passwords and key packages:

---

### 18.10.9.2.10 (BL) Ensure 'Choose how BitLocker-protected operating system drives can be recovered: Do not enable BitLocker until recovery information is stored to AD DS for operating system drives' is set to 'Enabled: True' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Choose how 
BitLocker-protected operating system drives can be recovered: Do not enable 
BitLocker until recovery information is stored to AD DS for operating system 
drives
```


**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)

---

### 18.10.9.2.11 (BL) Ensure 'Configure use of hardware-based encryption for operating system drives' is set to 'Disabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Configure use 
of hardware-based encryption for operating system drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Disabled:

---

### 18.10.9.2.12 (BL) Ensure 'Configure use of passwords for operating system drives' is set to 'Disabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Configure use of passwords for operating system drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Disabled

---

### 18.10.9.2.13 (BL) Ensure 'Require additional authentication at startup' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled:

---

### 18.10.9.2.14 (BL) Ensure 'Require additional authentication at startup: Allow BitLocker without a compatible TPM' is set to 'Enabled: False' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup: Allow BitLocker without a compatible 
TPM
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: False (unchecked)

---

### 18.10.9.2.15 (BL) Ensure 'Require additional authentication at startup: Configure TPM startup:' is set to 'Enabled: Do not allow TPM' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup: Configure TPM startup:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not allow TPM:

---

### 18.10.9.2.16 (BL) Ensure 'Require additional authentication at startup: Configure TPM startup PIN:' is set to 'Enabled: Require startup PIN with TPM' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup: Configure TPM startup PIN:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Require startup PIN with TPM:

---

### 18.10.9.2.17 (BL) Ensure 'Require additional authentication at startup: Configure TPM startup key:' is set to 'Enabled: Do not allow startup key with TPM' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup: Configure TPM startup key:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not allow startup key with TPM:

---
### 18.10.9.2.18 (BL) Ensure 'Require additional authentication at startup: Configure TPM startup key and PIN:' is set to 'Enabled: Do not allow startup key and PIN with TPM' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Operating System Drives\Require 
additional authentication at startup: Configure TPM startup key and PIN:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: Do not allow startup key and PIN with TPM:


---

### 18.10.9.3.1 (BL) Ensure 'Allow access to BitLocker-protected removable data drives from earlier versions of Windows' is set to 'Disabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Allow access to 
BitLocker-protected removable data drives from earlier versions of Windows
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Disabled:

---

### 18.10.9.3.2 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered' is set to 'Enabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled:

---

### 18.10.9.3.3 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Allow data recovery agent' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Allow data recovery 
agent
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)

---

### 18.10.9.3.4 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Recovery Password' is set to 'Enabled: Do not allow 48-digit recovery password' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Recovery Password
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not allow 48-digit recovery password

### 18.10.9.3.5 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Recovery Key' is set to 'Enabled: Do not allow 256-bit recovery key' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Recovery Key
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Do not allow 256-bit recovery key

---

### 18.10.9.3.6 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Omit recovery options from the BitLocker setup wizard' is set to 'Enabled: True' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Omit recovery options 
from the BitLocker setup wizard
```

**REMIDIAITON** To establish the recommended configuration via GP, set the following UI path to Enabled: True (checked)

---

### 18.10.9.3.7 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Save BitLocker recovery information to AD DS for removable data drives' is set to 'Enabled: False' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Save BitLocker 
recovery information to AD DS for removable data drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: False (unchecked)

---

### 18.10.9.3.8 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Configure storage of BitLocker recovery information to AD DS:' is set to 'Enabled: Backup recovery passwords and key packages' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Configure storage of 
BitLocker recovery information to AD DS:
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Enabled: Backup recovery passwords and key packages

---

### 18.10.9.3.9 (BL) Ensure 'Choose how BitLocker-protected removable drives can be recovered: Do not enable BitLocker until recovery information is stored to AD DS for removable data drives' is set to 'Enabled: False' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Choose how 
BitLocker-protected removable drives can be recovered: Do not enable 
BitLocker until recovery information is stored to AD DS for removable data 
drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: False (unchecked)

---

### 18.10.9.3.10 (BL) Ensure 'Configure use of hardware-based encryption for removable data drives' is set to 'Disabled' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Configure use of 
hardware-based encryption for removable data drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Disabled

---

### 18.10.9.3.11 (BL) Ensure 'Configure use of passwords for removable data drives' is set to 'Disabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Configure use of 
passwords for removable data drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to Disabled

---

### 18.10.9.3.12 (BL) Ensure 'Configure use of smart cards on removable data drives' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Configure use of 
smart cards on removable data drives
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled

---

### 18.10.9.3.13 (BL) Ensure 'Configure use of smart cards on removable data drives: Require use of smart cards on removable data drives' is set to 'Enabled: True' (Automated

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Configure use of 
smart cards on removable data drives: Require use of smart cards on removable 
data drives
```

**REMIDATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: True (checked)

---

### 18.10.9.3.14 (BL) Ensure 'Deny write access to removable drives not protected by BitLocker' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Deny write access 
to removable drives not protected by BitLocker
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled:

---

### 18.10.9.3.15 (BL) Ensure 'Deny write access to removable drives not protected by BitLocker: Do not allow write access to devices configured in another organization' is set to 'Enabled: False' (Automated)


```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Removable Data Drives\Deny write access 
to removable drives not protected by BitLocker: Do not allow write access to 
devices configured in another organization
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled: False (unchecked)

---

### 18.10.9.4 (BL) Ensure 'Disable new DMA devices when this computer is locked' is set to 'Enabled' (Automated)

```
Computer Configuration\Policies\Administrative Templates\Windows 
Components\BitLocker Drive Encryption\Disable new DMA devices when this 
computer is locked
```

**REMIDIATION** To establish the recommended configuration via GP, set the following UI path to 
Enabled

### 18.10.10
