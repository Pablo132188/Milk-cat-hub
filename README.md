-- Halloween Hub 2026 - Versão Simples
print("🎃 Iniciando Halloween Hub 2026...")

-- Esperar o jogo carregar
task.wait(2)

-- Criar interface básica
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "HalloweenHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Criar Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 400, 0, 300)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
title.Text = "🎃 Halloween Hub 2026"
title.TextColor3 = Color3.fromRGB(255, 170, 0)
title.TextSize = 20
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

-- Botão Fechar
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 30, 0, 30)
closeBtn.Position = UDim2.new(1, -35, 0, 5)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.Parent = mainFrame

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- Função para criar toggle
local function createToggle(parent, text, yPos, default)
    local toggleFrame = Instance.new("Frame")
    toggleFrame.Size = UDim2.new(1, -20, 0, 35)
    toggleFrame.Position = UDim2.new(0, 10, 0, yPos)
    toggleFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
    toggleFrame.Parent = parent
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0, 200, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = toggleFrame
    
    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0, 50, 0, 25)
    toggleBtn.Position = UDim2.new(1, -60, 0, 5)
    toggleBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    toggleBtn.Text = "OFF"
    toggleBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggleBtn.TextSize = 12
    toggleBtn.Font = Enum.Font.GothamBold
    toggleBtn.Parent = toggleFrame
    
    local enabled = default or false
    if enabled then
        toggleBtn.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
        toggleBtn.Text = "ON"
    end
    
    toggleBtn.MouseButton1Click:Connect(function()
        enabled = not enabled
        if enabled then
            toggleBtn.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
            toggleBtn.Text = "ON"
        else
            toggleBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
            toggleBtn.Text = "OFF"
        end
    end)
    
    return toggleBtn
end

-- Função para criar botão
local function createButton(parent, text, yPos, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 35)
    btn.Position = UDim2.new(0, 10, 0, yPos)
    btn.BackgroundColor3 = Color3.fromRGB(70, 70, 90)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 14
    btn.Font = Enum.Font.Gotham
    btn.Parent = parent
    
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- Criar toggles
createToggle(mainFrame, "Farm Halloween", 50, true)
createToggle(mainFrame, "Coletar Candy Corn", 90, true)
createToggle(mainFrame, "Farm Hell Rider", 130, true)
createToggle(mainFrame, "Farm Jack-O-Lanterns", 170, true)
createToggle(mainFrame, "Anti-Afk", 210, true)

-- Botões de teleporte
createButton(mainFrame, "🌊 Teleportar Sea 1", 250, function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(500, 50, 500)
    end
end)

print("✅ Menu criado com sucesso!")
