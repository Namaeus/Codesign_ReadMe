
# INSTALLATION GUIDE
**1.** Unzip the `cd_drawtextui.zip` folder.
 
**2.** Add the resource to your server start config: `ensure cd_drawtextui`. The name of the folder must not be changed or the resource will not function correctly.

## How to use?

- This can be triggered from the server or client. But this is a client event.
-  Multiple examples are posted below, choose one best suited to your experience level. The easiest way for you to implement this into your resources, would be to use one of the examples below as a template, and copy and paste your code into it.

|Show the UI| Hide the UI |
|--|--|
| `TriggerEvent('cd_drawtextui:ShowUI', 'show', TEXT_HERE)` | `TriggerEvent('cd_drawtextui:HideUI')` |


> **Example 1 : This is how to implement the UI for a single location.**

    Citizen.CreateThread(function()
	    local alreadyEnteredZone = false
	    local text = '<b>Title</b></p>[E] Press E to be bald'
	    while true do
	        wait = 5
	        local ped = PlayerPedId()
	        local inZone = false
	        local dist = #(GetEntityCoords(ped)-vector3(0,0,0))
	        if dist <= 5.0 then
	            wait = 5
	            inZone  = true

	            if IsControlJustReleased(0, 38) then
	                TriggerEvent('add your event here')
	            end
	        else
	            wait = 1000
	        end
	        
	        if inZone and not alreadyEnteredZone then
	            alreadyEnteredZone = true
	            TriggerEvent('cd_drawtextui:ShowUI', 'show', text)
	        end

	        if not inZone and alreadyEnteredZone then
	            alreadyEnteredZone = false
	            TriggerEvent('cd_drawtextui:HideUI')
	        end
	        Citizen.Wait(wait)
	    end
	end)

> **Example 2 : This is how to implement the UI while doing a for loop for multiple locations in 1 thread.**
	
	Config = {}
	Config.Example = {
	    [1] = vector3(1.1, 1.1, 1.1),
	    [2] = vector3(2.2, 2.2, 2.2),
	    [3] = vector3(3.3, 3.3, 3.3),
	}

	Citizen.CreateThread(function()
	    local alreadyEnteredZone = false
	    local text = '<b>Title</b></p>[E] Press E to be bald'
	    while true do
		wait = 5
		local ped = PlayerPedId()
		local inZone = false
		for cd = 1, #Config.Table do
		    local dist = #(GetEntityCoords(ped)-vector3(Config.Example[cd].x, Config.Example[cd].y, Config.Example[cd].z))
		    if dist <= 5.0 then
			wait = 5
			inZone  = true
	
			if IsControlJustReleased(0, 38) then
			    TriggerEvent('add your event here')
			end
			break
		    else
			wait = 2000
		    end
		end

		if inZone and not alreadyEnteredZone then
		    alreadyEnteredZone = true
		    TriggerEvent('cd_drawtextui:ShowUI', 'show', text)
		end

		if not inZone and alreadyEnteredZone then
		    alreadyEnteredZone = false
		    TriggerEvent('cd_drawtextui:HideUI')
		end
		Citizen.Wait(wait)
	    end
	end)

> **Example 3 : This is a more advanced method of the `example 2` above. This is more customisable and can handle all of the keypresses in said resource in a single thread.**

	Config = {}
	Config.Example = {
		[1] = {coords = vector3(1.1, 1.1, 1.1), distance = 5, key = 38, eventname = 'example:testevent', text = '<b>Title</b></p>[E] Press E to be bald'},
		[2] = {coords = vector3(2.2, 2.2, 2.2), distance = 5, key = 47, eventname = 'example:testevent', text = '<b>Title</b></p>[E] Press E to be bald'},
		[3] = {coords = vector3(3.3, 3.3, 3.3), distance = 5, key = 74, eventname = 'example:testevent', text = '<b>Title</b></p>[E] Press E to be bald'},
	}
    
    Citizen.CreateThread(function()
        local alreadyEnteredZone = false
        local text = nil
        while true do
            wait = 5
            local ped = PlayerPedId()
            local inZone = false
            for cd = 1, #Config.Example do
                local dist = #(GetEntityCoords(ped)-vector3(Config.Example[cd].coords.x, Config.Example[cd].coords.y, Config.Example[cd].coords.z))
                if dist <= Config.Example[cd].distance then
                    wait = 5
                    inZone  = true
                    text = Config.Example[cd].text

                    if IsControlJustReleased(0, Config.Example[cd].key) then
                        TriggerEvent(Config.Example[cd].eventname)
                    end
                    break
                else
                    wait = 2000
                end
            end
            
            if inZone and not alreadyEnteredZone then
                alreadyEnteredZone = true
                TriggerEvent('cd_drawtextui:ShowUI', 'show', text)
            end

            if not inZone and alreadyEnteredZone then
                alreadyEnteredZone = false
                TriggerEvent('cd_drawtextui:HideUI')
            end
            Citizen.Wait(wait)
        end
    end)




## Is the resource not working as expected?
- Make sure the name of the folder is `cd_drawtextui`.
- Check the server console and the in game F8 console for errors.
- If all else fails, contact the Codesign Team in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
