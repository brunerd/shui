# shui
shui is a shell script wrapper for presenting user dialogs in Applescript without needing to know Applescript

Download shui from the sources folder and if need be make executable with `chmod ugo+x ./shui` while in the same folder.

To get help: `./shui help`
To see a demo of all the actions: `./shui demo`

* shui is meant to be embedded in your scripts
* shui will allow you to present first class interfaces with your shell scripts with no external dependencies
* shui will set 4 global shell variables after it runs: `lastButton` `lastText` `lastChoice` and `lastGaveUp`

### Future Versions
Currently by default System Events is used, this will cause a dilaog box to allow Applescript to control System Events and is necessary for shui to work, in a future version this behavior will be changed
