---
layout: post
title: bash scripts for Nautilus/odrive integration
date: 2017-03-16 12:25
---

I saw an [article](https://fedoramagazine.org/integrating-scripts-nautilus/) on my Twitter feed that had been shared by [Scott Lowe](http://blog.scottlowe.org) about using scripts to that integrate into Nautilus (a pretty standard file manager for Linux distributions).  The article is from Fedora Magazine, but everything in the article worked for me on Ubuntu GNOME.

I've wanted to find a way use the [odrive Sync Agent](https://docs.odrive.com/v1.0/docs/odrive-sync-agent) from the GUI to make it more usable.  This seemed like the perfect way to do it.  So far I've been able to get simple **Sync** and **Unsync** scripts working:

First, make the required directory:

  `mkdir -p ~/.local/share/nautilus/scripts`

Next, we create a script file:

  `touch ~/.local/share/nautilus/scripts/Sync`

Then, we make it executable:

  `chmod +x ~/.local/share/nautilus/scripts/Sync`

Here is the script I came up with:

```
#!/bin/bash 
# Setting IFS to break on newlines because that's how the 
# $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS variable is created
IFS=$'\n'
# Setting path for the odrive binary
odrive="/home/nightcrawler/.odrive-agent/bin/odrive"
# Check if the odriveagent process is running
if pgrep -x "odriveagent" > /dev/null
then
	for i in $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS; do
		if $odrive sync "$i"
		then
			notify-send Synced "$i"
		else
			notify-send "Sync Failed" "$i"
		fi
	done
else
	notify-send Sync "The odrive agent is not running"
fi
```

It's that simple.  The same script will work to unsync files if you change the line: 

`if $odrive sync "$i"` 

to this: 

`if $odrive unsync "$i"`

I'm going to work on another script that will sync an entire folder and it's contents.  When I come up with that, I'll post it here too.
