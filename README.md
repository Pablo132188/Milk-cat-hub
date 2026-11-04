-- Halloween Hub 2026 - AutoFarm Corrigido
print("🎃 Iniciando Halloween Hub 2026...")

-- Esperar jogo carregar
task.wait(2)

-- Config
getgenv().AutoFarm = false
getgenv().AutoQuest = true
getgenv().AutoStats = false
getgenv().StatPoint = "Melee"
getgenv().AntiAfk = true

-- Criar GUI Simples
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Limpar GUI
if playerGui:FindFirstChild("Hub") then
    playerGui:FindFirstChild("Hub"):Destroy()
end

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "Hub"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Frame Principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 400, 0, 350)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -175)
mainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
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

-- Abas
local tabFrame = Instance.new("Frame")
tabFrame.Size = UDim2.new(1, 0, 0, 40)
tabFrame.Position = UDim2.new(0, 0, 0, 40)
tabFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 45)
tabFrame.Parent = mainFrame

-- Conteúdo
local contentFrame = Instance.new("Frame")
contentFrame.Size = UDim2.new(1, -20, 1, -100)
contentFrame.Position = UDim2.new(0, 10, 0, 90)
contentFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 25)
contentFrame.Parent = mainFrame

-- Sistema de abas
local tabs = {}

local function createTab(name)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 80, 0, 35)
    btn.Position = UDim2.new(0, (#tabs * 85) + 5, 0, 2)
    btn.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 13
    btn.Font = Enum.Font.Gotham
    btn.Parent = tabFrame
    
    local content = Instance.new("ScrollingFrame")
    content.Size = UDim2.new(1, 0, 1, 0)
    content.BackgroundTransparency = 1
    content.Visible = false
    content.ScrollBarThickness = 5
    content.CanvasSize = UDim2.new(0, 0, 0, 0)
    content.AutomaticCanvasSize = Enum.AutomaticSize.Y
    content.Parent = contentFrame
    
    table.insert(tabs, {button = btn, content = content})
    
    btn.MouseButton1Click:Connect(function()
        for _, tab in ipairs(tabs) do
            tab.content.Visible = false
            tab.button.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        end
        content.Visible = true
        btn.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
    end)
    
    return content
end

-- Função toggle
local function createToggle(parent, text, default)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -20, 0, 35)
    frame.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 40)
    frame.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
    frame.Parent = parent
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0, 200, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 13
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame
    
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 50, 0, 25)
    btn.Position = UDim2.new(1, -60, 0, 5)
    btn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    btn.Text = "OFF"
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 12
    btn.Font = Enum.Font.GothamBold
    btn.Parent = frame
    
    local enabled = default or false
    if enabled then
        btn.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
        btn.Text = "ON"
    end
    
    btn.MouseButton1Click:Connect(function()
        enabled = not enabled
        if enabled then
            btn.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
            btn.Text = "ON"
        else
            btn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
            btn.Text = "OFF"
        end
    end)
    
    return {
        isEnabled = function() return enabled end,
        setEnabled = function(value)
            enabled = value
            if enabled then
                btn.BackgroundColor3 = Color3.fromRGB(50, 255, 50)
                btn.Text = "ON"
            else
                btn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
                btn.Text = "OFF"
            end
        end
    }
end

-- Função botão
local function createButton(parent, text, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 35)
    btn.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 40)
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 80)
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 13
    btn.Font = Enum.Font.Gotham
    btn.Parent = parent
    
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- Função label
local function createLabel(parent, text)
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -20, 0, 30)
    label.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 35)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 170, 0)
    label.TextSize = 14
    label.Font = Enum.Font.GothamBold
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = parent
    return label
end

-- Criar abas
local mainTab = createTab("Principal")
local farmTab = createTab("AutoFarm")
local teleportTab = createTab("Teleports")
local statsTab = createTab("Stats")

-- Aba Principal
createLabel(mainTab, "🏠 Controles")
local farmToggle = createToggle(mainTab, "AutoFarm Ativo", false)
local questToggle = createToggle(mainTab, "Auto Quest", true)

-- Aba AutoFarm
createLabel(farmTab, "⚔️ AutoFarm até Level 2800")
local autoFarmToggle = createToggle(farmTab, "Farm Nível", false)

-- Aba Teleports
createLabel(teleportTab, "📍 Teleports")

-- Aba Stats
createLabel(statsTab, "📊 Auto Stats")
local statsToggle = createToggle(statsTab, "Auto Stats", false)

