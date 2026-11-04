-- Halloween Hub 2026 - Versão Completa Melhorada
print("🎃 Iniciando Halloween Hub 2026...")

-- Esperar o jogo carregar
task.wait(2)

-- Config Global
getgenv().Config = {
    ["StartFarm"] = true,
    ["Halloween"] = {
        ["Enabled"] = true,
        ["AutoCollectCandy"] = true,
        ["AutoKillHellRider"] = true,
        ["AutoFarmJackOLanterns"] = true,
        ["AutoOpenSpookyGacha"] = true,
        ["AutoTrickOrTreat"] = true,
    },
    ["SeaEvents"] = {
        ["Enabled"] = true,
        ["AutoHuntShip"] = true,
        ["AutoHuntKraken"] = true,
        ["AutoHuntSeaBeast"] = true,
        ["AutoHuntTerrorShark"] = true,
        ["AutoHuntMermaid"] = true,
    },
    ["Fruit"] = {
        ["AutoFarmSpawnedFruit"] = true,
        ["AutoSpinFruit"] = true,
        ["AutoStoreFruit"] = true,
    },
    ["Farm"] = {
        ["AutoQuest"] = true,
        ["AutoFarmMobs"] = true,
        ["AutoFarmBoss"] = true,
        ["AutoFarmLevel"] = true,
        ["AutoFarmMoney"] = true,
    },
    ["Settings"] = {
        ["FPSBooster"] = true,
        ["AntiAfk"] = true,
        ["AutoHop"] = true,
    },
}

-- Criar interface
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Limpar GUI anterior
if playerGui:FindFirstChild("HalloweenHub") then
    playerGui:FindFirstChild("HalloweenHub"):Destroy()
end

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "HalloweenHub"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = playerGui

-- Criar Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 600, 0, 500)
mainFrame.Position = UDim2.new(0.5, -300, 0.5, -250)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 35)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Barra de Título
local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 50)
titleBar.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -80, 1, 0)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "🎃 Halloween Hub 2026"
title.TextColor3 = Color3.fromRGB(255, 170, 0)
title.TextSize = 22
title.Font = Enum.Font.GothamBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = titleBar

-- Botão Fechar
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 35, 0, 35)
closeBtn.Position = UDim2.new(1, -40, 0, 7)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeBtn.BackgroundTransparency = 0.2
closeBtn.Text = "✕"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.TextSize = 18
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Parent = titleBar

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- Botão Minimizar
local minBtn = Instance.new("TextButton")
minBtn.Size = UDim2.new(0, 35, 0, 35)
minBtn.Position = UDim2.new(1, -80, 0, 7)
minBtn.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
minBtn.BackgroundTransparency = 0.2
minBtn.Text = "—"
minBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
minBtn.TextSize = 18
minBtn.Font = Enum.Font.GothamBold
minBtn.Parent = titleBar

minBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

-- Criar Abas
local tabsFrame = Instance.new("Frame")
tabsFrame.Size = UDim2.new(1, 0, 0, 50)
tabsFrame.Position = UDim2.new(0, 0, 0, 50)
tabsFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 50)
tabsFrame.BorderSizePixel = 0
tabsFrame.Parent = mainFrame

-- Container de Conteúdo
local contentFrame = Instance.new("Frame")
contentFrame.Size = UDim2.new(1, -20, 1, -120)
contentFrame.Position = UDim2.new(0, 10, 0, 110)
contentFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 30)
contentFrame.BorderSizePixel = 0
contentFrame.Parent = mainFrame

-- Sistema de Abas
local tabs = {}
local tabButtons = {}

local function createTab(name, icon, color)
    local tabBtn = Instance.new("TextButton")
    tabBtn.Size = UDim2.new(0, 90, 0, 40)
    tabBtn.Position = UDim2.new(0, (#tabButtons * 95) + 5, 0, 5)
    tabBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
    tabBtn.BackgroundTransparency = 0.3
    tabBtn.Text = icon .. " " .. name
    tabBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    tabBtn.TextSize = 14
    tabBtn.Font = Enum.Font.GothamBold
    tabBtn.Parent = tabsFrame
    
    local tabContent = Instance.new("ScrollingFrame")
    tabContent.Size = UDim2.new(1, 0, 1, 0)
    tabContent.BackgroundTransparency = 1
    tabContent.Visible = false
    tabContent.ScrollBarThickness = 5
    tabContent.CanvasSize = UDim2.new(0, 0, 0, 0)
    tabContent.AutomaticCanvasSize = Enum.AutomaticSize.Y
    tabContent.Parent = contentFrame
    
    table.insert(tabs, {button = tabBtn, content = tabContent, name = name, color = color})
    table.insert(tabButtons, tabBtn)
    
    tabBtn.MouseButton1Click:Connect(function()
        for _, tab in ipairs(tabs) do
            tab.content.Visible = false
            tab.button.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        end
        tabContent.Visible = true
        tabBtn.BackgroundColor3 = color
    end)
    
    return tabContent
end

-- Função para criar toggle melhorado
local function createToggle(parent, text, default, callback)
    local toggleFrame = Instance.new("Frame")
    toggleFrame.Size = UDim2.new(1, -20, 0, 45)
    toggleFrame.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 50)
    toggleFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    toggleFrame.BackgroundTransparency = 0.2
    toggleFrame.BorderSizePixel = 0
    toggleFrame.Parent = parent
    
    -- Borda esquerda colorida
    local border = Instance.new("Frame")
    border.Size = UDim2.new(0, 4, 1, 0)
    border.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
    border.BorderSizePixel = 0
    border.Parent = toggleFrame
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0, 200, 1, 0)
    label.Position = UDim2.new(0, 15, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = toggleFrame
    
    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0, 60, 0, 30)
    toggleBtn.Position = UDim2.new(1, -70, 0, 7)
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
        if callback then callback(enabled) end
    end)
    
    return toggleBtn
