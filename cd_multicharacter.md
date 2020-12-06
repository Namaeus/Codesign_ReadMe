# INSTALLATION GUIDE
**1.** Unzip the `cd_multicharacter.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization`. This is located inside the main `cd_multicharacter` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_multicharacter_SQLFILE`.

**4.** If you are using es_extended v1.2 or v1.final, then open up your database, go to your users table, and change the length/set of the `identifier` varchar from 40 to 50.

 **5.** Before starting the script, please read the `config.lua` (located inside the main cd_multicharacter folder), the `config.js` (located inside the html/js folder) and the `customise_me` (located inside the server and client folders) and configure the script to suit your servers needs.
 
 **6.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **7.** Add the script to your server start config: `start cd_multicharacter`. The name of the folder must not be changed or the script will not function correctly.

## Step 1
First we will need to do a small edit to stop es_extended regestering our character instantly instantly.

**ESX version 1.1 - essentialmode/client/main.lua/line 5 - hashout/remove this code.**

    -- 	Citizen.CreateThread(function()
    -- 		while true do
    -- 			Citizen.Wait(0)
    -- 			if NetworkIsSessionStarted() then
    -- 				TriggerServerEvent('es:firstJoinProper')
    -- 				TriggerEvent('es:allowedToSpawn')
    -- 				return
    -- 			end
    -- 		end
    -- end)
    
    -- TriggerServerEvent('es:firstJoinProper')

**ESX version 1.2** - es_extended/client/main.lua/line 36 - hashout/remove this code.

    -- 	if isFirstSpawn then
    -- 		TriggerServerEvent('esx:playerJoined')
    -- 	end

**ESX version 1.final - es_extended/client/main.lua/line 3 - hashout/remove this code.**

    --	Citizen.CreateThread(function()
    --		while true do
    -- 			Citizen.Wait(0)
    -- 			if NetworkIsPlayerActive(PlayerId()) then
    -- 				TriggerServerEvent('esx:onPlayerJoined')
    -- 				break
    -- 			end
    -- 		end
    -- end)

## Step 2
Ok now we need to copy and paste some code into your skin resource. We have multiple options for you, depending on which skin resource you use.

**esx_skin**
*There are 2 different versions for esx_skin, `loadskin2` and `loadskin3`. Both edited for different versions of esx_skin and skinchanger. You should try `use loadskin2 first`, but if you have errors in the skinchanger resource related to `blemishes`,  use the loadskin3 block of code, and replace the event name in client/customise_me/line 56 from “skinchanger:loadSkin2” to “skinchanger:loadSkin3”.*

> If your Config.SkinScript is set to `’esx’` then copy and paste this block of code below into the client side of your `skinchanger` resource.

**Other**
*This “other” section is where we add compatibility for other skin scripts at the request of our customers.*
> If your Config.SkinScript is set to `’other1’` or `’other2’` then copy and paste this block of code into your skin resource.



## Default Key-binds
> Left/Right Arrows - Cycle through the screens.
> Enter/Left Mouse - Select character.

## Is the script not working as expected?
 - Firstly always make sure the script has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
 - Make sure the name of the folder is `cd_multicharacter`.
 - If the script has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other scripts may be disabling that specific key.
-   If all else fails, contact the Codesign Team in your private discord channel in the Codesign discord.