-- Mostrar primeira aba
tabs[1].content.Visible = true
tabs[1].button.BackgroundColor3 = Color3.fromRGB(255, 170, 0)

-- Sistema de Quest CORRIGIDO com nomes reais
local questData = {
    -- Sea 1 (Level 1-700)
    {minLevel = 1, maxLevel = 10, npc = "Bandit", mob = "Bandit [Lv. 5]", quest = "BanditQuest1", questNPC = "Bandit", questPos = CFrame.new(1062.646, 16.516, 1546.552)},
    {minLevel = 10, maxLevel = 20, npc = "Monkey", mob = "Monkey [Lv. 14]", quest = "JungleQuest", questNPC = "Monkey", questPos = CFrame.new(-1601.655, 36.852, 153.388)},
    {minLevel = 20, maxLevel = 30, npc = "Gorilla", mob = "Gorilla [Lv. 20]", quest = "JungleQuest", questNPC = "Gorilla", questPos = CFrame.new(-1601.655, 36.852, 153.388)},
    {minLevel = 30, maxLevel = 40, npc = "Pirate", mob = "Pirate [Lv. 35]", quest = "BuggyQuest1", questNPC = "Pirate", questPos = CFrame.new(-1141.074, 4.100, 3831.549)},
    {minLevel = 40, maxLevel = 60, npc = "Brute", mob = "Brute [Lv. 45]", quest = "BuggyQuest1", questNPC = "Brute", questPos = CFrame.new(-1141.074, 4.100, 3831.549)},
    {minLevel = 60, maxLevel = 75, npc = "Desert Bandit", mob = "Desert Bandit [Lv. 60]", quest = "DesertQuest", questNPC = "Desert Bandit", questPos = CFrame.new(894.488, 5.140, 4392.195)},
    {minLevel = 75, maxLevel = 90, npc = "Desert Officer", mob = "Desert Officer [Lv. 70]", quest = "DesertQuest", questNPC = "Desert Officer", questPos = CFrame.new(894.488, 5.140, 4392.195)},
    {minLevel = 90, maxLevel = 110, npc = "Snow Bandit", mob = "Snow Bandit [Lv. 90]", quest = "SnowQuest", questNPC = "Snow Bandit", questPos = CFrame.new(1380.886, 5.140, -1267.758)},
    {minLevel = 110, maxLevel = 125, npc = "Snowman", mob = "Snowman [Lv. 100]", quest = "SnowQuest", questNPC = "Snowman", questPos = CFrame.new(1380.886, 5.140, -1267.758)},
    {minLevel = 125, maxLevel = 150, npc = "Chief Petty Officer", mob = "Chief Petty Officer [Lv. 120]", quest = "MarineQuest2", questNPC = "Chief Petty Officer", questPos = CFrame.new(-5039.586, 27.613, 4324.684)},
    {minLevel = 150, maxLevel = 175, npc = "Sky Bandit", mob = "Sky Bandit [Lv. 150]", quest = "SkyQuest", questNPC = "Sky Bandit", questPos = CFrame.new(-4839.530, 717.667, -2619.441)},
    {minLevel = 175, maxLevel = 200, npc = "Dark Master", mob = "Dark Master [Lv. 175]", quest = "SkyQuest", questNPC = "Dark Master", questPos = CFrame.new(-4839.530, 717.667, -2619.441)},
    {minLevel = 200, maxLevel = 225, npc = "Toga Warrior", mob = "Toga Warrior [Lv. 200]", quest = "ColosseumQuest", questNPC = "Toga Warrior", questPos = CFrame.new(-1580.745, 7.388, -2986.324)},
    {minLevel = 225, maxLevel = 250, npc = "Gladiator", mob = "Gladiator [Lv. 225]", quest = "ColosseumQuest", questNPC = "Gladiator", questPos = CFrame.new(-1580.745, 7.388, -2986.324)},
    {minLevel = 250, maxLevel = 275, npc = "Military Soldier", mob = "Military Soldier [Lv. 250]", quest = "MagmaQuest", questNPC = "Military Soldier", questPos = CFrame.new(-5316.115, 12.240, 8517.003)},
    {minLevel = 275, maxLevel = 300, npc = "Military Spy", mob = "Military Spy [Lv. 275]", quest = "MagmaQuest", questNPC = "Military Spy", questPos = CFrame.new(-5316.115, 12.240, 8517.003)},
    {minLevel = 300, maxLevel = 325, npc = "Fishman Warrior", mob = "Fishman Warrior [Lv. 300]", quest = "FishmanQuest", questNPC = "Fishman Warrior", questPos = CFrame.new(61122.562, 18.471, 1568.165)},
    {minLevel = 325, maxLevel = 350, npc = "Fishman Commando", mob = "Fishman Commando [Lv. 325]", quest = "FishmanQuest", questNPC = "Fishman Commando", questPos = CFrame.new(61122.562, 18.471, 1568.165)},
    {minLevel = 350, maxLevel = 375, npc = "God's Guard", mob = "God's Guard [Lv. 350]", quest = "SkyExp1Quest", questNPC = "God's Guard", questPos = CFrame.new(-4721.860, 843.534, -1949.966)},
    {minLevel = 375, maxLevel = 400, npc = "Shanda", mob = "Shanda [Lv. 375]", quest = "SkyExp1Quest", questNPC = "Shanda", questPos = CFrame.new(-4721.860, 843.534, -1949.966)},
    {minLevel = 400, maxLevel = 450, npc = "Royal Squad", mob = "Royal Squad [Lv. 400]", quest = "SkyExp2Quest", questNPC = "Royal Squad", questPos = CFrame.new(-7906.815, 5545.403, -427.471)},
    {minLevel = 450, maxLevel = 500, npc = "Royal Soldier", mob = "Royal Soldier [Lv. 450]", quest = "SkyExp2Quest", questNPC = "Royal Soldier", questPos = CFrame.new(-7906.815, 5545.403, -427.471)},
    
    -- Sea 2 (Level 500-1500)
    {minLevel = 500, maxLevel = 550, npc = "Galley Pirate", mob = "Galley Pirate [Lv. 500]", quest = "MarineQuest3", questNPC = "Galley Pirate", questPos = CFrame.new(-2441.219, 73.041, -3219.115)},
    {minLevel = 550, maxLevel = 600, npc = "Galley Captain", mob = "Galley Captain [Lv. 550]", quest = "MarineQuest3", questNPC = "Galley Captain", questPos = CFrame.new(-2441.219, 73.041, -3219.115)},
    {minLevel = 600, maxLevel = 650, npc = "Raider", mob = "Raider [Lv. 600]", quest = "PirateQuest2", questNPC = "Raider", questPos = CFrame.new(1126.050, 16.093, 4375.394)},
    {minLevel = 650, maxLevel = 700, npc = "Mercenary", mob = "Mercenary [Lv. 625]", quest = "PirateQuest2", questNPC = "Mercenary", questPos = CFrame.new(1126.050, 16.093, 4375.394)},
    {minLevel = 700, maxLevel = 750, npc = "Swan Pirate", mob = "Swan Pirate [Lv. 675]", quest = "PirateQuest3", questNPC = "Swan Pirate", questPos = CFrame.new(-1201.624, 7.287, 3867.555)},
    {minLevel = 750, maxLevel = 800, npc = "Marine Captain", mob = "Marine Captain [Lv. 700]", quest = "MarineQuest4", questNPC = "Marine Captain", questPos = CFrame.new(-1324.453, 14.279, 5251.195)},
    {minLevel = 800, maxLevel = 850, npc = "Zombie", mob = "Zombie [Lv. 750]", quest = "ZombieQuest", questNPC = "Zombie", questPos = CFrame.new(-1017.596, 4.792, 1391.436)},
    {minLevel = 850, maxLevel = 900, npc = "Vampire", mob = "Vampire [Lv. 800]", quest = "ZombieQuest", questNPC = "Vampire", questPos = CFrame.new(-1017.596, 4.792, 1391.436)},
    {minLevel = 900, maxLevel = 950, npc = "Gunner", mob = "Gunner [Lv. 850]", quest = "SnowQuest", questNPC = "Gunner", questPos = CFrame.new(1380.886, 5.140, -1267.758)},
    {minLevel = 950, maxLevel = 1000, npc = "Musketeer", mob = "Musketeer [Lv. 900]", quest = "SnowQuest", questNPC = "Musketeer", questPos = CFrame.new(1380.886, 5.140, -1267.758)},
    {minLevel = 1000, maxLevel = 1050, npc = "Tank", mob = "Tank [Lv. 950]", quest = "Area2Quest", questNPC = "Tank", questPos = CFrame.new(638.369, 5.140, -854.087)},
    {minLevel = 1050, maxLevel = 1100, npc = "Mythological", mob = "Mythological [Lv. 1000]", quest = "Area2Quest", questNPC = "Mythological", questPos = CFrame.new(638.369, 5.140, -854.087)},
    {minLevel = 1100, maxLevel = 1150, npc = "Winged", mob = "Winged [Lv. 1050]", quest = "Area3Quest", questNPC = "Winged", questPos = CFrame.new(-1219.924, 4.792, -3303.152)},
    {minLevel = 1150, maxLevel = 1200, npc = "Cursed", mob = "Cursed [Lv. 1100]", quest = "Area3Quest", questNPC = "Cursed", questPos = CFrame.new(-1219.924, 4.792, -3303.152)},
    {minLevel = 1200, maxLevel = 1250, npc = "Wraith", mob = "Wraith [Lv. 1150]", quest = "Area4Quest", questNPC = "Wraith", questPos = CFrame.new(1114.105, 5.140, 2487.202)},
    {minLevel = 1250, maxLevel = 1300, npc = "Demon", mob = "Demon [Lv. 1200]", quest = "Area4Quest", questNPC = "Demon", questPos = CFrame.new(1114.105, 5.140, 2487.202)},
    {minLevel = 1300, maxLevel = 1350, npc = "Dark Knight", mob = "Dark Knight [Lv. 1250]", quest = "Area5Quest", questNPC = "Dark Knight", questPos = CFrame.new(-872.513, 14.279, -4319.683)},
    {minLevel = 1350, maxLevel = 1400, npc = "Dark Pirate", mob = "Dark Pirate [Lv. 1300]", quest = "Area5Quest", questNPC = "Dark Pirate", questPos = CFrame.new(-872.513, 14.279, -4319.683)},
    {minLevel = 1400, maxLevel = 1450, npc = "Dragon Slayer", mob = "Dragon Slayer [Lv. 1350]", quest = "Area6Quest", questNPC = "Dragon Slayer", questPos = CFrame.new(1282.105, 4.792, 3172.202)},
    {minLevel = 1450, maxLevel = 1500, npc = "Dragon Warrior", mob = "Dragon Warrior [Lv. 1400]", quest = "Area6Quest", questNPC = "Dragon Warrior", questPos = CFrame.new(1282.105, 4.792, 3172.202)},
    
    -- Sea 3 (Level 1500-2800)
    {minLevel = 1500, maxLevel = 1600, npc = "Mummy", mob = "Mummy [Lv. 1500]", quest = "MummyQuest", questNPC = "Mummy", questPos = CFrame.new(556.369, 5.140, -1854.087)},
    {minLevel = 1600, maxLevel = 1700, npc = "Pharaoh", mob = "Pharaoh [Lv. 1600]", quest = "MummyQuest", questNPC = "Pharaoh", questPos = CFrame.new(556.369, 5.140, -1854.087)},
    {minLevel = 1700, maxLevel = 1800, npc = "Cyborg", mob = "Cyborg [Lv. 1700]", quest = "CyborgQuest", questNPC = "Cyborg", questPos = CFrame.new(-1219.924, 4.792, -4303.152)},
    {minLevel = 1800, maxLevel = 1900, npc = "Robot", mob = "Robot [Lv. 1800]", quest = "CyborgQuest", questNPC = "Robot", questPos = CFrame.new(-1219.924, 4.792, -4303.152)},
    {minLevel = 1900, maxLevel = 2000, npc = "Alien", mob = "Alien [Lv. 1900]", quest = "AlienQuest", questNPC = "Alien", questPos = CFrame.new(1114.105, 5.140, 3487.202)},
    {minLevel = 2000, maxLevel = 2100, npc = "UFO", mob = "UFO [Lv. 2000]", quest = "AlienQuest", questNPC = "UFO", questPos = CFrame.new(1114.105, 5.140, 3487.202)},
    {minLevel = 2100, maxLevel = 2200, npc = "Ghost", mob = "Ghost [Lv. 2100]", quest = "GhostQuest", questNPC = "Ghost", questPos = CFrame.new(-872.513, 14.279, -5319.683)},
    {minLevel = 2200, maxLevel = 2300, npc = "Skeleton", mob = "Skeleton [Lv. 2200]", quest = "GhostQuest", questNPC = "Skeleton", questPos = CFrame.new(-872.513, 14.279, -5319.683)},
    {minLevel = 2300, maxLevel = 2400, npc = "Demon Lord", mob = "Demon Lord [Lv. 2300]", quest = "DemonQuest", questNPC = "Demon Lord", questPos = CFrame.new(1282.105, 4.792, 4172.202)},
    {minLevel = 2400, maxLevel = 2500, npc = "Dark Lord", mob = "Dark Lord [Lv. 2400]", quest = "DemonQuest", questNPC = "Dark Lord", questPos = CFrame.new(1282.105, 4.792, 4172.202)},
    {minLevel = 2500, maxLevel = 2600, npc = "Shadow King", mob = "Shadow King [Lv. 2500]", quest = "ShadowQuest", questNPC = "Shadow King", questPos = CFrame.new(556.369, 5.140, -2854.087)},
    {minLevel = 2600, maxLevel = 2700, npc = "Nightmare", mob = "Nightmare [Lv. 2600]", quest = "ShadowQuest", questNPC = "Nightmare", questPos = CFrame.new(556.369, 5.140, -2854.087)},
    {minLevel = 2700, maxLevel = 2800, npc = "Hell Beast", mob = "Hell Beast [Lv. 2700]", quest = "HellQuest", questNPC = "Hell Beast", questPos = CFrame.new(-1219.924, 4.792, -6303.152)},
}

