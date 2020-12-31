# Key bindings setup
We have started using the FiveM native called `RegisterKeyMapping` [documentation here](http://runtime.fivem.net/doc/natives/?_0xD7664FD1). This removes the need for while loops checking every frame for keypresses, therefor allowing the resource to be more optimised. This FiveM native works by triggering the chat command it has been registered with when the keybind is pressed. This new method also allows each client to change their own key binds in game [Example Here](https://imgur.com/GRWKelR) `Open Gta5 settings > Key Bindings > FiveM`.

## How to change keys with KeyMapping

- **If you wish to change the default key bind, you must change it in the `configs/config.lua` BEFORE starting the resource on your server.**

- Once you have started the resource on your server for the first time with the RegisterKeyMapping enabled, the key **cannot** be changed in the config. Now the only way the key can be changed while still using the KeyMapping is for players to change the key for themselves in the in game Gta5 key binding settings. [Example Here](https://imgur.com/GRWKelR)  `Open Gta5 settings > Key Bindings > FiveM`.

## How to disable KeyMapping

-   This method can be disabled by removing the chat command/changing the name of the chat command and then restarting your server/restarting your chat resource.
    
-   The RegisterKeyMapping key bindings them self currently can not be removed from the Gta5 key bindings settings. Although once the chat command has been removed, it will not work anymore when you press the key.

-  Once you have disabled the RegisterKeyMapping method you can use other methods such as chat commands *(the name of the new chat command must be named differently from the original)* or while loops checking for key presses `IsControlJustReleased` or custom methods to trigger these events highlighted below.

> `TriggerEvent('cd_carhud:OpenSettingsUI')`  
> `TriggerEvent('cd_carhud:ToggleSeatbelt')`

## Notes
- Players may not be able to have multiple keys bound to the same key.

- According to a post on the FiveM forums you can remove unused keybinds [here](https://forum.cfx.re/t/registerkeymapping-question/1108639/10?u=ramp_rp). But we have not tested this, its on you if you wish to try it.

## Default key bindings
> Y - Open the settings UI.

> B - Toggle the seatbelt.
