# shui
shui is a shell script wrapper for presenting user dialogs in Applescript without needing to know Applescript

Download shui from the sources folder and if need be make executable with `chmod ugo+x ./shui` while in the same folder.

To get help: `./shui help`  
To see a demo of all the actions: `./shui demo`

* shui is meant to be embedded in your scripts
* shui will allow you to present first class macOS interfaces from your shell scripts with no other external dependencies
* shui will set 4 global shell variables after it runs: `lastButton` `lastText` `lastChoice` and `lastGaveUp`
* shui can be pronounced however you like, such as: "schway" or "shoe-eee", it is a contraction of shell + gui
