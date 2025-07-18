-- Serviços
local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")
local RunService = game:GetService("RunService")

local localPlayer = Players.LocalPlayer

-- Função para mostrar a mensagem no canto inferior direito
local function showMessage(text)
	local screenGui = Instance.new("ScreenGui")
	screenGui.Name = "ESP_MessageGui"
	screenGui.ResetOnSpawn = false
	screenGui.Parent = game:GetService("CoreGui")

	local label = Instance.new("TextLabel")
	label.Size = UDim2.new(0, 300, 0, 40)
	label.Position = UDim2.new(1, -310, 1, -50) -- canto inferior direito
	label.BackgroundTransparency = 0.3
	label.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	label.BorderSizePixel = 0
	label.TextColor3 = Color3.fromRGB(255, 255, 255)
	label.Font = Enum.Font.SourceSansBold
	label.TextScaled = true
	label.Text = text
	label.Parent = screenGui

	-- Remover a mensagem após 5 segundos
	task.delay(5, function()
		screenGui:Destroy()
	end)
end

-- Função para aplicar ESP a um jogador
local function applyESP(player)
	if player ~= localPlayer then
		local char = player.Character
		if char and char:FindFirstChild("HumanoidRootPart") then
			local highlight = Instance.new("Highlight")
			highlight.Name = "ESP_Highlight"
			highlight.FillTransparency = 1
			highlight.OutlineTransparency = 0
			highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
			highlight.Adornee = char
			highlight.Parent = char

			-- Remover o Highlight após 10 segundos
			task.delay(10, function()
				if highlight and highlight.Parent then
					highlight:Destroy()
				end
			end)
		end
	end
end

-- Aplicar ESP a todos os jogadores no jogo
for _, player in ipairs(Players:GetPlayers()) do
	applyESP(player)
end

-- Mostrar a mensagem de confirmação
showMessage("Esp executado")
