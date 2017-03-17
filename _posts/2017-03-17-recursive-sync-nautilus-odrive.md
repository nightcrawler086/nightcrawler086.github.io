---
layout: post
title: Recursive Sync with Nautilus/bash/odrive 
date: 2017-03-17 13:14
---

Continuing on from my previous post, I've come up with way to recursively sync a selected cloud folder or folders (`FolderName.cloudf`) from Nautilus.  If you want to know how to use scripts with Nautilus have a look at my previous post [here](http://blog.nightcrawler.me/2017/03/16/bash-scripts-nautilus-odrive-integration/).

The odrive client on the Mac had an option called **Sync subfolders and files**.  I was trying to mimic this functionality if I could.  I'll put the whole script at the end, but there are a couple pieces that I think warrant further explanation.

The first problem I had to solve was how to sync everything within the selected directory, when that directory could contain more directories?  The thing about odrive is, you won't see what's in the folder until you sync it.  The answer is a simple while loop:

`while [[ $(find "${i//.cloudf}" -type f -name "*.cloud*") ]]`

So, this while loop runs as long as it files files with a `.cloud` (file) or `.cloudf` (folder) extension inside the selected directory.  The `"${i//.cloudf}"` piece just trims off the `.cloudf` extension of the folder.  The while loop runs after I sync the selected folder, so it no longer has the `.cloudf` extension.

The next piece to figure out was how to sync all the files.  In my **Sync** and **Unsync** scripts the selected files were in the `$NAUTILUS_SCRIPT_SELECTED_FILE_PATHS` variable.  This is not the case when doing this recursively.  We can use `find` again to handle this.  I actually used two different find commands when I was writing this.  I'll show both of them.

The first `find` command:

`find "${i//.cloudf}" -type f -name "*.cloud*" -exec $ODRIVE sync "{}" \;`

This command worked just fine, but it was **slooow**.  I looked around and found that I could speed this up a little (or a lot?) with `xargs`.

The second `find` command with `xargs`:

`find "${i//.cloudf}" -type f -name "*.cloud*" -print0 | xargs -0 -n1 -P 4 $ODRIVE sync`

This command worked beautifully.  The `-P 4` tells xargs to use all 4 CPUs in my system.  The CPU usage in my system did jump quite a bit.  Here's what `htop` looked like while after I invoked the script:

[htop during recursive sync]({{ site.url }}/public/htop-recursive-sync.gif)

Here's what the whole script looks like:

```
#!/bin/bash 
# Setting IFS to break on newlines because that's how the 
# $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS variable is created

IFS=$'\n'
ODRIVE="/home/nightcrawler/.odrive-agent/bin/odrive"

if pgrep -x "odriveagent" > /dev/null
then
	for i in $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS; do
		if $ODRIVE sync "$i"
		then
			while [[ $(find "${i//.cloudf}" -type f -name "*.cloud*") ]]; do
				find "${i//.cloudf}" -type f -name "*.cloud*" -print0 | xargs -0 -n1 -P 4 $ODRIVE sync
			done
			notify-send "Recursive Sync Complete" "${i//.cloudf}"
		else
			notify-send "Sync Failed" "$i"
		fi
	done
else
	notify-send Sync "The odrive agent is not running"
fi
```

The only thing I might try to do is find a way to speed up the find command in the `while` loop.  Maybe using the `-maxdepth` option with a variable that increases with each iteration of the loop.
