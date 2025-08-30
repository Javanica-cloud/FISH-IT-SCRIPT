-- Load Rayfield UI
local Rayfield = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Rayfield/main/source"))()

local Window = Rayfield:CreateWindow({
    Name = "Fish It Hub | Compact UI",
    LoadingTitle = "Fish It Hub",
    LoadingSubtitle = "Compact & Organized",
    ConfigurationSaving = { Enabled=true, FolderName="FishItHub", FileName="CompactConfig" },
    KeySystem=false
})

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local RemoteFolder = ReplicatedStorage:WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_net@0.2.0.net"):WaitForChild("RE")

-- ======= FISHING TAB =======
local FishingTab = Window:CreateTab("🎣 Fishing", 4483362458)
local FishSection = FishingTab:CreateSection("Auto Fishing")
local AutoFishing, AutoPerfect, AutoAmazing = true, true, true

FishingTab:CreateToggle({ Name="Auto Fishing & Catch", CurrentValue=true, Flag="AutoFishing", Callback=function(v) AutoFishing=v end })
FishingTab:CreateToggle({ Name="Auto Perfect", CurrentValue=true, Flag="AutoPerfect", Callback=function(v) AutoPerfect=v end })
FishingTab:CreateToggle({ Name="Auto Amazing", CurrentValue=true, Flag="AutoAmazing", Callback=function(v) AutoAmazing=v end })

local FishingEvent = RemoteFolder:WaitForChild("Fishing")
spawn(function()
    while true do RunService.Heartbeat:Wait()
        if AutoFishing then
            pcall(function()
                FishingEvent:FireServer()
                if AutoPerfect then FishingEvent:FireServer("Perfect") end
                if AutoAmazing then FishingEvent:FireServer("Amazing") end
            end)
        end
    end
end)

-- ======= AUTO SELL TAB =======
local AutoSellTab = Window:CreateTab("💰 Auto Sell", 4483362458)
local AutoSell, SellThreshold = false, 50
local SellSection = AutoSellTab:CreateSection("Sell Settings")

AutoSellTab:CreateToggle({ Name="Auto Sell", CurrentValue=false, Flag="AutoSell", Callback=function(v) AutoSell=v end })
AutoSellTab:CreateSlider({ Name="Sell Threshold", Range={1,100}, Increment=1, Suffix="%", CurrentValue=50, Flag="SellThreshold", Callback=function(v) SellThreshold=v end })

local SellEvent = RemoteFolder:WaitForChild("Sell")
spawn(function()
    while true do RunService.Heartbeat:Wait()
        if AutoSell then pcall(function() SellEvent:FireServer(SellThreshold) end) end
    end
end)

-- ======= PLAYER TAB =======
local PlayerTab = Window:CreateTab("🧍 Player", 4483362458)
local PlayerSection = PlayerTab:CreateSection("Player Tweaks")
local FloatWater, TradeNoDelay, InfinityJump = true,true,true 
local WalkSpeed = 16

PlayerTab:CreateToggle({ Name="Float on Water", CurrentValue=true, Flag="FloatWater", Callback=function(v) FloatWater=v end })
PlayerTab:CreateToggle({ Name="Trade No Delay", CurrentValue=true, Flag="TradeNoDelay", Callback=function(v) TradeNoDelay=v end })
PlayerTab:CreateToggle({ Name="Infinity Jump", CurrentValue=true, Flag="InfinityJump", Callback=function(v) InfinityJump=v end })
PlayerTab:CreateSlider({ Name="Walk Speed", Range={16,500}, Increment=1, Suffix="Speed", CurrentValue=16, Flag="WalkSpeed", Callback=function(v)
    WalkSpeed=v
    Character.Humanoid.WalkSpeed=v
end })

local UserInputService = game:GetService("UserInputService")
UserInputService.JumpRequest:Connect(function()
    if InfinityJump then Character.Humanoid:ChangeState("Jumping") end
end)

-- Spawn Boat / Buy Rod / Buy Bait
PlayerTab:CreateSection("Auto Purchases")
PlayerTab:CreateButton({ Name="Spawn Boat", Callback=function() pcall(function() RemoteFolder:WaitForChild("SpawnBoat"):FireServer() end) end })
PlayerTab:CreateButton({ Name="Buy Rod", Callback=function() pcall(function() RemoteFolder:WaitForChild("BuyRod"):FireServer() end) end })
PlayerTab:CreateButton({ Name="Buy Bait", Callback=function() pcall(function() RemoteFolder:WaitForChild("BuyBait"):FireServer() end) end })

