-- Zeldris Hub v1.0.0.0

-- Tela de carregamento
local loadingGui = Instance.new("ScreenGui", game.CoreGui)
loadingGui.Name = "ZeldrisLoading"
loadingGui.ResetOnSpawn = false

local bg = Instance.new("Frame", loadingGui)
bg.Size = UDim2.new(1, 0, 1, 0)
bg.BackgroundColor3 = Color3.fromRGB(0, 0, 0)

local logo = Instance.new("ImageLabel", bg)
logo.Size = UDim2.new(0, 300, 0, 300)
logo.Position = UDim2.new(0.5, -150, 0.5, -150)
logo.BackgroundTransparency = 1
logo.Image = "rbxassetid://112133974686847"

wait(2)
for i = 0, 1, 0.05 do
	bg.BackgroundTransparency = i
	logo.ImageTransparency = i
	wait(0.05)
end
loadingGui:Destroy()

-- Evita duplicatas
if game.CoreGui:FindFirstChild("ZeldrisHub") then
	game.CoreGui.ZeldrisHub:Destroy()
end

local player = game.Players.LocalPlayer
local players = game.Players

-- UI Principal
local screenGui = Instance.new("ScreenGui", game.CoreGui)
screenGui.Name = "ZeldrisHub"
screenGui.ResetOnSpawn = false

-- Toggle
local toggle = Instance.new("TextButton", screenGui)
toggle.Size = UDim2.new(0, 40, 0, 40)
toggle.Position = UDim2.new(0, 10, 0.5, -20)
toggle.Text = "+"
toggle.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
toggle.Font = Enum.Font.SourceSansBold
toggle.TextSize = 24
toggle.Draggable = true
Instance.new("UICorner", toggle)

