# INSTALLATION GUIDE
**1.** Unzip the `cd_spawnselect.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_spawnselect` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_spawnselect_SQLFILE`.

**4.** Before starting the resource, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_spawnselect` folder . Now you can configure the resource to suit your servers needs.
 
**5.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.

**6.** Add the script to your server start config: `start cd_spawnselect` (it must be placed anywhere below your framework resource eg., es_extended, not above). The name of the folder must not be changed or the script will not function correctly.

## How to install
This script supports ESX and any other framework, but the method of triggering these events are slightly different. If your database does not have the `position` column in your `users` table, then you will have to use the custom framework method. All you will need to do is send the players last saved position in the database as the first argument.

 - The coordinates must be sent in a table (the table must include x, y, z).
 - You can also trigger this event from the server to client, just like you would with any other event.
 
|  ESX framework| Custom framework |
|--|--|
|`TriggerEvent('cd_spawnselect:OpenUI')`|`TriggerEvent('cd_spawnselect:OpenUI', coords)`|

## Where do i place this trigger event?
If you are using a multi-character script, we advise you to place the event inside that script, in a place where it will be triggered after you have chosen your character. But if you do not use a multi-character script, we advise you to place it inside your identity script, specifically at a place where your identity script checks if the player is a new or existing player. Only enable it for existing players as the spawn select ui will conflict with the identity ui for new players.

## Is the script not working as expected?
- Firstly always make sure the script has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_spawnselect`.
- Try enabling the test command in the config and see if it works that way.
- If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
