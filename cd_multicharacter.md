
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

There are 2 different versions for esx_skin, `loadskin2` and `loadskin3`. Both edited for different versions of esx_skin and skinchanger. You should try use `skinchanger:loadSkin2` first.

> If your Config.SkinScript is set to `’esx’` then copy and paste this block of code below into the client side of your `skinchanger` resource.

	RegisterNetEvent('skinchanger:loadSkin2')
	AddEventHandler('skinchanger:loadSkin2', function(multipedID, skin)
		local MultiPed = {}
		for i=1, #Components, 1 do
			MultiPed[Components[i].name] = Components[i].value
		end
		for k,v in pairs(skin) do
			MultiPed[k] = v
		end

		SetPedHeadBlendData			(multipedID, MultiPed['face'], MultiPed['face'], MultiPed['face'], MultiPed['skin'], MultiPed['skin'], MultiPed['skin'], 1.0, 1.0, 1.0, true)

		SetPedHairColor				(multipedID,			MultiPed['hair_color_1'],		MultiPed['hair_color_2'])					-- Hair Color
		SetPedHeadOverlay			(multipedID, 3,		MultiPed['age_1'],				(MultiPed['age_2'] / 10) + 0.0)			-- Age + opacity
		SetPedHeadOverlay			(multipedID, 0,		MultiPed['blemishes_1'],		(MultiPed['blemishes_2'] / 10) + 0.0)		-- Blemishes + opacity
		SetPedHeadOverlay			(multipedID, 1,		MultiPed['beard_1'],			(MultiPed['beard_2'] / 10) + 0.0)			-- Beard + opacity
		SetPedEyeColor				(multipedID,			MultiPed['eye_color'], 0, 1)												-- Eyes color
		SetPedHeadOverlay			(multipedID, 2,		MultiPed['eyebrows_1'],		(MultiPed['eyebrows_2'] / 10) + 0.0)		-- Eyebrows + opacity
		SetPedHeadOverlay			(multipedID, 4,		MultiPed['makeup_1'],			(MultiPed['makeup_2'] / 10) + 0.0)			-- Makeup + opacity
		SetPedHeadOverlay			(multipedID, 8,		MultiPed['lipstick_1'],		(MultiPed['lipstick_2'] / 10) + 0.0)		-- Lipstick + opacity
		SetPedComponentVariation	(multipedID, 2,		MultiPed['hair_1'],			MultiPed['hair_2'], 2)						-- Hair
		SetPedHeadOverlayColor		(multipedID, 1, 1,	MultiPed['beard_3'],			MultiPed['beard_4'])						-- Beard Color
		SetPedHeadOverlayColor		(multipedID, 2, 1,	MultiPed['eyebrows_3'],		MultiPed['eyebrows_4'])					-- Eyebrows Color
		SetPedHeadOverlayColor		(multipedID, 4, 1,	MultiPed['makeup_3'],			MultiPed['makeup_4'])						-- Makeup Color
		SetPedHeadOverlayColor		(multipedID, 8, 1,	MultiPed['lipstick_3'],		MultiPed['lipstick_4'])					-- Lipstick Color
		SetPedHeadOverlay			(multipedID, 5,		MultiPed['blush_1'],			(MultiPed['blush_2'] / 10) + 0.0)			-- Blush + opacity
		SetPedHeadOverlayColor		(multipedID, 5, 2,	MultiPed['blush_3'])														-- Blush Color
		SetPedHeadOverlay			(multipedID, 6,		MultiPed['complexion_1'],		(MultiPed['complexion_2'] / 10) + 0.0)		-- Complexion + opacity
		SetPedHeadOverlay			(multipedID, 7,		MultiPed['sun_1'],				(MultiPed['sun_2'] / 10) + 0.0)			-- Sun Damage + opacity
		SetPedHeadOverlay			(multipedID, 9,		MultiPed['moles_1'],			(MultiPed['moles_2'] / 10) + 0.0)			-- Moles/Freckles + opacity
		SetPedHeadOverlay			(multipedID, 10,		MultiPed['chest_1'],			(MultiPed['chest_2'] / 10) + 0.0)			-- Chest Hair + opacity
		SetPedHeadOverlayColor		(multipedID, 10, 1,	MultiPed['chest_3'])														-- Torso Color
		SetPedHeadOverlay			(multipedID, 11,		MultiPed['bodyb_1'],			(MultiPed['bodyb_2'] / 10) + 0.0)			-- Body Blemishes + opacity

		if MultiPed['ears_1'] == -1 then
			ClearPedProp(multipedID, 2)
		else
			SetPedPropIndex			(multipedID, 2,		MultiPed['ears_1'],			MultiPed['ears_2'], 2)						-- Ears Accessories
		end

		SetPedComponentVariation	(multipedID, 8,		MultiPed['tshirt_1'],			MultiPed['tshirt_2'], 2)					-- Tshirt
		SetPedComponentVariation	(multipedID, 11,		MultiPed['torso_1'],			MultiPed['torso_2'], 2)					-- torso parts
		SetPedComponentVariation	(multipedID, 3,		MultiPed['arms'],				MultiPed['arms_2'], 2)						-- Amrs
		SetPedComponentVariation	(multipedID, 10,		MultiPed['decals_1'],			MultiPed['decals_2'], 2)					-- decals
		SetPedComponentVariation	(multipedID, 4,		MultiPed['pants_1'],			MultiPed['pants_2'], 2)					-- pants
		SetPedComponentVariation	(multipedID, 6,		MultiPed['shoes_1'],			MultiPed['shoes_2'], 2)					-- shoes
		SetPedComponentVariation	(multipedID, 1,		MultiPed['mask_1'],			MultiPed['mask_2'], 2)						-- mask
		SetPedComponentVariation	(multipedID, 9,		MultiPed['bproof_1'],			MultiPed['bproof_2'], 2)					-- bulletproof
		SetPedComponentVariation	(multipedID, 7,		MultiPed['chain_1'],			MultiPed['chain_2'], 2)					-- chain
		SetPedComponentVariation	(multipedID, 5,		MultiPed['bags_1'],			MultiPed['bags_2'], 2)						-- Bag

		if MultiPed['helmet_1'] == -1 then
			ClearPedProp(multipedID, 0)
		else
			SetPedPropIndex			(multipedID, 0,		MultiPed['helmet_1'],			MultiPed['helmet_2'], 2)					-- Helmet
		end

		if MultiPed['glasses_1'] == -1 then
			ClearPedProp(multipedID, 1)
		else
			SetPedPropIndex			(multipedID, 1,		MultiPed['glasses_1'],			MultiPed['glasses_2'], 2)					-- Glasses
		end

		if MultiPed['watches_1'] == -1 then
			ClearPedProp(multipedID, 6)
		else
			SetPedPropIndex			(multipedID, 6,		MultiPed['watches_1'],			MultiPed['watches_2'], 2)					-- Watches
		end

		if MultiPed['bracelets_1'] == -1 then
			ClearPedProp(multipedID,	7)
		else
			SetPedPropIndex			(multipedID, 7,		MultiPed['bracelets_1'],		MultiPed['bracelets_2'], 2)				-- Bracelets
		end
		MultiPed = nil
	end)

