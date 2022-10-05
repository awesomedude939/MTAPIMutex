![Original Image]([https://i.gyazo.com/16c79a23c58758a96b097a1ff082fc2d.png])

**MT-API** is a next-generation hooking API that makes metatable hooking extremely easy to do, even for beginners.

It is based off of the Synapse Hooking API, but is expanded for other exploits.

____________________________________________________________________________________________________________


**Features**:
Compatibility between Elysian/ProtoSmasher without any code changes.
Easy to use, powerful but sleek API.
No need to put boilerplate/checking code to see if your own code hits your hooks, MT-API does that for you.
Fast hooking speed, even with lots of hooks installed. Don't cut down your FPS to 5 just because you have a MT hook.
It just works.

____________________________________________________________________________________________________________

Documentation:

Using MT-API was made to be very easy. You can add a hook just like this:
Code:
```
game.Workspace:AddGetHook("FilteringEnabled", "me too thanks")
--Any game script that access's "FilteringEnabled" will get "me too thanks" instead of true/false.
```
You can also have a optional callback function for your 'Get' hook. The table will be passed as the first argument.
Code:
```
game.Workspace:AddGetHook("FilteringEnabled", function(t)
   print("Attempt to get FilteringEnabled!")
   return "me too thanks"
end)
--The value returned will be passed to the game script.
```
MT-API also supports hooks for setting, not just getting:
Code:
```
game.Players.LocalPlayer.Character.Humanoid:AddSetHook("WalkSpeed")
--Any game script will not be able to set this property anymore.
```
It also supports callback functions. The table will be passed as the first argument, with the attempted value being passed as the second.
Code:
```
game.Players.LocalPlayer.Character.Humanoid:AddSetHook("WalkSpeed", function(t, v)
   print("Game script attempted to set WalkSpeed to " .. tostring(v) .. "!")
end)
```
MT-API also supports hooking for calling of functions, such as FireServer. The original function is passed as the first argument.
Code:
```
game.ReplicatedStorage.Test:AddCallHook("FireServer", function(o, ...)
   print'Nice try, The Streets!'
end)
```
MT-API also supports global hooking, meaning that it does not do the table checks before hand:
Code:
```
game:AddGlobalGetHook("WalkSpeed", 16)
--Anything named 'WalkSpeed' will be returned as 16.
```
Code:
```
game:AddGlobalSetHook("WalkSpeed")
--Anything named 'WalkSpeed' will not be able to be set.
```
Code:
```
game:AddGlobalCallHook("FireServer", function(t, o, ...)
   print("Attempt to call FireServer with instance " .. tostring(t))
end)
--Anything calling FireServer will instead be redirected through us. Note that the table will be passed now aswell as the first argument.
```
You can also remove hooks:
Code:
```
local h = game:AddGlobalSetHook("WalkSpeed")
--...
h:Remove() --It is removed now.

Finally, MT-API supports property emulation. It is extremely useful for bypassing anti-exploits:
Code:
game.Players.LocalPlayer.Character.Humanoid:AddPropertyEmulator("WalkSpeed")
game.Players.LocalPlayer.Character.Humanoid:AddPropertyEmulator("Health")

--Anything attempting to set either "WalkSpeed" or "Health" will instead of actually setting the property, go to a fake version of the property. When they attempt to read it back, it will return the emulated version.
```
Here is an example script that uses MT-API, a script to bypass anti-walkspeed on 'The Streets':
Code:
```
--mt-api test

if not getgenv().MTAPIMutex then loadstring(game:HttpGet("https://pastebin.com/raw/UwFCVrhS", true))() end

game.Players.LocalPlayer.Character.Humanoid:AddPropertyEmulator("WalkSpeed")
game.Players.LocalPlayer.Character.Humanoid:AddPropertyEmulator("Health")
game.Players.LocalPlayer.Character.Humanoid:AddCallHook("BreakJoints", function() end)
game.ReplicatedStorage.Test:AddCallHook("FireServer", function() end)
```

____________________________________________________________________________________________________________

Installation:
MT-API can be installed with one line in your script.

Code:
```
if not getgenv().MTAPIMutex then loadstring(game:HttpGet("https://pastebin.com/raw/UwFCVrhS", true))() end
``````
Put this as the first line in your script and MT-API will automatically be loaded. You can then use the functions as you wish. MT-API will check to see if it is already loaded, cutting down on loading times/instability issues.

I hope you have fun. Thanks!
