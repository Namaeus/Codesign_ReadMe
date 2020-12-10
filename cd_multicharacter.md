


# INSTALLATION GUIDE
**1.** Unzip the `cd_multicharacter.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_multicharacter` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_multicharacter_SQLFILE`.

**4.** If you are using es_extended v1.2 or v1.final, then open up your database, go to your users table, and change the length/set of the `identifier` varchar from 40 to 50.

 **5.** Before starting the resource, please read the `config.lua` (located inside the main cd_multicharacter folder), the `config.js` (located inside the html/js folder) and the `customise_me` (located inside the server and client folders) and configure the resource to suit your servers needs.
 
 **6.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
 **7.** Add the resource to your server start config: `ensure cd_multicharacter`. The name of the folder must not be changed or the resource will not function correctly.

## Step 1
First we will need to do a small edit to stop es_extended regestering our character instantly instantly.

**ESX version 1.1** - essentialmode/client/main.lua/line 5 - hashout/remove this code.

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

**ESX version 1.final** - es_extended/client/main.lua/line 3 - hashout/remove this code.

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

There are 2 different versions for esx_skin, `'skinchanger:loadskin2'` and `'skinchanger:loadskin3'`. Both edited for different versions of esx_skin and skinchanger. You should try use `skinchanger:loadSkin2` first.

> If your `Config.Skinresource` is set to `’esx’` then copy and paste this block of code below into the client side of your `skinchanger` resource.

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

> _If you have errors in the skinchanger resource related to  `blemishes`, use the `'skinchanger:loadSkin3'` block of code below, and replace the event name in client/customise_me/line 56 from `'skinchanger:loadSkin2'` to `'skinchanger:loadSkin3'`._

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

This 'other' section is where we add compatibility for other skin resources at the request of
 our customers.
> If your Config.Skinresource is set to `’other1’` or `’other2’` then copy and paste this block of code into your skin resource.
> 
    RegisterNetEvent('otherclothing:MultiCharSkin')
    AddEventHandler('otherclothing:MultiCharSkin', function(ped, skin)
	         -----SKIN-------
	        if ped then
	    		if skin then
	    			if skin['skin'] ~= nil then
	    				for i = 1, #drawable_names do
	    					if skin['skin'].drawables[0] == nil then
	    						if drawable_names[i] == "undershirts" and skin['skin'].drawables[tostring(i-1)][2] == -1 then
	    							SetPedComponentVariation(ped, i-1, 15, 0, 2)
	    						else
	    							SetPedComponentVariation(ped, i-1, skin['skin'].drawables[tostring(i-1)][2], skin['skin'].drawtextures[i][2], 2)
	    						end
	    					else
	    						if drawable_names[i] == "undershirts" and skin['skin'].drawables[i-1][2] == -1 then
	    							SetPedComponentVariation(ped, i-1, 15, 0, 2)
	    						else
	    							SetPedComponentVariation(ped, i-1, skin['skin'].drawables[i-1][2], skin['skin'].drawtextures[i][2], 2)
	    						end
	    					end
	    				end
					for i = 1, #prop_names do
						local propZ = (skin['skin'].drawables[0] == nil and skin['skin'].props[tostring(i-1)][2] or skin['skin'].props[i-1][2])
						ClearPedProp(ped, i-1)
						SetPedPropIndex(ped,i-1,propZ,skin['skin'].proptextures[i][2], true)
					end

					Citizen.Wait(500)
					if skin['skin'].model == 1885233650 or skin['skin'].model == -1667301416 then
						-----FACE-------
						if skin['face'] ~= nil then
							SetPedHairColor(ped, tonumber(skin['face'].hairColor[1]), tonumber(skin['face'].hairColor[2]))
							SetPedHeadBlendData(ped,
								tonumber(skin['face'].headBlend['shapeFirst']),
								tonumber(skin['face'].headBlend['shapeSecond']),
								tonumber(skin['face'].headBlend['shapeThird']),
								tonumber(skin['face'].headBlend['skinFirst']),
								tonumber(skin['face'].headBlend['skinSecond']),
								tonumber(skin['face'].headBlend['skinThird']),
								tonumber(skin['face'].headBlend['shapeMix']),
								tonumber(skin['face'].headBlend['skinMix']),
								tonumber(skin['face'].headBlend['thirdMix']),
							false)

							for i = 1, #face_features do
								SetPedFaceFeature(player, i-1, skin['face'].headStructure[i])
							end
							if json.encode(skin['face'].headOverlay) ~= "[]" then
								for i = 1, #head_overlays do
									if skin['face'].headOverlay[i].name == "eyecolor" then
										SetPedEyeColor(player, tonumber(skin['face'].headOverlay[i].val))
									else
										SetPedHeadOverlay(player,  i-1, tonumber(skin['face'].headOverlay[i].overlayValue),  tonumber(skin['face'].headOverlay[i].overlayOpacity))
									end
								end
						
								SetPedHeadOverlayColor(ped, 0, 0, tonumber(skin['face'].headOverlay[1].firstColour), tonumber(skin['face'].headOverlay[1].secondColour))
								SetPedHeadOverlayColor(ped, 1, 1, tonumber(skin['face'].headOverlay[2].firstColour), tonumber(skin['face'].headOverlay[2].secondColour))
								SetPedHeadOverlayColor(ped, 2, 1, tonumber(skin['face'].headOverlay[3].firstColour), tonumber(skin['face'].headOverlay[3].secondColour))
								SetPedHeadOverlayColor(ped, 3, 0, tonumber(skin['face'].headOverlay[4].firstColour), tonumber(skin['face'].headOverlay[4].secondColour))
								SetPedHeadOverlayColor(ped, 4, 2, tonumber(skin['face'].headOverlay[5].firstColour), tonumber(skin['face'].headOverlay[5].secondColour))
								SetPedHeadOverlayColor(ped, 5, 2, tonumber(skin['face'].headOverlay[6].firstColour), tonumber(skin['face'].headOverlay[6].secondColour))
								SetPedHeadOverlayColor(ped, 6, 0, tonumber(skin['face'].headOverlay[7].firstColour), tonumber(skin['face'].headOverlay[7].secondColour))
								SetPedHeadOverlayColor(ped, 7, 0, tonumber(skin['face'].headOverlay[8].firstColour), tonumber(skin['face'].headOverlay[8].secondColour))
								SetPedHeadOverlayColor(ped, 8, 2, tonumber(skin['face'].headOverlay[9].firstColour), tonumber(skin['face'].headOverlay[9].secondColour))
								SetPedHeadOverlayColor(ped, 9, 0, tonumber(skin['face'].headOverlay[10].firstColour), tonumber(skin['face'].headOverlay[10].secondColour))
								SetPedHeadOverlayColor(ped, 10, 1, tonumber(skin['face'].headOverlay[11].firstColour), tonumber(skin['face'].headOverlay[11].secondColour))
								SetPedHeadOverlayColor(ped, 11, 0, tonumber(skin['face'].headOverlay[12].firstColour), tonumber(skin['face'].headOverlay[12].secondColour))
							end
						else
							print('skin[face] is nil')
						end

						-----TATTOOS-------
						if skin['tattoo'] ~= nil then
							ClearPedDecorations(ped)
							for i = 1, #skin['tattoo'] do
								ApplyPedOverlay(ped, skin['tattoo'][i][1], skin['tattoo'][i][2])
							end
						else
							print('skin[tattoo] is nil')
						end
					end
				else
					print('skin[skin] is nil')
				end
			else
				print('skin is nil')
			end
		else
			print('ped is nil')
		end
	end)

## Are you using the advanced multi-character method?
If `Config.UseAdvancedMultiCharMethod` is enabled, and you fully understand what you are doing, replace these events in their respective files. This method is more complicated, and more work to set up, but is more optimised than the standard esx_kashacters method as it does not change every identifier in every defined table in the database every time a player connects.

- This is completely optional and we do not reccomend using this option unless you have advanced knowledge of lua.
- **WARNING** if you are not 100% sure what you are doing here, please contact a member of the Codesign Team before implementing these changes.
- When using this method, you will need to replace the native method of getting the steam id `GetPlayerIdentifiers(source[1]`, with `xPlayer.identifier` for all of your server sided resources.

**ESX version 1.1 - essentialmode/server/main.lua/line 41** - replace the existing block of code with this.
	
	RegisterServerEvent('es:firstJoinProper')
	AddEventHandler('es:firstJoinProper', function(charID)
		local Source = source
		Citizen.CreateThread(function()
			local id
			for k,v in ipairs(GetPlayerIdentifiers(Source)) do
				if string.match(v, 'steam:') then
					id = charID..''..v:sub(7)
					break
				end
			end

			if not id then
				DropPlayer(Source, "SteamID not found, please try reconnecting with Steam open.")
			else
				registerUser(id, Source)
				justJoined[Source] = true
				if(settings.defaultSettings.pvpEnabled)then
					TriggerClientEvent("es:enablePvp", Source)
				end
			end

			return
		end)
	end)

**ESX version 1.2 - es_extended/server/main.lua/line 1** - replace the existing block of code with this.

	RegisterNetEvent('esx:playerJoined')
	AddEventHandler('esx:playerJoined', function(charID)
		onPlayerJoined(source, charID)
	end)

	function onPlayerJoined(playerId, charID)
		local identifier

		for k,v in ipairs(GetPlayerIdentifiers(playerId)) do
			if string.match(v, 'license:') then
				identifier = charID..''..v:sub(9)
				break
			end
		end

		if identifier then
			MySQL.Async.fetchScalar('SELECT 1 FROM users WHERE identifier = @identifier', {
				['@identifier'] = identifier
			}, function(result)
				if result then
					loadESXPlayer(identifier, playerId)
				else
					MySQL.Async.execute('INSERT INTO users (identifier) VALUES (@identifier)', {
						['@identifier'] = identifier
					}, function(rowsChanged)
						loadESXPlayer(identifier, playerId)
					end)
				end
			end)
		else
			DropPlayer(playerId, 'Your Rockstar license could not be found')
		end
	end

**ESX version 1.final - es_extended/server/main.lua/line 6** - replace the existing block of code with this.
	
	RegisterNetEvent('esx:onPlayerJoined')
	AddEventHandler('esx:onPlayerJoined', function(charID)
		onPlayerJoined(source, charID)
	end)

	function onPlayerJoined(playerId, charID)
		local identifier

		for k,v in ipairs(GetPlayerIdentifiers(playerId)) do
			if string.match(v, 'license:') then
				identifier = charID..''..v:sub(9)
				break
			end
		end

		if identifier then
			if ESX.GetPlayerFromIdentifier(identifier) then
				DropPlayer(playerId, ('there was an error loading your character!\nError code: identifier-active-ingame\n\nThis error is caused by a player on this server who has the same identifier as you have. Make sure you are not playing on the same Rockstar account.\n\nYour Rockstar identifier: %s'):format(identifier))
			else
				MySQL.Async.fetchScalar('SELECT 1 FROM users WHERE identifier = @identifier', {
					['@identifier'] = identifier
				}, function(result)
					if result then
						loadESXPlayer(identifier, playerId)
					else
						local accounts = {}

						for account,money in pairs(Config.StartingAccountMoney) do
							accounts[account] = money
						end

						MySQL.Async.execute('INSERT INTO users (accounts, identifier) VALUES (@accounts, @identifier)', {
							['@accounts'] = json.encode(accounts),
							['@identifier'] = identifier
						}, function(rowsChanged)
							loadESXPlayer(identifier, playerId)
						end)
					end
				end)
			end
		else
			DropPlayer(playerId, 'there was an error loading your character!\nError code: identifier-missing-ingame\n\nThe cause of this error is not known, your identifier could not be found. Please come back later or report this problem to the server administration team.')
		end
	end

## Default Key-binds

> Left/Right Arrows - Cycle through the characters.

> Enter/Left Mouse - Select character.

## Is the resource not working as expected?
 - Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
 - Make sure the name of the folder is `cd_multicharacter`.
 - If the resource has started correctly, and there are no errors, try changing the keys in the config to one that you know works, as one of your other resources may be disabling that specific key.
-   If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).


