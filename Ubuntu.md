# Ubuntu 22

## Contents

### Other Pages
- [Main Page](README.md)
- [Windows 10](Windows_10.md)
- [Windows Server](Server.md)
- [Debian](Debian.md)

### Sub Headings
- [Ubuntu 22](#ubuntu-22)
	- [Contents](#contents)
		- [Other Pages](#other-pages)
		- [Sub Headings](#sub-headings)
	- [1 Initial Setup](#1-initial-setup)
		- [1 Filesystem Configuration](#1-filesystem-configuration)
			- [1 Disable Unused Filesystems](#1-disable-unused-filesystems)
			- [2 Configure tmp](#2-configure-tmp)
			- [3 Configure var](#3-configure-var)
			- [4 Configure var tmp](#4-configure-var-tmp)
			- [5 Configure var log](#5-configure-var-log)
			- [6 Configure var log audit](#6-configure-var-log-audit)
			- [7 Configure home](#7-configure-home)
			- [8 Configure dev shm](#8-configure-dev-shm)
			- [9 Disable Automounting](#9-disable-automounting)
			- [10 Disable USB Storage](#10-disable-usb-storage)
		- [2 Configure Software Updates](#2-configure-software-updates)
		- [3 Filesystem Integrity Checking](#3-filesystem-integrity-checking)
		- [4 Secure Boot Settings](#4-secure-boot-settings)
		- [5 Additional Process Hardening](#5-additional-process-hardening)
		- [6 Mandatory Access Control](#6-mandatory-access-control)
			- [1 Configure AppArmor](#1-configure-apparmor)
		- [7 Command Line Warning Banners](#7-command-line-warning-banners)
		- [8 GNOME Display Manager](#8-gnome-display-manager)
		- [9 Ensure updates patches and additional security software are installed](#9-ensure-updates-patches-and-additional-security-software-are-installed)
	- [2 Services](#2-services)
		- [Configure Time Synchronization](#configure-time-synchronization)
		- [Special Purpose Services](#special-purpose-services)
		- [Service Clients](#service-clients)
	- [3 Network Configuration](#3-network-configuration)
		- [Disable Unused Network Protocols and Devices](#disable-unused-network-protocols-and-devices)
		- [Network Parameters Host Only](#network-parameters-host-only)
		- [Network Parameters Host and Router](#network-parameters-host-and-router)
		- [Uncommon Network Protocols](#uncommon-network-protocols)
		- [Firewall Configuration](#firewall-configuration)
	- [4 Logging and Auditing](#4-logging-and-auditing)
		- [1 Configure System Accounting (auditd)](#1-configure-system-accounting-auditd)
		- [2 Configure Logging](#2-configure-logging)
	- [5 Access Authentication and Authorization](#5-access-authentication-and-authorization)
		- [1 Configure time-based job schedulers](#1-configure-time-based-job-schedulers)
		- [2 Configure SSH Server](#2-configure-ssh-server)
		- [3 Configure privilege escalation](#3-configure-privilege-escalation)
		- [4 Configure PAM](#4-configure-pam)
		- [5 User Account and](#5-user-account-and)
	- [6 System Maintenance](#6-system-maintenance)
		- [1 System File Permission](#1-system-file-permission)
		- [2 Local User and Group Settings](#2-local-user-and-group-settings)

---

> Commands starting with `#` may require you to start the command with `sudo` instead.

## 1 Initial Setup
### 1 Filesystem Configuration
#### 1 Disable Unused Filesystems
1. Ensure mounting of cramfs filesystems is disabled (Automated)

Run the following script to check if the filesystem is installed
``` bash
#!/usr/bin/env bash
{
	l_output="" l_output2=""
	l_mname="cramfs" # set module name
	# Check how module will be loaded
	l_loadable="$(modprobe -n -v "$l_mname")"
	if grep -Pq -- '^\h*install \/bin\/(true|false)' <<< "$l_loadable"; then
		l_output="$l_output\n - module: \"$l_mname\" is not loadable: \"$l_loadable\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loadable: \"$l_loadable\""
	fi
	# Check is the module currently loaded
	if ! lsmod | grep "$l_mname" > /dev/null 2>&1; then
		l_output="$l_output\n - module: \"$l_mname\" is not loaded"
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loaded"
	fi
	# Check if the module is deny listed
	if grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		l_output="$l_output\n - module: \"$l_mname\" is deny listed in: \"$(grep -Pl -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*)\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is not deny listed"
	fi
	# Report results. If no failures output in l_output2, we pass
	if [ -z "$l_output2" ]; then
		echo -e "\n- Audit Result:\n ** PASS **\n$l_output\n"
	else
		echo -e "\n- Audit Result:\n ** FAIL **\n - Reason(s) for audit failure:\n$l_output2\n"
		[ -n "$l_output" ] && echo -e "\n- Correctly set:\n$l_output\n"
	fi
}
```
Run the following script to remove the filesystem

``` bash
#!/usr/bin/env bash
{
	l_mname="cramfs" # set module name
	if ! modprobe -n -v "$l_mname" | grep -P -- '^\h*install \/bin\/(true|false)'; then
		echo -e " - setting module: \"$l_mname\" to be not loadable"
		echo -e "install $l_mname /bin/false" >> /etc/modprobe.d/"$l_mname".conf
	fi
	if lsmod | grep "$l_mname" > /dev/null 2>&1; then
		echo -e " - unloading module \"$l_mname\""
		modprobe -r "$l_mname"
	fi
	if ! grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		echo -e " - deny listing \"$l_mname\""
		echo -e "blacklist $l_mname" >> /etc/modprobe.d/"$l_mname".conf
	fi
}
```


2. Ensure mounting of squashfs filesystems is disabled (Automated)

> Snap packages use this filesystem

Run the following script to check if the filesystem is installed
``` bash
#!/usr/bin/env bash
{
	l_output="" l_output2=""
	l_mname="squashfs" # set module name
	# Check how module will be loaded
	l_loadable="$(modprobe -n -v "$l_mname")"
	if grep -Pq -- '^\h*install \/bin\/(true|false)' <<< "$l_loadable"; then
		l_output="$l_output\n - module: \"$l_mname\" is not loadable: \"$l_loadable\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loadable: \"$l_loadable\""
	fi
	# Check is the module currently loaded
	if ! lsmod | grep "$l_mname" > /dev/null 2>&1; then
		l_output="$l_output\n - module: \"$l_mname\" is not loaded"
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loaded"
	fi
	# Check if the module is deny listed
	if grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		l_output="$l_output\n - module: \"$l_mname\" is deny listed in: \"$(grep -Pl -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*)\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is not deny listed"
	fi
	# Report results. If no failures output in l_output2, we pass
	if [ -z "$l_output2" ]; then
		echo -e "\n- Audit Result:\n ** PASS **\n$l_output\n"
	else
		echo -e "\n- Audit Result:\n ** FAIL **\n - Reason(s) for audit failure:\n$l_output2\n"
		[ -n "$l_output" ] && echo -e "\n- Correctly set:\n$l_output\n"
	fi
}

```
Run the following script to remove the filesystem

``` bash
#!/usr/bin/env bash
{
 l_mname="squashfs" # set module name
 if ! modprobe -n -v "$l_mname" | grep -P -- '^\h*install \/bin\/(true|false)'; then
	echo -e " - setting module: \"$l_mname\" to be not loadable"
	echo -e "install $l_mname /bin/false" >> /etc/modprobe.d/"$l_mname".conf
 fi
 if lsmod | grep "$l_mname" > /dev/null 2>&1; then
	echo -e " - unloading module \"$l_mname\""
	modprobe -r "$l_mname"
 fi
 if ! grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
	echo -e " - deny listing \"$l_mname\""
	echo -e "blacklist $l_mname" >> /etc/modprobe.d/"$l_mname".conf
 fi
}

```

3. Ensure mounting of udf filesystems is disabled (Automated)

> Microsoft Azure uses this filesystem

Run the following script to check if the filesystem is installed
``` bash
#!/usr/bin/env bash
{
	l_output="" l_output2=""
	l_mname="udf" # set module name
	# Check how module will be loaded
	l_loadable="$(modprobe -n -v "$l_mname")"
	if grep -Pq -- '^\h*install \/bin\/(true|false)' <<< "$l_loadable"; then
		l_output="$l_output\n - module: \"$l_mname\" is not loadable: \"$l_loadable\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loadable: \"$l_loadable\""
	fi
	# Check is the module currently loaded
	if ! lsmod | grep "$l_mname" > /dev/null 2>&1; then
		l_output="$l_output\n - module: \"$l_mname\" is not loaded"
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loaded"
	fi
	# Check if the module is deny listed
	if grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		l_output="$l_output\n - module: \"$l_mname\" is deny listed in: \"$(grep -Pl -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*)\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is not deny listed"
	fi
	# Report results. If no failures output in l_output2, we pass
	if [ -z "$l_output2" ]; then
		echo -e "\n- Audit Result:\n ** PASS **\n$l_output\n"
	else
		echo -e "\n- Audit Result:\n ** FAIL **\n - Reason(s) for audit failure:\n$l_output2\n"
		[ -n "$l_output" ] && echo -e "\n- Correctly set:\n$l_output\n"
	fi
}
```
Run the following script to remove the filesystem

``` bash
#!/usr/bin/env bash
{
	l_mname="udf" # set module name
	if ! modprobe -n -v "$l_mname" | grep -P -- '^\h*install \/bin\/(true|false)'; then
		echo -e " - setting module: \"$l_mname\" to be not loadable"
		echo -e "install $l_mname /bin/false" >> /etc/modprobe.d/"$l_mname".conf
	fi
	if lsmod | grep "$l_mname" > /dev/null 2>&1; then
		echo -e " - unloading module \"$l_mname\""
		modprobe -r "$l_mname"
	fi
	if ! grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		echo -e " - deny listing \"$l_mname\""
		echo -e "blacklist $l_mname" >> /etc/modprobe.d/"$l_mname".conf
	fi
```

#### 2 Configure tmp
1. Ensure /tmp is a separate partition (Automated)

Run the following command and verify the output shows that `/tmp` is mounted.

```
# findmnt --kernel /tmp
TARGET SOURCE FSTYPE OPTIONS 
/tmp tmpfs tmpfs rw,nosuid,nodev,noexec,inode6
```

Ensure that systemd will mount the `/tmp` partition at boot time.

`# systemctl is-enabled tmp.mount`
`enabled`

First ensure that systemd is correctly configured to ensure that `/tmp` will be mounted at 
boot time.

`# systemctl unmask tmp.mount`

> **More Information**
> 
> ![Additional tmp information](images/ubuntu/1-1-2-1.png)

[\[1\]](https://www.freedesktop.org/wiki/Software/systemd/APIFileSystems/)
[\[2\]](https://www.freedesktop.org/software/systemd/man/latest/systemd-fstab-generator.html)

2. Ensure nodev option set on `/tmp` partition (Automated)

> This follows the same steps as 3. and 4.

Verify that the `nodev` option is set for the `/tmp` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /tmp | grep nodev

/tmp tmpfs tmpfs rw,nosuid,nodev,noexec,relatime,seclabel
```

Edit the `/etc/fstab` file and add `nodev` to the fourth field (mounting options) for the `/tmp`
partition.
Example:

`<device> /tmp <fstype> defaults,rw,nosuid,nodev,noexec,relatime 0 0`

Run the following command to remount `/tmp` with the configured options:

`# mount -o remount /tmp`

3. Ensure noexec option set on /tmp partition (Automated)

> This follows the same steps as 2. and 4.

Verify that the `noexec` option is set for the `/tmp` mount.
Run the following command to verify that the `noexec` mount option is set.
Example:

```
# findmnt --kernel /tmp | grep noexec

/tmp tmpfs tmpfs rw,nosuid,nodev,noexec,relatime,seclabel
```

Edit the `/etc/fstab` file and add `noexec` to the fourth field (mounting options) for the 
`/tmp` partition.
Example:

`<device> /tmp <fstype> defaults,rw,nosuid,nodev,noexec,relatime 0 0`

Run the following command to remount `/tmp` with the configured options:

`# mount -o remount /tmp`

4. Ensure nosuid option set on /tmp partition (Automated)

> This follows the same steps as 2. and 3.

Verify that the `nosuid` option is set for the `/tmp` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /tmp | grep nosuid

/tmp tmpfs tmpfs rw,nosuid,nodev,noexec,relatime,seclabel
```

Edit the `/etc/fstab` file and add `nosuid` to the fourth field (mounting options) for the 
`/tmp` partition.
Example:

`<device> /tmp <fstype> defaults,rw,nosuid,nodev,noexec,relatime 0 0`

Run the following command to remount `/tmp` with the configured options:

`# mount -o remount /tmp`

#### 3 Configure var
1. Ensure separate partition exists for /var (Automated)

Run the following command and verify output shows /var is mounted.
Example:

```
# findmnt --kernel /var

TARGET SOURCE FSTYPE OPTIONS
/var /dev/sdb ext4 rw,relatime,seclabel,data=ordered
```

For new installations, during installation create a custom partition setup and specify a 
separate partition for `/var`.
For systems that were previously installed, create a new partition and configure 
`/etc/fstab` as appropriate.

> When modifying `/var` it is advisable to bring the system to emergency mode (so auditd 
is not running), rename the existing directory, mount the new file system, and migrate 
the data over before returning to multi-user mode.

[\[1\]](https://tldp.org/HOWTO/LVM-HOWTO/)

2. Ensure nodev option set on /var partition (Automated)

> This follows the same steps as 3.

Verify that the `nodev` option is set for the `/var` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /var

/var /dev/sdb ext4 rw,nosuid,nodev,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nodev` option

**IF** the `/var` partition exists, edit the `/etc/fstab` file and add `nodev` to the fourth field 
(mounting options) for the `/var` partition.
Example:

`<device> /var <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var` with the configured options:

`# mount -o remount /var`

3. Ensure nosuid option set on /var partition (Automated)

> This follows the same steps as 3.

Verify that the `nosuid` option is set for the `/var` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /var

/var /dev/sdb ext4 rw,nosuid,nodev,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nosuid` option

**IF** the `/var` partition exists, edit the `/etc/fstab` file and add `nosuid` to the fourth field 
(mounting options) for the `/var` partition.
Example:

`<device> /var <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var` with the configured options:

`# mount -o remount /var`

#### 4 Configure var tmp
1. Ensure separate partition exists for /var/tmp (Automated)

Run the following command and verify output shows `/var/tmp` is mounted.
Example:

```
# findmnt --kernel /var/tmp

TARGET SOURCE FSTYPE OPTIONS
/var/tmp /dev/sdb ext4 rw,relatime,seclabel,data=ordered
```

For new installations, during installation create a custom partition setup and specify a 
separate partition for `/var/tmp`.
For systems that were previously installed, create a new partition and configure 
`/etc/fstab` as appropriate.

2. Ensure noexec option set on /var/tmp partition (Automated)

Verify that the `noexec` option is set for the `/var/tmp` mount.
Run the following command to verify that the `noexec` mount option is set.
Example:

```
# findmnt --kernel /var/tmp

/var/tmp /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `noexec` option

**IF** the `/var/tmp` partition exists, edit the `/etc/fstab` file and add `noexec` to the fourth field 
(mounting options) for the `/var/tmp` partition.
Example:

`<device> /var/tmp <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/tmp` with the configured options:

`# mount -o remount /var/tmp`

3. Ensure nosuid option set on /var/tmp partition (Automated)

Verify that the `nosuid` option is set for the `/var/tmp` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /var/tmp

/var/tmp /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nosuid` option

**IF** the `/var/tmp` partition exists, edit the `/etc/fstab` file and add `nosuid` to the fourth field 
(mounting options) for the `/var/tmp` partition.
Example:

`<device> /var/tmp <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/tmp` with the configured options:

`# mount -o remount /var/tmp`

4. Ensure nodev option set on /var/tmp partition (Automated)

Verify that the `nodev` option is set for the `/var/tmp` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /var/tmp

/var/tmp /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nodev` option

**IF** the `/var/tmp` partition exists, edit the `/etc/fstab` file and add `nodev` to the fourth field 
(mounting options) for the `/var/tmp` partition.
Example:

`<device> /var/tmp <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/tmp` with the configured options:

`# mount -o remount /var/tmp`


#### 5 Configure var log
1. Ensure separate partition exists for /var/log (Automated)

Run the following command and verify output shows `/var/log` is mounted.
Example:

```
# findmnt --kernel /var/log

TARGET SOURCE FSTYPE OPTIONS
/var/log /dev/sdb ext4 rw,relatime,seclabel,data=ordered
```

For new installations, during installation create a custom partition setup and specify a 
separate partition for `/var/log`.
For systems that were previously installed, create a new partition and configure 
`/etc/fstab` as appropriate.

2. Ensure nodev option set on /var/log partition (Automated)

Verify that the `nodev` option is set for the `/var/log` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /var/log

/var/log /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nodev` option

**IF** the `/var/log` partition exists, edit the `/etc/fstab` file and add `nodev` to the fourth field 
(mounting options) for the `/var/log` partition.
Example:

`<device> /var/log <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log` with the configured options:

`# mount -o remount /var/log`

3. Ensure noexec option set on /var/log partition (Automated)

Verify that the `noexec` option is set for the `/var/log` mount.
Run the following command to verify that the `noexec` mount option is set.
Example:

```
# findmnt --kernel /var/log

/var/log /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `noexec` option

**IF** the `/var/log` partition exists, edit the `/etc/fstab` file and add `noexec` to the fourth field 
(mounting options) for the `/var/log` partition.
Example:

`<device> /var/log <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log` with the configured options:

`# mount -o remount /var/log`

4. Ensure nosuid option set on /var/log partition (Automated)

Verify that the `nosuid` option is set for the `/var/log` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /var/log

/var/log /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nosuid` option

**IF** the `/var/log` partition exists, edit the `/etc/fstab` file and add `nosuid` to the fourth field 
(mounting options) for the `/var/log` partition.
Example:

`<device> /var/log <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log` with the configured options:

`# mount -o remount /var/log`

#### 6 Configure var log audit
1. Ensure separate partition exists for /var/log/audit (Automated)

Run the following command and verify output shows `/var/log/audit` is mounted.
Example:

```
# findmnt --kernel /var/log/audit

TARGET SOURCE FSTYPE OPTIONS
/var/log/audit /dev/sdb ext4 rw,relatime,seclabel,data=ordered
```

For new installations, during installation create a custom partition setup and specify a 
separate partition for `/var/log`.
For systems that were previously installed, create a new partition and configure 
`/etc/fstab` as appropriate.

2. Ensure noexec option set on /var/log/audit partition (Automated)

Verify that the `noexec` option is set for the `/var/log/audit` mount.
Run the following command to verify that the `noexec` mount option is set.
Example:

```
# findmnt --kernel /var/log/audit

/var/log/audit /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `noexec` option

**IF** the `/var/log/audit` partition exists, edit the `/etc/fstab` file and add `noexec` to the fourth field 
(mounting options) for the `/var/log/audit` partition.
Example:

`<device> /var/log/audit <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log/audit` with the configured options:

`# mount -o remount /var/log/audit`

3. Ensure nodev option set on /var/log/audit partition (Automated)

Verify that the `nodev` option is set for the `/var/log/audit` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /var/log/audit

/var/log/audit /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nodev` option

**IF** the `/var/log/audit` partition exists, edit the `/etc/fstab` file and add `nodev` to the fourth field 
(mounting options) for the `/var/log/audit` partition.
Example:

`<device> /var/log/audit <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log/audit` with the configured options:

`# mount -o remount /var/log/audit`

4. Ensure nosuid option set on /var/log/audit partition (Automated)

Verify that the `nosuid` option is set for the `/var/log/audit` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /var/log/audit

/var/log/audit /dev/sdb ext4 rw,nosuid,nodev,noexec,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nosuid` option

**IF** the `/var/log/audit` partition exists, edit the `/etc/fstab` file and add `nosuid` to the fourth field 
(mounting options) for the `/var/log/audit` partition.
Example:

`<device> /var/log/audit <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/var/log/audit` with the configured options:

`# mount -o remount /var/log/audit`


#### 7 Configure home
1. Ensure separate partition exists for /home (Automated)

Run the following command and verify output shows `/home` is mounted:

```
# findmnt --kernel /home

TARGET SOURCE FSTYPE OPTIONS
/home /dev/sdb ext4 rw,relatime,seclabel
```

For new installations, during installation create a custom partition setup and specify a 
separate partition for `/home`.
For systems that were previously installed, create a new partition and configure 
`/etc/fstab` as appropriate.

2. Ensure nodev option set on /home partition (Automated)

Verify that the `nodev` option is set for the `/home` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

```
# findmnt --kernel /home

/home /dev/sdb ext4 rw,nosuid,nodev,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nodev` option

**IF** the `/home` partition exists, edit the `/etc/fstab` file and add `nodev` to the fourth field 
(mounting options) for the `/home` partition.
Example:

`<device> /home <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/home` with the configured options:

`# mount -o remount /home`

3. Ensure nosuid option set on /home partition (Automated)

Verify that the `nosuid` option is set for the `/home` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

```
# findmnt --kernel /home

/home /dev/sdb ext4 rw,nosuid,nodev,relatime,seclabel
```

> **IF** output is produced, ensure it includes the `nosuid` option

**IF** the `/home` partition exists, edit the `/etc/fstab` file and add `nosuid` to the fourth field 
(mounting options) for the `/home` partition.
Example:

`<device> /home <fstype> defaults,rw,nosuid,nodev,relatime 0 0`

Run the following command to remount `/home` with the configured options:

`# mount -o remount /home`

#### 8 Configure dev shm
1. Ensure nodev option set on /dev/shm partition (Automated)

Verify that the `nodev` option is set for the `/dev/shm` mount.
Run the following command to verify that the `nodev` mount option is set.
Example:

`# findmnt --kernel /dev/shm | grep nodev`

Edit the `/etc/fstab` file and add nodev to the fourth field (mounting options) for the 
`/dev/shm` partition.
Run the following command to remount `/dev/shm` using the updated options from 
`/etc/fstab`:

`# mount -o remount /dev/shm`

2. Ensure noexec option set on /dev/shm partition (Automated)

Verify that the `noexec` option is set for the `/dev/shm` mount.
Run the following command to verify that the `noexec` mount option is set.
Example:

```
# findmnt --kernel /dev/shm | grep noexec

/dev/shm tmpfs tmpfs rw,nosuid,nodev,noexec,relatime,seclabel
```

Edit the `/etc/fstab` file and add `noexec` to the fourth field (mounting options) for the 
`/dev/shm` partition.
Example:

`<device> /dev/shm <fstype> defaults,rw,nosuid,nodev,noexec,relatime 0 0`

Run the following command to remount `/dev/shm` with the configured options:

`# mount -o remount /dev/shm`

3. Ensure nosuid option set on /dev/shm partition (Automated)

Verify that the `nosuid` option is set for the `/dev/shm` mount.
Run the following command to verify that the `nosuid` mount option is set.
Example:

`# findmnt --kernel /dev/shm | grep nosuid`

Edit the `/etc/fstab` file and add `nosuid` to the fourth field (mounting options) for the 
`/dev/shm` partition.
Run the following command to remount `/dev/shm` using the updated options from 
`/etc/fstab`:

`# mount -o remount /dev/shm`

#### 9 Disable Automounting

As a preference `autofs` should not be installed unless other packages depend on it.
Run the following command to verify `autofs` is not installed:

```
# systemctl is-enabled autofs

Failed to get unit file state for autofs.service: No such file or directory
```

Run the following command to verify `autofs` is not enabled if installed:

```
# systemctl is-enabled autofs

disabled
```

If there are no other packages that depends on `autofs`, remove the package with:

`# apt purge autofs`

**OR** if there are dependencies on the `autofs` package:
Run the following commands to mask `autofs`:

```
# systemctl stop autofs
# systemctl mask autofs
```

#### 10 Disable USB Storage

Run the following script to verify `usb-storage` is disabled:

``` bash
#!/usr/bin/env bash
{
	l_output="" l_output2=""
	l_mname="usb-storage" # set module name
	# Check how module will be loaded
	l_loadable="$(modprobe -n -v "$l_mname")"
	if grep -Pq -- '^\h*install \/bin\/(true|false)' <<< "$l_loadable"; then
		l_output="$l_output\n - module: \"$l_mname\" is not loadable: 
		\"$l_loadable\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loadable: 
		\"$l_loadable\""
	fi
	# Check is the module currently loaded
	if ! lsmod | grep "$l_mname" > /dev/null 2>&1; then
		l_output="$l_output\n - module: \"$l_mname\" is not loaded"
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is loaded"
	fi
	# Check if the module is deny listed
	if grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*; then
		l_output="$l_output\n - module: \"$l_mname\" is deny listed in: 
		\"$(grep -Pl -- "^\h*blacklist\h+$l_mname\b" /etc/modprobe.d/*)\""
	else
		l_output2="$l_output2\n - module: \"$l_mname\" is not deny listed"
	fi
	# Report results. If no failures output in l_output2, we pass
	if [ -z "$l_output2" ]; then
		echo -e "\n- Audit Result:\n ** PASS **\n$l_output\n"
	else
		echo -e "\n- Audit Result:\n ** FAIL **\n - Reason(s) for audit 
		failure:\n$l_output2\n"
		[ -n "$l_output" ] && echo -e "\n- Correctly set:\n$l_output\n"
	fi
}
```

Run the following script to disable `usb-storage`:

``` bash
#!/usr/bin/env bash
{
	l_mname="usb-storage" # set module name
	if ! modprobe -n -v "$l_mname" | grep -P -- '^\h*install \/bin\/(true|false)'; then
		echo -e " - setting module: \"$l_mname\" to be not loadable"
		echo -e "install $l_mname /bin/false" >> /etc/modprobe.d/"$l_mname".conf
	fi
	if lsmod | grep "$l_mname" > /dev/null 2>&1; then
		echo -e " - unloading module \"$l_mname\""
		modprobe -r "$l_mname"
	fi
	if ! grep -Pq -- "^\h*blacklist\h+$l_mname\b" /etc modprobe.d/*; then
		echo -e " - deny listing \"$l_mname\""
		echo -e "blacklist $l_mname" >> /etc/modprobe.d/"$l_mname".conf
	fi
}
```

### 2 Configure Software Updates
1. Ensure package manager repositories are configured (Manual)

Run the following command and verify package repositories are configured correctly:

`# apt-cache policy`

Configure your package manager repositories according to site policy.

2. Ensure GPG keys are configured (Manual)

Verify GPG keys are configured correctly for your package manager:

`# apt-key list`

Update your package manager GPG keys in accordance with site policy.

### 3 Filesystem Integrity Checking
1.  Ensure AIDE is installed (Automated)

Run the following commands to verify AIDE is installed:

```
# dpkg-query -W -f='${binary:Package}\t${Status}\t${db:Status-Status}\n' aide aide-common

aide install ok installed installed
aide-common install ok installed installed
```

Install AIDE using the appropriate package manager or manual installation:

`# apt install aide aide-common`

Configure AIDE as appropriate for your environment. Consult the AIDE documentation 
for options.

Run the following commands to initialize AIDE:

```
# aideinit
# mv /var/lib/aide/aide.db.new /var/lib/aide/aide.db
```

2. Ensure filesystem integrity is regularly checked (Automated)

Run the following commands to verify a cron job scheduled to run the aide check.

`# grep -Prs '^([^#\n\r]+\h+)?(\/usr\/s?bin\/|^\h*)aide(\.wrapper)?\h+(--check|([^#\n\r]+\h+)?\$AIDEARGS)\b' /etc/cron.* /etc/crontab /var/spool/cron/`

If cron will be used to schedule and run aide check:

Run the following command:

`# crontab -u root -e`

Add the following line to the crontab:

`0 5 * * * /usr/bin/aide.wrapper --config /etc/aide/aide.conf --check`

[\[1\]](https://github.com/konstruktoid/hardening/blob/master/config/aidecheck.service)
[\[2\]](https://github.com/konstruktoid/hardening/blob/master/config/aidecheck.timer)

### 4 Secure Boot Settings
1. Ensure bootloader password is set (Automated)

```
# grep "^set superusers" /boot/grub/grub.cfg

set superusers="<username>"

# grep "^password" /boot/grub/grub.cfg

password_pbkdf2 <username> <encrypted-password>
```

Create an encrypted password with `grub-mkpasswd-pbkdf2`:

```
# grub-mkpasswd-pbkdf2

Enter password: <password>
Reenter password: <password>
PBKDF2 hash of your password is <encrypted-password>
```

Add the following into a custom `/etc/grub.d` configuration file:

```
cat <<EOF
set superusers="<username>"
password_pbkdf2 <username> <encrypted-password>
EOF
```

Run the following command to update the grub2 configuration:

`# update-grub`

2. Ensure permissions on bootloader config are configured (Automated)

Run the following command and verify `Uid` and `Gid` are both `0/root` and Access is `0400` or more restrictive.

```
# stat /boot/grub/grub.cfg

Access: (0400/-r--------) Uid: ( 0/ root) Gid: ( 0/ root)
```

Run the following commands to set permissions on your grub configuration:

```
# chown root:root /boot/grub/grub.cfg
# chmod u-wx,go-rwx /boot/grub/grub.cfg
```

3. Ensure authentication required for single user mode (Automated)

Perform the following to determine if a password is set for the root user:

`# grep -Eq '^root:\$[0-9]' /etc/shadow || echo "root is locked"`

No result should be returned.

Run the following command and follow the prompts to set a password for the root user:

`# passwd root`

### 5 Additional Process Hardening
1. Ensure address space layout randomization (ASLR) is enabled (Automated)

Run the following script to verify kernel.randomize_va_space is set to 2:

``` bash
#!/usr/bin/env bash
{
	krp="" pafile="" fafile=""
	kpname="kernel.randomize_va_space" 
	kpvalue="2"
	searchloc="/run/sysctl.d/*.conf /etc/sysctl.d/*.conf /usr/local/lib/sysctl.d/*.conf /usr/lib/sysctl.d/*.conf /lib/sysctl.d/*.conf /etc/sysctl.conf"
	krp="$(sysctl "$kpname" | awk -F= '{print $2}' | xargs)"
	pafile="$(grep -Psl -- "^\h*$kpname\h*=\h*$kpvalue\b\h*(#.*)?$" $searchloc)"
	fafile="$(grep -s -- "^\s*$kpname" $searchloc | grep -Pv --"\h*=\h*$kpvalue\b\h*" | awk -F: '{print $1}')"
	if [ "$krp" = "$kpvalue" ] && [ -n "$pafile" ] && [ -z "$fafile" ]; then
		echo -e "\nPASS:\n\"$kpname\" is set to \"$kpvalue\" in the running configuration and in \"$pafile\""
	else
		echo -e "\nFAIL: "
		[ "$krp" != "$kpvalue" ] && echo -e "\"$kpname\" is set to \"$krp\" in the running configuration\n"
		[ -n "$fafile" ] && echo -e "\n\"$kpname\" is set incorrectly in \"$fafile\""
		[ -z "$pafile" ] && echo -e "\n\"$kpname = $kpvalue\" is not set in a kernel parameter configuration file\n"
	fi
}
```

Set the following parameter in `/etc/sysctl.conf` or a `/etc/sysctl.d/*` file:
Example:

`# printf "kernel.randomize_va_space = 2" >> /etc/sysctl.d/60-kernel_sysctl.conf`

Run the following command to set the active kernel parameter:

`# sysctl -w kernel.randomize_va_space=2`

[\[1\]](https://manpages.ubuntu.com/manpages/focal/man5/sysctl.d.5.html)

2. Ensure prelink is not installed (Automated)

Verify `prelink` is not installed:

```
# dpkg-query -W -f='${binary:Package}\t${Status}\t${db:Status-Status}\n' prelink

prelink unknown ok not-installed not-installed
```

Run the following command to restore binaries to normal:

`# prelink -ua`

Uninstall prelink using the appropriate package manager or manual installation:

`# apt purge prelink`

3. Ensure Automatic Error Reporting is not enabled (Automated)

Run the following command to verify that the Apport Error Reporting Service is not enabled:

`# dpkg-query -s apport > /dev/null 2>&1 && grep -Psi --'^\h*enabled\h*=\h*[^0]\b' /etc/default/apport`

Nothing should be returned.

Run the following command to verify that the apport service is not active:

`# systemctl is-active apport.service | grep '^active'`

Nothing should be returned.

Edit `/etc/default/apport` and add or edit the enabled parameter to equal 0:

`enabled=0`

Run the following commands to stop and disable the apport service

```
# systemctl stop apport.service
# systemctl --now disable apport.service
```

4. Ensure core dumps are restricted (Automated)

Run the following commands and verify output matches:

```
# grep -Es '^(\*|\s).*hard.*core.*(\s+#.*)?$' /etc/security/limits.conf /etc/security/limits.d/*

* hard core 0

# sysctl fs.suid_dumpable

fs.suid_dumpable = 0

# grep "fs.suid_dumpable" /etc/sysctl.conf /etc/sysctl.d/*

fs.suid_dumpable = 0
```

Run the following command to check if systemd-coredump is installed:  
`# systemctl is-enabled coredump.service`

if `enabled`, `masked`, or `disabled` is returned systemd-coredump is installed

Add the following line to `/etc/security/limits.conf` or a `/etc/security/limits.d/*`file:  
`* hard core 0`

Set the following parameter in `/etc/sysctl.conf` or a `/etc/sysctl.d/*` file:  
`fs.suid_dumpable = 0`

Run the following command to set the active kernel parameter:  
`# sysctl -w fs.suid_dumpable=0`

**IF** systemd-coredump is installed:  
edit `/etc/systemd/coredump.conf` and add/modify the following lines:

```
Storage=none
ProcessSizeMax=0
```

Run the command:  
`systemctl daemon-reload`

### 6 Mandatory Access Control
#### 1 Configure AppArmor
1. Ensure AppArmor is installed (Automated)

Verify that AppArmor is installed:

```
# dpkg-query -W -f='${binary:Package}\t${Status}\t${db:Status-Status}\n' apparmor

apparmor install ok installed installed
```

Install AppArmor.

`# apt install apparmor`

2. Ensure AppArmor is enabled in the bootloader configuration (Automated)

Run the following commands to verify that all `linux` lines have the `apparmor=1` and `security=apparmor` parameters set:

```
# grep "^\s*linux" /boot/grub/grub.cfg | grep -v "apparmor=1"

Nothing should be returned
# grep "^\s*linux" /boot/grub/grub.cfg | grep -v "security=apparmor"

Nothing should be returned
```

Edit `/etc/default/grub` and add the `apparmor=1` and `security=apparmor` parameters to the `GRUB_CMDLINE_LINUX=` line

`GRUB_CMDLINE_LINUX="apparmor=1 security=apparmor"`

Run the following command to update the `grub2` configuration:

`# update-grub`

3. Ensure all AppArmor Profiles are in enforce or complain mode (Automated)

Run the following command and verify that profiles are loaded, and are in either enforce or complain mode:

`# apparmor_status | grep profiles`

```
37 profiles are loaded.
35 profiles are in enforce mode.
2 profiles are in complain mode.
4 processes have profiles defined.
```

Run the following command and verify no processes are unconfined:

`# apparmor_status | grep processes`

```
4 processes have profiles defined.
4 processes are in enforce mode.
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
```

Run the following command to set all profiles to enforce mode

`# aa-enforce /etc/apparmor.d/*`

**OR**

Run the following command to set all profiles to complain mode:

`# aa-complain /etc/apparmor.d/*`

4. Ensure all AppArmor Profiles are enforcing (Automated)

Run the following commands and verify that profiles are loaded and are not in complain mode:

`# apparmor_status | grep profiles`

```
34 profiles are loaded.
34 profiles are in enforce mode.
0 profiles are in complain mode.
2 processes have profiles defined.
```

Run the following command and verify that no processes are unconfined:

`apparmor_status | grep processes`

```
2 processes have profiles defined.
2 processes are in enforce mode.
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.
```

Run the following command to set all profiles to enforce mode:

`# aa-enforce /etc/apparmor.d/*`

### 7 Command Line Warning Banners
1. Ensure message of the day is configured properly (Automated)

Run the following command and verify no results are returned:

`# grep -Eis "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= -f2 | sed -e 's/"//g'))" /etc/motd`

Edit the `/etc/motd` file with the appropriate contents according to your site policy, 
remove any instances of `\m`, `\r`, `\s`, `\v` or references to the OS platform

**OR** if the motd is not used, this file can be removed.  
Run the following command to remove the motd file:

`# rm /etc/motd`

2. Ensure local login warning banner is configured properly (Automated)

Run the following command and verify that the contents match site policy:

`# cat /etc/issue`

Run the following command and verify no results are returned:

`# grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= -f2 | sed -e 's/"//g'))" /etc/issue`

Edit the `/etc/issue` file with the appropriate contents according to your site policy, remove any instances of `\m`, `\r`, `\s`, `\v` or references to the `OS platform`

`# echo "Authorized uses only. All activity may be monitored and reported." > /etc/issue`

3. Ensure remote login warning banner is configured properly (Automated)

Run the following command and verify that the contents match site policy:

`# cat /etc/issue.net`

Run the following command and verify no results are returned:

`# grep -E -i "(\\\v|\\\r|\\\m|\\\s|$(grep '^ID=' /etc/os-release | cut -d= -f2 | sed -e 's/"//g'))" /etc/issue.net`

Edit the `/etc/issue.net` file with the appropriate contents according to your site policy, remove any instances of `\m`, `\r`, `\s`, `\v` or references to the `OS platform`

`# echo "Authorized uses only. All activity may be monitored and reported." > /etc/issue.net`

4. Ensure permissions on /etc/motd are configured (Automated)

Run the following command and verify: `Uid` and `Gid` are both `0/root` and `Access` is `644`, or the file doesn't exist.

```
# stat -L /etc/motd

Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
	OR
stat: cannot stat '/etc/motd': No such file or directory
```

Run the following commands to set permissions on `/etc/motd`:

```
# chown root:root $(readlink -e /etc/motd)
# chmod u-x,go-wx $(readlink -e /etc/motd)
```

**OR** run the following command to remove the `/etc/motd` file:

`# rm /etc/motd`

5. Ensure permissions on /etc/issue are configured (Automated)

Run the following command and verify `Uid` and `Gid` are both `0/root` and `Access` is `644`:

```
# stat -L /etc/issue

Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```

Run the following commands to set permissions on `/etc/issue`:

```
# chown root:root $(readlink -e /etc/issue)
# chmod u-x,go-wx $(readlink -e /etc/issue)
```

6. Ensure permissions on /etc/issue.net are configured (Automated)

Run the following command and verify `Uid` and `Gid` are both `0/root` and `Access` is `644`:

```
# stat -L /etc/issue.net

Access: (0644/-rw-r--r--) Uid: ( 0/ root) Gid: ( 0/ root)
```

Run the following commands to set permissions on `/etc/issue.net`:

```
# chown root:root $(readlink -e /etc/issue.net)
# chmod u-x,go-wx $(readlink -e /etc/issue.net)
```

### 8 GNOME Display Manager
1. Ensure GNOME Display Manager is removed (Automated)



2. 



3. 



4. 



5. 



6. 



7. 



8. 



9. 



10. 



### 9 Ensure updates patches and additional security software are installed

Run the following commands: 

`# apt update`

`# apt upgrade`

---

## 2 Services
### Configure Time Synchronization

### Special Purpose Services

### Service Clients

---

## 3 Network Configuration
### Disable Unused Network Protocols and Devices

### Network Parameters Host Only

### Network Parameters Host and Router

### Uncommon Network Protocols

### Firewall Configuration

---

## 4 Logging and Auditing

###  1 Configure System Accounting (auditd)

1. **Ensure auditing is enabled**

	default event logs will be logged to `/var/log/audit/audit.log`

	which will be configured in `/etc/audit/auditd.conf`.

	The following types of audit rules can be specified:
	* Control rules: Configuration of the auditing system.
	* File system rules: Allow the auditing of access to a particular file or a directory.
	Also known as file watches.
	* System call rules: Allow logging of system calls that any specified program
	makes.  

	<br>

	Audit rules can be set:
	* On the command line using the auditctl utility. These rules are not persistent
	across reboots.
    * In `/etc/audit/audit.rules`. These rules have to be merged and loaded before
	they are active.   

	<br>

	Run the following command and verify and audispd-plugins are installed:
	```
	# dpkg-query -W -f='${binary:Package}\t${Status}\t${db:Status-Status}\n'
	```
	```
	auditd audispd-plugins   

	audispd-plugins install ok installed installed
	auditd install ok installed installed
	```

	If plugin is not installed run the following command
	```
	# apt install auditd audispd-plugins

	```

	<br>

	**Ensure auditd service is enabled and active (Automated)**  

	Run the following command to verify `auditd` is enabled:
	```
	# systemctl is-enabled auditd
	```
	```
	enabled
	```

	Verify result is "enabled".
	Run the following command to verify auditd is active:
	```
	# systemctl is-active auditd
	```
	```
	active

	```
	Verify result is active

	Run the following command to enable and start auditd:
	```
	# systemctl --now enable auditd
	```

	<br>

	**Ensure auditing for processes that start prior to auditd is
	enabled (Automated)**

	Run the following command:
	```
	# find /boot -type f -name 'grub.cfg' -exec grep -Ph -- '^\h*linux' {} + |
	grep -v 'audit=1'

	```
	Nothing should be returned.

	*Remediation:*

	Edit /etc/default/grub and add audit=1 to GRUB_CMDLINE_LINUX:
	Example:

	```
	GRUB_CMDLINE_LINUX="audit=1"
	```

	Run the following command to update the grub2 configuration:
	```
	# update-grub
	```

	<br>

	**Ensure audit_backlog_limit is sufficient (Automated)**

	Run the following command and verify the audit_backlog_limit= parameter is set:

	```
	# find /boot -type f -name 'grub.cfg' -exec grep -Ph -- '^\h*linux' {} + |
	grep -Pv 'audit_backlog_limit=\d+\b'

	```
	Nothing should be returned.

	*Remediation:*   

	Edit `/etc/default/` grub and add `audit_backlog_limit=N` to GRUB_CMDLINE_LINUX.
	The recommended size for `N` is `8192` or larger.
	Example:

	```
	GRUB_CMDLINE_LINUX="audit_backlog_limit=8192"
	```

	Run the following command to update the grub2 configuration:

	```
	# update-grub
	```

	Default Value:
	if `audit_backlog_limit` is not set, the system defaults to `audit_backlog_limit=64`   
	   
	<br>

2. Configure Data Retention

3. Configure auditd rules 

4. Configure auditd file access  

### 2 Configure Logging

1. Sercurity principals for logging
   
2. Configure journald 
   
3. Ensure journald is configured to send logs to remote log host
   
4. configure rsyslog 


---

## 5 Access Authentication and Authorization

### 1 Configure time-based job schedulers 

### 2 Configure SSH Server 

### 3 Configure privilege escalation 

### 4 Configure PAM

### 5 User Account and 

---

## 6 System Maintenance

### 1 System File Permission 

### 2 Local User and Group Settings 

