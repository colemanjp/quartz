---
title: "Erase Disk with hdparm"
author: "John Coleman"
date: "2023-02-19"
tags: 
     - howto
---

# Erase Disk with hdparm

Erase disk /dev/sdc

## Verify disk is not mounted

## Confirm not Frozen. Check if Enhanced Erase is Supported. 


`/usr/sbin/hdparm -I /dev/sdc | egrep -i 'frozen|erase|security level'`
```
	  not	frozen
	  		supported: enhanced erase
	  	2min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```
## Set Password

Will be reset to null on erase

`/usr/sbin/hdparm --user-master u --security-set-pass p /dev/sdc`
```
	  security_password: "p"
	  
	  /dev/sdc:
	   Issuing SECURITY_SET_PASS command, password="p", user=user, mode=high
```
## Confirm Password Set (Security level high)

`/usr/sbin/hdparm -I /dev/sdc | egrep -i 'frozen|erase|security level'`
```
	  	not	frozen
	  		supported: enhanced erase
	  	Security level high
	  	2min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```
## Erase Drive 

`/usr/sbin/hdparm --user-master u --security-erase-enhanced p /dev/sdc`
	

## Reference 

[ATA Secure Erase](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase)
