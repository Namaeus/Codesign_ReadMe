# INSTALLATION GUIDE
**1.** Unzip the `cd_dispatch.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_dispatch` folder.
**1.** Unzip the `cd_dispatch.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_dispatch` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_dispatch_SQLFILE`.

 **4.** Before starting the script, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_dispatch` folder . Now you can configure the script to suit your servers needs.
 
 **5.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **6.** Add the script to your server start config: `cd_dispatch`. The name of the folder must not be changed or the script will not function correctly.

### How to install

**Step 1** - We need to get the data from the client and send it to the server.

    TriggerServerEvent('testevent', exports['cd_dispatch']:GetPlayerInfo())

*By default, the export will include the players current location, but if you wish to send a set location, you can send the coords as a vector3 format.*
`TriggerServerEvent('testevent', exports['cd_dispatch']:GetPlayerInfo(), vector3(0,0,0))`


> The export shown above will return this table below. (If the player is not
> in a vehicle it will not return any vehicle data.)

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
	AddEventHandler(‘testevent’, function(data, customcoords)
		if customcoords ~= nil then
			data.coords = customcoords
		end
		TriggerClientEvent('cd_dispatch:AddNotification', -1, {
			job = 'police', --everyone who has this job will recieve this notification.
			coords = data.coords,
			title = '10-15 - Store Robbery',
			message = 'A '..data.sex..' robbing a store at '..data.street_1..', '..data.street_2, --you can remove the sex/streets etc if you dont want to display them.
			flash = 0, --set to 1 to make the ui flash, used for panic button calls etc.
			blip = { --blip info.
				sprite = 431, --blips icon - more can be found here https://docs.fivem.net/docs/game-references/blips/.
				scale = 1.2, --size of the blip.
				colour = 3, --colour of the blip - can be found at then bottom of this website page https://docs.fivem.net/docs/game-references/blips/.
				flashes = false, --if set to true the blip will flash, used for more important calls.
				text = '911 - Store Robbery',
				time = (5*60*1000),--the amount of time until the blip fades (default is 5 mins.)
				sound = 1, --the sound when recieving a notification (1 = 1 sound, 2 = 2 sounds, 3 = 3 sounds, 4 = panic button alert sound).
			}
		})
	end)








## Is the script not working as expected?
- Firstly always make sure the script has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_dispatch`.
- If the script has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other scripts may be disabling that specific key.
- If all else fails, contact the Codesign Team in your private discord channel in the Codesign discord.

