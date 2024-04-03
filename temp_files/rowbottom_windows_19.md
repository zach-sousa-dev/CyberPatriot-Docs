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

## 1. Account wPolicies 
### 1.1 Password Policies
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

