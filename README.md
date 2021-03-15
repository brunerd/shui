# shui
shui is a shell script wrapper for presenting user dialogs in Applescript without needing to know Applescript

Download shui from the sources folder and if need be make executable with `chmod ugo+x ./shui` while in the same folder.

To get help: `./shui help`  
To see a demo of all the actions: `./shui demo`

* shui allows you to present first class macOS interfaces from your shell scripts with no other external dependencies
* shui can be embedded and invoked by your shell scripts
* shui can also output the Applescript you need to invoke via `osascript` in your own scripts (use the `-o` or `-V` option)
* shui can be pronounced however you like, such as: "schway" or "shoe-eee", it is a contraction of shell + gui

## shui demo video

See the shui demo in action:  
[![shui demo](https://img.youtube.com/vi/Yms5oOvVfz0/0.jpg)](https://www.youtube.com/watch?v=Yms5oOvVfz0)

## shui help contents
```
shui - add Applescript user interaction to your shell script (https://github.com/brunerd/shui)

Usage:
shui [<UI Type>] -p "<prompt text>" 

UI Types:
alert: alert with icon of the calling appication (use -a), prompt (-p) is bold, message text (-P) is smaller, can set level (-L) to critical
application: presents list of Launch Services registered applicatins can specify -m for multiple
button (default): button based reply, use -b to change button names (max 3), defaults to "Cancel,OK" like Applescript does
color: no options, presents color picker and returns "R,G,B" with individual values (0-65535)
file: pick one file or multiple (-m), -d for default folder, -P to specify preferred file extensions or UTIs, -h hidden items, -s show bundle contents
folder: pick one file or multiple (-m), -d for default folder, -P to specify preferred file extensions, -h hidden items, -s show bundle contents
list: pick one or mutiple (-m) items from a list of choices, use -D for custom delimiter (comma default)
text: like button but with a single line text entry box, set pre-filled text with -P, hidden text with -h
url: returns a URL, default is file servers, use -S to set the kind of server to look for, valid value listed below

Required:
-p "prompt text"	alert/button/file/folder/list: the text prompt presented to the user, required for all type (except color)

Options (begins with UI type(s) which apply or "all"):

-a "<application>"	all (except filename): specify the application that will present the Applescript dialog, alert will have app icon and block app

-b "<button>;...;..."	button: max 3 button names, comma or semi-colon delimited (if commas AND semi-colons are present, semis "win") 
						if no buttons specified it defaults to the standard Applescript "Cancel,OK"
-b "<OK>,[<Cancel>]"	list: max 2 button names, comma delimited, first is the OK button name, second is Cancel button name (optional)

-B "n"			all: beep n number of times

-c "name/number"	button: specify the cancel button by name or number (use with alert and buttons named "Cancel")

-d "name/number"	button: default button name or number (0 will suppress Applescript OK button default if -b not specified)
-d "<Folder Path>"	file/folder: default location (Unix Path), using ~ will resolve to the console user's home folder

-D "<delimiter>"	list: Delimiter for -l list items, can specify literal character like $'\n' or use these two named shortcuts "LF" "IFS"

-e 			list: allow empty selection

-g "seconds"		alert/button: give-up timeout in seconds (dismisses windows and moves on)

-h			text: hidden text entry (dots)
-h			file/folder: show hidden files in picker

-i "<path>"		button: path to icon file or application bundle (Icon^M first, then Info.plist)

-l "item,item,..."	list: items for list, comma delimited is default unless newline is detected (change delimiter with -D)

-L "<level>"		alert: default is ‌"informational"/"‌warning" (same), "critical" adds a caution sign over the calling app (-a) icon

-m			application/file/folder/list: allow multiple selections

-n			alert/button: non-Blocking window, spawns to a background and moves on, response is not captured, one button maximum
 			Note: If this is NOT the last alert window it is advisable to use a giveup (-g) value, additional dialogs will occlude previous ones (use -X to clear)

-N			alert/button: same as (-n) non-blocking window except button 1 is default

-o			all: output Applescript code

-P "message text"	alert: "parenthetical" message text below the bold prompt text
-P "<R>,<G>,<B>"	color: pre-chosen RGB color values 0-65536
-P "filename"		filename: pre-filled file name (default folder set with -d)
-P "extension,UTI,..."	file: "preferred" file extensions/UTIs available to choose in picker
-P "item,item..."	list: pre-chosen items, default delimiter is comma unless a newline is present or can be set with -D
-P "pre-fill text"	text: pre-filled text (may be hidden with -h)

-S "<Service>"		url: look for specific services, useful values are: "file" (default) and "web" 
			Less useful but still valid values are: "ftp", "media", "telnet", "news", and "remote" (applications)

-s			file/folder: show package/bundle contents (as a folder basically)

-t "Title text"		button/list/text: window title (can be hardcoded)

-v			all: output results in format suitable for initializing shell variables using eval
-V			all: output results in format suitable for initializing shell variables plus Applescript and raw Result/Error output from "osascript"

-X			alert/button: kill any "System Events" based windows (-a specified), useful for non-Blocking without give up

shui sets these GLOBAL variables within the script's running context (use -v to output these if shui is standalone/non-embedded):
	lastButton - value of button from button, text, and list replies
	lastText   - Text string from text reply
	lastChoice - File or Folder Unix path from files/filename/folders
	lastGaveUp - true or false, button and text reply types only, when a give up (-g) value is specified
	lastCancel - true or false, since Cancel produces an error and no result this helps determine if clicked
	lastResult - full Result output (stdout) from osascript that is parsed into the above values
	lastError  - full Error (stderr) output from osascript
```
