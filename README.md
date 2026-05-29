local player = game.Players.LocalPlayer
local RunService = game:GetService("RunService")

local ativoTP = false
local fly = false
local noclip = false

local pos1 = Vector3.new(220,47,51)
local pos2 = Vector3.new(-37,19,51)

-- GUI
local gui = Instance.new("ScreenGui")
gui.Parent = game.CoreGui
gui.ResetOnSpawn = false

-- MAIN
local main = Instance.new("Frame")
main.Parent = gui
main.Size = UDim2.new(0,340,0,500)
main.Position = UDim2.new(0,20,0.5,-250)
main.BackgroundColor3 = Color3.fromRGB(20,20,20)
main.BorderSizePixel = 0
main.ClipsDescendants = true

Instance.new("UICorner", main).CornerRadius = UDim.new(0,28)

-- RGB
local stroke = Instance.new("UIStroke")
stroke.Parent = main
stroke.Thickness = 3

task.spawn(function()
	local hue = 0
	
	while true do
		
		stroke.Color = Color3.fromHSV(hue,1,1)
		
		hue += 0.002
		
		if hue >= 1 then
			hue = 0
		end
		
		task.wait()
	end
end)

-- FUNDO
local fundo = Instance.new("ImageLabel")
fundo.Parent = main
fundo.Size = UDim2.new(1,0,1,0)
fundo.BackgroundTransparency = 1
fundo.Image = "rbxassetid://11351620343"
fundo.ImageTransparency = 0.35
fundo.ScaleType = Enum.ScaleType.Crop

-- ESCURECER
local blur = Instance.new("Frame")
blur.Parent = main
blur.Size = UDim2.new(1,0,1,0)
blur.BackgroundColor3 = Color3.new(0,0,0)
blur.BackgroundTransparency = 0.35
blur.BorderSizePixel = 0

-- TOPO
local top = Instance.new("Frame")
top.Parent = main
top.Size = UDim2.new(1,0,0,60)
top.BackgroundColor3 = Color3.fromRGB(0,0,0)
top.BorderSizePixel = 0

Instance.new("UICorner", top).CornerRadius = UDim.new(0,28)

-- TITULO
local title = Instance.new("TextLabel")
title.Parent = top
title.Size = UDim2.new(1,0,1,0)
title.BackgroundTransparency = 1
title.Text = "🎀 Hello Kitty Hub 🎀"
title.TextColor3 = Color3.new(1,1,1)
title.TextScaled = true
title.Font = Enum.Font.GothamBold

-- HELLO KITTY
local kitty = Instance.new("ImageLabel")
kitty.Parent = main
kitty.Size = UDim2.new(0,110,0,110)
kitty.Position = UDim2.new(0.5,-55,0,70)
kitty.BackgroundTransparency = 1
kitty.Image = "rbxassetid://11735687651"

task.spawn(function()
	while true do
		
		kitty.Position = kitty.Position + UDim2.new(0,0,0,-0.01)
		task.wait(0.5)
		kitty.Position = kitty.Position + UDim2.new(0,0,0,0.01)
		task.wait(0.5)
	end
end)

-- SCROLL
local scroll = Instance.new("ScrollingFrame")
scroll.Parent = main
scroll.Size = UDim2.new(1,0,1,-190)
scroll.Position = UDim2.new(0,0,0,190)
scroll.BackgroundTransparency = 1
scroll.BorderSizePixel = 0
scroll.CanvasSize = UDim2.new(0,0,0,600)
scroll.ScrollBarThickness = 4

-- botão
local function createButton(text,y)

	local b = Instance.new("TextButton")
	b.Parent = scroll
	b.Size = UDim2.new(0,250,0,45)
	b.Position = UDim2.new(0.5,-125,0,y)
	b.BackgroundColor3 = Color3.fromRGB(0,0,0)
	b.TextColor3 = Color3.new(1,1,1)
	b.TextScaled = true
	b.Font = Enum.Font.GothamBold
	b.Text = text
	b.BorderSizePixel = 0
	
	Instance.new("UICorner", b).CornerRadius = UDim.new(0,14)
	
	local s = Instance.new("UIStroke")
	s.Parent = b
	s.Color = Color3.fromRGB(255,105,180)
	s.Thickness = 2
	
	return b
end

local tpBtn = createButton("TP OFF",0)
local flyBtn = createButton("FLY OFF",60)
local noclipBtn = createButton("NOCLIP OFF",120)

