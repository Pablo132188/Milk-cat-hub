--[[
    BLOX FRUITS HUB - HALLOWEEN 2026 EDITION
    Compatível: Delta, Xeno, Synapse, Fluxus
    Usando Rayfield Library (incluída no script)
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

-- Carregar Rayfield Library
local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/shlexware/Rayfield/main/source'))()

-- Verificar se Rayfield carregou
if not Rayfield then
    print("❌ Erro: Não foi possível carregar Rayfield!")
    return
end

print("✅ Rayfield carregado com sucesso!")

-- Criar Window
local Window = Rayfield:CreateWindow({
    Name = "🎃 Halloween Hub 2026",
    LoadingTitle = "Carregando Halloween Hub 2026...",
    LoadingSubtitle = "by NaNa Hub",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "HalloweenHub2026",
        FileName = "Config"
    },
    KeySystem = false,
    KeySettings = {
        Title = "Halloween Hub 2026",
        Subtitle = "Chave do Sistema",
        Note = "Sem chave necessária",
        Key = "Halloween2026",
        SaveKey = true
    }
})

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
        ["AutoBuyPumpkinBits"] = true,
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
        ["FruitSniper"] = true,
    },
    ["Farm"] = {
        ["AutoQuest"] = true,
        ["AutoFarmMobs"] = true,
        ["AutoFarmBoss"] = true,
        ["AutoFarmLevel"] = true,
        ["AutoFarmMoney"] = true,
        ["AutoFarmMastery"] = true,
    },
    ["Settings"] = {
        ["FPSBooster"] = true,
        ["AntiAfk"] = true,
        ["AutoHop"] = true,
        ["HopTime"] = 3000,
    },
    ["AutoChat"] = {
        ["Enabled"] = true,
        ["Content"] = {"🎃 Halloween Hub 2026", "NaNa Hub On Top"},
        ["TimeChat"] = 300,
        ["RandomChat"] = true,
    },
}

-- Criar Aba Principal
local MainTab = Window:CreateTab("🏠 Principal", 4483362458)

local MainSection = MainTab:CreateSection("Controles Principais")

local StartFarmToggle = MainTab:CreateToggle({
    Name = "Iniciar Farm",
    CurrentValue = true,
    Flag = "StartFarm",
    Callback = function(Value)
        getgenv().Config.StartFarm = Value
    end,
})

local HideUIToggle = MainTab:CreateToggle({
    Name = "Esconder UI",
    CurrentValue = false,
    Flag = "HideUI",
    Callback = function(Value)
        if Value then
            Rayfield:Destroy()
        end
    end,
})

local TeleportSection = MainTab:CreateSection("Teleports")

local TeleportSea1Button = MainTab:CreateButton({
    Name = "🌊 Teleportar Sea 1",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(500, 50, 500) -- Ilha Central casinhas
            Rayfield:Notify({
                Title = "Teleportado!",
                Content = "Sea 1 - Ilha Central (Casinhas)",
                Duration = 3,
                Image = 4483362458,
            })
        end
    end,
})

local TeleportSea2Button = MainTab:CreateButton({
    Name = "🌊 Teleportar Sea 2",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(-2000, 50, 1000) -- Frente do Café
            Rayfield:Notify({
                Title = "Teleportado!",
                Content = "Sea 2 - Frente do Café",
                Duration = 3,
                Image = 4483362458,
            })
        end
    end,
})

local TeleportSea3Button = MainTab:CreateButton({
    Name = "🌊 Teleportar Sea 3",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(3000, 50, -2000) -- Perto da Mansão
            Rayfield:Notify({
                Title = "Teleportado!",
                Content = "Sea 3 - Perto da Mansão",
                Duration = 3,
                Image = 4483362458,
            })
        end
    end,
})

-- Criar Aba Halloween
local HalloweenTab = Window:CreateTab("🎃 Halloween", 4483362458)

