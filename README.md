-- Halloween Hub 2026 - Versão Completa com AutoFarm Funcional
print("🎃 Iniciando Halloween Hub 2026...")

-- Esperar o jogo carregar
task.wait(2)

-- Config Global
getgenv().Config = {
    ["StartFarm"] = true,
    ["AutoFarm"] = false,
    ["AutoQuest"] = true,
    ["AutoStats"] = false,
    ["AutoStatsPoint"] = "Melee",
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
        ["SpecificFruit"] = "Dragon",
    },
    ["Settings"] = {
        ["FPSBooster"] = true,
        ["AntiAfk"] = true,
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

-- Função para criar toggle
local function createToggle(parent, text, default, callback)
    local toggleFrame = Instance.new("Frame")
    toggleFrame.Size = UDim2.new(1, -20, 0, 45)
    toggleFrame.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 50)
    toggleFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    toggleFrame.BackgroundTransparency = 0.2
    toggleFrame.BorderSizePixel = 0
    toggleFrame.Parent = parent
    
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

-- Função para criar botão
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
local farmTab = createTab("Farm", "⚔️", Color3.fromRGB(150, 255, 50))
local halloweenTab = createTab("Halloween", "🎃", Color3.fromRGB(255, 100, 0))
local seaTab = createTab("Sea", "🌊", Color3.fromRGB(0, 150, 255))
local fruitTab = createTab("Frutas", "🍎", Color3.fromRGB(255, 50, 50))
local teleportTab = createTab("Teleports", "📍", Color3.fromRGB(200, 100, 255))
local statsTab = createTab("Stats", "📊", Color3.fromRGB(100, 200, 100))
local settingsTab = createTab("Config", "⚙️", Color3.fromRGB(200, 200, 200))

-- Aba Principal
createLabel(mainTab, "🏠 Controles Principais")
createToggle(mainTab, "Iniciar Farm", true, function(value)
    getgenv().Config.StartFarm = value
end)

createLabel(mainTab, "📊 Status")
createButton(mainTab, "Ver Nível", function()
    local level = player.Data.Level.Value
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "Nível",
        Text = "Seu nível é: " .. tostring(level),
        Duration = 3
    })
end, Color3.fromRGB(100, 200, 100))

-- Aba Farm
createLabel(farmTab, "⚔️ AutoFarm de Nível")
createToggle(farmTab, "AutoFarm Ativo", false, function(value)
    getgenv().Config.AutoFarm = value
end)

createToggle(farmTab, "Auto Quest", true, function(value)
    getgenv().Config.AutoQuest = value
end)

createLabel(farmTab, "⚔️ Farm Geral")
createToggle(farmTab, "Farm Mobs", true, function(value)
    getgenv().Config.Farm.AutoFarmMobs = value
end)

createToggle(farmTab, "Farm Boss", true, function(value)
    getgenv().Config.Farm.AutoFarmBoss = value
end)

createToggle(farmTab, "Farm Money", true, function(value)
    getgenv().Config.Farm.AutoFarmMoney = value
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

-- Aba Teleports
createLabel(teleportTab, "📍 Teleports - Sea 1")
createButton(teleportTab, "🏝️ Pirate Island", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(1041.886, 16.273, 1424.937) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏝️ Marine Island", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-2896.686, 41.488, 2009.274) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏟️ Colosseum", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-1541.088, 7.389, -2987.405) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏜️ Desert", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(1094.320, 6.569, 4231.635) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🌆 Fouatin City", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(5529.723, 429.357, 4245.549) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🌴 Jungle", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-1615.188, 36.852, 150.804) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏰 Marine Fort", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-4846.149, 20.652, 4393.650) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏘️ Middle Town", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-705.997, 7.852, 1547.521) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "⛓️ Prison", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(4841.844, 5.651, 741.329) end
end, Color3.fromRGB(0, 150, 255))

createButton(teleportTab, "🏴‍☠️ Pirate Village", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-1146.429, 4.752, 3818.503) end
end, Color3.fromRGB(0, 150, 255))

