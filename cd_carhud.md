



# INSTALLATION GUIDE
**1.** Unzip the `cd_carhud.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_carhud` folder.

 **3.** Before starting the resource, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_carhud` folder. Now you can configure the resource to suit your servers needs.
 
 **4.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **5.** Add the resource name to your server start config: `ensure cd_carhud`. The name of the folder must not be changed or the resource will not function correctly.

## Required Edits

**Add your vehicle fuel checks into this function**  - configs/client_customise_me.lua/line 52.

There are already 2 examples of how you would do this, the default is using the FiveM native to get a vehices fuel, and the hashed out one is using the one from legacy fuel.

    function GetFuel(vehicle)
	    return GetVehicleFuelLevel(vehicle) --Default fivem native example.
	    --return DecorGetFloat(vehicle, '_FUEL_LEVEL') --Legacy Fuel example.
	    --return return math.ceil((100 / GetVehicleHandlingFloat(vehicle, "CHandlingData", "fPetrolTankVolume")) * math.ceil(GetVehicleFuelLevel(vehicle))) --FRFuel example.
	    --return --(You can return your own vehicle fuel checks here)
    end


## FAQ

### Can i change the default UI settings?
> Yes you can, this can be done from `configs/ui_config.js.` If you already have saved settings in your cache, you will need to open the settings UI and click the default settings option for the new defaults to be set.

### Optimisation?
> The balance between performance and optimisation is something that you need to decide. You simply can’t have the resource peforming at its peak performance by updating the UI every frame without that having an effect on the optimisation. Although, the resource has been created in such a way where you can allow your players to decide whether they want peak performance from the UI at the cost of loosing 1-2 fps or if they want to keep the fps at the cost of the UI being less responsive when updating the UI values. But there is a middle ground which we do recommend where you can get the best of both worlds with a little compromise.

 - **Seat belt (0.03*ms*)** - By default, the thread for the seat belt in `client/functions.lua` consumes the majority of the ms. It can be reduced by 0.02*ms* by disabling `Config.DisableExitingVehicle`. The ms can be reduced by 0.03*ms* in total by disabling the seatbelt completely if you don't wish to use it or you have a more optimised one - `Config.Seatbelt.ENABLE`.

 - **Carhud UI (0.02*ms*)** - The refresh rate of the UI can also play a huge factor in optimisation. The default refresh rate value is 500*ms*. But you can set this default value for all players at the bottom of the `configs/ui_config.js`. The UI by itself with all elements and settings enabled will use 0.02*ms* during use. Each individual player can also modify this value, lowering it will result in the UI being more responsive at the cost of increased resource usage.

### Will the settings save after i relog?
Yes the settings will save after you relog, after a server restart, after you clear your client cache and will even apply if you play on another server which uses cd_carhud . It does not use the database to save this data.

## Key binds
We have started using the fivem native called `RegisterKeyMapping` [documentation here](http://runtime.fivem.net/doc/natives/?_0xD7664FD1). This removes the need for while loops checking every frame for keypresses, therefor allowing the resource to be more optimised. This new method allows each client to change their own key binds in game [example here](https://imgur.com/GRWKelR).

- One thing to note is that players may not be able to have multiple keys bound to the same key.
- In order to change the key in the config, or disable it, you may have to clear your client cache for it to update in game.
- Alternatively you can disable the RegisterKeyMapping method in the config and use other methods such as chat commands or while loops with keypresses to trigger these events highlighted  below.
> `TriggerEvent('cd_carhud:OpenSettingsUI')`
> `TriggerEvent('cd_carhud:ToggleSeatbelt')`

### Default Key-binds
> E - Open the settings UI.

> B - Toggle the seatbelt.

## Is the resource not working as expected?
- Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_carhud`.
- If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
- If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
