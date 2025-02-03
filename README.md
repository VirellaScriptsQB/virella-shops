Dependencies VIRELLA - SHOPS FINAL
Make sure the following dependencies are installed on your server:
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



STEP 1 :
qb-core
qb-menu
qb-input
okokBanking (Optional, for bank payment support)
Installation
Step 1: Add Resource to Server
Download and extract the virella-shops resource to your FiveM resources folder.
Ensure the folder is named virella-shops.
Step 2: Add Resource to Server Config
Add the following line to your server.cfg:


STEP 2:
cfg
Copy
Edit
ensure virella-shops / FYI IF ITS A STANDALONE SCRIPT SUCH AS THIS YOU DO NOT NEED TO ENSURE JUST MAKE SURE YOU HAVE THE FOLLOWING DEPENDENCIES EITHER OKOKBANKING WORKS WITH VIRELLA-SHOPS OR QB-BANKING
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------






STEP 3: Configure Shops
Modify the config.lua file to define your shops, items, tax settings, and other custom features. Examples are provided in the file.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------






----- STEP 4
Define shops under Config.ShopPoints.
Set tax rates in Config.TaxSystem.
Customize opening hours, stock, and item lists.
Step 4: Ensure Dependencies
Make sure all dependencies are installed and configured correctly:
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



STEP 5 : JUST DOUBLE CHECK AND MAKE SURE THAT YOU HAVE ALL THE REQUIRED SCRIPTS IN ORDER TO START THIS ONE! OTHERWISE THIS SCRIPT WILL NOT WORK AS INTENDED!
cfg
Copy
Edit
ensure qb-core
ensure qb-menu
ensure qb-input
ensure okokBanking  # Optional
Configuration Guide
Shop Points
Define your shops in Config.ShopPoints. Example:
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

lua
Copy
Edit
["general_store_1"] = {
    location = vector3(116.47, -1089.09, 29.23),
    pedModel = "mp_m_shopkeep_01",
    interactText = "Browse Items",
    currency = "cash",
    blip = { enabled = true, name = "General Store" },
    openHours = { start = 9, finish = 21 },  -- Opens at 9 AM and closes at 9 PM
    items = {
        { name = "water_bottle", label = "Water Bottle", price = 5, stock = 50 },
        { name = "sandwich", label = "Sandwich", price = 10, stock = 30 }
    }
}
Tax System
Configure tax settings in Config.TaxSystem. Example:

lua
Copy
Edit
Config.TaxSystem = {
    defaultTaxRate = 0.1,          -- Default tax rate (10%)
    shopTaxOverrides = {
        ["weapon_shop_1"] = 0.2    -- 20% tax rate for weapon shop
    },
    exemptJobs = { "police", "ems" },  -- Exempted jobs from taxes
    taxApplyDelay = 2000           -- Delay before tax is deducted after a purchase (milliseconds)
}
Stock Management
Enable or disable stock with the Config.StockSystem setting:

lua
Copy
Edit
Config.StockSystem = {
    enabled = true,
    restockTime = 3600,  -- Restock every 1 hour
    maxStock = {
        ["water_bottle"] = 50,
        ["sandwich"] = 30
    }
}
Quantity Selection (qb-input)
Players can choose how many items they want to purchase using qb-input. This allows precise control over item purchases, and total costs are calculated accordingly.




============== STEP 6 PAYMENT OPTIONS ============== THIS IS FOR SPECIFIC SHOPS, IF YOU WAN'T A SHOP TO EITHER ACCEPT BANK , CASH , OR MARKEDBILLS , MAKE SURE YOU CHOOSE THE CORRECT CURRENCY SETTING IN THE CONFIG.LUA WHILE SETTING UP THE SHOP! :)
Payment Options
Players can choose to pay using cash or bank balance.
Bank payments are processed through okokBanking.
Commands
No commands are required for this resource. All interactions are handled through in-game NPCs and qb-menu interfaces.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



----- SIMPLE SCRIPT NOTES ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


SHOP CONFIGURATION EXAMPLES : all you need to do for this shop to be placed is copy vector 3 in game where you want it restart the script and ped should appear
this depends whether or not you want a gang / job / weapon / or general shop. I will not explain the rest its pretty straight Forward i would like to say.

