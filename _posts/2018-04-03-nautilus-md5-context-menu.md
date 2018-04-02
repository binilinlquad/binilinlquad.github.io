---
layout: default
title: MD5 inside Nautilus
----
Nautilus script for MD5 through Context menu
============================================
Grab md5 and zenity through apt-get and put this script into `~/.local/share/nautilus/script/md5`

~~~ bash
#!/bin/bash
zenity --info --text `md5sum $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS` --title "md5 of $NAUTILUS_SCRIPT_SELECTED_FILE_PATHS"
~~~

then make it executable with `chmod +x ~/.local/share/nautilus/script/md5`

After restart Nautilus, you can find it under Scripts when right-click at file
Steps above is run in Ubuntu 14.04
[Reference](https://help.ubuntu.com/community/NautilusScriptsHowto)
