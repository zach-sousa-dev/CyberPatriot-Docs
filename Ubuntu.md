# Ubuntu 22

## Contents

### Other Pages
- [Main Page](README.md)
- [Windows 10](Windows_10.md)
- [Windows Server](Server.md)
- [Debian](Debian.md)

### Sub Headings
- [1 Initial Setup](#1-initial-setup)
  - [Filesystem Configuration](#filesystem-configuration)
  - [Configure Software Updates](#configure-software-updates)
  - [Filesystem Integrity Checking](#filesystem-integrity-checking)
  - [Secure Boot Settings](#secure-boot-settings)
  - [Additional Process Hardening](#additional-process-hardening)
  - [Mandatory Access Control](#mandatory-access-control)
  - [Command Line Warning Banners](#command-line-warning-banners)
  - [GNOME Display Manager](#gnome-display-manager)
- [2 Services](#2-services)
  - [Configure Time Synchronization](#configure-time-synchronization)
  - [Special Purpose Services](#special-purpose-services)
  - [Service Clients](#service-clients)
- [3 Network Configuration](#3-network-configuration)
  - [Disable Unused Network Protocols and Devices](#disable-unused-network-protocols-and-devices)
  - [Network Parameters(Host Only)](#network-parameters-host-only)
  - [Network Parameters Host and Router](#network-parameters-host-and-router)
  - [Uncommon Network Protocols](#uncommon-network-protocols)
  - [Firewall Configuration](#firewall-configuration)
- [4 Logging and Auditing](#4-logging-and-auditing)
- [5 Access Authentication and Authorization](#5-access-authentication-and-authorization)
- [6 System Maintenance](#6-system-maintenance)

## 1 Initial Setup
### Filesystem Configuration
#### Disable Unused Filesystems
1. Ensure mounting of cramfs filesystems is disabled 
(Automated)

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


2. Ensure mounting of squashfs filesystems is disabled 
(Automated)

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

3. Ensure mounting of udf filesystems is disabled 
(Automated)

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

### Configure Software Updates

### Filesystem Integrity Checking

### Secure Boot Settings

### Additional Process Hardening

### Mandatory Access Control

### Command Line Warning Banners

### GNOME Display Manager

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

---

## 5 Access Authentication and Authorization

---

## 6 System Maintenance
