# Kitty---HUB-
```lua
local player = game.Players.LocalPlayer
local RunService = game:GetService("RunService")

local tp = false
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
main.Position = UDim2.new(0.5,-170,0.5,-250)
main.BackgroundColor3 = Color3.fromRGB(15,15,15)
main.BorderSizePixel = 0
main.ClipsDescendants = true

Instance.new("UICorner",main).CornerRadius = UDim.new(0,28)

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

-- TOPO
local top = Instance.new("Frame")
top.Parent = main
top.Size = UDim2.new(1,0,0,60)
top.BackgroundColor3 = Color3.fromRGB(0,0,0)
top.BorderSizePixel = 0

local topcorner = Instance.new("UICorner",top)
topcorner.CornerRadius = UDim.new(0,28)

-- TITULO
local title = Instance.new("TextLabel")
title.Parent = top
title.Size = UDim2.new(1,0,1,0)
title.BackgroundTransparency = 1
title.Text = "🎀 Hello Kitty Hub 🎀"
title.TextColor3 = Color3.new(1,1,1)
title.TextScaled = true
title.Font = Enum.Font.GothamBold

-- FECHAR
local fechar = Instance.new("TextButton")
fechar.Parent = main
fechar.Size = UDim2.new(0,35,0,35)
fechar.Position = UDim2.new(1,-45,0,12)
fechar.BackgroundColor3 = Color3.fromRGB(255,20,147)
fechar.Text = "X"
fechar.TextScaled = true
fechar.TextColor3 = Color3.new(1,1,1)
fechar.Font = Enum.Font.GothamBold
fechar.BorderSizePixel = 0

Instance.new("UICorner",fechar).CornerRadius = UDim.new(1,0)

-- ABRIR
local abrir = Instance.new("ImageButton")
abrir.Parent = gui
abrir.Visible = false
abrir.Size = UDim2.new(0,70,0,70)
abrir.Position = UDim2.new(0,15,0.5,-35)
abrir.BackgroundTransparency = 1
abrir.Image = "rbxassetid://11735687651"

-- KITTY
local kitty = Instance.new("ImageLabel")
kitty.Parent = main
kitty.Size = UDim2.new(0,110,0,110)
kitty.Position = UDim2.new(0.5,-55,0,75)
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

-- BOTÃO
local function criarBotao(texto,y)

	local b = Instance.new("TextButton")
	b.Parent = scroll
	b.Size = UDim2.new(0,250,0,45)
	b.Position = UDim2.new(0.5,-125,0,y)
	b.BackgroundColor3 = Color3.fromRGB(0,0,0)
	b.TextColor3 = Color3.new(1,1,1)
	b.TextScaled = true
	b.Font = Enum.Font.GothamBold
	b.Text = texto
	b.BorderSizePixel = 0

	Instance.new("UICorner",b).CornerRadius = UDim.new(0,14)

	local s = Instance.new("UIStroke")
	s.Parent = b
	s.Color = Color3.fromRGB(255,105,180)
	s.Thickness = 2

	return b
end

local tpBtn = criarBotao("TP OFF",0)
local flyBtn = criarBotao("FLY OFF",60)
local noclipBtn = criarBotao("NOCLIP OFF",120)

-- INPUTS
local function criarInput(txt,pos)

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

	Instance.new("UICorner",box).CornerRadius = UDim.new(0,10)

	local s = Instance.new("UIStroke")
	s.Parent = box
	s.Color = Color3.fromRGB(255,105,180)

	return box
end

local boxX = criarInput("X",-120)
local boxY = criarInput("Y",-35)
local boxZ = criarInput("Z",50)

boxX.Text = tostring(pos2.X)
boxY.Text = tostring(pos2.Y)
boxZ.Text = tostring(pos2.Z)

local apply = criarBotao("APLICAR",260)

-- INSTA
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

-- FECHAR / ABRIR
fechar.MouseButton1Click:Connect(function()

	main.Visible = false
	abrir.Visible = true
end)

abrir.MouseButton1Click:Connect(function()

	main.Visible = true
	abrir.Visible = false
end)

-- TP
tpBtn.MouseButton1Click:Connect(function()

	tp = not tp

	if tp then
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

		if tp then

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
```
