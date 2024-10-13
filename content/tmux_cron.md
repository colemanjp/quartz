---
title: "Run Command in Tmux from Cron"
author: "John Coleman"
date: "2023-02-02"
tags: 
     - howto
---

Application run from cron needs a tty

One way to accomplish that is to run it inside tmux.

# Wrapper Script Manages tmux and Launches Command

Run the command `script01.sh` inside tmux. Create a separate tmux session for `script01.sh` to make this easy.

```
#!/bin/sh

# Script that is run in tmux
SCRIPT="${HOME}/script01.sh"

# Name the tmux session
SESSION=script01

# If session doesn't exist, create it
if /usr/bin/tmux has -t "${SESSION}" 2>/dev/null
then
        :
else
        /usr/bin/tmux new-session -d -s "${SESSION}"
fi

# Run SCRIPT in the tmux SESSION
/usr/bin/tmux send-keys -t "${SESSION}":0 "${SCRIPT}" ENTER
```

# Launch the Wrapper Script from cron

`15 10 * * * "${HOME}"/wrapper.sh > /dev/null`