-- COORDENADAS
local function createBox(txt,pos)

	local box = Instance.new("TextBox")
	box.Parent = scroll
	box.Size = UDim2.new(0,70,0,35)
	box.Position = UDim2.new(0.5,pos,0,200)
	box.BackgroundColor3 = Color3.fromRGB(0,0,0)
	box.TextColor3 = Color3.new(1,1,1)
	box.TextScaled = true
	box.Font = Enum.Font.GothamBold
	box.PlaceholderText = txt
	box.BorderSizePixel = 0
	
	Instance.new("UICorner", box).CornerRadius = UDim.new(0,10)
	
	local s = Instance.new("UIStroke")
	s.Parent = box
	s.Color = Color3.fromRGB(255,105,180)
	
	return box
end

local boxX = createBox("X",-120)
local boxY = createBox("Y",-35)
local boxZ = createBox("Z",50)

boxX.Text = tostring(pos2.X)
boxY.Text = tostring(pos2.Y)
boxZ.Text = tostring(pos2.Z)

local apply = createButton("APLICAR",260)

-- FECHAR
local close = Instance.new("TextButton")
close.Parent = main
close.Size = UDim2.new(0,35,0,35)
close.Position = UDim2.new(1,-45,0,10)
close.BackgroundColor3 = Color3.fromRGB(255,20,147)
close.Text = "X"
close.TextColor3 = Color3.new(1,1,1)
close.TextScaled = true
close.Font = Enum.Font.GothamBold
close.BorderSizePixel = 0

Instance.new("UICorner", close).CornerRadius = UDim.new(1,0)

-- ABRIR
local open = Instance.new("ImageButton")
open.Parent = gui
open.Visible = false
open.Size = UDim2.new(0,70,0,70)
open.Position = UDim2.new(0,10,0.5,-35)
open.BackgroundTransparency = 1
open.Image = "rbxassetid://11735687651"

close.MouseButton1Click:Connect(function()
	main.Visible = false
	open.Visible = true
end)

open.MouseButton1Click:Connect(function()
	main.Visible = true
	open.Visible = false
end)

-- insta
local insta = Instance.new("TextLabel")
insta.Parent = gui
insta.Size = UDim2.new(0,220,0,30)
insta.Position = UDim2.new(1,-230,1,40)
insta.BackgroundTransparency = 1
insta.Text = "@larahdelreys"
insta.TextColor3 = Color3.new(1,1,1)
insta.TextScaled = true
insta.Font = Enum.Font.GothamBold

task.spawn(function()
	for i = 40,-10,-1 do
		
		insta.Position = UDim2.new(1,-230,1,i)
		
		task.wait(0.01)
	end
end)

-- TP
tpBtn.MouseButton1Click:Connect(function()

	ativoTP = not ativoTP
	
	if ativoTP then
		tpBtn.Text = "TP ON"
		tpBtn.BackgroundColor3 = Color3.fromRGB(255,20,147)
	else
		tpBtn.Text = "TP OFF"
		tpBtn.BackgroundColor3 = Color3.fromRGB(0,0,0)
	end
end)

apply.MouseButton1Click:Connect(function()

	pos2 = Vector3.new(
		tonumber(boxX.Text) or pos2.X,
		tonumber(boxY.Text) or pos2.Y,
		tonumber(boxZ.Text) or pos2.Z
	)
end)

task.spawn(function()

	while true do
		
		if ativoTP then
			
			local char = player.Character
			
			if char and char:FindFirstChild("HumanoidRootPart") then
				
				local hrp = char.HumanoidRootPart
				
				hrp.CFrame = CFrame.new(pos1)
				task.wait(1)
				
				hrp.CFrame = CFrame.new(pos2)
				task.wait(1)
			end
		end
		
		task.wait()
	end
end)

-- FLY
flyBtn.MouseButton1Click:Connect(function()

	fly = not fly
	
	if fly then
		flyBtn.Text = "FLY ON"
		flyBtn.BackgroundColor3 = Color3.fromRGB(255,20,147)
	else
		flyBtn.Text = "FLY OFF"
		flyBtn.BackgroundColor3 = Color3.fromRGB(0,0,0)
	end
end)

RunService.RenderStepped:Connect(function()

	if fly then
		
		local char = player.Character
		
		if char and char:FindFirstChild("HumanoidRootPart") then
			
			char.HumanoidRootPart.Velocity = Vector3.new(0,50,0)
		end
	end
end)

-- NOCLIP
noclipBtn.MouseButton1Click:Connect(function()

	noclip = not noclip
	
	if noclip then
		noclipBtn.Text = "NOCLIP ON"
		noclipBtn.BackgroundColor3 = Color3.fromRGB(255,20,147)
	else
		noclipBtn.Text = "NOCLIP OFF"
		noclipBtn.BackgroundColor3 = Color3.fromRGB(0,0,0)
	end
end)

RunService.Stepped:Connect(function()

	if noclip then
		
		local char = player.Character
		
		if char then
			
			for _,v in pairs(char:GetDescendants()) do
				
				if v:IsA("BasePart") then
					v.CanCollide = false
				end
			end
		end
	end
end)
