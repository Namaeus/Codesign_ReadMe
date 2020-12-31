



# INSTALLATION GUIDE
**1.** Unzip the `cd_dispatch.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_dispatch` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_dispatch_SQLFILE`.

**4.** Before starting the resource, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_dispatch` folder . Now you can configure the resource to suit your servers needs.
 
 **5.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **6.** Add the resource to your server start config: `ensure cd_dispatch`. The name of the folder must not be changed or the resource will not function correctly.

## Optional Modifications

**Are you using a multi-character resource?**

If so, trigger this event from the multicharacter resource after you have fully spawned in. `TriggerEvent('cd_dispatch:GrabInfo')`

**Do you want to display which radio channels each player (who has access to use the dispatch) is in?**

If so, you will need to be using some sort of voice radio resource. This event needs to be triggered from your radio resource, specifically when a player (who has access to use the dispatch) joins/changes a radio channel - [example.](https://imgur.com/6j7wEYM)

`TriggerServerEvent('cd_dispatch:GetRadioChannel', RADIO_CHANNEL_HERE)` *You must send the radio channel as a string or a number.*

**Do you use locales instead of job checks?**

This is only needed if your police don't switch jobs to go off duty, but instead have an on/off duty locale system.
`TriggerEvent('cd_dispatch:OnDutyChecks, BOOLEAN)` *You must send as a Boolean (true or false).*

## How to install - (this is a test example)

**Step 1** - We need to get the data from the client and send it to the server.

    TriggerServerEvent('testevent', exports['cd_dispatch']:GetPlayerInfo())

*By default, the export will include the players current location, but if you wish to send a set location, you can send the coordinates as a vector3 format.*
`TriggerServerEvent('testevent', exports['cd_dispatch']:GetPlayerInfo(), vector3(0,0,0))`

> The export shown above will return this table below. If the player is not in a vehicle it will not return any vehicle data.

    return {
	    ped = ped,
	    coords = coords,
	    street_1 = streetnames.street1,
	    street_2 = streetnames.street2,
	    sex = sex,
	    vehicle = vehicle,
	    vehicle_label = vehicle_label,
	    vehicle_colour = vehicle_colour
    }

**Step 2** - Now we need to configure the data that has been received in server event, and send it back to the clients for all the players with the chosen job who will receiving this message.


	RegisterServerEvent('testevent')
	AddEventHandler('testevent', function(data, customcoords)
		if customcoords ~= nil then
			data.coords = customcoords
		end
		TriggerClientEvent('cd_dispatch:AddNotification', -1, {
			job = 'police', 
			coords = data.coords,
			title = '10-15 - Store Robbery',
			message = 'A '..data.sex..' robbing a store at '..data.street_1..', '..data.street_2, 
			flash = 0, 
			blip = {
				sprite = 431, 
				scale = 1.2, 
				colour = 3,
				flashes = false, 
				text = '911 - Store Robbery',
				time = (5*60*1000),
				sound = 1,
			}
		})
	end)

> ### Notification Guide ^
> - **job** = Everyone who has this job will receive this notification.
> - **message** = You can remove the sex/streets etc if you don't want to display them.
> - **flash** = Set to 1 to make the UI flash, used for panic button calls etc.
> - **sprite** = The icon for the blips. [More can be found here.](https://docs.fivem.net/docs/game-references/blips/)
> - **scale** = Size of the blip.
> - **colour** = Colour of the blip. [More can be found here at the bottom.](https://docs.fivem.net/docs/game-references/blips/)
> - **flashes** - If set to true the blip will flash, used for more important calls.
> - **time** - The amount of time until the blip fades (default is 5 mins.)
> - **sound** - The sound when receiving a notification (1 = 1 sound, 2 = 2 sounds, 3 = 3 sounds, 4 = panic button alert sound). *But these can be configured in the client/customise_me/line 38.*

## Key bindings setup
We have started using the FiveM native called `RegisterKeyMapping` [documentation here](http://runtime.fivem.net/doc/natives/?_0xD7664FD1). This removes the need for while loops checking every frame for keypresses, therefor allowing the resource to be more optimised. This FiveM native works by triggering the chat command it has been registered with when the keybind is pressed. This new method also allows each client to change their own key binds in game [Example Here](https://imgur.com/GRWKelR) `Open Gta5 settings > Key Bindings > FiveM`.

### How to change keys with KeyMapping

- **If you wish to change the default key bind, you must change it in the `configs/config.lua` BEFORE starting the resource on your server.**

- Once you have started the resource on your server for the first time with the RegisterKeyMapping enabled, the key **cannot** be changed in the config. Now the only way the key can be changed while still using the KeyMapping is for players to change the key for themselves in the in game Gta5 key binding settings. [Example Here](https://imgur.com/GRWKelR) `Open Gta5 settings > Key Bindings > FiveM`.

### How to disable KeyMapping

- This method can be disabled by removing the chat command/changing the name of the chat command and then restarting your server/restarting your chat resource.
    
- The RegisterKeyMapping key bindings them self currently can not be removed from the Gta5 key bindings settings. Although once the chat command it was registered with has been removed, it will not work anymore when you press the key.

- Once you have disabled the RegisterKeyMapping method you can use other methods such as chat commands *(the name of the new chat command must be named differently from the original)* or while loops checking for key presses `IsControlJustReleased` or custom methods to trigger these events highlighted below.

> `TriggerEvent('cd_dispatch:KEY_smallui')`
> `TriggerEvent('cd_dispatch:KEY_largeui')`
> `TriggerEvent('cd_dispatch:KEY_responding')`

### Notes
- Players may not be able to have multiple keys bound to the same key.

- According to a post on the FiveM forums you can remove unused keybinds [here](https://forum.cfx.re/t/registerkeymapping-question/1108639/10?u=ramp_rp). But we have not tested this, its on you if you wish to try it.

### Default Key bindings

> U - Open the Small UI.

> L - Open the large UI. This can only be opened while the small UI is open.

> G - Respond to a notification.

> Left/Right Arrows - Scroll through the notifications on the small UI.

## Is the resource not working as expected?
- Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_dispatch`.
- If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
- If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