-- ======= TELEPORT TAB =======
local TeleportTab = Window:CreateTab("🗺️ Teleport", 4483362458)
local TeleportSection = TeleportTab:CreateSection("Locations")
local Teleports = {
    ["Coral Reefs"]=Vector3.new(-2945,66,2248), ["Kohana"]=Vector3.new(-645,16,606),
    ["Weather Machine"]=Vector3.new(-1535,2,1917), ["Lost Isle [Sisypuhus]"]=Vector3.new(-3703,-136,-1019),
    ["Winter Fest"]=Vector3.new(1616,4,3280), ["Esoteric Depths"]=Vector3.new(3214,-1303,1411),
    ["Tropical Grove"]=Vector3.new(-2047,6,3662), ["Stingray Shores"]=Vector3.new(2,4,2839),
    ["Lost Isle [Treasure Room]"]=Vector3.new(-3594,-285,-1635), ["Lost Isle [Lost Shore]"]=Vector3.new(-3672,70,-912),
    ["Kohana Volcano"]=Vector3.new(-512,24,191), ["Crater Island"]=Vector3.new(1019,20,5071)
}
for name,pos in pairs(Teleports) do
    TeleportTab:CreateButton({ Name=name, Callback=function() Character.HumanoidRootPart.CFrame=CFrame.new(pos) end })
end

-- ======= BUY WEATHER TAB =======
local WeatherTab = Window:CreateTab("☁️ Weather", 4483362458)
local WeatherList={"Cloud","Storm","Wind","Radiant","Snow"}
local AutoBuyWeather=true 
WeatherTab:CreateToggle({ Name="Auto Buy Weather", CurrentValue=true, Flag="AutoBuyWeather", Callback=function(v) AutoBuyWeather=v end })
local WeatherEvent=RemoteFolder:WaitForChild("BuyWeather")
for _,w in pairs(WeatherList) do
    WeatherTab:CreateButton({ Name="Buy "..w, Callback=function() pcall(function() WeatherEvent:FireServer(w) end) end })
end
spawn(function()
    while true do RunService.Heartbeat:Wait()
        if AutoBuyWeather then
            for _,w in pairs(WeatherList) do pcall(function() WeatherEvent:FireServer(w) end) end
        end
    end
end)

-- ======= EVENT TAB =======
local EventTab = Window:CreateTab("🎉 Event", 4483362458)
local EventRemote=RemoteFolder:FindFirstChild("Event")
local AutoFarmEvent=true
EventTab:CreateToggle({ Name="Auto Farm Event", CurrentValue=true, Flag="AutoFarmEvent", Callback=function(v) AutoFarmEvent=v end })
EventTab:CreateButton({ Name="Refresh Event List", Callback=function() pcall(function() EventRemote:FireServer("RefreshList") end) end })
EventTab:CreateButton({ Name="Teleport to Event", Callback=function() pcall(function() EventRemote:FireServer("Teleport") end) end })
spawn(function()
    while true do RunService.Heartbeat:Wait()
        if AutoFarmEvent then pcall(function() EventRemote:FireServer("Farm") end) end
    end
end)

-- ======= SETTINGS TAB =======
local SettingsTab = Window:CreateTab("⚙️ Settings", 4483362458)
local AntiAFK, AntiLag=true,true
SettingsTab:CreateToggle({ Name="Anti AFK", CurrentValue=true, Flag="AntiAFK", Callback=function(v)
    AntiAFK=v
    if v then
        local vu=game:GetService("VirtualUser")
        game:GetService("Players").LocalPlayer.Idled:Connect(function()
            vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
            wait(1)
            vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        end)
    end
end})
SettingsTab:CreateToggle({ Name="Anti Lag / Low Texture", CurrentValue=true, Flag="AntiLag", Callback=function(v)
    AntiLag=v
    if v then
        game:GetService("Lighting").GlobalShadows=true
        game:GetService("Lighting").FogEnd=9e9
        for _,v in pairs(workspace:GetDescendants()) do
            if v:IsA("BasePart") then v.Material=Enum.Material.Plastic v.Reflectance=0 end
        end
    end
end})
SettingsTab:CreateButton({ Name="Rejoin Server", Callback=function()
    game:GetService("TeleportService"):Teleport(game.PlaceId, LocalPlayer)
end})

print("Fish It Hub | Compact UI Loaded ✅")
