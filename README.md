-- // CONFIGURAÇÃO INICIAL
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.ResetOnSpawn = false

-- // BOTÃO FLUTUANTE
local btn = Instance.new("TextButton", gui)
btn.Size = UDim2.new(0, 120, 0, 45)
btn.Position = UDim2.new(0.05, 0, 0.35, 0)
btn.BackgroundColor3 = Color3.fromRGB(0, 120, 255)
btn.Text = "Menu"
btn.TextColor3 = Color3.new(1,1,1)
btn.Font = Enum.Font.GothamBold
btn.TextSize = 18
btn.Active = true
btn.Draggable = true

-- // PAINEL PRINCIPAL
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 250, 0, 200)
frame.Position = UDim2.new(0.2, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.Visible = false
frame.BorderSizePixel = 0
frame.Active = true

-- Arredondar cantos
Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 10)

-- // TÍTULO DO PAINEL
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, -60, 0, 40)
title.Position = UDim2.new(0, 10, 0, 0)
title.Text = "Teleporte Pro"
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextSize = 20
title.TextXAlignment = Enum.TextXAlignment.Left

-- // BOTÃO FECHAR
local close = Instance.new("TextButton", frame)
close.Size = UDim2.new(0, 40, 0, 40)
close.Position = UDim2.new(1, -45, 0, 0)
close.Text = "X"
close.TextColor3 = Color3.new(1,0.3,0.3)
close.BackgroundTransparency = 1
close.Font = Enum.Font.GothamBold
close.TextSize = 24

-- // BOTÃO MINIMIZAR
local mini = Instance.new("TextButton", frame)
mini.Size = UDim2.new(0, 40, 0, 40)
mini.Position = UDim2.new(1, -90, 0, 0)
mini.Text = "-"
mini.TextColor3 = Color3.new(1,1,1)
mini.BackgroundTransparency = 1
mini.Font = Enum.Font.GothamBold
mini.TextSize = 34

-- // BOTÃO MARCAR POSIÇÃO
local marcar = Instance.new("TextButton", frame)
marcar.Size = UDim2.new(1, -20, 0, 60)
marcar.Position = UDim2.new(0, 10, 0, 50)
marcar.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
marcar.TextColor3 = Color3.new(1,1,1)
marcar.Font = Enum.Font.GothamBold
marcar.TextSize = 20
marcar.Text = "Marcar posição"
Instance.new("UICorner", marcar).CornerRadius = UDim.new(0, 8)

-- // BOTÃO TELEPORTAR
local teleportar = Instance.new("TextButton", frame)
teleportar.Size = UDim2.new(1, -20, 0, 60)
teleportar.Position = UDim2.new(0, 10, 0, 120)
teleportar.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
teleportar.TextColor3 = Color3.new(1,1,1)
teleportar.Font = Enum.Font.GothamBold
teleportar.TextSize = 20
teleportar.Text = "Teleportar"
Instance.new("UICorner", teleportar).CornerRadius = UDim.new(0, 8)

-- // VARIÁVEL DA POSIÇÃO
local posicaoSalva = nil

-- // MOSTRAR PAINEL
btn.MouseButton1Click:Connect(function()
	frame.Visible = not frame.Visible
end)

-- // FECHAR
close.MouseButton1Click:Connect(function()
	frame.Visible = false
end)

-- // MINIMIZAR
local minimizado = false
mini.MouseButton1Click:Connect(function()
	minimizado = not minimizado
	if minimizado then
		marcar.Visible = false
		teleportar.Visible = false
		frame.Size = UDim2.new(0, 250, 0, 40)
	else
		marcar.Visible = true
		teleportar.Visible = true
		frame.Size = UDim2.new(0, 250, 0, 200)
	end
end)

-- // MARCAR POSIÇÃO
marcar.MouseButton1Click:Connect(function()
	local char = player.Character
	if char and char:FindFirstChild("HumanoidRootPart") then
		posicaoSalva = char.HumanoidRootPart.CFrame
		marcar.Text = "Posição marcada!"
		task.wait(1)
		marcar.Text = "Marcar posição"
	end
end)

-- // TELEPORTAR
teleportar.MouseButton1Click:Connect(function()
	if posicaoSalva then
		local char = player.Character
		if char and char:FindFirstChild("HumanoidRootPart") then
			char.HumanoidRootPart.CFrame = posicaoSalva
		end
	end
end) 

