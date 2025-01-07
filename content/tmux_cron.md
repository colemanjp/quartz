---
title: "Run Command in Tmux from Cron"
author: "John Coleman"
date: "2025-01-07"
tags: 
     - howto
---

Application run from cron needs a tty

One way to accomplish that is to run it inside tmux.

# Wrapper Script Manages tmux and Launches Command

Run a command inside tmux. Create a separate tmux session to make this easy.

```
#!/bin/sh

# Check if required arguments are provided
if [ $# -ne 2 ]; then
    echo "Usage: $0 <script_path> <session_name>"
    exit 1
fi

# Script that is run in tmux
SCRIPT="$1"
# Name the tmux session
SESSION="$2"

# Verify script exists
if [ ! -f "${SCRIPT}" ]; then
    echo "Error: Script '${SCRIPT}' not found"
    exit 1
fi

# If session doesn't exist, create it
if /usr/bin/tmux has -t "${SESSION}" 2>/dev/null; then
    :
else
    /usr/bin/tmux new-session -d -s "${SESSION}"
fi

# Run SCRIPT in the tmux SESSION
/usr/bin/tmux send-keys -t "${SESSION}":0 "${SCRIPT}" ENTER
```
# Launch the Wrapper Script example.sh in Session "example" from cron

`15 10 * * * "${HOME}"/wrapper.sh "${HOME}/example.sh" example> /dev/null`
