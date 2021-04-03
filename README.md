# Silent-Aim-Framework
Made By Stefanuk12 ( Thanks bro! )

# Examples

`Namecall Version:`
```lua
--// Namecall Version // --
-- // Metatable Variables
local mt = getrawmetatable(game)
local backupindex = mt.__index
setreadonly(mt, false)
-- // Load Silent Aim
local ValiantAimHacks = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/Stefanuk12/ROBLOX/master/Universal/Experimental%20Silent%20Aim%20Module.lua"))()
-- // Hook
mt.__namecall = newcclosure(function(...)
    -- // Vars
    local args = {...}
    local method = getnamecallmethod()
    -- // Checks
    if (method == "FireServer") then
        if (args[1].Name == "RemoteNameHere") then
            -- change args
            -- // Return changed arguments
            return backupnamecall(unpack(args))
        end
    end
    -- // Return
    return backupnamecall(...)
end)
-- // Revert Metatable readonly status
setreadonly(mt, true)
```

`Index Version:`
```lua
-- // Index Version // --
-- // Metatable Variables
local mt = getrawmetatable(game)
local backupindex = mt.__index
setreadonly(mt, false)
-- // Load Silent Aim
local ValiantAimHacks = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/Stefanuk12/ROBLOX/master/Universal/Experimental%20Silent%20Aim%20Module.lua"))()
-- // Hook
mt.__index = newcclosure(function(t, k)
    -- // Check if it trying to get our mouse's hit or target
    if (t:IsA("Mouse") and (k == "Hit" or k == "Target")) then
        -- // If we can use the silent aim
        if (ValiantAimHacks.checkSilentAim()) then
            -- // Vars
            local TargetPart = ValiantAimHacks.SelectedPart
            -- // Return modded val
            return (k == "Hit" and TargetPart.CFrame or TargetPart)
        end
    end
    -- // Return
    return backupindex(t, k)
end)
-- // Revert Metatable readonly status
setreadonly(mt, true)
```
