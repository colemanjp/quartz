---
title: "Paladin Forensic Crash With LUKS and LVM"
author: "John Coleman"
date: "2025-01-07"
tags: 
     - howto
     - forensics
---

# Sumuri Paladin Forensic Carbon 8.05 Tool Crash with LUKS and LVM
While trying to examine a Linux machine with encrypted LVMs in **Forensic Mode,** the Paladin Toolbox GUI crashes and won't restart, either from the GUI or /usr/bin/toolbox.

Since **Forensic Mode** requires you to use Paladin Toolbox to mount read+write and prevents you from mounting storage read+write from the command line, you are stuck.

# Solution
Before decrypting and mounting the LVMs, mount your target disk read-write with the GUI Toolbox 

## Mount Target Disk with GUI

## Open a Terminal

## Find Source Partition

`sudo fdisk -l`

## Decrypt Source

`sudo cryptsetup luksOpen /dev/nvme0n1p6 xxx`

## Process LVMs

`sudo vgscan`

`sudo lvscan`

## Mount Filesystem 

`sudo mkdir /tmp/home`

`sudo mount -o ro,noload /dev/mapper/fedora_localhost--live-home /tmp/home`

## Process Evidence
