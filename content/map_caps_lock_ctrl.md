---
title: "Map Caps Lock to Ctrl"
author: "John Coleman"
date: "2023-04-05"
tags:
     - howto
---

# Map Caps Lock to Ctrl

Map caps lock to ctrl in software

## Gnome Using Tweak Tool

![](map_caps_lock_ctrl_tweak.png)

## Gnome Using dconf-editor

![](map_caps_lock_ctrl_dconf.png)

## Xfce Using Settings Manager

Settings Manager -> Session and Startup -> Application Autostart

`setxkbmap -option 'ctrl:nocaps'`

creates an entry in $HOME/.config/autostart

![](map_caps_lock_ctrl_xfce.png)
