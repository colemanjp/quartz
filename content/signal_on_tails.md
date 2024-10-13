---
title: "Install Signal on Tails"
author: "John Coleman"
date: "2023-01-09"
tags: 
     - howto
---
Install and configure Signal with persistence on Tails

# Preparation

Boot off Tails USB

Enable admin password

Unlock persistent storage

Start 

Start Tor Connection

Applications > Tails > Persistent Storage > Network Connections > On

Applications > Tails > Persistent Storage > Additional Software > On

Applications > Tails > Persistent Storage > Dotfiles > On

# Install Signal

Open Terminal application

## Create Directories for Persistence

`sudo mkdir -m 755 /live/persistence/TailsData_unlocked/sources.list.d`

`sudo mkdir -m 755 /live/persistence/TailsData_unlocked/keyrings`

`sudo mkdir -m 755 /live/persistence/TailsData_unlocked/Signal`

`sudo chown amnesia:amnesia /live/persistence/TailsData_unlocked/Signal`

`sudo mkdir -m755 -p /live/persistence/TailsData_unlocked/dotfiles/.local/share/applications`

`cd /live/persistence/TailsData_unlocked/dotfiles/`

`sudo chown -Rh amnesia:amnesia .local`

## Add Persistence Directories to Persistence.conf 

```
sudo bash -c "echo '/etc/apt/sources.list.d  source=sources.list.d,link' >> /live/persistence/TailsData_unlocked/persistence.conf"
```


```
sudo bash -c "echo '/usr/share/keyrings/persistent source=keyrings' >> /live/persistence/TailsData_unlocked/persistence.conf"
```

```
sudo bash -c "echo '/home/amnesia/.config/Signal source=Signal' >> /live/persistence/TailsData_unlocked/persistence.conf"
```
## Download and Install Signal GPG Keyring

`cd $HOME`

`torify wget https://updates.signal.org/desktop/apt/keys.asc -O- | gpg --dearmor > signal-desktop-keyring.gpg`

`sudo cp signal-desktop-keyring.gpg /live/persistence/TailsData_unlocked/keyrings`

```
sudo bash -c "echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/persistent/signal-desktop-keyring.gpg] tor+https://updates.signal.org/desktop/apt xenial main' > /live/persistence/TailsData_unlocked/sources.list.d/signal.list"
```

## Install Custom Signal Startup Script

This script sets environment variables needed run Signal on Tails

```
cat >$HOME/Persistent/signal.sh<<EOF
#!/bin/sh
export HTTP_PROXY=socks://127.0.0.1:9050
export HTTPS_PROXY=socks://127.0.0.1:9050
signal-desktop
EOF
```
`chmod 755 $HOME/Persistent/signal.sh`

## Create Desktop Script for Signal 

This creates an icon for the custom signal.sh script.  When you run Signal, pick the generic diamond Signal icon rather than the built in one. 

```
cat >/live/persistence/TailsData_unlocked/dotfiles/.local/share/applications/Signal.desktop<<EOF
[Desktop Entry]
Name=Signal
GenericName=Signal Desktop Messenger
Exec=/home/amnesia/Persistent/signal.sh
Terminal=false
Type=Application
EOF
```

## Reboot and Install signal-desktop Package

`sudo reboot`

`sudo apt get update`

`sudo apt install signal-desktop`

Click "Install Every Time" when prompted.  This creates an entry in /live/persistence/TailsData_unlocked/live-additional-software.conf 
          


# Reference

[Signal download](https://signal.org/en/download/linux/)

[Add new repos to Tails](https://tails.boum.org/doc/first_steps/additional_software/#index6h1)

[Apt doesn't allow symlinks for signing keys](https://gitlab.tails.boum.org/tails/tails/-/issues/17510)