local HalloweenSection = HalloweenTab:CreateSection("Halloween 2026")

local HalloweenToggle = HalloweenTab:CreateToggle({
    Name = "Farm Halloween 2026",
    CurrentValue = true,
    Flag = "HalloweenEnabled",
    Callback = function(Value)
        getgenv().Config.Halloween.Enabled = Value
    end,
})

local CollectCandyToggle = HalloweenTab:CreateToggle({
    Name = "Coletar Candy Corn",
    CurrentValue = true,
    Flag = "CollectCandy",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoCollectCandy = Value
    end,
})

local HellRiderToggle = HalloweenTab:CreateToggle({
    Name = "Farm Hell Rider",
    CurrentValue = true,
    Flag = "HellRider",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoKillHellRider = Value
    end,
})

local JackOLanternToggle = HalloweenTab:CreateToggle({
    Name = "Farm Jack-O-Lanterns",
    CurrentValue = true,
    Flag = "JackOLanterns",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoFarmJackOLanterns = Value
    end,
})

local SpookyGachaToggle = HalloweenTab:CreateToggle({
    Name = "Abrir Spooky Gacha",
    CurrentValue = true,
    Flag = "SpookyGacha",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoOpenSpookyGacha = Value
    end,
})

local TrickOrTreatToggle = HalloweenTab:CreateToggle({
    Name = "Trick-or-Treat",
    CurrentValue = true,
    Flag = "TrickOrTreat",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoTrickOrTreat = Value
    end,
})

local PumpkinBitsToggle = HalloweenTab:CreateToggle({
    Name = "Farm Pumpkin Bits",
    CurrentValue = true,
    Flag = "PumpkinBits",
    Callback = function(Value)
        getgenv().Config.Halloween.AutoBuyPumpkinBits = Value
    end,
})

local HalloweenTeleportSection = HalloweenTab:CreateSection("Teleports do Evento")

local TeleportEventSea1 = HalloweenTab:CreateButton({
    Name = "🎃 Teleportar Evento Sea 1",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(500, 50, 500) -- Casinhas ilha central
        end
    end,
})

local TeleportEventSea2 = HalloweenTab:CreateButton({
    Name = "🎃 Teleportar Evento Sea 2",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(-2000, 50, 1000) -- Frente do café
        end
    end,
})

local TeleportEventSea3 = HalloweenTab:CreateButton({
    Name = "🎃 Teleportar Evento Sea 3",
    Callback = function()
        local hrp = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            hrp.CFrame = CFrame.new(3000, 50, -2000) -- Perto da mansão
        end
    end,
})

-- Criar Aba Sea Events
local SeaTab = Window:CreateTab("🌊 Sea Events", 4483362458)

local SeaSection = SeaTab:CreateSection("Sea Events")

local SeaEventsToggle = SeaTab:CreateToggle({
    Name = "Caçar Sea Events",
    CurrentValue = true,
    Flag = "SeaEvents",
    Callback = function(Value)
        getgenv().Config.SeaEvents.Enabled = Value
    end,
})

local ShipToggle = SeaTab:CreateToggle({
    Name = "Caçar Navios",
    CurrentValue = true,
    Flag = "Ships",
    Callback = function(Value)
        getgenv().Config.SeaEvents.AutoHuntShip = Value
    end,
})

local KrakenToggle = SeaTab:CreateToggle({
    Name = "Caçar Kraken",
    CurrentValue = true,
    Flag = "Kraken",
    Callback = function(Value)
        getgenv().Config.SeaEvents.AutoHuntKraken = Value
    end,
})

local SeaBeastToggle = SeaTab:CreateToggle({
    Name = "Caçar Sea Beast",
    CurrentValue = true,
    Flag = "SeaBeast",
    Callback = function(Value)
        getgenv().Config.SeaEvents.AutoHuntSeaBeast = Value
    end,
})

