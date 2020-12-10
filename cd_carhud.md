# INSTALLATION GUIDE
**1.** Unzip the `cd_carhud.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_carhud` folder.

 **3.** Before starting the resource, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_carhud` folder . Now you can configure the resource to suit your servers needs.
 
 **4.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **5** Add the script to your server start config: `cd_carhud`. The name of the folder must not be changed or the script will not function correctly.

## Required Edits

**Add your vehicle fuel checks into this function -** configs/client_customise_me.lua/line 52

*There are already 2 examples of how you would do this, the default is using the FiveM native to get a vehices fuel, and the hashed out one is using the one from legacy fuel.*

    function GetFuel(vehicle)
	    return GetVehicleFuelLevel(vehicle) --Default example.
	    --return DecorGetFloat(vehicle, '_FUEL_LEVEL') --Legacy Fuel example. You can return your own vehicle fuel checks here.
    end


## FAQ

**Can i change the default UI settings?**
> Yes you can, this can be done from `configs/ui_config.js.`

**Optimisation?**
> The balance between performance and optimisation is something that you need to decide. You simply can’t have the resource peforming at its peak performance by updating the UI every frame without that having an effect on the optimisation. Although the resource has been created in such a way  where you can allow your players to decide wether they want peak performance from the UI at the cost of loosing 1-2 fps or if they want to keep the fps at the cost of a small delay when updating the UI. But there is a middle ground which we do recommend where you can get the best of both worlds with a little compromise.

 - **Seat belt** - By default, the thread for the seat belt in `configs/client_customise_me.lua` consumes the majority of the ms. It can be lowered by 0.03 by disabling `Config.DisableExitingVehicle`. The `Config.SeatbeltLoopTimer` can also be increased from 50 to 200 (or even more to reduce more ms) to reduce 0.02. The ms can be reduced by 0.06 in total by disabling the seatbelt completely - `Config.Seatbelt.ENABLE`.

 - **Default UI refresh rate** - The refresh rate of the ui can also play a huge factor in this. You can set the default refresh rate value for all players at the bottom of the `configs/ui_config.js`. It is set by default to 100*ms* but you can increase it to 250-500 to further reduce the ms from 0.05 to 0.02 while still not noticing any delay in the UI. You could also change the refresh rate to 1000ms and total ms usage will only be 0.01*ms*, but this time you will notice the delay when the UI values ae being updated.





## Is the resource not working as expected?
- Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_carhud`.
- If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
- If all else fails, contact the Codesign Team in your private discord channel in the Codesign discord.

