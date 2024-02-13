
    -- Wait until the game loads
    if not game:IsLoaded() then
        game.Loaded:Wait()
    end

    -- Roblox Services
    local MarketplaceService = game:GetService("MarketplaceService")
    local SoundService = game:GetService("SoundService")
    local RunService = game:GetService("RunService")
    local VirtualUser = game:GetService("VirtualUser")
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
    local ContextActionService = game:GetService("ContextActionService")
    local StarterGui = game:GetService("StarterGui")
    local UserInputService = game:GetService("UserInputService")
    local Http = game:GetService("HttpService")
    local TPS = game:GetService("TeleportService")
    local Players = game:GetService("Players")
    local PlayerGui = Players.LocalPlayer:WaitForChild("PlayerGui")
    local VirtualInputManager = game:GetService("VirtualInputManager")
    local Lighting = game:GetService("Lighting")
    local Workspace = game:GetService("Workspace")
    local Api = "https://games.roblox.com/v1/games/"

    -- Variables
    local LocalPlayer = Players.LocalPlayer
    local Character = LocalPlayer.Character
    local PlayerData
    local PlayerEffectsData = nil
    local PlaceId = game.PlaceId
    local JobId = game.JobId
    local RemoteEvents = ReplicatedStorage:WaitForChild("Remotes")
    local mt = getrawmetatable(game)
    setreadonly(mt, false)

    -- Main Script Module
    local ScriptValues = {
        ScriptVersion = "v3.1",
        ScriptOwner = "Mangnex",
        FolderName = "Lycan-X Hub",
        SettingsFile = "CoS_Loader.json",
        AutoLoadSettings = getgenv().AutoLoadConfigurations or false,
        NotificationSoundId = 1760921747,
        WarningSoundId = 3165700530,
        ErrorSoundId = 5188022160,
        SupportedExecutors = {"Synapse X", "Codex", "Delta", "Electron", "Fluxus", "Valyse"},
        ExecutorsIdentifier = {
            "Fingerprint",
            "Krnl-Fingerprint",
            "Syn-Fingerprint",
            "SW-Fingerprint",
            "Flux-Fingerprint",
            "Valyse-Fingerprint",
            "Electron-Fingerprint",
            "Delta-Figerprint"
        },
        DisconnectTypes = {{"ban", {"ban", "perm"}}, {"network", {"internet connection", "network"}}},
        AdministratorRoles = {"ðŸ’ŽAdministrator", "â­Friends/Family", "Testing", "ï¸ðŸ› ï¸Developer", "ðŸ‘‘Co-Owner", "ðŸ‘‘Owner"},
        RoleCaution = {"â¤ï¸Contributor", "ðŸ“Tester", "Community Artist", "ðŸŽ¥Content Creator"}
    }

    local GameValues = {
        Stats_Values = {
            FoodType = "Omnivore",
            Stats = "Land",
            WalkSpeed = 100,
            SprintSpeed = 100,
            TurnRadius = 1,
            FlySpeed = 0,
            BiteCooldown = 2
        },
    }

    local SelectTokens = {}

    local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
    local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
    local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

    local Options = Fluent.Options

    local Window = Fluent:CreateWindow({
        Title = "Lycan-X Hub | Cos Recode Script ".. ScriptValues.ScriptVersion .."",
        SubTitle = "by ".. ScriptValues.ScriptOwner .."",
        TabWidth = 160,
        Size = UDim2.fromOffset(580, 400),
        Acrylic = true, 
        Theme = "Dark",
        MinimizeKey = Enum.KeyCode.Q    
    })

    if not _G.AlreadyExecuted == true then
        local screenGui = Instance.new("ScreenGui")
        screenGui.Parent = game.CoreGui

        local CloseButton = Instance.new("ImageButton")
        CloseButton.Parent = screenGui
        CloseButton.Position = UDim2.new(0.01, 0, 0.3, 0)
        CloseButton.Size = UDim2.new(0, 43, 0, 43)
        CloseButton.BackgroundTransparency = 0
        CloseButton.Image = "rbxassetid://14076923102"
        CloseButton.BackgroundColor3 = Color3.new(0, 0, 0)
        CloseButton.BorderColor3 = Color3.new(1, 1, 1)
        CloseButton.ClipsDescendants = true

        local UICorner = Instance.new("UICorner")
        UICorner.Parent = CloseButton

        local UIStroke = Instance.new("UIStroke")
        UIStroke.Parent = CloseButton
        UIStroke.Thickness = 2

        CloseButton.MouseButton1Click:Connect(
            function()
                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Q, false, game)
            end
        )       
    end

    _G.AlreadyExecuted = true

    local Tabs = {
        Main = Window:AddTab({ Title = "Main", Icon = "home" }),
        CustomStats = Window:AddTab({ Title = "Custom Stats", Icon = "rocket" }),
        AutoFarm = Window:AddTab({ Title = "AutoFarm", Icon = "bot" }),
        ArtifactAutoFarm = Window:AddTab({ Title = "Artifact AutoFarm", Icon = "slack" }),
        Teleports = Window:AddTab({ Title = "Teleports", Icon = "map-pin" }),
        Event = Window:AddTab({ Title = "Event", Icon = "heart" }), --calender-clock
        Esp = Window:AddTab({ Title = "Esp", Icon = "locate-fixed" }),
        Others = Window:AddTab({ Title = "Others", Icon = "settings" }),
    }

    Tabs.Event:AddParagraph({
        Title = "Valentine Day Event (09/02/24)"
    })

    SaveManager:SetLibrary(Fluent)
    InterfaceManager:SetLibrary(Fluent)

    SaveManager:IgnoreThemeSettings()

    SaveManager:SetIgnoreIndexes({})

    Window:SelectTab(1)
    SaveManager:BuildConfigSection(Tabs.Others)

    local NotificationSound
    local WarningSound
    local ErrorSound

    NotificationSound = Instance.new("Sound")
    NotificationSound.Name = "NotificationSound"
    NotificationSound.SoundId = "rbxassetid://" .. ScriptValues.NotificationSoundId
    NotificationSound.Volume = 2
    NotificationSound.Parent = SoundService

    WarningSound = Instance.new("Sound")
    WarningSound.Name = "WarningSound"
    WarningSound.SoundId = "rbxassetid://" .. ScriptValues.WarningSoundId
    WarningSound.Volume = 2
    WarningSound.Parent = SoundService

    ErrorSound = Instance.new("Sound")
    ErrorSound.Name = "ErrorSound"
    ErrorSound.SoundId = "rbxassetid://" .. ScriptValues.ErrorSoundId
    ErrorSound.Volume = 2
    ErrorSound.Parent = SoundService

    local function Notification(SoundType, Text)
        if SoundType == "Notification" then
            NotificationSound:Play()
            Fluent:Notify({
                Title = "Notification",
                Content = Text,
                Duration = 5
            })
        elseif SoundType == "Warning" then
            WarningSound:Play()
            Fluent:Notify({
                Title = "Warning",
                Content = Text,
                Duration = 5
            })
        elseif SoundType == "Error" then
            ErrorSound:Play()
            Fluent:Notify({
                Title = "Error",
                Content = Text,
                Duration = 5
            })
        end
    end

    -- Get Creature Stats
    if Character and PlayerData then
        PlayerData = Workspace.Characters[LocalPlayer.Name].Data
        GameValues.Stats_Values.FoodType = PlayerData:GetAttribute("ft")
        GameValues.Stats_Values.Stats = PlayerData:GetAttribute("ct")
        GameValues.Stats_Values.BiteCooldown = PlayerData:GetAttribute("BiteCooldown")
        GameValues.Stats_Values.TurnRadius = PlayerData:GetAttribute("tr")
        GameValues.Stats_Values.WalkSpeed = math.round(PlayerData:GetAttribute("s"))
        GameValues.Stats_Values.SprintSpeed = math.round(PlayerData:GetAttribute("ss"))
        if PlayerData and PlayerData:GetAttribute("fs") then
            GameValues.Stats_Values.FlySpeed = math.round(PlayerData:GetAttribute("fs"))
        end
    end

    -- Functions
    local function GetPlayerData()
        pcall(
            function()
                Character = LocalPlayer.Character
                if Character then
                    PlayerData = workspace.Characters[LocalPlayer.Name].Data
                    PlayerEffectsData = Workspace.Characters[LocalPlayer.Name].Ailments
                    GameValues.Stats_Values.FoodType = PlayerData:GetAttribute("ft")
                    GameValues.Stats_Values.Stats = PlayerData:GetAttribute("ct")
                end
            end
        )
    end

    RunService.Heartbeat:Connect(GetPlayerData)

    local function AutoCollectGachaTokensTp(tokens)
        local OriginalPosition = Character.HumanoidRootPart.Position

        for i, v in ipairs(tokens) do
            local Token = Workspace.Interactions.SpawnedTokens:FindFirstChild(v)
            if Token then
                local TokenPosition = Token.Position
                Character.HumanoidRootPart.CFrame = CFrame.new(TokenPosition)
                task.wait(2)
                local TokenExists = Workspace.Interactions.SpawnedTokens:FindFirstChild(v) ~= nil
                if TokenExists then
                    VirtualInputManager:SendKeyEvent(true, "E", false, game)
                    task.wait(1)
                end
                Notification("Notification", "An " .. v .. " has been collected!")
                Character.HumanoidRootPart.CFrame = CFrame.new(OriginalPosition)
            end
        end
    end

    local function AutoCollectGachaTokensNoTp()
        for i, v in ipairs(SelectTokens) do
            local Token = Workspace.Interactions.SpawnedTokens:FindFirstChild(v)
            if Token then
                local TokenExists = Workspace.Interactions.SpawnedTokens:FindFirstChild(v) ~= nil
                if TokenExists then
                    RemoteEvents:WaitForChild("GetSpawnedTokenRemote"):InvokeServer()
                    task.wait(1)
                    Token:Destroy()
                end
                Notification("Notification", "An " .. v .. " has been collected!")
                break
            end
        end
    end

    local function NearestFood()
        local CurrentStats = GameValues.Stats_Values.Stats
        local CurrentFoodType = GameValues.Stats_Values.FoodType
        local PossibleFood = {}
        local TargetDistance = math.huge
        local Target

        if CurrentStats == "Flier" or CurrentStats == "Land" then
            if CurrentFoodType == "Carnivore" or CurrentFoodType == "Omnivore" then
                table.insert(PossibleFood, "Chunk")
                table.insert(PossibleFood, "Carnivore Carcass")
                table.insert(PossibleFood, "Carcass")
                table.insert(PossibleFood, "Herbivore Carcass")
            end
            if CurrentFoodType == "Herbivore" or CurrentFoodType == "Omnivore" then
                table.insert(PossibleFood, "Berries")
                table.insert(PossibleFood, "Grass")
                table.insert(PossibleFood, "Fruit")
            end
        elseif CurrentStats == "Aquatic" or CurrentStats == "SemiAquatic" then
            if CurrentFoodType == "Carnivore" or CurrentFoodType == "Omnivore" then
                table.insert(PossibleFood, "Ribs")
            end
            if CurrentFoodType == "Herbivore" or CurrentFoodType == "Omnivore" then
                table.insert(PossibleFood, "Seaweed Pods")
                table.insert(PossibleFood, "Algae")
            end
        end

        for i, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
            if table.find(PossibleFood, v.Name) then
                local FoodPart = v:FindFirstChild("Food")
                if FoodPart then
                    local Distance = (Character.HumanoidRootPart.Position - FoodPart.Position).Magnitude
                    local FoodValue = v:GetAttribute("Value")
                    if Distance < TargetDistance and FoodValue ~= 0 then
                        TargetDistance = Distance
                        Target = v
                    end
                end
            end
        end
        return Target
    end

    local function FindNearestPlayer()
        local GetPlayers = Players:GetPlayers()
        local TargetDistance = math.huge
        local Target

        if not Character then
            return nil
        end

        for _, v in ipairs(GetPlayers) do
            if v ~= LocalPlayer then
                local SelectedPlayer = v.Character
                if SelectedPlayer and SelectedPlayer.PrimaryPart then
                    local Distance = (Character.HumanoidRootPart.Position - SelectedPlayer.PrimaryPart.Position).Magnitude
                    if Distance < TargetDistance then
                        TargetDistance = Distance
                        Target = v
                    end
                end
            end
        end

        return Target
    end

    local function GetMail()
        local OriginalPosition = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
        local MailPosition = Vector3.new(1889, 237, 588)

        LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(MailPosition))
        
        local Mail = workspace:WaitForChild("Valentine Event", math.huge):WaitForChild("VolcanoMail", math.huge)
        
        RemoteEvents:WaitForChild("GetLetterRemote"):InvokeServer(workspace:WaitForChild("Valentine Event"):WaitForChild("VolcanoMail"))
        task.wait(0.1)       
        RemoteEvents:WaitForChild("DeliverLetterRemote"):FireServer(workspace:WaitForChild("Valentine Event"):WaitForChild("Mailbox"):WaitForChild("Mailbox"))
        
        LocalPlayer.Character:SetPrimaryPartCFrame(CFrame.new(OriginalPosition))
    end

    local playerRemovingConnection = {}
    local EspEnable = false
    local playerNameTags = {}

    function createPlayerNameTag(player)
        local character = player.Character
        if character then
            local playerNameTag = Instance.new("BillboardGui")
            playerNameTag.Name = "PlayerNameTag"
            playerNameTag.Size = UDim2.new(0, 150, 0, 60)
            playerNameTag.Adornee = character:FindFirstChild("Head")
            playerNameTag.AlwaysOnTop = true
            playerNameTag.StudsOffset = Vector3.new(0, 2, 0)

            local playerNameLabel = Instance.new("TextLabel")
            playerNameLabel.Name = "PlayerNameLabel"
            playerNameLabel.Text = player.Name
            playerNameLabel.Font = Enum.Font.FredokaOne
            playerNameLabel.FontSize = Enum.FontSize.Size12
            playerNameLabel.Size = UDim2.new(1, 0, 0.2, 0)
            playerNameLabel.TextStrokeTransparency = 0.5
            playerNameLabel.TextColor3 = Color3.new(1, 1, 1)
            playerNameLabel.BackgroundTransparency = 1
            playerNameLabel.Parent = playerNameTag

            local characterNameLabel = Instance.new("TextLabel")
            characterNameLabel.Name = "CharacterNameLabel"
            characterNameLabel.Text = "Species: " .. character.Data:GetAttribute("Species")
            characterNameLabel.Font = Enum.Font.FredokaOne
            characterNameLabel.FontSize = Enum.FontSize.Size12
            characterNameLabel.Size = UDim2.new(1, 0, 0.2, 0)
            characterNameLabel.Position = UDim2.new(0, 0, 0.25, 0)
            characterNameLabel.TextStrokeTransparency = 0.5
            characterNameLabel.TextColor3 = Color3.new(1, 1, 1)
            characterNameLabel.BackgroundTransparency = 1
            characterNameLabel.Parent = playerNameTag

            local healthLabel = Instance.new("TextLabel")
            healthLabel.Name = "HealthLabel"
            if character and character.Data:GetAttribute("h") then
                healthLabel.Text = "Health: " .. math.round(character.Data:GetAttribute("h"))
            else
                healthLabel.Text = "Health: N/A"
            end
            healthLabel.Font = Enum.Font.FredokaOne
            healthLabel.FontSize = Enum.FontSize.Size12
            healthLabel.Size = UDim2.new(1, 0, 0.2, 0)
            healthLabel.Position = UDim2.new(0, 0, 0.5, 0)
            healthLabel.TextStrokeTransparency = 0.5
            healthLabel.TextColor3 = Color3.new(1, 1, 1)
            healthLabel.BackgroundTransparency = 1
            healthLabel.Parent = playerNameTag

            playerNameTag.Parent = game.Workspace.CurrentCamera

            playerNameTags[player] = playerNameTag

            playerRemovingConnection =
                player.Removing:Connect(
                function()
                    removePlayerNameTag(player)
                    playerRemovingConnection:Disconnect()
                end
            )
        end
    end

    function removePlayerNameTag(player)
        local playerNameTag = playerNameTags[player]
        if playerNameTag then
            playerNameTag:Destroy()
            playerNameTags[player] = nil
        end
    end

    function updatePlayerNames()
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and Character then
                if EspEnable then
                    if not playerNameTags[player] then
                        createPlayerNameTag(player)
                    end
                elseif playerNameTags[player] then
                    removePlayerNameTag(player)
                end
            elseif playerNameTags[player] then
                removePlayerNameTag(player)
            end
        end
    end

    function updatePlayerNames()
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and Character then
                if EspEnable then
                    if not playerNameTags[player] then
                        createPlayerNameTag(player)
                    end
                elseif playerNameTags[player] then
                    removePlayerNameTag(player)
                end
            elseif playerNameTags[player] then
                removePlayerNameTag(player)
            end
        end
    end

    local function FPSCount()
        Back = Drawing.new("Square")
        Back.Color = Color3.fromRGB(20, 20, 20)
        Back.Position =
            Vector2.new(
            game:GetService("Workspace").CurrentCamera.ViewportSize.X / 2.24,
            game:GetService("Workspace").CurrentCamera.ViewportSize.Y / 1000
        )
        Back.Size = Vector2.new(180, 35)
        Back.Transparency = 0.5
        Back.Visible = true
        Back.Filled = true

        Fps = Drawing.new("Text")
        Fps.Text = ""
        Fps.Color = Color3.fromRGB(200, 200, 200)
        Fps.Position =
            Vector2.new(
            game:GetService("Workspace").CurrentCamera.ViewportSize.X / 2.22,
            game:GetService("Workspace").CurrentCamera.ViewportSize.Y / 1000
        )
        Fps.Size = 30
        Fps.Visible = true
        game.Stats:WaitForChild("Network")
        game.Stats.Network:WaitForChild("ServerStatsItem")
        game.Stats.Network.ServerStatsItem:WaitForChild("Data Ping")

        while wait(0.1) do
            ping = string.split(string.split(game.Stats.Network.ServerStatsItem["Data Ping"]:GetValueString(), " ")[1], ".")
            fps = string.split(game.Stats.Workspace.Heartbeat:GetValueString(), ".")
            Fps.Text = "FPS " .. fps[1] .. "  Ping " .. ping[1]
            if tonumber(fps[1]) < 40 then
                Fps.Color = Color3.fromRGB(255, 100, 100)
            end
            if tonumber(ping[1]) and tonumber(ping[1]) > 400 then
                Fps.Color = Color3.fromRGB(255, 40, 40)
            end
            if tonumber(fps[1]) > 40 and tonumber(ping[1]) and tonumber(ping[1]) < 400 then
                Fps.Color = Color3.fromRGB(200, 200, 200)
            end
        end
    end

    -- UI Variables
    local AutoMudRollValue
    local AutoEatValue
    local AutoDrinkValue
    local AutoGachaTokensNoTpValue
    local AutoGachaTokensTpValue
    local AutoHideValue
    local AutoMissionsValue
    local NoMeteorDamageValue
    local InfStaminaValue
    local NoLavaDamageValue
    local NoDrowningDamageValue
    local InstReturnValue = false
    local HWCompleted = false
    local AWCompleted = false
    local GWCompleted = false
    local VWCompleted = false
    local BWCompleted = false
    local EWCompleted = false
    local NWCompleted = false
    local ARWCompleted = false
    local ReviveCreatures = {}
    local FoodNames = {"Carnivore Carcass", "Herbivore Carcass", "Omnivore Carcass", "Chunk", "Carcass"}

    local ReviveAllDeadCreatures = Tabs.Main:AddButton({
        Title = "Revive All Dead Creatures", 
        Description = "Using this function will reset the creature's death stat!",
        Callback = function()
            local DataFolder = PlayerGui.Data
            local SlotsFrame = PlayerGui.SaveSelectionGui.ContainerFrame.AllSlotsFrame.SlotsFrame

            local Slots = {"Slot1", "Slot2", "Slot3"}
            local DeadCreatures = 0

            for i = 1, 3 do
                local Slot = SlotsFrame[tostring(i)]
                local CreatureFrame = Slot.InnerFrame.CreatureFrame
                local CreatureName = CreatureFrame.NameLabel.Text
                local HealthFrame = Slot.InnerFrame.CreatureFrame.StatsFrame.Health
                local MaxHealth = HealthFrame.Max.Text:gsub("/", "")
            
                if CreatureFrame.Visible == true then
                    local creatureData = {
                        Name = CreatureName,
                        MaxHealth = tonumber(MaxHealth),
                    }
            
                    table.insert(ReviveCreatures, creatureData)
                end
            end 
            
            local function CheckDeadCreature(Data)
                local Dino = Data:FindFirstChild("Dino")
                local Health = Data:FindFirstChild("Health")
            
                if Dino then
                    for _, v in ipairs(ReviveCreatures) do
                        if Dino.Value == v.Name and Health.Value == 0 then
                            Health.Value = v.MaxHealth
                            DeadCreatures = DeadCreatures + 1
                        end
                    end
                end
            end
            
            for _, Slots in pairs(DataFolder.Slots:GetChildren()) do
                CheckDeadCreature(Slots)
            end
            
            for _, Slot in pairs(Slots) do
                local CreatureSlots = DataFolder[Slot]
            
                if CreatureSlots then
                    CheckDeadCreature(CreatureSlots)
                end
            end        

            if DeadCreatures > 0 then
                Notification("Notification", "" .. DeadCreatures .. " creatures were successfully revived!")
            else
                Notification("Error", "There are no dead creatures!")
            end
    end})

    local AutoBreakChocolatePile = Tabs.Event:AddToggle(
        "AutoBreakChocolatePile",{
        Title = "Auto Break Chocolate Pile (No Tp)", 
        Description = "Automatically complete the Chocolate Minigame",
        Default = false, 
        Callback = function(state)
            AutoBreakChocolatePileValue = state
            task.spawn(
                function()
                    while AutoBreakChocolatePileValue do
                        task.wait(1)
                        for i = 1, 40 do
                            RemoteEvents:WaitForChild("CompleteForageableRemote"):InvokeServer(i)
                            task.wait()
                        end
                    end
                end
            )
    end})

    local AutoMailDeliver = Tabs.Event:AddToggle(
        "AutoMailDeliver",{
        Title = "Auto Mail Deliver (Tp)", 
        Description = "Automatically complete Mail Minigame",
        Default = false, 
        Callback = function(state)
            AutoMailDeliverValue = state
            task.spawn(
                function()
                    while AutoMailDeliverValue do
                        task.wait(1)
                        pcall(
                            function()
                                local Mail = workspace:WaitForChild("Valentine Event"):FindFirstChild("VolcanoMail")                                
                                if Mail then
                                    if PlayerGui.Data.Valentines_2024.LovelyLetter.LastCompleted.Value + 60 < os.time(os.date("!*t")) then  
                                        for _, v in ipairs(workspace["Valentine Event"]:GetChildren()) do
                                            if v:IsA("MeshPart") and v.Name:sub(-4) == "Mail" then
                                                RemoteEvents:WaitForChild("GetLetterRemote"):InvokeServer(v)
                                                task.wait(0.1)                                     
                                                RemoteEvents:WaitForChild("DeliverLetterRemote"):FireServer(workspace:WaitForChild("Valentine Event"):WaitForChild("Mailbox"):WaitForChild("Mailbox"))
                                                break
                                            end
                                        end                                   
                                    end
                                else
                                    GetMail()
                                end
                            end
                        )
                    end
                end
            )
    end})

    local GetMaxStorageSlots = Tabs.ArtifactAutoFarm:AddButton({
        Title = "Load Warden Autofarm GUI", 
        Description = "If you have previously activated this function, DO NOT activate it again!",
        Callback = function()
            if not _G.WardenAutofarmEnabled == true then
            VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.Q, false, game)
            local screenGui = Instance.new("ScreenGui")
            screenGui.Parent = game.CoreGui

            local CloseButton = Instance.new("ImageButton")
            CloseButton.Parent = screenGui
            CloseButton.Position = UDim2.new(0.01, 0, 0.4, 0)
            CloseButton.Size = UDim2.new(0, 43, 0, 43)
            CloseButton.BackgroundTransparency = 0
            CloseButton.Image = "rbxassetid://12974429433"
            CloseButton.BackgroundColor3 = Color3.new(0, 0, 0)
            CloseButton.BorderColor3 = Color3.new(1, 1, 1)
            CloseButton.ClipsDescendants = true

            local UICorner = Instance.new("UICorner")
            UICorner.Parent = CloseButton

            local UIStroke = Instance.new("UIStroke")
            UIStroke.Parent = CloseButton
            UIStroke.Thickness = 2

            CloseButton.MouseButton1Click:Connect(
                function()
                    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.RightShift, false, game)
                end
            ) 

            local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

            local Window = OrionLib:MakeWindow({Name = "Premium Warden AutoFarm", HidePremium = true, SaveConfig = ScriptValues.AutoLoadSettings, ConfigFolder = ScriptValues.FolderName, IntroEnabled = false})

            local AutoFarm = Window:MakeTab({
                Name = "AutoFarm",
                Icon = "rbxassetid://12974429433",
                PremiumOnly = false
            })

            local WSAF = AutoFarm:AddSection({
                Name = "Warden Shrine AutoFarm"
            })

            local FoodDebuged = {}

            local DebugFood = AutoFarm:AddButton({
                Name = "Debug Food (TP)",
                Callback = function()
                    local OriginalPosition = LocalPlayer.Character.HumanoidRootPart.CFrame 

                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                        if table.find(FoodNames, v.Name) then
                            local FoodValue = v:GetAttribute("Value")
                            if FoodValue > 100 and not FoodDebuged[v] then
                                FoodDebuged[v] = true 
                                LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(v.WorldPivot.Position)
                                RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                task.wait(1)
                                RemoteEvents:WaitForChild("Food"):FireServer(v)
                                wait(1)
                            end
                        end
                    end
                    
                    LocalPlayer.Character.HumanoidRootPart.CFrame = OriginalPosition
                    FoodDebuged = {}
                end    
            })

            local HellionWarden = AutoFarm:AddToggle({
                Name = "Auto Hellion Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoHellion = state
                    task.spawn(function()
                        while AutoHellion do
                            task.wait(0.1)
                            pcall(function()
                                if not HWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoHellion and not HWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()               
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Hellion")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoHellion and not HWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Hellion")
                                        end
                                    end 
                                end
                            end)
                        end
                    end)
                end    
            })

            local HWStatus = AutoFarm:AddLabel("Status: Avaible")
            local HWProgress = AutoFarm:AddLabel("Progress: 0/50")

            local AngelicWarden = AutoFarm:AddToggle({
                Name = "Auto Angelic Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoAngelic = state
                    task.spawn(function()
                        while AutoAngelic do
                            task.wait(0.1)
                            pcall(function()
                                if not AWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoAngelic and not AWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Angelic")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoAngelic and not AWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Angelic")
                                        end
                                    end 
                                end
                            end)
                        end
                    end)
                end    
            })

            local AWStatus = AutoFarm:AddLabel("Status: Avaible")
            local AWProgress = AutoFarm:AddLabel("Progress: 0/150")

            local GarraWarden = AutoFarm:AddToggle({
                Name = "Auto Garra Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoGarra = state
                    task.spawn(function()
                        while AutoGarra do
                            task.wait(0.1)
                            pcall(function()
                                if not GWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoGarra and not GWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Garra")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoGarra and not GWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Garra")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local GWStatus = AutoFarm:AddLabel("Status: Avaible")
            local GWProgress = AutoFarm:AddLabel("Progress: 0/250")

            local VerdantWarden = AutoFarm:AddToggle({
                Name = "Auto Verdant Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoVerdant = state
                    task.spawn(function()
                        while AutoVerdant do
                            task.wait(0.1)
                            pcall(function()
                                if not VWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoVerdant and not VWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Verdant")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoVerdant and not VWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Verdant")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local VWStatus = AutoFarm:AddLabel("Status: Avaible")
            local VWProgress = AutoFarm:AddLabel("Progress: 0/500")

            local BorealWarden = AutoFarm:AddToggle({
                Name = "Auto Boreal Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoBoreal = state
                    task.spawn(function()
                        while AutoBoreal do
                            task.wait(0.1)
                            pcall(function()
                                if not BWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoBoreal and not BWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Boreal")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoBoreal and not BWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Boreal")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local BWStatus = AutoFarm:AddLabel("Status: Avaible")
            local BWProgress = AutoFarm:AddLabel("Progress: 0/750")

            local EigionWarden = AutoFarm:AddToggle({
                Name = "Auto Eigion Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoEigion = state
                    task.spawn(function()
                        while AutoEigion do
                            task.wait(0.1)
                            pcall(function()
                                if not EWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoEigion and not EWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Eigion")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoEigion and not EWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Eigion")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local EWStatus = AutoFarm:AddLabel("Status: Avaible")
            local EWProgress = AutoFarm:AddLabel("Progress: 0/1000")

            local NovusWarden = AutoFarm:AddToggle({
                Name = "Auto Novus Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoNovus = state
                    task.spawn(function()
                        while AutoNovus do
                            task.wait(0.1)
                            pcall(function()
                                if not NWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoNovus and not NWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Novus")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoNovus and not NWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Novus")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local NWStatus = AutoFarm:AddLabel("Status: Avaible")
            local NWProgress = AutoFarm:AddLabel("Progress: 0/1500")

            local ArdorWarden = AutoFarm:AddToggle({
                Name = "Auto Ardor Warden Sacrifice",
                Default = false,
                Callback = function(state)
                    local AutoArdor = state
                    task.spawn(function()
                        while AutoArdor do
                            task.wait(0.1)
                            pcall(function()
                                if not ARWCompleted then
                                    for _, v in ipairs(Workspace.Interactions.Food:GetChildren()) do
                                        if v.Name == "Carcass" and AutoArdor and not ARWCompleted then
                                            RemoteEvents:WaitForChild("FoodChunk"):FireServer(v)
                                            task.wait()                  
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Ardor")
                                        elseif v:IsA("Model") and table.find(FoodNames, v.Name) and AutoArdor and not ARWCompleted then         
                                            RemoteEvents:WaitForChild("FoodPickup"):FireServer(v)
                                            task.wait()
                                            RemoteEvents:WaitForChild("WardenOffering"):InvokeServer("Ardor")
                                        end
                                    end
                                end
                            end)
                        end
                    end)
                end    
            })

            local ARWStatus = AutoFarm:AddLabel("Status: Avaible")
            local ARWProgress = AutoFarm:AddLabel("Progress: 0/2500")

            local WS = {
                ["Hellion"] = HWStatus,
                ["Angelic"] = AWStatus,
                ["Garra"] = GWStatus,
                ["Verdant"] = VWStatus,
                ["Boreal"] = BWStatus,
                ["Eigion"] = EWStatus,
                ["Novus"] = NWStatus,
                ["Ardor"] = ARWStatus
            }

            local WP = {
                ["Hellion"] = HWProgress,
                ["Angelic"] = AWProgress,
                ["Garra"] = GWProgress,
                ["Verdant"] = VWProgress,
                ["Boreal"] = BWProgress,
                ["Eigion"] = EWProgress,
                ["Novus"] = NWProgress,
                ["Ardor"] = ARWProgress
            }

            local WMV = {
                ["Hellion"] = 50,
                ["Angelic"] = 150,
                ["Garra"] = 250,
                ["Verdant"] = 500,
                ["Boreal"] = 750,
                ["Eigion"] = 1000,
                ["Novus"] = 1500,
                ["Ardor"] = 2500,
            }

            _G.WardenAutofarmEnabled = true

            task.spawn(function()
                while true do
                    task.wait(1)
                    pcall(function()
                        for _, v in pairs(PlayerGui.Data.WardenShrines.Cooldowns:GetChildren()) do
                            local WSN = v.Name
                            local WC = v.Value
                            local CT = os.time()
                        
                            local WN = WSN:match("^(.-)LastCompleted$") or ""

                            local TC = WC + (30 * 60)
                        
                            if WC == 0 or TC <= CT then
                                if WS[WN] then
                                    WS[WN]:Set("Status: Avaible")
                                    WP[WN]:Set("Progress: ".. PlayerGui.Data.WardenShrines.ShrineValues[WN].Value .."/".. WMV[WN] .."")
                                    if WN == "Hellion" then
                                        HWCompleted = false
                                    elseif WN == "Garra" then
                                        GWCompleted = false
                                    elseif WN == "Verdant" then
                                        VWCompleted = false
                                    elseif WN == "Angelic" then
                                        AWCompleted = false
                                    elseif WN == "Boreal" then
                                        BWCompleted = false
                                    elseif WN == "Eigion" then
                                        EWCompleted = false
                                    elseif WN == "Novus" then
                                        NWCompleted = false
                                    elseif WN == "Ardor" then
                                        ARWCompleted = false
                                    end
                                end
                            else
                                if TC > CT then
                                    if WS[WN] then
                                        WS[WN]:Set("Status: On Coldown (".. (TC - CT) .." seconds)")
                                        WP[WN]:Set("Progress: Completed")
                                        if WN == "Hellion" then
                                            HWCompleted = true
                                        elseif WN == "Garra" then
                                            GWCompleted = true
                                        elseif WN == "Verdant" then
                                            VWCompleted = true
                                        elseif WN == "Angelic" then
                                            AWCompleted = true
                                        elseif WN == "Boreal" then
                                            BWCompleted = true
                                        elseif WN == "Eigion" then
                                            EWCompleted = true
                                        elseif WN == "Novus" then
                                            NWCompleted = true
                                        elseif WN == "Ardor" then
                                            ARWCompleted = true
                                        end
                                    end
                                end
                            end
                        end
                    end)
                end
            end)
            end
    end})

    local GetMaxStorageSlots = Tabs.Main:AddButton({
        Title = "Get Max Storage Slots", 
        Description = "Resets when you leave EXCEPT for the creatures you stored!",
        Callback = function()
            PlayerGui.Data.StorageCap.Value = 13
    end})


    local InstantReturnLobby = Tabs.Main:AddToggle(
        "AInstantLobbyReturn",{
        Title = "Instant Lobby Return", 
        Description = "No cooldown when returning to the lobby!",
        Default = false, 
        Callback = function(state)
            InstReturnValue = state
    end})

    PlayerGui.HUDGui.SideFrame.Other.ButtonsFrame.Return.UpperLabel.MouseButton1Click:Connect(
        function()
            if InstReturnValue == true then
                Character.HumanoidRootPart.CFrame = CFrame.new(9999999999, 197, 990) 
            end
        end
    )

    local AutoScentHidden = Tabs.Main:AddToggle(
        "AutoScentHidden",{
        Title = "Auto Scent Hidden", 
        Description = "Prevent other players from sniffing your creature!",
        Default = false, 
        Callback = function(state)
            AutoHideValue = state
            task.spawn(
                function()
                    while AutoHideValue do
                        task.wait(0.1)
                        pcall(
                            function()
                                if PlayerEffectsData and not PlayerEffectsData:GetAttribute("HideScent") then
                                    RemoteEvents:WaitForChild("HideScent"):FireServer()
                                end
                            end
                        )
                    end
                end
            )
    end})

    local InfiniteStamina = Tabs.Main:AddToggle(
        "InfiniteStamina",{
        Title = "Infinite Stamina", 
        Description = "You will never get tired again!",
        Default = false, 
        Callback = function(state)
            InfStaminaValue = state
            task.spawn(
                function()
                    while InfStaminaValue do
                        task.wait()
                        pcall(
                            function()
                                if PlayerData then
                                    PlayerData:SetAttribute("st", 99999999999999999999999999999999999)
                                    PlayerData:SetAttribute("sr", 99999999999999999999999999999999999)
                                end
                            end
                        )
                    end
                end
            )
    end})

    local NoLavaDamage = Tabs.Main:AddToggle(
        "NoLavaDamage",{
        Title = "No Lava Damage",
        Description = "Allows you to step on the lava on Volcano Island without taking damage!", 
        Default = false, 
        Callback = function(state)
            NoLavaDamageValue = state

            local namecall = mt.__namecall
            mt.__namecall =
                newcclosure(
                function(self, ...)
                    local method = getnamecallmethod()
                    local args = {...}

                    if method == "FireServer" and tostring(self) == "LavaSelfDamage" and NoLavaDamageValue then
                        return
                    end
                    return namecall(self, table.unpack(args))
                end
            )
    end})

    local NoDrowningDamage = Tabs.Main:AddToggle(
        "NoDrowningDamage",{
        Title = "No Drowning Damage", 
        Description = "Even if your Oxygen is 0 you won't take damage!",
        Default = false, 
        Callback = function(state)
            NoDrowningDamageValue = state

            local BlockRemoteEvent = {
                "OxygenRemote",
                "DrownRemote",
            }

            local namecall = mt.__namecall
            mt.__namecall =
                newcclosure(
                function(self, ...)
                    local method = getnamecallmethod()
                    local args = {...}

                    if method == "FireServer" and table.find(BlockRemoteEvent, tostring(self)) and NoDrowningDamageValue then
                        return
                    end
                    return namecall(self, table.unpack(args))
                end
            )
    end})

    local NoMeteorDamage = Tabs.Main:AddToggle(
        "NoMeteorDamage",{
        Title = "No Meteor Damage", 
        Description = "Prevents you from losing health if a meteor falls on you!",
        Default = false, 
        Callback = function(state)
            NoMeteorDamageValue = state
            local BlockRemoteEvent = {
                "MeteorSelfDamage",
                "RequestMeteors",
                "MeteorFlySelfDamage"
            }

            local namecall = mt.__namecall
            mt.__namecall =
                newcclosure(
                function(self, ...)
                    local method = getnamecallmethod()
                    local args = {...}

                    if method == "FireServer" and table.find(BlockRemoteEvent, tostring(self)) and NoMeteorDamageValue then
                        return
                    end
                    return namecall(self, table.unpack(args))
                end
            )
    end})

    local AutoEat = Tabs.AutoFarm:AddToggle(
        "AutoEat",{
        Title = "Auto Eat", 
        Default = false, 
        Callback = function(state)
            AutoEatValue = state
            local AutoEatActive = false
            local OriginalFood
            local OriginalPosition
            if AutoEatValue then
                task.spawn(
                    function()
                        while AutoEatValue do
                            task.wait(1)
                            pcall(
                                function()
                                    if PlayerGui.HUDGui.BottomFrame.Other.Hunger.HoverLabel.Text ~= "100%" then
                                        local Food = NearestFood()
                                        if OriginalFood ~= Food then
                                            OriginalFood = Food
                                            AutoEatActive = true
                                        end

                                        if Food then
                                            if Food:GetAttribute("Value") == 0 then
                                                OriginalFood = nil
                                            else
                                                local FoodPosition = Food.Food.Position
                                                if not OriginalPosition then
                                                    OriginalPosition = Character.HumanoidRootPart.Position
                                                end
                                                Character.HumanoidRootPart.CFrame = CFrame.new(FoodPosition)
                                                repeat
                                                    task.wait()
                                                    RemoteEvents:WaitForChild("Food"):FireServer(Food)
                                                    Character.HumanoidRootPart.CFrame = CFrame.new(FoodPosition)
                                                until PlayerGui.HUDGui.BottomFrame.Other.Hunger.HoverLabel.Text == "100%" or
                                                    not AutoEatValue or
                                                    AutoEatActive == false or
                                                    Food:GetAttribute("Value") == 0
                                                if PlayerGui.HUDGui.BottomFrame.Other.Hunger.HoverLabel.Text == "100%" then
                                                    Character.HumanoidRootPart.CFrame = CFrame.new(OriginalPosition)
                                                    OriginalPosition = nil
                                                    AutoEatActive = false
                                                end
                                            end
                                        else
                                            OriginalFood = nil
                                        end
                                    else
                                        OriginalFood = nil
                                    end
                                end
                            )
                        end
                    end
                )
            end  
    end})

    local AutoDrink = Tabs.AutoFarm:AddToggle(
        "AutoDrink",{
        Title = "Auto Drink", 
        Default = false, 
        Callback = function(state)
            AutoDrinkValue = state
            task.spawn(
                function()
                    while AutoDrinkValue do
                        task.wait()
                        pcall(
                            function()
                                if PlayerGui.HUDGui.BottomFrame.Other.Thirst.HoverLabel.Text ~= "100%" then
                                    game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("DrinkRemote"):FireServer(
                                        workspace:WaitForChild("Interactions"):WaitForChild("Lakes"):WaitForChild("Lake")
                                    )
                                end
                            end
                        )
                    end
                end
            )
    end})

    local AutoMudRoll = Tabs.AutoFarm:AddToggle(
        "AutoMudRoll",{
        Title = "Auto Mud Roll", 
        Default = false, 
        Callback = function(state)
            AutoMudRollValue = state
            local OriginalPosition

            local function teleportToMud()
            while AutoMudRollValue do
                local Target = nil
                local TargetDistance = math.huge
    
                for i, v in ipairs(workspace.Interactions:GetChildren()) do
                    if v.Name == "Mud" then
                        local Distance = (LocalPlayer.Character.HumanoidRootPart.Position - v.Position).Magnitude
                        if Distance < TargetDistance then
                        TargetDistance = Distance
                        Target = v
                        end
                    end
                end
    
                if Target and AutoMudRollValue then
                    local MudPosition = Target.Position + Vector3.new(0, Target.Size.Y / 2, 0)
                    if not OriginalPosition then
                        OriginalPosition = LocalPlayer.Character.HumanoidRootPart.Position
                    end
    
                    repeat
                        task.wait()
                        LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(MudPosition)
                        RemoteEvents.Mud:FireServer(Target)
                    until PlayerEffectsData:GetAttribute("Muddy")
                    task.wait()
                    if PlayerEffectsData and PlayerEffectsData:GetAttribute("Muddy") then
                        LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(OriginalPosition)
                        OriginalPosition = nil
                        break
                    end
                else
                    break
                end
                if not PlayerEffectsData or not PlayerEffectsData:GetAttribute("Muddy") then
                    teleportToMud()
                end
            end
            end
    
            task.spawn(function()
            while AutoMudRollValue do
                task.wait()
                pcall(function()
                    if not PlayerEffectsData or not PlayerEffectsData:GetAttribute("Muddy") then
                        teleportToMud()
                    end
                end)
            end
            end)
    end})

    local SelectTokensType = Tabs.AutoFarm:AddDropdown("SelectTokensType", {
        Title = "Types tokens to collect",
        Description = "You can select what type of tokens are collected automatically!",
        Values = {"Photovore Tokens", "Galaxy Tokens", "Monster Tokens", "Sweet Tokens", "Mecha Tokens"},
        Multi = true,
        Default = {"Photovore Tokens", "Galaxy Tokens", "Monster Tokens", "Sweet Tokens", "Mecha Tokens"},
    })

    SelectTokensType:OnChanged(function(Value)
        SelectTokens = {}
        for Value, State in next, Value do
            if Value == "Photovore Tokens" then
                table.insert(SelectTokens, "ExplorerGachaToken")
            elseif Value == "Galaxy Tokens" then
                table.insert(SelectTokens, "GalaxyExplorerGachaToken")
            elseif Value == "Monster Tokens" then
                table.insert(SelectTokens, "MonsterExplorerGachaToken")
            elseif Value == "Sweet Tokens" then
                table.insert(SelectTokens, "SweetExplorerGachaToken")
            elseif Value == "Mecha Tokens" then
                table.insert(SelectTokens, "MutateExplorerGachaToken")
            end
        end
    end)

    local AutoFarmAllGachTokensNoTp = Tabs.AutoFarm:AddToggle(
        "AutoFarmAllGachTokensNoTp",{
        Title = "AutoFarm Gacha Tokens", 
        Description = "Automatically collect all tokens and notify you when it collects them!",
        Default = false, 
        Callback = function(state)
            AutoGachaTokensTpValue = state
            task.spawn(
                function()
                    while AutoGachaTokensTpValue do
                        task.wait()
                        pcall(
                            function()
                                AutoCollectGachaTokensNoTp()
                            end
                        )
                    end
                end
            )
    end})

    local AutoFarmAllGachTokensNoTp = Tabs.AutoFarm:AddToggle(
        "AutoFarmAllGachTokensNoTp",{
        Title = "Auto Complete Current Mision", 
        Description = "Automatically complete the mission for the region you are in!",
        Default = false, 
        Callback = function(state)
            AutoMissionsValue = state
            task.spawn(function()
                while AutoMissionsValue do
                    task.wait()
                    pcall(function()
                        local CurrentRegion = PlayerGui.HUDGui.SideFrame.Other.MinimapFrame.Region.Text:gsub(
                            "(%a)([%w_']*)",
                            function(first, rest)
                                return first:upper() .. rest:lower()
                            end
                        )

                        local CurrentMission = PlayerGui.Data.Missions.RegionMissions:FindFirstChild(CurrentRegion)

                        if CurrentMission then
                            if not CurrentMission.AttackCreature.Value then
                                Options.AutoScentHidden:SetValue(AutoMissionsValue)
                                Character.HumanoidRootPart.CFrame = CFrame.new(FindNearestPlayer().Character.PrimaryPart.Position)
                                local args = {
                                    [1] = {
                                        [1] = FindNearestPlayer().Character
                                    }
                                }
                                
                                game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("CharactersDamageRemote"):FireServer(unpack(args))
                                
                            end
                            if not CurrentMission.DrinkWater.Value then
                                Options.AutoDrink:SetValue(AutoMissionsValue)
                            else
                                Options.AutoDrink:SetValue(false)
                            end
                            if not CurrentMission.EatFood.Value then
                                Options.AutoEat:SetValue(AutoMissionsValue)
                            else
                                Options.AutoEat:SetValue(false)
                            end
                            if not CurrentMission.Sniff.Value then
                                RemoteEvents.SetMissionRemote:FireServer(1)
                            end
                            if not CurrentMission.ConcealScent.Value then
                                Options.AutoMudRoll:SetValue(AutoMissionsValue)
                            else
                                Options.AutoMudRoll:SetValue(false)
                            end
                        else
                            Options.AutoMudRoll:SetValue(false)
                            Options.AutoEat:SetValue(false)
                            Options.AutoDrink:SetValue(false)
                            Options.AutoScentHidden:SetValue(true)
                        end
                    end)
                end
            end)  
    end})

    local BiteCooldown = Tabs.CustomStats:AddSlider("Bite Cooldown", {
        Title = "Bite Cooldown",
        Default = GameValues.Stats_Values.BiteCooldown,
        Min = 0,
        Max = 10,
        Rounding = 1,
        Callback = function(BiteCooldownValue)
            GameValues.Stats_Values.BiteCooldown = BiteCooldownValue
        end
    })

    local OriginalBiteCooldown

    local SetBiteCooldown = Tabs.CustomStats:AddToggle(
        "SetBiteCooldown",{
        Title = "Enable Custom Bite Cooldown", 
        Description = "Activating this modifies your Stat, if you deactivate it it will return to its original value",
        Default = false, 
        Callback = function(state)
            ActiveBiteCooldown = state

            if ActiveBiteCooldown and PlayerData and PlayerData:GetAttribute("BiteCooldown") then
                OriginalBiteCooldown = PlayerData:GetAttribute("BiteCooldown")
            end

            task.spawn(function()
                while ActiveBiteCooldown do
                    task.wait()
                    pcall(function()
                        if PlayerData and PlayerData:GetAttribute("BiteCooldown") then
                            PlayerData:SetAttribute('BiteCooldown', GameValues.Stats_Values.BiteCooldown)
                        end
                    end)
                end

                PlayerData:SetAttribute('BiteCooldown', OriginalBiteCooldown)
            end)
    end})

    local TurnRadius = Tabs.CustomStats:AddSlider("TurnRadius", {
        Title = "Turn Radius",
        Default = GameValues.Stats_Values.TurnRadius,
        Min = 0,
        Max = 10,
        Rounding = 1,
        Callback = function(TurnRadiusValue)
            GameValues.Stats_Values.TurnRadius = TurnRadiusValue
        end
    })

    local OriginalTurnRadius

    local SetTurnRadius = Tabs.CustomStats:AddToggle(
        "SetTurnRadius",{
        Title = "Enable Custom Turn Radius", 
        Description = "Activating this modifies your Stat, if you deactivate it it will return to its original value",
        Default = false, 
        Callback = function(state)
            ActiveTurnRadius = state

            if ActiveTurnRadius and PlayerData and PlayerData:GetAttribute("tr") then
                OriginalTurnRadius = PlayerData:GetAttribute("tr")
            end

            task.spawn(function()
                while ActiveTurnRadius do
                    task.wait()
                    pcall(function()
                        if PlayerData and PlayerData:GetAttribute("tr") then
                            PlayerData:SetAttribute('tr', GameValues.Stats_Values.TurnRadius)
                        end
                    end)
                end

                PlayerData:SetAttribute('tr', OriginalTurnRadius)
            end)
    end})

    local WalkSpeed = Tabs.CustomStats:AddSlider("WalkSpeed", {
        Title = "Walk Speed",
        Default = GameValues.Stats_Values.WalkSpeed,
        Min = 0,
        Max = 500,
        Rounding = 1,
        Callback = function(WalkSpeedValue)
            GameValues.Stats_Values.WalkSpeed = WalkSpeedValue
        end
    })

    local OriginalWalkSpeed

    local SetWalkSpeed = Tabs.CustomStats:AddToggle(
        "SetWalkSpeed",{
        Title = "Enable Custom Walk Speed", 
        Description = "Activating this modifies your Stat, if you deactivate it it will return to its original value",
        Default = false, 
        Callback = function(state)
            ActiveWalkSpeed = state

            if ActiveWalkSpeed and PlayerData and PlayerData:GetAttribute("s") then
                OriginalWalkSpeed = PlayerData:GetAttribute("s")
            end

            task.spawn(function()
                while ActiveWalkSpeed do
                    task.wait()
                    pcall(function()
                        if PlayerData and PlayerData:GetAttribute("s") then
                            PlayerData:SetAttribute('s', GameValues.Stats_Values.WalkSpeed)
                        end
                    end)
                end

                PlayerData:SetAttribute('s', OriginalWalkSpeed)
            end)
    end})

    local SprintSpeed = Tabs.CustomStats:AddSlider("SprintSpeed", {
        Title = "Sprint Speed",
        Default = GameValues.Stats_Values.SprintSpeed,
        Min = 0,
        Max = 500,
        Rounding = 1,
        Callback = function(SprintSpeedValue)
            GameValues.Stats_Values.SprintSpeed = SprintSpeedValue
        end
    })

    local OriginalSprintSpeed

    local SetSprintSpeed = Tabs.CustomStats:AddToggle(
        "SetSprintSpeed",{
        Title = "Enable Custom SprintSpeed", 
        Description = "Activating this modifies your Stat, if you deactivate it it will return to its original value",
        Default = false, 
        Callback = function(state)
            ActiveSprintSpeed = state

            if ActiveSprintSpeed and PlayerData and PlayerData:GetAttribute("ss") then
                OriginalSprintSpeed = PlayerData:GetAttribute("ss")
            end

            task.spawn(function()
                while ActiveSprintSpeed do
                    task.wait()
                    pcall(function()
                        if PlayerData and PlayerData:GetAttribute("ss") then
                            PlayerData:SetAttribute('ss', GameValues.Stats_Values.SprintSpeed)
                        end
                    end)
                end

                PlayerData:SetAttribute('ss', OriginalSprintSpeed)
            end)
    end})

    local FlySpeed = Tabs.CustomStats:AddSlider("FlySpeed", {
        Title = "Fly Speed",
        Default = GameValues.Stats_Values.FlySpeed,
        Min = 0,
        Max = 500,
        Rounding = 1,
        Callback = function(FlySpeedValue)
            GameValues.Stats_Values.FlySpeed = FlySpeedValue
        end
    })

    local OriginalFlySpeed

    local SetFlySpeed = Tabs.CustomStats:AddToggle(
        "SetFlySpeed",{
        Title = "Enable Custom FlySpeed", 
        Description = "Activating this modifies your Stat, if you deactivate it it will return to its original value",
        Default = false, 
        Callback = function(state)
            ActiveFlySpeed = state

            if ActiveFlySpeed and PlayerData and PlayerData:GetAttribute("fs") then
                OriginalFlySpeed = PlayerData:GetAttribute("fs")
            end

            task.spawn(function()
                while ActiveFlySpeed do
                    task.wait()
                    pcall(function()
                        if PlayerData and PlayerData:GetAttribute("fs") then
                            PlayerData:SetAttribute('fs', GameValues.Stats_Values.FlySpeed)
                        end
                    end)
                end

                PlayerData:SetAttribute('fs', OriginalFlySpeed)
            end)
    end})

    local RegionTeleport = Tabs.Teleports:AddDropdown("Dropdown", {
        Title = "Region Teleport",
        Description = "Allows you to teleport to all regions of the game!",
        Values = {
            "Volcano Island",
            "Jungle",
            "Pride Rocks",
            "Flower Cave",
            "Redwoods",
            "Swamp Hill",
            "Central Rockfaces",
            "Mountains",
            "Tundra",
            "Desert",
            "Mesa",
            "Rocky Drop",
            "Seaweed Depths",
            "Grassy shoal",
            "Coral Reef",
            "Algae Sandbar"
        },
        Multi = false,
        Default = 1,
    })

    local Location = "Volcano Island"

    RegionTeleport:OnChanged(function(Value)
        Location = Value
    end)

    local TeleportsToRegion = Tabs.Teleports:AddButton({
        Title = "Teleport to the Region", 
        Callback = function()
            if Location == "Volcano Island" then
                Character.HumanoidRootPart.CFrame = CFrame.new(2110.90576171875, 197.5357666015625, 990.8245239257812)
            elseif Location == "Jungle" then
                Character.HumanoidRootPart.CFrame = CFrame.new(2492.14501953125, 247.40225219726562, -960.7867431640625)
            elseif Location == "Pride Rocks" then
                Character.HumanoidRootPart.CFrame = CFrame.new(1851.840087890625, 184.30699157714844, -270.3717346191406)
            elseif Location == "Redwoods" then
                Character.HumanoidRootPart.CFrame = CFrame.new(313.9095764160156, 205.7820281982422, -1293.3677978515625)
            elseif Location == "Swamp Hill" then
                Character.HumanoidRootPart.CFrame = CFrame.new(1136.76123046875, 265.67974853515625, -2424.72021484375)
            elseif Location == "Central Rockfaces" then
                Character.HumanoidRootPart.CFrame = CFrame.new(552.7372436523438, 257.4394836425781, -595.3549194335938)
            elseif Location == "Mountains" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-1343.4755859375, 304.9347839355469, -498.11639404296875)
            elseif Location == "Tundra" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-1362.8814697265625, 364.01275634765625, -2329.2890625)
            elseif Location == "Flower Cave" then
                Character.HumanoidRootPart.CFrame = CFrame.new(46.076683044433594, 206.91854858398438, 1446.542724609375)
            elseif Location == "Desert" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-1436.7159423828125, 289.0160217285156, 1151.845703125)
            elseif Location == "Mesa" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-2323.075439453125, 218.92166137695312, 223.17633056640625)
            elseif Location == "Rocky Drop" then
                Character.HumanoidRootPart.CFrame = CFrame.new(1060.55078125, 58.14997863769531, 536.1812744140625)
            elseif Location == "Seaweed Depths" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-55.02280807495117, -33.18986129760742, 891.3093872070312)
            elseif Location == "Grassy shoal" then
                Character.HumanoidRootPart.CFrame = CFrame.new(-792.256103515625, 102.60992431640625, 2084.94091796875)
            elseif Location == "Coral Reef" then
                Character.HumanoidRootPart.CFrame = CFrame.new(1102.585693359375, 67.89586639404297, 1187.44091796875)
            elseif Location == "Algae Sandbar" then
                Character.HumanoidRootPart.CFrame = CFrame.new(1133.808837890625, 93.5822525024414, -1550.64013671875)
            end
    end})

    local ExplorerGachaTokenEsp = Tabs.Esp:AddToggle(
        "ExplorerGachaTokenEsp",{
        Title = "Explorer Gacha Token Esp", 
        Default = false, 
        Callback = function(state)
            PhotovoreGachaEspValue = state
            task.spawn(
                function()
                    while PhotovoreGachaEspValue do
                        RunService.Heartbeat:Wait()
                        pcall(
                            function()
                                local explorerCapsule =
                                    workspace.Interactions.SpawnedTokens:FindFirstChild("ExplorerGachaToken")
                                local billboardGui = nil
                                if explorerCapsule then
                                    billboardGui = explorerCapsule:FindFirstChild("ExplorerGachaTokenCapsuleBillboard")
                                    if not billboardGui then
                                        billboardGui = Instance.new("BillboardGui")
                                        local textLabel = Instance.new("TextLabel")
                                        billboardGui.Size = UDim2.new(0, 100, 0, 50)
                                        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                                        billboardGui.AlwaysOnTop = true
                                        billboardGui.LightInfluence = 1
                                        billboardGui.Parent = explorerCapsule

                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Size = UDim2.new(1.5, 0, 1.5, 0)
                                        textLabel.Text = "Photovore Gacha Token"
                                        textLabel.TextColor3 = Color3.new(255, 0, 0)
                                        textLabel.TextScaled = true
                                        textLabel.Parent = billboardGui
                                    end

                                    for _, billboard in ipairs(explorerCapsule:GetChildren()) do
                                        if billboard:IsA("BillboardGui") and billboard ~= billboardGui then
                                            billboard:Destroy()
                                        elseif PhotovoreGachaEspValue == false then
                                            billboard:Destroy()
                                        end
                                    end
                                end
                            end
                        )
                    end
                end
            )
    end})

    local GalaxyExplorerGachaTokenEsp = Tabs.Esp:AddToggle(
        "GalaxyExplorerGachaTokenEsp",{
        Title = "Galaxy Explorer Gacha Token Esp", 
        Default = false, 
        Callback = function(state)
            GalaxyExplorerCapsuleEspValue = state
            spawn(
                function()
                    while GalaxyExplorerCapsuleEspValue do
                        RunService.Heartbeat:Wait()
                        pcall(
                            function()
                                local GalaxyExplorerCapsule =
                                    workspace.Interactions.SpawnedTokens:FindFirstChild("GalaxyExplorerGachaToken")
                                local billboardGui = nil
                                if GalaxyExplorerCapsule then
                                    billboardGui = GalaxyExplorerCapsule:FindFirstChild("GalaxyExplorerCapsuleBillboard")
                                    if not billboardGui then
                                        billboardGui = Instance.new("BillboardGui")
                                        local textLabel = Instance.new("TextLabel")
                                        billboardGui.Size = UDim2.new(0, 100, 0, 50)
                                        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                                        billboardGui.AlwaysOnTop = true
                                        billboardGui.LightInfluence = 1
                                        billboardGui.Parent = GalaxyExplorerCapsule

                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Size = UDim2.new(1.5, 0, 1.5, 0)
                                        textLabel.Text = "Galaxy Gacha Token"
                                        textLabel.TextColor3 = Color3.new(255, 0, 0)
                                        textLabel.TextScaled = true
                                        textLabel.Parent = billboardGui
                                    end

                                    for _, billboard in ipairs(GalaxyExplorerCapsule:GetChildren()) do
                                        if billboard:IsA("BillboardGui") and billboard ~= billboardGui then
                                            billboard:Destroy()
                                        elseif GalaxyExplorerCapsuleEspValue == false then
                                            billboard:Destroy()
                                        end
                                    end
                                end
                            end
                        )
                    end
                end
            )
    end})

    local MechaGachaTokenEsp = Tabs.Esp:AddToggle(
        "MechaGachaTokenEsp",{
        Title = "Mecha Gacha Token Esp", 
        Default = false, 
        Callback = function(state)
            MechaCapsuleEspValue = state
            task.spawn(
                function()
                    while MechaCapsuleEspValue do
                        RunService.Heartbeat:Wait()
                        pcall(
                            function()
                                local MechaCapsule =
                                    workspace.Interactions.SpawnedTokens:FindFirstChild("MutateExplorerGachaToken")
                                local billboardGui = nil
                                if MechaCapsule then
                                    billboardGui = MechaCapsule:FindFirstChild("MutateExplorerGachaToken")
                                    if not billboardGui then
                                        billboardGui = Instance.new("BillboardGui")
                                        local textLabel = Instance.new("TextLabel")
                                        billboardGui.Size = UDim2.new(0, 100, 0, 50)
                                        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                                        billboardGui.AlwaysOnTop = true
                                        billboardGui.LightInfluence = 1
                                        billboardGui.Parent = MechaCapsule

                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Size = UDim2.new(1, 0, 1, 0)
                                        textLabel.Text = "Mecha Capsule"
                                        textLabel.TextColor3 = Color3.new(255, 0, 0)
                                        textLabel.TextScaled = true
                                        textLabel.Parent = billboardGui
                                    end

                                    for _, billboard in ipairs(MechaCapsule:GetChildren()) do
                                        if billboard:IsA("BillboardGui") and billboard ~= billboardGui then
                                            billboard:Destroy()
                                        elseif MechaCapsuleEspValue == false then
                                            billboard:Destroy()
                                        end
                                    end
                                end
                            end
                        )
                    end
                end
            )
    end})

    local MonsterGachaTokenEsp = Tabs.Esp:AddToggle(
        "MonsterGachaTokenEsp",{
        Title = "Monster Gacha Token Esp", 
        Default = false, 
        Callback = function(state)
            MonsterCapsuleEspValue = state
            task.spawn(
                function()
                    while MonsterCapsuleEspValue do
                        RunService.Heartbeat:Wait()
                        pcall(
                            function()
                                local MonsterCapsule =
                                    workspace.Interactions.SpawnedTokens:FindFirstChild("MonsterExplorerGachaToken")
                                local billboardGui = nil
                                if MonsterCapsule then
                                    billboardGui = MonsterCapsule:FindFirstChild("MonsterExplorerGachaToken")
                                    if not billboardGui then
                                        billboardGui = Instance.new("BillboardGui")
                                        local textLabel = Instance.new("TextLabel")
                                        billboardGui.Size = UDim2.new(0, 100, 0, 50)
                                        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                                        billboardGui.AlwaysOnTop = true
                                        billboardGui.LightInfluence = 1
                                        billboardGui.Parent = MonsterCapsule

                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Size = UDim2.new(1, 0, 1, 0)
                                        textLabel.Text = "Monster Capsule"
                                        textLabel.TextColor3 = Color3.new(255, 0, 0)
                                        textLabel.TextScaled = true
                                        textLabel.Parent = billboardGui
                                    end

                                    for _, billboard in ipairs(MonsterCapsule:GetChildren()) do
                                        if billboard:IsA("BillboardGui") and billboard ~= billboardGui then
                                            billboard:Destroy()
                                        elseif MonsterCapsuleEspValue == false then
                                            billboard:Destroy()
                                        end
                                    end
                                end
                            end
                        )
                    end
                end
            )
    end})

    local SweetGachaTokenEsp = Tabs.Esp:AddToggle(
        "SweetGachaTokenEsp",{
        Title = "Sweet Gacha Token Esp", 
        Default = false, 
        Callback = function(state)
            MonsterCapsuleEspValue = state
            spawn(
                function()
                    while MonsterCapsuleEspValue do
                        RunService.Heartbeat:Wait()
                        pcall(
                            function()
                                local MonsterCapsule =
                                    workspace.Interactions.SpawnedTokens:FindFirstChild("SweetExplorerGachaToken")
                                local billboardGui = nil
                                if MonsterCapsule then
                                    billboardGui = MonsterCapsule:FindFirstChild("SweetExplorerGachaToken")
                                    if not billboardGui then
                                        billboardGui = Instance.new("BillboardGui")
                                        local textLabel = Instance.new("TextLabel")
                                        billboardGui.Size = UDim2.new(0, 100, 0, 50)
                                        billboardGui.StudsOffset = Vector3.new(0, 2, 0)
                                        billboardGui.AlwaysOnTop = true
                                        billboardGui.LightInfluence = 1
                                        billboardGui.Parent = MonsterCapsule

                                        textLabel.BackgroundTransparency = 1
                                        textLabel.Size = UDim2.new(1, 0, 1, 0)
                                        textLabel.Text = "Monster Capsule"
                                        textLabel.TextColor3 = Color3.new(255, 0, 0)
                                        textLabel.TextScaled = true
                                        textLabel.Parent = billboardGui
                                    end

                                    for _, billboard in ipairs(MonsterCapsule:GetChildren()) do
                                        if billboard:IsA("BillboardGui") and billboard ~= billboardGui then
                                            billboard:Destroy()
                                        elseif MonsterCapsuleEspValue == false then
                                            billboard:Destroy()
                                        end
                                    end
                                end
                            end
                        )
                    end
                end
            )
    end})

    local PlayerEsp = Tabs.Esp:AddToggle(
        "PlayerEsp",{
        Title = "Player Esp", 
        Default = false, 
        Callback = function(state)
            EspEnable = state
            task.spawn(
                function()
                    while EspEnable do
                        task.wait(0.1)
                        pcall(
                            function()
                                updatePlayerNames()
                            end
                        )
                    end
                end
            )
    end})

    local FPSPingcount = Tabs.Others:AddButton({
        Title = "FPS / Ping count", 
        Callback = function()
            NotificationSound:Play()
            FPSCount()
    end})

    local AntiAfk = Tabs.Others:AddButton({
        Title = "Anti Afk", 
        Callback = function()
            NotificationSound:Play()
            LocalPlayer.Idled:connect(
                function()
                    VirtualUser:CaptureController()
                    VirtualUser:ClickButton2(Vector2.new())
                end
            )
    end})

    local RejoinServer = Tabs.Others:AddButton({
        Title = "Rejoin Server", 
        Callback = function()
            NotificationSound:Play()
            TPS:Teleport(PlaceId, LocalPlayer)
    end})

    local TeleportFewPeople = Tabs.Others:AddButton({
        Title = "Teleport to a server with few people", 
        Callback = function()
            NotificationSound:Play()
            local _place = PlaceId
            local _servers = Api .. _place .. "/servers/Public?sortOrder=Asc&limit=100"
            function ListServers(cursor)
                local Raw = game:HttpGet(_servers .. ((cursor and "&cursor=" .. cursor) or ""))
                return Http:JSONDecode(Raw)
            end

            local Server, Next
            repeat
                local Servers = ListServers(Next)
                Server = Servers.data[1]
                Next = Servers.nextPageCursor
            until Server

            TPS:TeleportToPlaceInstance(_place, Server.id, LocalPlayer)
    end})

    local LowQualityTextures = Tabs.Others:AddButton({
        Title = "Low Quality Textures", 
        Callback = function()
            NotificationSound:Play()
            for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
                if v:IsA("BasePart") and not v.Parent:FindFirstChild("Humanoid") then
                    v.Material = "SmoothPlastic"
                    if v:IsA("Texture") then
                        v:Destroy()
                    end
                end
            end
    end})

    local HopServer = Tabs.Others:AddButton({
        Title = "Hop Server (Never the same servers) ", 
        Callback = function()
            NotificationSound:Play()
            local PlaceID = PlaceId
            local AllIDs = {}
            local foundAnything = ""
            local actualHour = os.date("!*t").hour
            local Deleted = false
            local File =
                pcall(
                function()
                    AllIDs = game:GetService("HttpService"):JSONDecode(readfile("NotSameServers.json"))
                end
            )
            if not File then
                table.insert(AllIDs, actualHour)
                writefile("NotSameServers.json", game:GetService("HttpService"):JSONEncode(AllIDs))
            end
            local function TPReturner()
                local Site
                if foundAnything == "" then
                    Site =
                        game.HttpService:JSONDecode(
                        game:HttpGet(
                            "https://games.roblox.com/v1/games/" .. PlaceID .. "/servers/Public?sortOrder=Asc&limit=100"
                        )
                    )
                else
                    Site =
                        game.HttpService:JSONDecode(
                        game:HttpGet(
                            "https://games.roblox.com/v1/games/" ..
                                PlaceID .. "/servers/Public?sortOrder=Asc&limit=100&cursor=" .. foundAnything
                        )
                    )
                end
                local ID = ""
                if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
                    foundAnything = Site.nextPageCursor
                end
                local num = 0
                for i, v in pairs(Site.data) do
                    local Possible = true
                    ID = tostring(v.id)
                    if tonumber(v.maxPlayers) > tonumber(v.playing) then
                        for _, Existing in pairs(AllIDs) do
                            if num ~= 0 then
                                if ID == tostring(Existing) then
                                    Possible = false
                                end
                            else
                                if tonumber(actualHour) ~= tonumber(Existing) then
                                    local delFile =
                                        pcall(
                                        function()
                                            delfile("NotSameServers.json")
                                            AllIDs = {}
                                            table.insert(AllIDs, actualHour)
                                        end
                                    )
                                end
                            end
                            num = num + 1
                        end
                        if Possible == true then
                            table.insert(AllIDs, ID)
                            wait()
                            pcall(
                                function()
                                    writefile("NotSameServers.json", game:GetService("HttpService"):JSONEncode(AllIDs))
                                    wait()
                                    game:GetService("TeleportService"):TeleportToPlaceInstance(
                                        PlaceID,
                                        ID,
                                        game.Players.LocalPlayer
                                    )
                                end
                            )
                            wait(4)
                        end
                    end
                end
            end

            local function Teleport()
                while wait() do
                    pcall(
                        function()
                            TPReturner()
                            if foundAnything ~= "" then
                                TPReturner()
                            end
                       end
                    )
                end
            end

            Teleport()
    end})

    local ResetServerHopInfo = Tabs.Others:AddButton({
        Title = "Reset Server Hop Info", 
        Callback = function()
            NotificationSound:Play()
            delfile("NotSameServers.json")
    end})

    NotificationSound:Play()
    Fluent:Notify({
        Title = "Notification",
        Content = "Script Made By Mangnex#9524",
        Duration = 5
    })
