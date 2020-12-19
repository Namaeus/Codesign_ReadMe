
# INSTALLATION GUIDE
**1.** Unzip the `cd_playerhud.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_playerhud` folder.

 **3.** Before starting the resource, please read the `config.lua` (located inside the main cd_playerhud folder), the `config.js` (located inside the html/js folder) and the `customise_me` (located inside the server and client folders) and configure the resource to suit your servers needs.
 
 **4.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **5.** Add the resource to your server start config: `ensure cd_playerhud`. The name of the folder must not be changed or the resource will not function correctly.

## How to install

This resource completely replaces esx_status. It can also replace esx_basic needs if you choose (check the server sided customise_me if you wish to completely replace esx_basic needs). But if you choose to remain using esx_basic needs, you will have to replace the trigger events in the server side that adds hunger/thirst when using items.

> TriggerClientEvent('cd_playerhud:status:add', source,  Status_Type,  Amount)

> TriggerClientEvent('cd_playerhud:status:remove', source,  Status_Type,  Amount)

> TriggerClientEvent('cd_playerhud:status:set', source,  Status_Type,  Amount)

- *The `Status_Type` must be sent as a string and the `Amount` must be sent as a number.*
- *Example: 0 is empty food and 100 is full food.*
- *You can also trigger these events from the client to client, just like you would with any other events.*

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

**Below is an seperate additional event that may come in handy for you.**

*You can use the `GetMoney()` function in the client customise_me.lua to get and set the money values on the watch UI, but if you wish to set them values via a trigger event, then this is the event you can use.*
> `TriggerClientEvent('cd_playerhud:SetCustomMoneyValues', source, Action_Type, Money_Type, Amount)`

|Action_Type| Money_Type |Amount|
|--|--|--|
|‘add’|'bank'|0-100|
|‘remove’|'cash'|0-100|
|’set||0-100|

## Key binds
We have started using the fivem native called `RegisterKeyMapping` [documentation here](http://runtime.fivem.net/doc/natives/?_0xD7664FD1). This removes the need for while loops checking every frame for keypresses, therefor allowing the resource to be more optimised. This new method allows each client to change their own key binds in game [example here](https://imgur.com/GRWKelR).

- One thing to note is that players may not be able to have multiple keys bound to the same key.
- In order to change the key in the config, or disable it, you may have to clear your client cache for it to update in game.
- Alternatively you can disable the RegisterKeyMapping method in the config and use other methods such as chat commands or while loops with keypresses to trigger these events highlighted  below.
> `TriggerEvent('cd_playerhud:OpenWatchUI')`

## Default Key-binds
> Tab - Toggle the watch ui.

> K - Toggle move mode.

> Left/Right Arrows - Cycle through the screens.

## Is the resource not working as expected?
 - Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
 - Make sure the name of the folder is `cd_playerhud`.
 - If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
-   If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).

