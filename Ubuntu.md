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
		- [7 Command Line Warning Banners](#7-command-line-warning-banners)
		- [8 GNOME Display Manager](#8-gnome-display-manager)
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

### 3 Filesystem Integrity Checking

### 4 Secure Boot Settings

### 5 Additional Process Hardening

### 6 Mandatory Access Control

### 7 Command Line Warning Banners

### 8 GNOME Display Manager

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

1. Ensure auditing is enabled 

2. Configure  Data Retention

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
