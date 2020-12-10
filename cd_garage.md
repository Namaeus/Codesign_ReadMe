# INSTALLATION GUIDE
**1.** Unzip the `cd_garage.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_garage` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_garage_SQLFILE`.

 **4.** Before starting the resource, please read the `config.lua` (located inside the main cd_garage folder), the `config.js` (located inside the html/js folder) and the `customise_me` (located inside the server and client folders) and configure the resource to suit your servers needs.
 
 **5.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **6.** Add the resource to your server start config: `ensure cd_garage`. The name of the folder must not be changed or the resource will not function correctly.

## Install the dependencies
There are 4 resources that this garage depends upon. These are provided in your purchase and are located inside the `zips` folder. Unzip these files, add them to your resources folder, then add them to the server start config also.

    start cd_garage
    start cd_garageshell
    start cd_drawtextui
    start cd_easytime

## Required modifications
If you are using an older version of es_extended, the modifications below are required. If the lines of code below are not already inside said functions, then copy and paste them into them.

**es_extended/client/functions** - search for a function called `ESX.Game.GetVehicleProperties`.

    bodyHealth = ESX.Math.Round(GetVehicleBodyHealth(vehicle), 1),
    engineHealth = ESX.Math.Round(GetVehicleEngineHealth(vehicle), 1),
    fuelLevel = ESX.Math.Round(GetVehicleFuelLevel(vehicle), 1),

**es_extended/client/functions**   - search for a function called `ESX.Game.SetVehicleProperties`.

    if props.bodyHealth then SetVehicleBodyHealth(vehicle, props.bodyHealth + 0.0) end
    if props.engineHealth then SetVehicleEngineHealth(vehicle, props.engineHealth + 0.0) end
    if props.fuelLevel then SetVehicleFuelLevel(vehicle, props.fuelLevel + 0.0) end


## Optional modifications

**Are you using boat or air garages?**

> If so, when a player purchases a boat/air vehicle, you will need to update the `garage_type` for this vehicle in the database. If you do not use boat/air vehicles, you can ignore this as the default garage_type value in the database is car.

- There garage_type can only be set to 3 values: `’car’` `’boat’` `’air’` and these values must be sent as a string.
 - You can enter this value using your own method or you can use the export below.
 - If you choose to use the export below, it can only be used client side and you must send the vehicle id.


	    exports['cd_garage']:GetGarageType(vehicle)

**Do you want to use the property garages?**

> If you use a paid property resource, then it’s really the developer of said resource who will be best suited to help you with the property garages, as the Codesign Team dosen't have access to their resources and we can’t have access to them without the developers permission, considering we haven't purchased them. But, we have made it extremely simply for you yourself to implement this into your property resource.

|Spawning a vehicle| Storing a vehicle |
|--|--|
| `TriggerEvent('cd_garage:PropertyGarage', Action)` | `TriggerEvent('cd_garage:StoreVehicle_Main', 1, false)` |
|*You must send either `‘quick’` or `’inside’` as the first argument. (Replacing `Action` above.)*|*The first and second argument must alays stay the same. (As seen above).*|

## Exports
These exports are completely optional, and there for you if you wish to use them.

>Server Side Exports

`exports['cd_garage']:GetGarageLimit(source)` - Returns the players garage limit amount from the users table in the database. You must send the players server id.

`exports['cd_garage']:GetGarageCount(source, garage_type)` - Returns the amount of vehicles the player owns. You must send the players server id, but the garage_type is optional. *(If the garage_type is nil, the players car count will be returned.  There garage_type can only be set to 3 values:  ( ‘car’ / ‘boat’ / ‘air’ ) and these values must be sent as a string).*

> Client Side Exports

`exports['cd_garage']:GetGarageType(vehicle)` - Returns the type of vehicle ( ‘car’ / ‘boat’ / ‘air’ ). You must send the vehicle id.

`exports['cd_garage']:GetAdvStats(plate)` - Returns the mileage information table (plate /mileage /maxhealth). You must send the plate by using tostring(GetVehicleNumberPlateText(vehicle)).

## Chat commands

All of these chat commands can be disabled/enabled in the config. You can use the events below to trigger them from other resources instead of using chat commands.

`/impound`  - Use the built in vehicle impound system to impound a vehicle.

`/transfervehicle (targetID)`  - Use the built in vehicle transfer system to transfer a vehicle to another player.

`/checkmiles`  - Use the built in mileage system to check the mileage of the vehicle you are in.

`/garagespace (add) (serverid)`  - If using garage space limt, players with defined jobs can sell garage slots to other players.

`/jobcar`  - Use the built in job vehicle garages to spawn vehicles for certain jobs.

## Events
Again, these events are completely optional, and there for you if you wish to use them.

`TriggerEvent('cd_garage:checkmileage')` - To check the vehicles mileage instead of using the chat command.

`TriggerEvent('cd_garage:ImpoundVehicle')` - To impound vehicles instead of using the impount chat command.

`TriggerEvent('cd_garage:TransferVehicle', targetID)` - To transfer a vehicle instead of using the chat command. You must send the players server id.

`TriggerServerEvent('cd_garage:SaveAllMiles')` - This event can be triggered 1 minute before a server restart to force save the mileage of every players vehicles.

## Is the resource not working as expected?
- Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
- Make sure the name of the folder is `cd_garage`.
- If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