> _If you have errors in the skinchanger resource related to  `blemishes`, use the `"skinchanger:loadSkin3"` block of code below, and replace the event name in client/customise_me/line 56 from “skinchanger:loadSkin2” to “skinchanger:loadSkin3”._

	RegisterNetEvent('skinchanger:loadSkin3')
	AddEventHandler('skinchanger:loadSkin3', function(multipedID, skin)
		local MultiPed = {}
		for i=1, #Components, 1 do
			MultiPed[Components[i].name] = Components[i].value
		end
		for k,v in pairs(skin) do
			MultiPed[k] = v
		end

		SetPedHeadBlendData			(multipedID, MultiPed['face'], MultiPed['face'], MultiPed['face'], MultiPed['skin'], MultiPed['skin'], MultiPed['skin'], 1.0, 1.0, 1.0, true)

		SetPedHairColor				(multipedID,			MultiPed['hair_color_1'],		MultiPed['hair_color_2'])					-- Hair Color
		SetPedHeadOverlay			(multipedID, 3,		MultiPed['age_1'],				(MultiPed['age_2'] / 10) + 0.0)			-- Age + opacity
		SetPedHeadOverlay			(multipedID, 1,		MultiPed['beard_1'],			(MultiPed['beard_2'] / 10) + 0.0)			-- Beard + opacity
		SetPedEyeColor				(multipedID,			MultiPed['eye_color'], 0, 1)												-- Eyes color
		SetPedHeadOverlay			(multipedID, 2,		MultiPed['eyebrows_1'],		(MultiPed['eyebrows_2'] / 10) + 0.0)		-- Eyebrows + opacity
		SetPedHeadOverlay			(multipedID, 4,		MultiPed['makeup_1'],			(MultiPed['makeup_2'] / 10) + 0.0)			-- Makeup + opacity
		SetPedHeadOverlay			(multipedID, 8,		MultiPed['lipstick_1'],		(MultiPed['lipstick_2'] / 10) + 0.0)		-- Lipstick + opacity
		SetPedComponentVariation	(multipedID, 2,		MultiPed['hair_1'],			MultiPed['hair_2'], 2)						-- Hair
		SetPedHeadOverlayColor		(multipedID, 1, 1,	MultiPed['beard_3'],			MultiPed['beard_4'])						-- Beard Color
		SetPedHeadOverlayColor		(multipedID, 2, 1,	MultiPed['eyebrows_3'],		MultiPed['eyebrows_4'])					-- Eyebrows Color
		SetPedHeadOverlayColor		(multipedID, 4, 1,	MultiPed['makeup_3'],			MultiPed['makeup_4'])						-- Makeup Color
		SetPedHeadOverlayColor		(multipedID, 8, 1,	MultiPed['lipstick_3'],		MultiPed['lipstick_4'])					-- Lipstick Color
		SetPedHeadOverlay			(multipedID, 5,		MultiPed['blush_1'],			(MultiPed['blush_2'] / 10) + 0.0)			-- Blush + opacity
		SetPedHeadOverlayColor		(multipedID, 5, 2,	MultiPed['blush_3'])														-- Blush Color
		SetPedHeadOverlay			(multipedID, 9,		MultiPed['moles_1'],			(MultiPed['moles_2'] / 10) + 0.0)			-- Moles/Freckles + opacity
		SetPedHeadOverlay			(multipedID, 10,		MultiPed['chest_1'],			(MultiPed['chest_2'] / 10) + 0.0)			-- Chest Hair + opacity
		SetPedHeadOverlayColor		(multipedID, 10, 1,	MultiPed['chest_3'])														-- Torso Color

		if MultiPed['ears_1'] == -1 then
			ClearPedProp(multipedID, 2)
		else
			SetPedPropIndex			(multipedID, 2,		MultiPed['ears_1'],			MultiPed['ears_2'], 2)						-- Ears Accessories
		end

		SetPedComponentVariation	(multipedID, 8,		MultiPed['tshirt_1'],			MultiPed['tshirt_2'], 2)					-- Tshirt
		SetPedComponentVariation	(multipedID, 11,		MultiPed['torso_1'],			MultiPed['torso_2'], 2)					-- torso parts
		SetPedComponentVariation	(multipedID, 3,		MultiPed['arms'],				MultiPed['arms_2'], 2)						-- Amrs
		SetPedComponentVariation	(multipedID, 10,		MultiPed['decals_1'],			MultiPed['decals_2'], 2)					-- decals
		SetPedComponentVariation	(multipedID, 4,		MultiPed['pants_1'],			MultiPed['pants_2'], 2)					-- pants
		SetPedComponentVariation	(multipedID, 6,		MultiPed['shoes_1'],			MultiPed['shoes_2'], 2)					-- shoes
		SetPedComponentVariation	(multipedID, 1,		MultiPed['mask_1'],			MultiPed['mask_2'], 2)						-- mask
		SetPedComponentVariation	(multipedID, 9,		MultiPed['bproof_1'],			MultiPed['bproof_2'], 2)					-- bulletproof
		SetPedComponentVariation	(multipedID, 7,		MultiPed['chain_1'],			MultiPed['chain_2'], 2)					-- chain
		SetPedComponentVariation	(multipedID, 5,		MultiPed['bags_1'],			MultiPed['bags_2'], 2)						-- Bag

		if MultiPed['helmet_1'] == -1 then
			ClearPedProp(multipedID, 0)
		else
			SetPedPropIndex			(multipedID, 0,		MultiPed['helmet_1'],			MultiPed['helmet_2'], 2)					-- Helmet
		end

		if MultiPed['glasses_1'] == -1 then
			ClearPedProp(multipedID, 1)
		else
			SetPedPropIndex			(multipedID, 1,		MultiPed['glasses_1'],			MultiPed['glasses_2'], 2)					-- Glasses
		end

		if MultiPed['watches_1'] == -1 then
			ClearPedProp(multipedID, 6)
		else
			SetPedPropIndex			(multipedID, 6,		MultiPed['watches_1'],			MultiPed['watches_2'], 2)					-- Watches
		end

		if MultiPed['bracelets_1'] == -1 then
			ClearPedProp(multipedID,	7)
		else
			SetPedPropIndex			(multipedID, 7,		MultiPed['bracelets_1'],		MultiPed['bracelets_2'], 2)				-- Bracelets
		end

		SetPedFaceFeature(multipedID, 0, MultiPed['nose_width'])
		SetPedFaceFeature(multipedID, 1, MultiPed['nose_peak_hight']) 
		SetPedFaceFeature(multipedID, 2, MultiPed['nose_peak_lenght'])
		SetPedFaceFeature(multipedID, 3, MultiPed['nose_bone_high']) 
		SetPedFaceFeature(multipedID, 4, MultiPed['nose_peak_lowering'])
		SetPedFaceFeature(multipedID, 5, MultiPed['nose_bone_twist'])  
		SetPedFaceFeature(multipedID, 6, MultiPed['eyebrown_high']) 
		SetPedFaceFeature(multipedID, 7, MultiPed['eyebrown_forward'])
		SetPedFaceFeature(multipedID, 8, MultiPed['cheeks_bone_high']) 
		SetPedFaceFeature(multipedID, 9, MultiPed['cheeks_bone_width'])
		SetPedFaceFeature(multipedID, 10, MultiPed['cheeks_width'])
		SetPedFaceFeature(multipedID, 11, MultiPed['eyes_openning'])  
		SetPedFaceFeature(multipedID, 12, MultiPed['lips_thickness'])
		SetPedFaceFeature(multipedID, 13, MultiPed['jaw_bone_width'])
		SetPedFaceFeature(multipedID, 14, MultiPed['jaw_bone_back_lenght']) 
		
		SetPedFaceFeature(multipedID, 15, MultiPed['chimp_bone_lowering']) 
		SetPedFaceFeature(multipedID, 16, MultiPed['chimp_bone_lenght']) 
		SetPedFaceFeature(multipedID, 17, MultiPed['chimp_bone_width']) 
		SetPedFaceFeature(multipedID, 18, MultiPed['chimp_hole']) 
		SetPedFaceFeature(multipedID, 19, MultiPed['neck_thikness'])
		MultiPed = nil
	end)

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