end

-- Função para criar botão melhorado
local function createButton(parent, text, callback, color)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 45)
    btn.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 50)
    btn.BackgroundColor3 = color or Color3.fromRGB(60, 60, 80)
    btn.BackgroundTransparency = 0.2
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 14
    btn.Font = Enum.Font.GothamBold
    btn.Parent = parent
    
    btn.MouseButton1Click:Connect(function()
        btn.BackgroundColor3 = Color3.fromRGB(100, 100, 120)
        task.wait(0.1)
        btn.BackgroundColor3 = color or Color3.fromRGB(60, 60, 80)
        callback()
    end)
    
    return btn
end

-- Função para criar label
local function createLabel(parent, text, color)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -20, 0, 35)
    label.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 40)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = color or Color3.fromRGB(255, 170, 0)
    label.TextSize = 16
    label.Font = Enum.Font.GothamBold
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = parent
    return label
end

-- Função para criar dropdown
local function createDropdown(parent, text, options, default, callback)
    local dropFrame = Instance.new("Frame")
    dropFrame.Size = UDim2.new(1, -20, 0, 45)
    dropFrame.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 50)
    dropFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    dropFrame.BorderSizePixel = 0
    dropFrame.Parent = parent
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0, 150, 1, 0)
    label.Position = UDim2.new(0, 15, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = dropFrame
    
    local dropBtn = Instance.new("TextButton")
    dropBtn.Size = UDim2.new(0, 120, 0, 30)
    dropBtn.Position = UDim2.new(1, -130, 0, 7)
    dropBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 80)
    dropBtn.Text = default or options[1] or "Selecionar"
    dropBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    dropBtn.TextSize = 12
    dropBtn.Font = Enum.Font.Gotham
    dropBtn.Parent = dropFrame
    
    local index = 1
    dropBtn.MouseButton1Click:Connect(function()
        index = index % #options + 1
        dropBtn.Text = options[index]
        if callback then callback(options[index]) end
    end)
    
    return dropBtn
end

-- Criar Abas
local mainTab = createTab("Principal", "🏠", Color3.fromRGB(255, 170, 0))
local halloweenTab = createTab("Halloween", "🎃", Color3.fromRGB(255, 100, 0))
local seaTab = createTab("Sea", "🌊", Color3.fromRGB(0, 150, 255))
local fruitTab = createTab("Frutas", "🍎", Color3.fromRGB(255, 50, 50))
local farmTab = createTab("Farm", "⚔️", Color3.fromRGB(150, 255, 50))
local settingsTab = createTab("Config", "⚙️", Color3.fromRGB(200, 200, 200))

-- Aba Principal
createLabel(mainTab, "🏠 Controles Principais")
createToggle(mainTab, "Iniciar Farm", true, function(value)
    getgenv().Config.StartFarm = value
end)

createLabel(mainTab, "📍 Teleports")
createButton(mainTab, "🌊 Sea 1 - Ilha Central", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(500, 50, 500) end
end, Color3.fromRGB(0, 150, 255))

createButton(mainTab, "🌊 Sea 2 - Frente Café", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-2000, 50, 1000) end
end, Color3.fromRGB(0, 150, 255))

createButton(mainTab, "🌊 Sea 3 - Mansão", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(3000, 50, -2000) end
end, Color3.fromRGB(0, 150, 255))

createLabel(mainTab, "⚡ Status")
createButton(mainTab, "📊 Ver Nível", function()
    local level = player.Data.Level.Value
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "Nível",
        Text = "Seu nível é: " .. tostring(level),
        Duration = 3
    })
end, Color3.fromRGB(100, 200, 100))