local TerrorSharkToggle = SeaTab:CreateToggle({
    Name = "Caçar Terror Shark",
    CurrentValue = true,
    Flag = "TerrorShark",
    Callback = function(Value)
        getgenv().Config.SeaEvents.AutoHuntTerrorShark = Value
    end,
})

local MermaidToggle = SeaTab:CreateToggle({
    Name = "Caçar Mermaid",
    CurrentValue = true,
    Flag = "Mermaid",
    Callback = function(Value)
        getgenv().Config.SeaEvents.AutoHuntMermaid = Value
    end,
})

-- Criar Aba Frutas
local FruitTab = Window:CreateTab("🍎 Frutas", 4483362458)

local FruitSection = FruitTab:CreateSection("Frutas")

local SpawnedFruitToggle = FruitTab:CreateToggle({
    Name = "Farm Frutas Spawnadas",
    CurrentValue = true,
    Flag = "SpawnedFruit",
    Callback = function(Value)
        getgenv().Config.Fruit.AutoFarmSpawnedFruit = Value
    end,
})

local AutoSpinToggle = FruitTab:CreateToggle({
    Name = "Auto Spin",
    CurrentValue = true,
    Flag = "AutoSpin",
    Callback = function(Value)
        getgenv().Config.Fruit.AutoSpinFruit = Value
    end,
})

local StoreFruitToggle = FruitTab:CreateToggle({
    Name = "Armazenar Frutas",
    CurrentValue = true,
    Flag = "StoreFruit",
    Callback = function(Value)
        getgenv().Config.Fruit.AutoStoreFruit = Value
    end,
})

local FruitSniperToggle = FruitTab:CreateToggle({
    Name = "Fruit Sniper",
    CurrentValue = true,
    Flag = "FruitSniper",
    Callback = function(Value)
        getgenv().Config.Fruit.FruitSniper = Value
    end,
})

local FruitInput = FruitTab:CreateInput({
    Name = "Fruta Específica",
    PlaceholderText = "Dragon",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        getgenv().Config.Fruit.SpecificFruit = Text
    end,
})

-- Criar Aba Farm
local FarmTab = Window:CreateTab("⚔️ Farm", 4483362458)

local FarmSection = FarmTab:CreateSection("Farm Geral")

local QuestToggle = FarmTab:CreateToggle({
    Name = "Auto Quest",
    CurrentValue = true,
    Flag = "AutoQuest",
    Callback = function(Value)
        getgenv().Config.Farm.AutoQuest = Value
    end,
})

local MobsToggle = FarmTab:CreateToggle({
    Name = "Farm Mobs",
    CurrentValue = true,
    Flag = "FarmMobs",
    Callback = function(Value)
        getgenv().Config.Farm.AutoFarmMobs = Value
    end,
})

local BossToggle = FarmTab:CreateToggle({
    Name = "Farm Boss",
    CurrentValue = true,
    Flag = "FarmBoss",
    Callback = function(Value)
        getgenv().Config.Farm.AutoFarmBoss = Value
    end,
})

local LevelToggle = FarmTab:CreateToggle({
    Name = "Farm Level",
    CurrentValue = true,
    Flag = "FarmLevel",
    Callback = function(Value)
        getgenv().Config.Farm.AutoFarmLevel = Value
    end,
})

local MoneyToggle = FarmTab:CreateToggle({
    Name = "Farm Money",
    CurrentValue = true,
    Flag = "FarmMoney",
    Callback = function(Value)
        getgenv().Config.Farm.AutoFarmMoney = Value
    end,
})

local MasteryToggle = FarmTab:CreateToggle({
    Name = "Farm Mastery",
    CurrentValue = true,
    Flag = "FarmMastery",
    Callback = function(Value)
        getgenv().Config.Farm.AutoFarmMastery = Value
    end,
})

-- Criar Aba Config
local SettingsTab = Window:CreateTab("⚙️ Config", 4483362458)

local SettingsSection = SettingsTab:CreateSection("Configurações")