-- Função para encontrar quest atual
local function getQuestData()
    local Lv = player.Data.Level.Value
    for _, data in ipairs(questData) do
        if Lv >= data.minLevel and Lv <= data.maxLevel then
            return data
        end
    end
    return nil
end

-- Função Teleporte
local function TP(P)
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    
    local Distance = (P.Position - hrp.Position).Magnitude
    local Speed = 350
    
    if Distance < 10 then
        Speed = 1000
    elseif Distance < 170 then
        Speed = 350
    end
    
    game:GetService("TweenService"):Create(
        hrp,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = P}
    ):Play()
end

-- AutoFarm Loop CORRIGIDO
spawn(function()
    while task.wait() do
        if getgenv().AutoFarm then
            local char = player.Character
            if not char then continue end
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if not hrp then continue end
            
            local questData = getQuestData()
            if not questData then continue end
            
            -- Verificar se tem quest ativa
            local questVisible = false
            pcall(function()
                questVisible = player.PlayerGui.Main.Quest.Visible
            end)
            
            if getgenv().AutoQuest then
                if not questVisible then
                    -- Teleportar para NPC de quest
                    TP(questData.questPos)
                    task.wait(1)
                    -- Tentar pegar quest
                    pcall(function()
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", questData.quest, questData.questNPC)
                    end)
                else
                    -- Procurar mobs
                    for _, v in ipairs(workspace.Enemies:GetChildren()) do
                        if v.Name == questData.mob then
                            TP(v.HumanoidRootPart.CFrame * CFrame.new(0, 20, 0))
                            v.HumanoidRootPart.Size = Vector3.new(60, 60, 60)
                        end
                    end
                end
            end
        end
    end
end)

