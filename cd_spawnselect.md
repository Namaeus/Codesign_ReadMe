## SET UP INSTRUCTIONS
**1.** Unzip the `cd_spawnselect.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_spawnselect` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_spawnselect_SQLFILE`.

 **4.** Before starting the script, please read the `config.lua` (located inside the main cd_terminalhacker folder), the `config.js` (located inside the html/js folder) and the `customise_me`  (located inside the server and client folders) and configure the script to suit your servers needs.
 
 **5.** **WARNING** do not delete any files, do not change file names and do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **6.** Add the script to your server start config: `start cd_spawnselect`. The name of the folder must not be changed or the script will not function correctly.

### How to install
*This script supports ESX and any other framework, but the method of triggering these events are slightly different. If your database does not have the `position` column in your `users` table, then you will have to use the custom framework method. All you will need to do is send the players last saved position in the database as the first argument.*

 - The coordinates must be sent in a table (the table must include x, y, z).
 - You can also trigger this event from the server to client, just like you would with any other event.
 
|  ESX framework| Custom framework |
|--|--|
| TriggerEvent('cd_spawnselect:OpenUI') | TriggerEvent('cd_spawnselect:OpenUI', coords) |


### Where do i put this trigger event?
If you are using a multi-character script, we advise you to place the event inside that script, in a place where it will be triggered after you have chosen your character. But if you do not use a multi-character script, we advise you to place it inside your identity script, specifically at a place where your identity script checks if the player is a new or existing player.
