-- Halloween Hub 2026 - AutoFarm até Level 2800
print("🎃 Iniciando...")

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
mainFrame.Size = UDim2.new(0, 450, 0, 400)
mainFrame.Position = UDim2.new(0.5, -225, 0.5, -200)
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
local currentTab = nil

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

-- Sistema de Quest até Level 2800
local function CheckQuest()
    local Lv = player.Data.Level.Value
    
    -- Sea 1 (Level 1-700)
    if Lv <= 10 then return "Bandit [Lv. 5]", "Bandit", "BanditQuest1", "Bandit", CFrame.new(1062.646, 16.516, 1546.552)
    elseif Lv <= 20 then return "Monkey [Lv. 14]", "Monkey", "JungleQuest", "Monkey", CFrame.new(-1601.655, 36.852, 153.388)
    elseif Lv <= 30 then return "Gorilla [Lv. 20]", "Gorilla", "JungleQuest", "Gorilla", CFrame.new(-1601.655, 36.852, 153.388)
    elseif Lv <= 40 then return "Pirate [Lv. 35]", "Pirate", "BuggyQuest1", "Pirate", CFrame.new(-1141.074, 4.100, 3831.549)
    elseif Lv <= 60 then return "Brute [Lv. 45]", "Brute", "BuggyQuest1", "Brute", CFrame.new(-1141.074, 4.100, 3831.549)
    elseif Lv <= 75 then return "Desert Bandit [Lv. 60]", "Desert Bandit", "DesertQuest", "Desert Bandit", CFrame.new(894.488, 5.140, 4392.195)
    elseif Lv <= 90 then return "Desert Officer [Lv. 70]", "Desert Officer", "DesertQuest", "Desert Officer", CFrame.new(894.488, 5.140, 4392.195)
    elseif Lv <= 110 then return "Snow Bandit [Lv. 90]", "Snow Bandit", "SnowQuest", "Snow Bandit", CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv <= 125 then return "Snowman [Lv. 100]", "Snowman", "SnowQuest", "Snowman", CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv <= 150 then return "Chief Petty Officer [Lv. 120]", "Chief Petty Officer", "MarineQuest2", "Chief Petty Officer", CFrame.new(-5039.586, 27.613, 4324.684)
    elseif Lv <= 175 then return "Sky Bandit [Lv. 150]", "Sky Bandit", "SkyQuest", "Sky Bandit", CFrame.new(-4839.530, 717.667, -2619.441)
    elseif Lv <= 200 then return "Dark Master [Lv. 175]", "Dark Master", "SkyQuest", "Dark Master", CFrame.new(-4839.530, 717.667, -2619.441)
    elseif Lv <= 225 then return "Toga Warrior [Lv. 200]", "Toga Warrior", "ColosseumQuest", "Toga Warrior", CFrame.new(-1580.745, 7.388, -2986.324)
    elseif Lv <= 250 then return "Gladiator [Lv. 225]", "Gladiator", "ColosseumQuest", "Gladiator", CFrame.new(-1580.745, 7.388, -2986.324)
    elseif Lv <= 275 then return "Military Soldier [Lv. 250]", "Military Soldier", "MagmaQuest", "Military Soldier", CFrame.new(-5316.115, 12.240, 8517.003)
    elseif Lv <= 300 then return "Military Spy [Lv. 275]", "Military Spy", "MagmaQuest", "Military Spy", CFrame.new(-5316.115, 12.240, 8517.003)
    elseif Lv <= 325 then return "Fishman Warrior [Lv. 300]", "Fishman Warrior", "FishmanQuest", "Fishman Warrior", CFrame.new(61122.562, 18.471, 1568.165)
    elseif Lv <= 350 then return "Fishman Commando [Lv. 325]", "Fishman Commando", "FishmanQuest", "Fishman Commando", CFrame.new(61122.562, 18.471, 1568.165)
    elseif Lv <= 375 then return "God's Guard [Lv. 350]", "God's Guard", "SkyExp1Quest", "God's Guard", CFrame.new(-4721.860, 843.534, -1949.966)
    elseif Lv <= 400 then return "Shanda [Lv. 375]", "Shanda", "SkyExp1Quest", "Shanda", CFrame.new(-4721.860, 843.534, -1949.966)
    elseif Lv <= 450 then return "Royal Squad [Lv. 400]", "Royal Squad", "SkyExp2Quest", "Royal Squad", CFrame.new(-7906.815, 5545.403, -427.471)
    elseif Lv <= 500 then return "Royal Soldier [Lv. 450]", "Royal Soldier", "SkyExp2Quest", "Royal Soldier", CFrame.new(-7906.815, 5545.403, -427.471)
    
    -- Sea 2 (Level 500-1500)
    elseif Lv <= 550 then return "Galley Pirate [Lv. 500]", "Galley Pirate", "MarineQuest3", "Galley Pirate", CFrame.new(-2441.219, 73.041, -3219.115)
    elseif Lv <= 600 then return "Galley Captain [Lv. 550]", "Galley Captain", "MarineQuest3", "Galley Captain", CFrame.new(-2441.219, 73.041, -3219.115)
    elseif Lv <= 650 then return "Raider [Lv. 600]", "Raider", "PirateQuest2", "Raider", CFrame.new(1126.050, 16.093, 4375.394)
    elseif Lv <= 700 then return "Mercenary [Lv. 625]", "Mercenary", "PirateQuest2", "Mercenary", CFrame.new(1126.050, 16.093, 4375.394)
    elseif Lv <= 750 then return "Swan Pirate [Lv. 675]", "Swan Pirate", "PirateQuest3", "Swan Pirate", CFrame.new(-1201.624, 7.287, 3867.555)
    elseif Lv <= 800 then return "Marine Captain [Lv. 700]", "Marine Captain", "MarineQuest4", "Marine Captain", CFrame.new(-1324.453, 14.279, 5251.195)
    elseif Lv <= 850 then return "Zombie [Lv. 750]", "Zombie", "ZombieQuest", "Zombie", CFrame.new(-1017.596, 4.792, 1391.436)
    elseif Lv <= 900 then return "Vampire [Lv. 800]", "Vampire", "ZombieQuest", "Vampire", CFrame.new(-1017.596, 4.792, 1391.436)
    elseif Lv <= 950 then return "Gunner [Lv. 850]", "Gunner", "SnowQuest", "Gunner", CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv <= 1000 then return "Musketeer [Lv. 900]", "Musketeer", "SnowQuest", "Musketeer", CFrame.new(1380.886, 5.140, -1267.758)
    elseif Lv <= 1050 then return "Tank [Lv. 950]", "Tank", "Area2Quest", "Tank", CFrame.new(638.369, 5.140, -854.087)
    elseif Lv <= 1100 then return "Mythological [Lv. 1000]", "Mythological", "Area2Quest", "Mythological", CFrame.new(638.369, 5.140, -854.087)
    elseif Lv <= 1150 then return "Winged [Lv. 1050]", "Winged", "Area3Quest", "Winged", CFrame.new(-1219.924, 4.792, -3303.152)
    elseif Lv <= 1200 then return "Cursed [Lv. 1100]", "Cursed", "Area3Quest", "Cursed", CFrame.new(-1219.924, 4.792, -3303.152)
    elseif Lv <= 1250 then return "Wraith [Lv. 1150]", "Wraith", "Area4Quest", "Wraith", CFrame.new(1114.105, 5.140, 2487.202)
    elseif Lv <= 1300 then return "Demon [Lv. 1200]", "Demon", "Area4Quest", "Demon", CFrame.new(1114.105, 5.140, 2487.202)
    elseif Lv <= 1350 then return "Dark Knight [Lv. 1250]", "Dark Knight", "Area5Quest", "Dark Knight", CFrame.new(-872.513, 14.279, -4319.683)
    elseif Lv <= 1400 then return "Dark Pirate [Lv. 1300]", "Dark Pirate", "Area5Quest", "Dark Pirate", CFrame.new(-872.513, 14.279, -4319.683)
    elseif Lv <= 1450 then return "Dragon Slayer [Lv. 1350]", "Dragon Slayer", "Area6Quest", "Dragon Slayer", CFrame.new(1282.105, 4.792, 3172.202)
    elseif Lv <= 1500 then return "Dragon Warrior [Lv. 1400]", "Dragon Warrior", "Area6Quest", "Dragon Warrior", CFrame.new(1282.105, 4.792, 3172.202)
    
    -- Sea 3 (Level 1500-2800)
    elseif Lv <= 1600 then return "Mummy [Lv. 1500]", "Mummy", "MummyQuest", "Mummy", CFrame.new(556.369, 5.140, -1854.087)
    elseif Lv <= 1700 then return "Pharaoh [Lv. 1600]", "Pharaoh", "MummyQuest", "Pharaoh", CFrame.new(556.369, 5.140, -1854.087)
    elseif Lv <= 1800 then return "Cyborg [Lv. 1700]", "Cyborg", "CyborgQuest", "Cyborg", CFrame.new(-1219.924, 4.792, -4303.152)
    elseif Lv <= 1900 then return "Robot [Lv. 1800]", "Robot", "CyborgQuest", "Robot", CFrame.new(-1219.924, 4.792, -4303.152)
    elseif Lv <= 2000 then return "Alien [Lv. 1900]", "Alien", "AlienQuest", "Alien", CFrame.new(1114.105, 5.140, 3487.202)
    elseif Lv <= 2100 then return "UFO [Lv. 2000]", "UFO", "AlienQuest", "UFO", CFrame.new(1114.105, 5.140, 3487.202)
    elseif Lv <= 2200 then return "Ghost [Lv. 2100]", "Ghost", "GhostQuest", "Ghost", CFrame.new(-872.513, 14.279, -5319.683)
    elseif Lv <= 2300 then return "Skeleton [Lv. 2200]", "Skeleton", "GhostQuest", "Skeleton", CFrame.new(-872.513, 14.279, -5319.683)
    elseif Lv <= 2400 then return "Demon Lord [Lv. 2300]", "Demon Lord", "DemonQuest", "Demon Lord", CFrame.new(1282.105, 4.792, 4172.202)
    elseif Lv <= 2500 then return "Dark Lord [Lv. 2400]", "Dark Lord", "DemonQuest", "Dark Lord", CFrame.new(1282.105, 4.792, 4172.202)
    elseif Lv <= 2600 then return "Shadow King [Lv. 2500]", "Shadow King", "ShadowQuest", "Shadow King", CFrame.new(556.369, 5.140, -2854.087)
    elseif Lv <= 2700 then return "Nightmare [Lv. 2600]", "Nightmare", "ShadowQuest", "Nightmare", CFrame.new(556.369, 5.140, -2854.087)
    elseif Lv <= 2800 then return "Hell Beast [Lv. 2700]", "Hell Beast", "HellQuest", "Hell Beast", CFrame.new(-1219.924, 4.792, -6303.152)
    end
    
    return nil, nil, nil, nil, nil
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

-- AutoFarm Loop
spawn(function()
    while task.wait() do
        if getgenv().AutoFarm then
            local char = player.Character
            if not char then continue end
            local hrp = char:FindFirstChild("HumanoidRootPart")
            if not hrp then continue end
            
            local Ms, NM, LQ, NQ, CQ = CheckQuest()
            if not Ms then continue end
            
            if getgenv().AutoQuest then
                if player.PlayerGui.Main.Quest.Visible == false then
                    TP(CQ)
                    task.wait(0.9)
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", LQ, NQ)
                elseif player.PlayerGui.Main.Quest.Visible == true then
                    for _, v in ipairs(workspace.Enemies:GetChildren()) do
                        if v.Name == Ms then
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
        if farmToggle.isEnabled() then
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