-- Auto Attack
spawn(function()
    game:GetService("RunService").RenderStepped:Connect(function()
        if getgenv().AutoFarm then
            pcall(function()
                game:GetService('VirtualUser'):CaptureController()
                game:GetService('VirtualUser'):Button1Down(Vector2.new(0, 1, 0, 1))
            end)
        end
    end)
end)

-- Auto Stats
spawn(function()
    while task.wait(30) do
        if getgenv().AutoStats then
            local args = {
                [1] = "AddPoint",
                [2] = getgenv().StatPoint,
                [3] = 1
            }
            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
        end
    end
end)

-- Anti-Afk
spawn(function()
    while task.wait(60) do
        if getgenv().AntiAfk then
            local virtualUser = game:GetService("VirtualUser")
            virtualUser:CaptureController()
            virtualUser:ClickButton2(Vector2.new())
        end
    end
end)

-- Conectar toggles
farmToggle.setEnabled(false)
autoFarmToggle.setEnabled(false)
questToggle.setEnabled(true)
statsToggle.setEnabled(false)

-- Atualizar toggles
task.spawn(function()
    while task.wait(0.1) do
        if farmToggle.isEnabled() or autoFarmToggle.isEnabled() then
            getgenv().AutoFarm = true
        else
            getgenv().AutoFarm = false
        end
        
        if questToggle.isEnabled() then
            getgenv().AutoQuest = true
        else
            getgenv().AutoQuest = false
        end
        
        if statsToggle.isEnabled() then
            getgenv().AutoStats = true
        else
            getgenv().AutoStats = false
        end
    end
end)

print("✅ Script carregado!")