-- Aba Halloween
createLabel(halloweenTab, "🎃 Halloween 2026")
createToggle(halloweenTab, "Farm Halloween", true, function(value)
    getgenv().Config.Halloween.Enabled = value
end)

createToggle(halloweenTab, "Coletar Candy Corn", true, function(value)
    getgenv().Config.Halloween.AutoCollectCandy = value
end)

createToggle(halloweenTab, "Farm Hell Rider", true, function(value)
    getgenv().Config.Halloween.AutoKillHellRider = value
end)

createToggle(halloweenTab, "Farm Jack-O-Lanterns", true, function(value)
    getgenv().Config.Halloween.AutoFarmJackOLanterns = value
end)

createToggle(halloweenTab, "Abrir Spooky Gacha", true, function(value)
    getgenv().Config.Halloween.AutoOpenSpookyGacha = value
end)

createToggle(halloweenTab, "Trick-or-Treat", true, function(value)
    getgenv().Config.Halloween.AutoTrickOrTreat = value
end)

createLabel(halloweenTab, "📍 Teleports do Evento")
createButton(halloweenTab, "🎃 Evento Sea 1", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(500, 50, 500) end
end, Color3.fromRGB(255, 100, 0))

createButton(halloweenTab, "🎃 Evento Sea 2", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-2000, 50, 1000) end
end, Color3.fromRGB(255, 100, 0))

createButton(halloweenTab, "🎃 Evento Sea 3", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(3000, 50, -2000) end
end, Color3.fromRGB(255, 100, 0))

-- Aba Sea Events
createLabel(seaTab, "🌊 Sea Events")
createToggle(seaTab, "Caçar Sea Events", true, function(value)
    getgenv().Config.SeaEvents.Enabled = value
end)

createToggle(seaTab, "Caçar Navios", true, function(value)
    getgenv().Config.SeaEvents.AutoHuntShip = value
end)

createToggle(seaTab, "Caçar Kraken", true, function(value)
    getgenv().Config.SeaEvents.AutoHuntKraken = value
end)

createToggle(seaTab, "Caçar Sea Beast", true, function(value)
    getgenv().Config.SeaEvents.AutoHuntSeaBeast = value
end)

createToggle(seaTab, "Caçar Terror Shark", true, function(value)
    getgenv().Config.SeaEvents.AutoHuntTerrorShark = value
end)

createToggle(seaTab, "Caçar Mermaid", true, function(value)
    getgenv().Config.SeaEvents.AutoHuntMermaid = value
end)

-- Aba Frutas
createLabel(fruitTab, "🍎 Frutas")
createToggle(fruitTab, "Farm Frutas Spawnadas", true, function(value)
    getgenv().Config.Fruit.AutoFarmSpawnedFruit = value
end)

createToggle(fruitTab, "Auto Spin", true, function(value)
    getgenv().Config.Fruit.AutoSpinFruit = value
end)

createToggle(fruitTab, "Armazenar Frutas", true, function(value)
    getgenv().Config.Fruit.AutoStoreFruit = value
end)

createDropdown(fruitTab, "Fruta Específica", {"Dragon", "Leopard", "Venom", "Dough", "Shadow", "Control", "Spirit", "Mammoth"}, "Dragon", function(value)
    getgenv().Config.Fruit.SpecificFruit = value
end)

-- Aba Farm
createLabel(farmTab, "⚔️ Farm Geral")
createToggle(farmTab, "Auto Quest", true, function(value)
    getgenv().Config.Farm.AutoQuest = value
end)

createToggle(farmTab, "Farm Mobs", true, function(value)
    getgenv().Config.Farm.AutoFarmMobs = value
end)

createToggle(farmTab, "Farm Boss", true, function(value)
    getgenv().Config.Farm.AutoFarmBoss = value
end)

createToggle(farmTab, "Farm Level", true, function(value)
    getgenv().Config.Farm.AutoFarmLevel = value
end)

createToggle(farmTab, "Farm Money", true, function(value)
    getgenv().Config.Farm.AutoFarmMoney = value
end)

-- Aba Config
createLabel(settingsTab, "⚙️ Configurações")
createToggle(settingsTab, "FPS Booster", true, function(value)
    getgenv().Config.Settings.FPSBooster = value
    if value then
        pcall(function()
            settings().Rendering.EnableFRM = true
            settings().Rendering.FrameRateManager:SetFrameRate(60)
        end)
    end
end)

createToggle(settingsTab, "Anti-Afk", true, function(value)
    getgenv().Config.Settings.AntiAfk = value
end)

createToggle(settingsTab, "Auto Hop", true, function(value)
    getgenv().Config.Settings.AutoHop = value
end)

createLabel(settingsTab, "📝 Informações")
createButton(settingsTab, "ℹ️ Sobre o Script", function()
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "Halloween Hub 2026",
        Text = "Versão 1.0\nFeito para Blox Fruits\nby NaNa Hub",
        Duration = 5
    })
