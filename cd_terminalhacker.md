## SET UP INSTRUCTIONS
**1.** Unzip the `cd_terminalhacker.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_terminalhacker` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_terminalhacker_SQLFILE`.

 **4.** Before starting the script, please read the `config.lua` (this located inside the main cd_terminalhacker folder) and the `config.js` (this located inside html/js folder) and configure the script to suit your servers needs.
 
 **5.** **WARNING** do not delete any files, do not change file names and do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **6.** Add the script to your server start config: `cd_terminalhacker`. The name of the folder must not be changed or the script will not function correctly.

### Example
*The code below can only be placed inside a client.lua file, not a server.lua file.*
```
local example = exports['cd_terminalhacker']:StartTerminalHacking()
if example.success then
	print('im a winner')
	print(example.time) --Returns the amount of time taken to complete (in seconds).
	print(example.score) --Returns the score. (You gain a higher score from downloading more optional files).
else
	print('i suck so bad')
end
```

**About the game**

The point of the hacking game is to find the proper .exe file somewhere in a remote pc's directory.
Some .exe files are corrupted and will set you back. (You need to figure which are which)
Along your search path you are supposed to download additional files from the file system and gain score.
Score and time taken determine the leaderboard placement, and the server owner can set their own actions based on time and score.