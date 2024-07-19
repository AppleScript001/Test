local Material = loadstring(game:HttpGet("https://raw.githubusercontent.com/Kinlei/MaterialLua/master/Module.lua"))()
Crystal = {}
for i,v in pairs(workspace.mapCrystalsFolder:GetChildren()) do
    table.insert(Crystal,v.Name) 
end
local X = Material.Load({
	Title = "⚡ Ninja Legends 💨 | AppleScript001",
	Style = 2,
	SizeX = 370,
	SizeY = 360,
	Theme = "Dark",
	ColorOverrides = {
		MainFrame = Color3.fromRGB(0,9,55)
	}
})
local W = X.New({
	Title = "Main"
})
W.Toggle({
	Text = "Auto Swing",
	Callback = function(Value)
	_G.Swing = Value
	while _G.Swing do
	task.wait(0.1)
	game:GetService("Players").LocalPlayer:WaitForChild("ninjaEvent"):FireServer("swingKatana")	
end
end,
Enabled = false
})
W.Toggle({
	Text = "Auto Sell x35 Coins",
	Callback = function(Value)
	_G.Sell = Value
	while _G.Sell do
	task.wait(1)
	for _,v in pairs(workspace.sellAreaCircles:GetChildren()[20]:GetDescendants()) do
		if v:IsA("TouchTransmitter") then
		firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 0) --0 is touch
		firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, v.Parent, 1) -- 1 is untouch
end
end
end
end,
Enabled = false
})
W.Toggle({
	Text = "Auto Collect Chi-Coins",
	Callback = function(Value)
	_G.Chi = Value
	while _G.Chi do
	task.wait(1)
	local plr = game.Players.LocalPlayer
	for _,v in pairs(workspace.Hoops:GetDescendants()) do
	if v.ClassName == "MeshPart" then
	v.touchPart.CFrame = plr.Character.HumanoidRootPart.CFrame
end
end
end
end,
Enabled = false
})
W.Button({
	Text = "KOTH",
	Callback = function()
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").kingOfTheHillPart.CFrame
	end,
})
local Cry = X.New({
	Title = "Crystals"
})
local cc = Y.Dropdown({
	Text = "Select | Crystal",
	Callback = function(t)
        Crystals = t
	end,
	Options = Crystal
})
Cry.Button(
    {
        Text = "Refresh/Crystals",
        Callback = function()
            table.clear(Crystal)
            for i, v in pairs(workspace.mapCrystalsFolder:GetDescendants()) do
                    if not table.find(Crystal, tostring(v)) then
                        table.insert(Crystal, tostring(v))
                        cc:SetOptions(Crystal)
                end
            end
        end
    }
)
Cry.Toggle({
	Text = "Auto Buy x1",
	Callback = function(Value)
	_G.Crys = Value
	while _G.Crys do
	task.wait(0.1)
	game:GetService("ReplicatedStorage"):WaitForChild("rEvents"):WaitForChild("openCrystalRemote"):InvokeServer("openCrystal", Crystal)
	
end
end,
Cry.Button({
	Text = "Tp-Checks",
	Callback = function()
		for i,v in pairs(workspace.mapCrystalsFolder[Crystals]:GetDescendants()) do
			if v.Name == "containerNamePart" then
			game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.CFrame
			end
		end
	end,
})
Enabled = false
})