end, Color3.fromRGB(200, 200, 200))

-- Mostrar primeira aba
tabs[1].content.Visible = true
tabs[1].button.BackgroundColor3 = Color3.fromRGB(255, 170, 0)

-- Funções principais

-- Detectar Sea atual
local function getSea()
    local map = workspace:FindFirstChild("Map")
    if map then
        if map:FindFirstChild("Sea1") then return 1 end
        if map:FindFirstChild("Sea2") then return 2 end
        if map:FindFirstChild("Sea3") then return 3 end
    end
    return 0
end

-- Função para encontrar Jack-O-Lanterns
local function findJackOLanterns()
    for _, v in ipairs(workspace:GetChildren()) do
        if v.Name:match("Jack") or v.Name:match("Pumpkin") or 
           v.Name:match("Lantern") or v.Name:match("Candy") then
            if v:FindFirstChild("HumanoidRootPart") then
                return v
            end
        end
    end
    return nil
end

-- Função para encontrar Hell Rider
local function findHellRider()
    for _, v in ipairs(workspace:GetChildren()) do
        if v.Name:match("Hell") or v.Name:match("Rider") or 
           v.Name:match("Devil") then
            if v:FindFirstChild("HumanoidRootPart") then
                return v
            end
        end
    end
    return nil
end

-- Função para encontrar Candy Corn
local function findCandyCorn()
    for _, v in ipairs(workspace:GetChildren()) do
        if v.Name:match("Candy") or v.Name:match("Corn") then
            return v
        end
    end
    return nil
end

-- Função para encontrar frutas spawnadas
local function findSpawnedFruit()
    for _, v in ipairs(workspace:GetChildren()) do
        if v:IsA("Tool") and v:FindFirstChild("Fruit") then
            return v
        end
    end
    return nil
end

-- Função para encontrar Sea Events
local function findSeaEvent()
    for _, v in ipairs(workspace:GetChildren()) do
        if v.Name:match("Kraken") or v.Name:match("SeaBeast") or 
           v.Name:match("Terror") or v.Name:match("Ship") or
           v.Name:match("Mermaid") then
            return v
        end
    end
    return nil
end

-- Loop Principal
spawn(function()
    while task.wait(0.5) do
        if not getgenv().Config.StartFarm then continue end
        
        local char = player.Character
        if not char then continue end
        
        local hrp = char:FindFirstChild("HumanoidRootPart")
        if not hrp then continue end
        
        -- Farm Halloween 2026
        if getgenv().Config.Halloween.Enabled then
            -- Farm Hell Rider
            if getgenv().Config.Halloween.AutoKillHellRider then
                local hellRider = findHellRider()
                if hellRider then
                    hrp.CFrame = hellRider.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5)
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Down()
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Up()
                end
            end
            
            -- Farm Jack-O-Lanterns
            if getgenv().Config.Halloween.AutoFarmJackOLanterns then
                local jack = findJackOLanterns()
                if jack then
                    hrp.CFrame = jack.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5)
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Down()
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Up()
                end
            end
            
            -- Coletar Candy Corn
            if getgenv().Config.Halloween.AutoCollectCandy then
                local candy = findCandyCorn()
                if candy then
                    hrp.CFrame = candy.Position
                    task.wait(0.1)
                end
            end
        end
        
        -- Sea Events
        if getgenv().Config.SeaEvents.Enabled then
            local event = findSeaEvent()
            if event and event:FindFirstChild("HumanoidRootPart") then
                hrp.CFrame = event.HumanoidRootPart.CFrame * CFrame.new(0, 0, 10)
                task.wait(0.1)
                game:GetService("VirtualUser"):Button1Down()
                task.wait(0.1)
                game:GetService("VirtualUser"):Button1Up()
            end
        end
        
        -- Frutas
        if getgenv().Config.Fruit.AutoFarmSpawnedFruit then
            local fruit = findSpawnedFruit()
            if fruit and fruit:FindFirstChild("Handle") then
                hrp.CFrame = fruit.Handle.CFrame
                task.wait(0.1)
            end
        end
    end
end)

-- Anti-Afk
spawn(function()
    while task.wait(60) do
        if getgenv().Config.Settings.AntiAfk then
            local virtualUser = game:GetService("VirtualUser")
            virtualUser:CaptureController()
            virtualUser:ClickButton2(Vector2.new())
        end
    end
end)

-- FPS Booster
if getgenv().Config.Settings.FPSBooster then
    pcall(function()
        settings().Rendering.EnableFRM = true
        settings().Rendering.FrameRateManager:SetFrameRate(60)
    end)
end

print("✅ Halloween Hub 2026 carregado com sucesso!")
