
# INSTALLATION GUIDE
**1.** Unzip the `cd_easytime.zip` folder.

 **2.** Before starting the script, please read the `config.lua` (this is located inside the main cd_easytime folder) and configure the script to suit your servers needs.
 
**3.** Add the resource to your server start config: `ensure cd_easytime`. The name of the folder must not be changed or the resource will not function correctly.

## How do I use?
The default command to open the UI is `/easytime`. If you are not using esx you will need to set `Config.Framework` to 'custom' and add your own code for the permissions check in `server/server.lua line 229`.

## How do I enable persistent weather?
Firstly enable the `Config.PersistentWeather` option in the config.lua. Then in order to save the settings before a server restart, you must trigger this server event `TriggerServerEvent('cd_easytime:SaveSettings')`. The settings will be saved in the `settings.txt` file.  Now when the server/script restarts, these settings will automatically re apply for all players. Staff can also manually save these settings through the UI.

## Shell support
When a player enters a shell you will need to trigger the client event below,. When this happens the time will change to night time and weather will change to clear for this player only to ensure there are no visual anomaly's.
|When entering a shell| When exiting a shell |
|--|--|
| `TriggerEvent('cd_easytime:PauseSync', true)` | `TriggerEvent('cd_easytime:PauseSync', false)` |

## Is the resource not working as expected?
- Make sure the name of the folder is `cd_easytime`.
- Check the server console and the in game F8 console for errors.
- If all else fails, contact the Codesign Team in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