local FPSBoosterToggle = SettingsTab:CreateToggle({
    Name = "FPS Booster",
    CurrentValue = true,
    Flag = "FPSBooster",
    Callback = function(Value)
        getgenv().Config.Settings.FPSBooster = Value
        if Value then
            settings().Rendering.EnableFRM = true
            settings().Rendering.FrameRateManager:SetFrameRate(60)
            for _, v in ipairs(workspace:GetDescendants()) do
                if v:IsA("ParticleEmitter") or v:IsA("Trail") or v:IsA("Fire") then
                    v.Enabled = false
                end
            end
        end
    end,
})

local AntiAfkToggle = SettingsTab:CreateToggle({
    Name = "Anti-Afk",
    CurrentValue = true,
    Flag = "AntiAfk",
    Callback = function(Value)
        getgenv().Config.Settings.AntiAfk = Value
    end,
})

local AutoHopToggle = SettingsTab:CreateToggle({
    Name = "Auto Hop",
    CurrentValue = true,
    Flag = "AutoHop",
    Callback = function(Value)
        getgenv().Config.Settings.AutoHop = Value
    end,
})

local AutoChatToggle = SettingsTab:CreateToggle({
    Name = "Auto Chat",
    CurrentValue = true,
    Flag = "AutoChat",
    Callback = function(Value)
        getgenv().Config.AutoChat.Enabled = Value
    end,
})

local ChatInput = SettingsTab:CreateInput({
    Name = "Mensagem do Chat",
    PlaceholderText = "🎃 Halloween Hub 2026",
    RemoveTextAfterFocusLost = false,
    Callback = function(Text)
        getgenv().Config.AutoChat.Content[1] = Text
    end,
})

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

-- Função para encontrar NPC do evento
local function findEventNPC(npcName)
    for _, v in ipairs(workspace:GetChildren()) do
        if v.Name:match(npcName) then
            if v:FindFirstChild("HumanoidRootPart") then
                return v
            end
        end
    end
    return nil
end

-- Loop Principal
spawn(function()
    while task.wait(0.5) do
        if not getgenv().Config.StartFarm then continue end
        
        local char = game.Players.LocalPlayer.Character
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
            
            -- Abrir Spooky Gacha
            if getgenv().Config.Halloween.AutoOpenSpookyGacha then
                local gachaNPC = findEventNPC("Spooky")
                if gachaNPC then
                    hrp.CFrame = gachaNPC.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5)
                    task.wait(0.5)
                    -- Simular clique no gacha
                    game:GetService("VirtualUser"):Button1Down()
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Up()
                end
            end
            
            -- Trick-or-Treat
            if getgenv().Config.Halloween.AutoTrickOrTreat then
                local trickNPC = findEventNPC("Trick")
                if trickNPC then
                    hrp.CFrame = trickNPC.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5)
                    task.wait(0.5)
                    game:GetService("VirtualUser"):Button1Down()
                    task.wait(0.1)
                    game:GetService("VirtualUser"):Button1Up()
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

-- Auto Chat
spawn(function()
    while task.wait(getgenv().Config.AutoChat.TimeChat) do
        if getgenv().Config.AutoChat.Enabled then
            local msg = getgenv().Config.AutoChat.Content[1]
            if getgenv().Config.AutoChat.RandomChat then
                msg = getgenv().Config.AutoChat.Content[math.random(1, #getgenv().Config.AutoChat.Content)]
            end
            game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(msg, "All")
        end
    end
end)

-- Notificação de carregamento
Rayfield:Notify({
    Title = "🎃 Halloween Hub 2026",
    Content = "Carregado com sucesso! Executor: " .. Executor,
    Duration = 5,
    Image = 4483362458,
})

print("🎃 Halloween Hub 2026 carregado com sucesso!")
print("✅ Compatível com: " .. Executor)
print("⚠️ Use em servidor privado para evitar banimento!")