-- Hub
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 400, 0, 450)
frame.Position = UDim2.new(0.3, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.Active = true
frame.Visible = false
frame.Draggable = true
Instance.new("UICorner", frame)

-- Barra de navegação
local navBar = Instance.new("Frame", frame)
navBar.Size = UDim2.new(1, 0, 0, 40)
navBar.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Instance.new("UICorner", navBar)

local line = Instance.new("Frame", navBar)
line.Size = UDim2.new(0, 40, 0, 4)
line.Position = UDim2.new(0, 10, 1, -4)
line.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", line)

local function createIconButton(parent, imageId, position, callback)
	local btn = Instance.new("ImageButton", parent)
	btn.Size = UDim2.new(0, 30, 0, 30)
	btn.Position = position
	btn.BackgroundTransparency = 1
	btn.Image = imageId
	btn.MouseButton1Click:Connect(callback)
	return btn
end

local homeBtn = createIconButton(navBar, "rbxassetid://6031094670", UDim2.new(0, 10, 0, 5), function()
	line:TweenPosition(UDim2.new(0, 10, 1, -4), "Out", "Sine", 0.2, true)
	scrolling.Visible = true
	settingsFrame.Visible = false
end)

local gearBtn = createIconButton(navBar, "rbxassetid://6031280882", UDim2.new(0, 50, 0, 5), function()
	line:TweenPosition(UDim2.new(0, 50, 1, -4), "Out", "Sine", 0.2, true)
	scrolling.Visible = false
	settingsFrame.Visible = true
end)

-- Conteúdo Home
local scrolling = Instance.new("ScrollingFrame", frame)
scrolling.Size = UDim2.new(1, -20, 1, -60)
scrolling.Position = UDim2.new(0, 10, 0, 50)
scrolling.CanvasSize = UDim2.new(0, 0, 0, 0)
scrolling.ScrollBarThickness = 6
scrolling.BackgroundTransparency = 1
scrolling.AutomaticCanvasSize = Enum.AutomaticSize.Y

local layout = Instance.new("UIListLayout", scrolling)
layout.Padding = UDim.new(0, 10)
layout.SortOrder = Enum.SortOrder.LayoutOrder

-- Campo animado
local function createButtonWithInput(label, placeholder, callback)
	local container = Instance.new("Frame")
	container.Size = UDim2.new(1, 0, 0, 40)
	container.BackgroundTransparency = 1
	container.LayoutOrder = 1
	container.ClipsDescendants = true

	local button = Instance.new("TextButton", container)
	button.Size = UDim2.new(1, 0, 0, 40)
	button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	button.Text = label
	button.TextColor3 = Color3.fromRGB(255, 255, 255)
	button.Font = Enum.Font.SourceSansBold
	button.TextSize = 18
	Instance.new("UICorner", button)

	local inputBox = Instance.new("TextBox", container)
	inputBox.Size = UDim2.new(1, 0, 0, 40)
	inputBox.Position = UDim2.new(0, 0, 0, 40)
	inputBox.PlaceholderText = placeholder
	inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
	inputBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	inputBox.Font = Enum.Font.SourceSans
	inputBox.TextSize = 18
	inputBox.Visible = false
	Instance.new("UICorner", inputBox)

	local expanded = false
	button.MouseButton1Click:Connect(function()
		if not expanded then
			inputBox.Visible = true
			container:TweenSize(UDim2.new(1, 0, 0, 90), "Out", "Sine", 0.25, true)
			wait(0.25)
			inputBox:CaptureFocus()
			expanded = true
		else
			container:TweenSize(UDim2.new(1, 0, 0, 40), "Out", "Sine", 0.25, true)
			wait(0.25)
			inputBox.Visible = false
			expanded = false
		end
	end)

	inputBox.FocusLost:Connect(function(enter)
		if enter and inputBox.Text ~= "" then
			callback(inputBox.Text)
			container:TweenSize(UDim2.new(1, 0, 0, 40), "Out", "Sine", 0.25, true)
			wait(0.25)
			inputBox.Visible = false
			expanded = false
		end
	end)

	container.Parent = scrolling
end

createButtonWithInput("Teleport", "Nome do jogador", function(text)
	local target = players:FindFirstChild(text)
	if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
		player.Character:MoveTo(target.Character.HumanoidRootPart.Position)
	end
end)

createButtonWithInput("Bring", "Nome do jogador", function(text)
	local target = players:FindFirstChild(text)
	if target and target.Character and player.Character and player.Character.PrimaryPart then
		target.Character:SetPrimaryPartCFrame(player.Character.PrimaryPart.CFrame + Vector3.new(2, 0, 0))
	end
end)

createButtonWithInput("Kill", "Nome do jogador", function(text)
	local target = players:FindFirstChild(text)
	if target and target.Character and target.Character:FindFirstChild("Humanoid") then
		target.Character.Humanoid.Health = 0
	end
end)

createButtonWithInput("Roupa", "ID da roupa", function(id)
	pcall(function()
		local asset = game:GetService("InsertService"):LoadAsset(tonumber(id))
		for _, v in pairs(asset:GetDescendants()) do
			if v:IsA("Accessory") or v:IsA("Clothing") then
				v.Parent = player.Character
			end
		end
		asset:Destroy()
	end)
end)

-- Infinite Yield
local infYBtn = Instance.new("TextButton", scrolling)
infYBtn.Size = UDim2.new(1, 0, 0, 40)
infYBtn.Text = "Abrir Infinite Yield"
infYBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 90)
infYBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
infYBtn.Font = Enum.Font.SourceSansBold
infYBtn.TextSize = 18
Instance.new("UICorner", infYBtn)

infYBtn.MouseButton1Click:Connect(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
end)
infYBtn.Parent = scrolling

-- Aba Configurações
local settingsFrame = Instance.new("Frame", frame)
settingsFrame.Size = UDim2.new(1, -20, 1, -60)
settingsFrame.Position = UDim2.new(0, 10, 0, 50)
settingsFrame.BackgroundTransparency = 1
settingsFrame.Visible = false

local colorInput = Instance.new("TextBox", settingsFrame)
colorInput.Size = UDim2.new(1, 0, 0, 40)
colorInput.PlaceholderText = "Digite a cor em RGB. Ex: 255,0,0"
colorInput.TextColor3 = Color3.fromRGB(255, 255, 255)
colorInput.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
colorInput.Font = Enum.Font.SourceSans
colorInput.TextSize = 18
Instance.new("UICorner", colorInput)

colorInput.FocusLost:Connect(function(enter)
	if enter then
		local r, g, b = colorInput.Text:match("(%d+),(%d+),(%d+)")
		if r and g and b then
			frame.BackgroundColor3 = Color3.fromRGB(tonumber(r), tonumber(g), tonumber(b))
		end
	end
end)

-- Toggle
toggle.MouseButton1Click:Connect(function()
	frame.Visible = not frame.Visible
	toggle.Text = frame.Visible and "-" or "+"
end)