Config.ShopPoints = {
    -- ***General Shops***
    general_shops = {
        ["general_store_1"] = {
            location = vector3(116.47, -1089.09, 29.23),
            pedModel = "mp_m_shopkeep_01",
            interactText = "Browse Items",
            currency = "cash",  -- Accepts cash payment
            blip = { enabled = true, name = "General Store" },
            openHours = { start = 0, finish = 0 },  -- Always open if shopAlwaysOpen is true
            items = {
                { name = "water_bottle", label = "Water Bottle", price = 5, stock = 50 },
                { name = "sandwich", label = "Sandwich", price = 10, stock = 30 }
            }
        }
    },

    -- ***Weapon Shops***
    weapon_shops = {
        ["weapon_shop_1"] = {
            location = vector3(1692.41, 3759.17, 34.705),
            pedModel = "s_m_y_ammucity_01",
            interactText = "Browse Weapons",
            currency = "markedbills",  -- Accepts marked bills for payment
            blip = { enabled = false, name = "Weapon Shop" },
            openHours = { start = 10, finish = 22 },  -- Shop opens from 10 AM to 10 PM
            items = {
                { name = "pistol", label = "Pistol", price = 1500, stock = 5 },
                { name = "pistol_ammo", label = "Pistol Ammo", price = 100, stock = 100 }
            }
        }
    },

    -- ***Gang Shops***
    gang_shops = {
        ["gang_shop_lostmc"] = {
            location = vector3(2450.32, 4969.13, 45.57),
            pedModel = "g_m_y_mexgoon_03",
            interactText = "Gang Supplies",
            currency = "cash",  -- Cash payment
            requiredGang = "lostmc",  -- Restricted to the "Lost MC" gang
            protectionFee = 0.05,  -- 5% extra fee if not in the gang
            blip = { enabled = false },  -- No blip for gang shop
            openHours = { start = 18, finish = 4 },  -- Shop opens at 6 PM and closes at 4 AM
            items = {
                { name = "lockpick", label = "Lockpick", price = 50, stock = 20 },
                { name = "handcuffs", label = "Handcuffs", price = 150, stock = 10 }
            }
        }
    },

    -- ***Job-Restricted Shops***
    job_shops = {
        ["police_shop"] = {
            location = vector3(451.75, -980.16, 30.69),
            pedModel = "s_m_y_cop_01",
            interactText = "Police Equipment",
            currency = "bank",  -- Payment through bank account
            requiredJob = "police",  -- Restricted to police job
            blip = { enabled = false, name = "Police Armory" },
            openHours = { start = 6, finish = 22 },  -- Open from 6 AM to 10 PM
            items = {
                { name = "pistol_ammo", label = "Pistol Ammo", price = 100, stock = 200 },
                { name = "flashlight", label = "Flashlight", price = 50, stock = 50 }
            }
        }
    }
}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------















Events
Client Events
shopPoints:openMenu – Opens the shop menu.
shopPoints:selectQuantity – Prompts the player to select the quantity of an item.
shopPoints:choosePayment – Allows the player to choose a payment method.
shopPoints:purchaseItem – Triggers the purchase event.
Server Events
shopPoints:handlePurchase – Processes item purchases, deducts payment, and applies taxes.
Example Scenario
A player approaches the NPC at a general store.
They press E to interact and open the qb-menu.
They select an item, e.g., Water Bottle.
qb-input prompts them to choose the quantity.
After selecting the quantity (e.g., 5), they choose their payment method (cash or bank).
The purchase is processed, and if applicable, tax is deducted from their bank account.
The player receives the items in their inventory.
Known Issues & Troubleshooting
Incorrect Quantity or Stock Issues: Ensure quantity is properly handled in both client and server scripts.
Dependency Errors: Verify that qb-core, qb-menu, and qb-input are installed and up to date.
Bank Payment Issues: Ensure okokBanking is installed if bank payments are enabled.
Credits
Developed by: Virella

Special thanks to the QBCore community and contributors for their support.

License
This script is licensed under the terms provided by the developer. Redistribution without permission is prohibited. Contact the developer for any modifications or custom requests.

Enjoy the Virella-Shops experience! For support, reach out through your server's development channels. Happy roleplaying! 😊
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

