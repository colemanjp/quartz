---
title: "Proteus with Ax Instead of Axiom"
author: "John Coleman"
date: "2025-01-15"
tags: 
     - howto
---

The Project Discovery [proteus](https://github.com/pry0cc/proteus) automation tool uses [axiom](https://github.com/pry0cc/axiom). I'm not sure if proteus is still maintained, but I want to continue using it for automation with [ax](https://github.com/attacksurge/ax), which replaced axiom. Fortunately, it is relatively simple to port proteus to use ax. 

I run my fork of proteus [https://github.com/colemanjp/proteus](https://github.com/colemanjp/proteus) with ax on an LXC container running debian-12-standard_12.7-1_amd64.tar.zst.

You can see the simple changes [here](https://github.com/pry0cc/proteus/compare/main...colemanjp:proteus:main). Some edits may be needed for your environment. In particular, the mounts in docker-compose.yml

