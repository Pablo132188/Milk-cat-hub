--[[
    BLOX FRUITS HUB - HALLOWEEN 2026 EDITION
    Compatível: Delta, Xeno, Synapse, Fluxus
    Interface 100% nativa - Funciona offline
]]

-- Detectar Executor
local Executor = "Unknown"
if getgenv and getgenv().Xeno then 
    Executor = "Xeno"
elseif getgenv and getgenv().Delta then 
    Executor = "Delta"
elseif syn and syn.queue_on_teleport then 
    Executor = "Synapse"
elseif fluxus then 
    Executor = "Fluxus"
elseif hookfunction then 
    Executor = "Generic"
end

print("🎃 Halloween Hub 2026 | Executor: " .. Executor)
print("✅ Iniciando interface nativa...")

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

-- Criar Interface
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Verificar se já existe
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
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 550, 0, 450)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -225)
mainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
mainFrame.BackgroundTransparency = 0.05
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Criar Barra de Título
local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 45)
titleBar.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 1, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "🎃 Halloween Hub 2026"
titleLabel.TextColor3 = Color3.fromRGB(255, 170, 0)
titleLabel.TextSize = 22
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Parent = titleBar

-- Botão Fechar
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 35, 0, 35)
closeButton.Position = UDim2.new(1, -40, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeButton.BackgroundTransparency = 0.3
closeButton.Text = "✕"
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.TextSize = 18
closeButton.Font = Enum.Font.GothamBold
closeButton.Parent = titleBar

closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- Botão Minimizar
local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.new(0, 35, 0, 35)
minimizeButton.Position = UDim2.new(1, -80, 0, 5)
minimizeButton.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
minimizeButton.BackgroundTransparency = 0.3
minimizeButton.Text = "—"
minimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeButton.TextSize = 18
minimizeButton.Font = Enum.Font.GothamBold
minimizeButton.Parent = titleBar

minimizeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

-- Criar Abas
local tabsFrame = Instance.new("Frame")
tabsFrame.Size = UDim2.new(1, 0, 0, 45)
tabsFrame.Position = UDim2.new(0, 0, 0, 45)
tabsFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 45)
tabsFrame.BorderSizePixel = 0
tabsFrame.Parent = mainFrame

-- Container de Conteúdo
local contentFrame = Instance.new("Frame")
contentFrame.Size = UDim2.new(1, -20, 1, -110)
contentFrame.Position = UDim2.new(0, 10, 0, 100)
contentFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
contentFrame.BorderSizePixel = 0
contentFrame.Parent = mainFrame

-- Sistema de Abas
local tabs = {}
local currentTab = nil

local function createTab(name, icon)
    local tabButton = Instance.new("TextButton")
    tabButton.Size = UDim2.new(0, 90, 0, 40)
    tabButton.Position = UDim2.new(0, (#tabs * 95) + 5, 0, 2)
    tabButton.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
    tabButton.BackgroundTransparency = 0.2
    tabButton.Text = icon .. " " .. name
    tabButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    tabButton.TextSize = 14
    tabButton.Font = Enum.Font.Gotham
    tabButton.Parent = tabsFrame
    
    local tabContent = Instance.new("ScrollingFrame")
    tabContent.Size = UDim2.new(1, 0, 1, 0)
    tabContent.BackgroundTransparency = 1
    tabContent.Visible = false
    tabContent.ScrollBarThickness = 5
    tabContent.CanvasSize = UDim2.new(0, 0, 0, 0)
    tabContent.AutomaticCanvasSize = Enum.AutomaticSize.Y
    tabContent.Parent = contentFrame
    
    table.insert(tabs, {button = tabButton, content = tabContent, name = name})
    
    tabButton.MouseButton1Click:Connect(function()
        for _, tab in ipairs(tabs) do
            tab.content.Visible = false
            tab.button.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        end
        tabContent.Visible = true
        tabButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
        currentTab = tabContent
    end)
    
    return tabContent
end

-- Função para criar toggles
local function createToggle(parent, text, default, callback)
    local toggleFrame = Instance.new("Frame")
    toggleFrame.Size = UDim2.new(1, -20, 0, 40)
    toggleFrame.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 45)
    toggleFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
    toggleFrame.BackgroundTransparency = 0.3
    toggleFrame.BorderSizePixel = 0
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
    
    local toggleButton = Instance.new("TextButton")
    toggleButton.Size = UDim2.new(0, 60, 0, 30)
    toggleButton.Position = UDim2.new(1, -70, 0, 5)
    toggleButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    toggleButton.Text = "OFF"
    toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggleButton.TextSize = 12
    toggleButton.Font = Enum.Font.GothamBold
    toggleButton.Parent = toggleFrame
    
    local enabled = default or false
    if enabled then
        toggleButton.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
        toggleButton.Text = "ON"
    end
    
    toggleButton.MouseButton1Click:Connect(function()
        enabled = not enabled
        if enabled then
            toggleButton.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
            toggleButton.Text = "ON"
        else
            toggleButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
            toggleButton.Text = "OFF"
        end
        callback(enabled)
    end)
    
    return toggleButton
end

-- Função para criar botões
local function createButton(parent, text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -20, 0, 40)
    button.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 45)
    button.BackgroundColor3 = Color3.fromRGB(70, 70, 90)
    button.BackgroundTransparency = 0.2
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 14
    button.Font = Enum.Font.Gotham
    button.Parent = parent
    
    button.MouseButton1Click:Connect(function()
        button.BackgroundColor3 = Color3.fromRGB(100, 100, 120)
        task.wait(0.1)
        button.BackgroundColor3 = Color3.fromRGB(70, 70, 90)
        callback()
    end)
    
    return button
end

-- Função para criar labels
local function createLabel(parent, text)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -20, 0, 30)
    label.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 35)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 170, 0)
    label.TextSize = 16
    label.Font = Enum.Font.GothamBold
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = parent
    return label
end

-- Criar Abas
local mainTab = createTab("Principal", "🏠")
local halloweenTab = createTab("Halloween", "🎃")
local seaTab = createTab("Sea", "🌊")
local fruitTab = createTab("Frutas", "🍎")
local farmTab = createTab("Farm", "⚔️")
local settingsTab = createTab("Config", "⚙️")

-- Aba Principal
createLabel(mainTab, "🏠 Controles Principais")
createToggle(mainTab, "Iniciar Farm", true, function(value)
    getgenv().Config.StartFarm = value
end)

createLabel(mainTab, "📍 Teleports")
createButton(mainTab, "🌊 Teleportar Sea 1", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(500, 50, 500)
    end
end)

createButton(mainTab, "🌊 Teleportar Sea 2", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(-2000, 50, 1000)
    end
end)

createButton(mainTab, "🌊 Teleportar Sea 3", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(3000, 50, -2000)
    end
end)

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
    if hrp then
        hrp.CFrame = CFrame.new(500, 50, 500)
    end
end)

createButton(halloweenTab, "🎃 Evento Sea 2", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(-2000, 50, 1000)
    end
end)

createButton(halloweenTab, "🎃 Evento Sea 3", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        hrp.CFrame = CFrame.new(3000, 50, -2000)
    end
end)

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
end)

createToggle(settingsTab, "Anti-Afk", true, function(value)
    getgenv().Config.Settings.AntiAfk = value
end)

createToggle(settingsTab, "Auto Hop", true, function(value)
    getgenv().Config.Settings.AutoHop = value
end)

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

print("🎃 Halloween Hub 2026 carregado com sucesso!")
print("✅ Interface nativa criada!")
print("✅ Compatível com: " .. Executor)
