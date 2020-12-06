## INSTALLATION GUIDE
**1.** Unzip the `cd_playerhud.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_playerhud` folder.

 **3.** Before starting the script, please read the `config.lua` (located inside the main cd_playerhud folder), the `config.js` (located inside the html/js folder) and the `customise_me` (located inside the server and client folders) and configure the script to suit your servers needs.
 
 **4.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **5.** Add the script to your server start config: `start cd_playerhud`. The name of the folder must not be changed or the script will not function correctly.

### How to install

*This script completely replaces esx_status. It can also replace esx_basic needs if you choose (check the server sided customise_me if you wish to completely replace esx_basic needs also). But if you choose to remain using esx_basic needs, you will have to replace the trigger events in the server side that adds hunger/thirst when using items.*

### Hunger and Thirst

> TriggerClientEvent('cd_playerhud:status:add', source, Status_Type, Amount)
> TriggerClientEvent('cd_playerhud:status:remove', source, Status_Type, Amount)
> TriggerClientEvent('cd_playerhud:status:set', source, Status_Type, Amount)

- *The `type` must be sent as a string and the `amount` must be sent as a number.*
- *Example: 0 is empty food and 100 is full food.*
- *You can also trigger these events from the server to client, just like you would with any other events.*

|Status_Type| Amount|
|--|--|
| ‘hunger’ |0-100|
|’thirst’|0-100|
|’stress’|0-100|
**Below is an example, replace the esx_status event with the cd_playerhud event.**
```
ESX.RegisterUsableItem('bread', function(source)
local xPlayer = ESX.GetPlayerFromId(source)
xPlayer.removeInventoryItem('bread', 1)

—-TriggerClientEvent('esx_status:add', source, 'hunger', 200000)
TriggerClientEvent('cd_playerhud:status:add', source, 'hunger', 20)

TriggerClientEvent('esx_basicneeds:onEat', source)
xPlayer.showNotification(_U('used_bread'))
end)
```
### Setting Money Values
*You can use the `GetMoney()` function in the client customise_me.lua to get and set the money values on the watch UI, but if you wish to set them values via a triger event, this is the event you can use.*
> TriggerClientEvent('cd_playerhud:SetCustomMoneyValues', source, Action_Type, Money_Type, Amount)

|Action_Type| Money_Type |
|--|--|
|‘add’|bank|
|‘remove’|cash|
|’set||


### Default Key-binds
> Tab - Toggle the watch ui.
> K - Toggle move mode.
> Left/Right Arrows - Cycle through the screens.

### Is the script not working as expected?
 - Firstly always make sure the script has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
 - Make sure the name of the folder is `cd_playerhud`.
 - If the script has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other scripts may be disabling that specific key.
-   If all else fails, contact the Codesign Team in your private discord channel in the Codesign discord.

