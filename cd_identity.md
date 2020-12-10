# INSTALLATION GUIDE
**1.** Unzip the `cd_identity.zip` folder.

**2.** Paste your Authorisation Token into the file named `authorization.lua`. This is located inside the main `cd_identity` folder.

**3.** Install the SQL file. This is located inside the `READ_ME_AFTER_PURCHASING` folder, it's named `cd_identity_SQLFILE`.

**4.** Before starting the resource, please read all of the configurable files inside the `configs` folder. This is located inside the main `cd_identity` folder . Now you can configure the resource to suit your servers needs.
 
**5.** **WARNING** do not edit the obfuscated files in any way, as this will result in you being blacklisted.
 
**6.** Add the resource to your server start config: `ensure cd_identity`. The name of the folder must not be changed or the resource will not function correctly.

## How to use?
This can be triggered from the server or client. In the `server_customise_me.lua` file you will have access to customise the sql query, so you can decide what data gets saved to the database. But make sure you only trigger this event after your character has already been loaded in by esx, because esx will insert most of your characters data into the database, and we will update the database with the rest of the data that we have just created in the identity UI.
|From Server| From Client |
|--|--|
| `TriggerclientEvent('cd_identity:OpenIdentityUI', source)` | `Triggerevent('cd_identity:OpenIdentityUI')` |

## Is the resource not working as expected?
- Firstly always make sure the resource has started correctly. Check for obvious error prints. Then check the server console prints for a blue print saying `Authorised Successfully` and check for a client sided print saying `Successful`.
- Make sure the name of the folder is `cd_identity`.
- If all else fails, contact the Codesign Team in your private discord channel in the [Codesign Discord](https://discord.gg/HmDFGp62Tr).