createLabel(teleportTab, "📍 Teleports - Sky")
createButton(teleportTab, "☁️ Sky 1", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-4967.836, 717.671, -2623.843) end
end, Color3.fromRGB(150, 150, 255))

createButton(teleportTab, "☁️ Sky 2", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-7876.077, 5545.581, -381.199) end
end, Color3.fromRGB(150, 150, 255))

createLabel(teleportTab, "📍 Teleports - Outros")
createButton(teleportTab, "❄️ Snow", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(1100.361, 5.290, -1151.541) end
end, Color3.fromRGB(150, 200, 255))

createButton(teleportTab, "🌊 Under Water", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(61135.292, 18.471, 1597.682) end
end, Color3.fromRGB(0, 100, 200))

createButton(teleportTab, "🌋 Magma Village", function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.CFrame = CFrame.new(-5248.271, 8.699, 8452.890) end
end, Color3.fromRGB(255, 100, 0))

-- Aba Stats
createLabel(statsTab, "📊 Auto Stats")
createToggle(statsTab, "Auto Stats Ativo", false, function(value)
    getgenv().Config.AutoStats = value
end)

createDropdown(statsTab, "Ponto de Stat", {"Melee", "Defense", "Sword", "Gun", "Devil Fruit"}, "Melee", function(value)
    getgenv().Config.AutoStatsPoint = value
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

-- Mostrar primeira aba
tabs[1].content.Visible = true
tabs[1].button.BackgroundColor3 = Color3.fromRGB(255, 170, 0)

-- Funções do AutoFarm

-- Sistema de Quest
local function CheckQuest()
    local Lv = player.Data.Level.Value
    if Lv == 0 or Lv <= 10 then
        Ms = "Bandit [Lv. 5]"
        NM = "Bandit"
        LQ = "BanditQuest1"
        NQ = "Bandit"
        CQ = CFrame.new(1062.646, 16.516, 1546.552)
    elseif Lv == 10 or Lv <= 20 then
        Ms = "Monkey [Lv. 14]"
        NM = "Monkey"
        LQ = "JungleQuest"
        NQ = "Monkey"
        CQ = CFrame.new(-1601.655, 36.852, 153.388)
    elseif Lv == 20 or Lv <= 30 then
        Ms = "Gorilla [Lv. 20]"
        NM = "Gorilla"
        LQ = "JungleQuest"
        NQ = "Gorilla"
        CQ = CFrame.new(-1601.655, 36.852, 153.388)
    elseif Lv == 30 or Lv <= 40 then
        Ms = "Pirate [Lv. 35]"
        NM = "Pirate"
        LQ = "BuggyQuest1"
        NQ = "Pirate"
        CQ = CFrame.new(-1141.074, 4.100, 3831.549)
    elseif Lv == 40 or Lv <= 60 then
        Ms = "Brute [Lv. 45]"
        NM = "Brute"
        LQ = "BuggyQuest1"
        NQ = "Brute"
        CQ = CFrame.new(-1141.074, 4.100, 3831.549)
    elseif Lv == 60 or Lv <= 75 then
        Ms = "Desert Bandit [Lv. 60]"
        NM = "Desert Bandit"
        LQ = "DesertQuest"
        NQ = "Desert Bandit"
        CQ = CFrame.new(894.488, 5.140, 4392.195)
    elseif Lv == 75 or Lv <= 90 then
        Ms = "Desert Officer [Lv. 70]"
        NM = "Desert Officer"
        LQ = "DesertQuest"
        NQ = "Desert Officer"
        CQ = CFrame.new(894.488, 5.140, 4392.195)
    elseif Lv == 90 or Lv <= 110 then
        Ms = "Snow Bandit [Lv. 90]"
        NM = "Snow Bandit"
        LQ = "SnowQuest"
        NQ = "Snow Bandit"
        CQ = CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv == 110 or Lv <= 125 then
        Ms = "Snowman [Lv. 100]"
        NM = "Snowman"
        LQ = "SnowQuest"
        NQ = "Snowman"
        CQ = CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv == 125 or Lv <= 150 then
        Ms = "Chief Petty Officer [Lv. 120]"
        NM = "Chief Petty Officer"
