--[[
════════════════════════════════════════════════════════════════
    🔥 KAKA HUB V4 - FPS HUB COMPLETO COM SISTEMA DE KEYS 🔥
    Discord: https://discord.gg/u5VcCE7s2a
    ✨ ATUALIZADO: Aimbot com detecção inteligente de times!
    ✨ NOVO: Sistema de 3 dedos para abrir o hub!
════════════════════════════════════════════════════════════════
]]--

print("🔥 KAKA HUB V4 inicializando sistema de autenticação...")

-- ═══════════════════════════════════════════════════════════
--  🔧 CONFIGURAÇÕES DAS KEYS
-- ═══════════════════════════════════════════════════════════

local KEY_CONFIG = {
    Keys = {
        "KAKA-2026-PREMIUM",
        "KAKA-VIP-GOLD",
        "KAKA-ULTIMATE",
        "TESTE-KEY-123"
        -- Adicione mais keys aqui
    },
    
    DiscordLink = "https://discord.gg/u5VcCE7s2a",
    KeyLink = "https://4br.me/r8uk0gW",
    HubName = "KAKA HUB V4",
    NotificationTime = 3,
}

-- ═══════════════════════════════════════════════════════════
--  🎨 CORES DO KAKA HUB V4
-- ═══════════════════════════════════════════════════════════

local COLORS = {
    Background = Color3.fromRGB(20, 20, 30),
    Secondary = Color3.fromRGB(30, 30, 45),
    Primary = Color3.fromRGB(138, 43, 226),      -- Roxo principal
    PrimaryDark = Color3.fromRGB(100, 30, 180),  -- Roxo escuro
    Accent = Color3.fromRGB(186, 85, 211),       -- Roxo claro
    Text = Color3.fromRGB(255, 255, 255),
    TextDim = Color3.fromRGB(200, 200, 200),
    Success = Color3.fromRGB(46, 204, 113),
    Error = Color3.fromRGB(231, 76, 60),
    Shadow = Color3.fromRGB(0, 0, 0)
}

-- ═══════════════════════════════════════════════════════════
--  🛠️ SERVIÇOS
-- ═══════════════════════════════════════════════════════════

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local LocalPlayer = Players.LocalPlayer

-- ═══════════════════════════════════════════════════════════
--  ✨ FUNÇÕES DE ANIMAÇÃO DO SISTEMA DE KEYS
-- ═══════════════════════════════════════════════════════════

local function Tween(object, goal, duration, style, direction)
    local tweenInfo = TweenInfo.new(
        duration or 0.3,
        style or Enum.EasingStyle.Quad,
        direction or Enum.EasingDirection.Out
    )
    local tween = TweenService:Create(object, tweenInfo, goal)
    tween:Play()
    return tween
end

local function PulseEffect(object)
    spawn(function()
        local original = object.Size
        Tween(object, {Size = original + UDim2.new(0, 5, 0, 5)}, 0.15)
        wait(0.15)
        Tween(object, {Size = original}, 0.15)
    end)
end

-- ═══════════════════════════════════════════════════════════
--  🖼️ CRIAR INTERFACE DO SISTEMA DE KEYS
-- ═══════════════════════════════════════════════════════════

local function CreateKeySystem()
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "KakaKeySystem_" .. math.random(1000, 9999)
    ScreenGui.ResetOnSpawn = false
    ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    ScreenGui.IgnoreGuiInset = true
    
    local BlurFrame = Instance.new("Frame")
    BlurFrame.Name = "BlurFrame"
    BlurFrame.Size = UDim2.new(1, 0, 1, 0)
    BlurFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    BlurFrame.BackgroundTransparency = 0.3
    BlurFrame.BorderSizePixel = 0
    BlurFrame.Parent = ScreenGui
    
    local MainContainer = Instance.new("Frame")
    MainContainer.Name = "MainContainer"
    MainContainer.Size = UDim2.new(0, 500, 0, 400)
    MainContainer.Position = UDim2.new(0.5, -250, 0.5, -200)
    MainContainer.BackgroundColor3 = COLORS.Background
    MainContainer.BorderSizePixel = 0
    MainContainer.ClipsDescendants = true
    MainContainer.Parent = ScreenGui
    
    local MainCorner = Instance.new("UICorner")
    MainCorner.CornerRadius = UDim.new(0, 15)
    MainCorner.Parent = MainContainer
    
    local Shadow = Instance.new("ImageLabel")
    Shadow.Size = UDim2.new(1, 40, 1, 40)
    Shadow.Position = UDim2.new(0, -20, 0, -20)
    Shadow.BackgroundTransparency = 1
    Shadow.Image = "rbxassetid://5554236805"
    Shadow.ImageColor3 = COLORS.Shadow
    Shadow.ImageTransparency = 0.5
    Shadow.ScaleType = Enum.ScaleType.Slice
    Shadow.SliceCenter = Rect.new(23, 23, 277, 277)
    Shadow.ZIndex = 0
    Shadow.Parent = MainContainer
    
    local TopBar = Instance.new("Frame")
    TopBar.Name = "TopBar"
    TopBar.Size = UDim2.new(1, 0, 0, 60)
    TopBar.BackgroundColor3 = COLORS.Primary
    TopBar.BorderSizePixel = 0
    TopBar.Parent = MainContainer
    
    local TopCorner = Instance.new("UICorner")
    TopCorner.CornerRadius = UDim.new(0, 15)
    TopCorner.Parent = TopBar
    
    local TopFill = Instance.new("Frame")
    TopFill.Size = UDim2.new(1, 0, 0, 30)
    TopFill.Position = UDim2.new(0, 0, 1, -30)
    TopFill.BackgroundColor3 = COLORS.Primary
    TopFill.BorderSizePixel = 0
    TopFill.Parent = TopBar
    
    local Gradient = Instance.new("UIGradient")
    Gradient.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, COLORS.Primary),
        ColorSequenceKeypoint.new(1, COLORS.PrimaryDark)
    }
    Gradient.Rotation = 90
    Gradient.Parent = TopBar
    
    local Icon = Instance.new("TextLabel")
    Icon.Size = UDim2.new(0, 50, 0, 50)
    Icon.Position = UDim2.new(0, 15, 0, 5)
    Icon.BackgroundTransparency = 1
    Icon.Text = "🔑"
    Icon.TextColor3 = COLORS.Text
    Icon.Font = Enum.Font.GothamBold
    Icon.TextSize = 28
    Icon.Parent = TopBar
    
    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, -160, 1, 0)
    Title.Position = UDim2.new(0, 70, 0, 0)
    Title.BackgroundTransparency = 1
    Title.Text = "KAKA HUB V4"
    Title.TextColor3 = COLORS.Text
    Title.Font = Enum.Font.GothamBold
    Title.TextSize = 22
    Title.TextXAlignment = Enum.TextXAlignment.Left
    Title.Parent = TopBar
    
    local Subtitle = Instance.new("TextLabel")
    Subtitle.Size = UDim2.new(1, 0, 0, 15)
    Subtitle.Position = UDim2.new(0, 0, 1, -18)
    Subtitle.BackgroundTransparency = 1
    Subtitle.Text = "Sistema de Autenticacao"
    Subtitle.TextColor3 = Color3.fromRGB(220, 220, 220)
    Subtitle.Font = Enum.Font.Gotham
    Subtitle.TextSize = 12
    Subtitle.TextXAlignment = Enum.TextXAlignment.Left
    Subtitle.Parent = Title
    
    local CloseButton = Instance.new("TextButton")
    CloseButton.Name = "CloseButton"
    CloseButton.Size = UDim2.new(0, 40, 0, 40)
    CloseButton.Position = UDim2.new(1, -50, 0, 10)
    CloseButton.BackgroundColor3 = COLORS.Error
    CloseButton.Text = "✕"
    CloseButton.TextColor3 = COLORS.Text
    CloseButton.Font = Enum.Font.GothamBold
    CloseButton.TextSize = 20
    CloseButton.AutoButtonColor = false
    CloseButton.Parent = TopBar
    
    local CloseCorner = Instance.new("UICorner")
    CloseCorner.CornerRadius = UDim.new(0, 10)
    CloseCorner.Parent = CloseButton
    
    local Content = Instance.new("Frame")
    Content.Size = UDim2.new(1, -50, 1, -110)
    Content.Position = UDim2.new(0, 25, 0, 75)
    Content.BackgroundTransparency = 1
    Content.Parent = MainContainer
    
    local Description = Instance.new("TextLabel")
    Description.Size = UDim2.new(1, 0, 0, 70)
    Description.BackgroundTransparency = 1
    Description.Text = "🔐 Digite sua chave de acesso para usar o hub\n\nSe voce nao possui uma chave, pegue nos botoes abaixo"
    Description.TextColor3 = COLORS.TextDim
    Description.Font = Enum.Font.Gotham
    Description.TextSize = 14
    Description.TextWrapped = true
    Description.TextYAlignment = Enum.TextYAlignment.Top
    Description.Parent = Content
    
    local InputFrame = Instance.new("Frame")
    InputFrame.Size = UDim2.new(1, 0, 0, 50)
    InputFrame.Position = UDim2.new(0, 0, 0, 85)
    InputFrame.BackgroundColor3 = COLORS.Secondary
    InputFrame.BorderSizePixel = 0
    InputFrame.Parent = Content
    
    local InputCorner = Instance.new("UICorner")
    InputCorner.CornerRadius = UDim.new(0, 10)
    InputCorner.Parent = InputFrame
    
    local InputIcon = Instance.new("TextLabel")
    InputIcon.Size = UDim2.new(0, 40, 1, 0)
    InputIcon.BackgroundTransparency = 1
    InputIcon.Text = "🔑"
    InputIcon.TextColor3 = COLORS.Accent
    InputIcon.Font = Enum.Font.GothamBold
    InputIcon.TextSize = 20
    InputIcon.Parent = InputFrame
    
    local KeyInput = Instance.new("TextBox")
    KeyInput.Name = "KeyInput"
    KeyInput.Size = UDim2.new(1, -50, 1, 0)
    KeyInput.Position = UDim2.new(0, 45, 0, 0)
    KeyInput.BackgroundTransparency = 1
    KeyInput.PlaceholderText = "Digite sua key aqui..."
    KeyInput.PlaceholderColor3 = COLORS.TextDim
    KeyInput.Text = ""
    KeyInput.TextColor3 = COLORS.Text
    KeyInput.Font = Enum.Font.GothamMedium
    KeyInput.TextSize = 15
    KeyInput.TextXAlignment = Enum.TextXAlignment.Left
    KeyInput.ClearTextOnFocus = false
    KeyInput.Parent = InputFrame
    
    local VerifyButton = Instance.new("TextButton")
    VerifyButton.Name = "VerifyButton"
    VerifyButton.Size = UDim2.new(1, 0, 0, 50)
    VerifyButton.Position = UDim2.new(0, 0, 0, 145)
    VerifyButton.BackgroundColor3 = COLORS.Primary
    VerifyButton.Text = "✓ VERIFICAR KEY"
    VerifyButton.TextColor3 = COLORS.Text
    VerifyButton.Font = Enum.Font.GothamBold
    VerifyButton.TextSize = 16
    VerifyButton.AutoButtonColor = false
    VerifyButton.Parent = Content
    
    local VerifyCorner = Instance.new("UICorner")
    VerifyCorner.CornerRadius = UDim.new(0, 10)
    VerifyCorner.Parent = VerifyButton
    
    local VerifyGradient = Instance.new("UIGradient")
    VerifyGradient.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, COLORS.Primary),
        ColorSequenceKeypoint.new(1, COLORS.PrimaryDark)
    }
    VerifyGradient.Rotation = 90
    VerifyGradient.Parent = VerifyButton
    
    -- BOTÃO PEGAR KEY (NOVO)
    local GetKeyButton = Instance.new("TextButton")
    GetKeyButton.Name = "GetKeyButton"
    GetKeyButton.Size = UDim2.new(1, 0, 0, 45)
    GetKeyButton.Position = UDim2.new(0, 0, 0, 205)
    GetKeyButton.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
    GetKeyButton.Text = "🔑 PEGAR KEY AQUI"
    GetKeyButton.TextColor3 = COLORS.Text
    GetKeyButton.Font = Enum.Font.GothamBold
    GetKeyButton.TextSize = 14
    GetKeyButton.AutoButtonColor = false
    GetKeyButton.Parent = Content
    
    local GetKeyCorner = Instance.new("UICorner")
    GetKeyCorner.CornerRadius = UDim.new(0, 10)
    GetKeyCorner.Parent = GetKeyButton
    
    -- BOTÃO DISCORD CRIADOR (RENOMEADO)
    local DiscordButton = Instance.new("TextButton")
    DiscordButton.Name = "DiscordButton"
    DiscordButton.Size = UDim2.new(1, 0, 0, 45)
    DiscordButton.Position = UDim2.new(0, 0, 0, 260)
    DiscordButton.BackgroundColor3 = COLORS.Accent
    DiscordButton.Text = "💬 DISCORD CRIADOR"
    DiscordButton.TextColor3 = COLORS.Text
    DiscordButton.Font = Enum.Font.GothamBold
    DiscordButton.TextSize = 14
    DiscordButton.AutoButtonColor = false
    DiscordButton.Parent = Content
    
    local DiscordCorner = Instance.new("UICorner")
    DiscordCorner.CornerRadius = UDim.new(0, 10)
    DiscordCorner.Parent = DiscordButton
    
    local StatusLabel = Instance.new("TextLabel")
    StatusLabel.Name = "StatusLabel"
    StatusLabel.Size = UDim2.new(1, 0, 0, 25)
    StatusLabel.Position = UDim2.new(0, 0, 1, -30)
    StatusLabel.BackgroundTransparency = 1
    StatusLabel.Text = ""
    StatusLabel.TextColor3 = COLORS.Text
    StatusLabel.Font = Enum.Font.GothamMedium
    StatusLabel.TextSize = 13
    StatusLabel.Visible = false
    StatusLabel.Parent = MainContainer
    
    return ScreenGui, {
        MainContainer = MainContainer,
        CloseButton = CloseButton,
        KeyInput = KeyInput,
        VerifyButton = VerifyButton,
        GetKeyButton = GetKeyButton,
        DiscordButton = DiscordButton,
        StatusLabel = StatusLabel,
        InputFrame = InputFrame
    }
end

-- ═══════════════════════════════════════════════════════════
--  🔍 VERIFICAR KEY
-- ═══════════════════════════════════════════════════════════

local function VerifyKey(key)
    for _, validKey in ipairs(KEY_CONFIG.Keys) do
        if key == validKey then
            return true
        end
    end
    return false
end

-- ═══════════════════════════════════════════════════════════
--  📢 MOSTRAR STATUS
-- ═══════════════════════════════════════════════════════════

local function ShowStatus(label, message, isSuccess)
    label.Text = message
    label.TextColor3 = isSuccess and COLORS.Success or COLORS.Error
    label.Visible = true
    label.TextTransparency = 1
    
    Tween(label, {TextTransparency = 0}, 0.3)
    
    task.wait(KEY_CONFIG.NotificationTime)
    
    Tween(label, {TextTransparency = 1}, 0.3).Completed:Wait()
    label.Visible = false
end

-- ═══════════════════════════════════════════════════════════
--  🎮 SISTEMA DE AUTENTICAÇÃO COM 3 DEDOS
-- ═══════════════════════════════════════════════════════════

local function StartKeySystem(onSuccess)
    local gui, elements = CreateKeySystem()
    gui.Parent = CoreGui
    
    -- Iniciar invisível
    gui.Enabled = false
    
    -- Sistema de 3 dedos para abrir a tela de Key
    local activeTouches = {}
    local keySystemOpen = false
    
    local function countTouches()
        local count = 0
        for _, active in pairs(activeTouches) do
            if active then count = count + 1 end
        end
        return count
    end
    
    UserInputService.TouchStarted:Connect(function(touch, gameProcessed)
        if keySystemOpen then return end
        
        activeTouches[touch] = true
        
        if countTouches() >= 3 then
            keySystemOpen = true
            gui.Enabled = true
            
            elements.MainContainer.Size = UDim2.new(0, 0, 0, 0)
            elements.MainContainer.Position = UDim2.new(0.5, 0, 0.5, 0)
            
            Tween(
                elements.MainContainer,
                {
                    Size = UDim2.new(0, 500, 0, 400),
                    Position = UDim2.new(0.5, -250, 0.5, -200)
                },
                0.5,
                Enum.EasingStyle.Back
            )
            
            print("🔑 Sistema de Keys aberto com 3 dedos!")
        end
    end)
    
    UserInputService.TouchEnded:Connect(function(touch, gameProcessed)
        activeTouches[touch] = false
    end)
    
    elements.VerifyButton.MouseEnter:Connect(function()
        Tween(elements.VerifyButton, {BackgroundColor3 = COLORS.Accent}, 0.2)
        PulseEffect(elements.VerifyButton)
    end)
    
    elements.VerifyButton.MouseLeave:Connect(function()
        Tween(elements.VerifyButton, {BackgroundColor3 = COLORS.Primary}, 0.2)
    end)
    
    -- Hover efeito botão Pegar Key
    elements.GetKeyButton.MouseEnter:Connect(function()
        Tween(elements.GetKeyButton, {BackgroundColor3 = Color3.fromRGB(60, 220, 130)}, 0.2)
    end)
    
    elements.GetKeyButton.MouseLeave:Connect(function()
        Tween(elements.GetKeyButton, {BackgroundColor3 = Color3.fromRGB(46, 204, 113)}, 0.2)
    end)
    
    elements.DiscordButton.MouseEnter:Connect(function()
        Tween(elements.DiscordButton, {BackgroundColor3 = Color3.fromRGB(200, 100, 230)}, 0.2)
    end)
    
    elements.DiscordButton.MouseLeave:Connect(function()
        Tween(elements.DiscordButton, {BackgroundColor3 = COLORS.Accent}, 0.2)
    end)
    
    elements.KeyInput.Focused:Connect(function()
        Tween(elements.InputFrame, {BackgroundColor3 = Color3.fromRGB(40, 40, 60)}, 0.2)
    end)
    
    elements.KeyInput.FocusLost:Connect(function()
        Tween(elements.InputFrame, {BackgroundColor3 = COLORS.Secondary}, 0.2)
    end)
    
    elements.VerifyButton.MouseButton1Click:Connect(function()
        local key = elements.KeyInput.Text:gsub("^%s*(.-)%s*$", "%1")
        
        if key == "" then
            ShowStatus(elements.StatusLabel, "❌ Por favor, digite uma key!", false)
            return
        end
        
        PulseEffect(elements.VerifyButton)
        
        if VerifyKey(key) then
            ShowStatus(elements.StatusLabel, "✅ Key valida! Carregando hub...", true)
            
            task.wait(1.5)
            
            Tween(
                elements.MainContainer,
                {
                    Size = UDim2.new(0, 0, 0, 0),
                    Position = UDim2.new(0.5, 0, 0.5, 0)
                },
                0.4,
                Enum.EasingStyle.Back,
                Enum.EasingDirection.In
            ).Completed:Wait()
            
            gui:Destroy()
            
            if onSuccess then
                onSuccess()
            end
        else
            ShowStatus(elements.StatusLabel, "❌ Key invalida! Tente novamente.", false)
            elements.KeyInput.Text = ""
            
            local original = elements.InputFrame.Position
            for i = 1, 3 do
                Tween(elements.InputFrame, {Position = original + UDim2.new(0, -10, 0, 0)}, 0.05)
                wait(0.05)
                Tween(elements.InputFrame, {Position = original + UDim2.new(0, 10, 0, 0)}, 0.05)
                wait(0.05)
            end
            Tween(elements.InputFrame, {Position = original}, 0.1)
        end
    end)
    
    -- Botão Pegar Key
    elements.GetKeyButton.MouseButton1Click:Connect(function()
        PulseEffect(elements.GetKeyButton)
        setclipboard(KEY_CONFIG.KeyLink)
        ShowStatus(elements.StatusLabel, "🔑 Link da key copiado! Cole no navegador!", true)
    end)
    
    -- Botão Discord Criador
    elements.DiscordButton.MouseButton1Click:Connect(function()
        PulseEffect(elements.DiscordButton)
        setclipboard(KEY_CONFIG.DiscordLink)
        ShowStatus(elements.StatusLabel, "💬 Discord do criador copiado!", true)
    end)
    
    elements.CloseButton.MouseButton1Click:Connect(function()
        Tween(
            elements.MainContainer,
            {
                Size = UDim2.new(0, 0, 0, 0),
                Position = UDim2.new(0.5, 0, 0.5, 0)
            },
            0.3,
            Enum.EasingStyle.Back,
            Enum.EasingDirection.In
        ).Completed:Wait()
        gui:Destroy()
    end)
    
    elements.KeyInput.FocusLost:Connect(function(enterPressed)
        if enterPressed then
            elements.VerifyButton.MouseButton1Click:Fire()
        end
    end)
    
    local dragging, dragInput, dragStart, startPos
    
    local function update(input)
        local delta = input.Position - dragStart
        Tween(elements.MainContainer, {Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )}, 0.1, Enum.EasingStyle.Linear)
    end
    
    elements.MainContainer.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = elements.MainContainer.Position
            
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)
    
    elements.MainContainer.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            update(input)
        end
    end)
end

-- ═══════════════════════════════════════════════════════════
--  🚀 INICIAR SISTEMA E CARREGAR HUB
-- ═══════════════════════════════════════════════════════════

StartKeySystem(function()
    print("✅ Key verificada com sucesso!")
    print("🚀 Carregando KAKA HUB V4...")
    
    -- ═══════════════════════════════════════════════════
    --              🔥 SEU HUB COMEÇA AQUI 🔥
    -- ═══════════════════════════════════════════════════
    
    local Camera = workspace.CurrentCamera
    local RunService = game:GetService("RunService")
    local Teams = game:GetService("Teams")

    -- ═══════════════════════════════════════════════════
    --                  CONFIGURAÇÕES DO HUB
    -- ═══════════════════════════════════════════════════

    local Settings = {
        Aimbot = {
            Enabled = false,
            FOV = 150,
            WallCheck = true,
            TargetPart = "Head",
            TeamCheck = true
        },
        ESP = {
            Enabled = false,
            BoxColor = Color3.fromRGB(255, 0, 255),
            NameColor = Color3.fromRGB(255, 255, 255),
            DistanceColor = Color3.fromRGB(0, 255, 255),
            HealthBarEnabled = true
        },
        Teleport = {
            SelectedPlayer = nil
        }
    }

    -- ═══════════════════════════════════════════════════
    --           FUNÇÕES DE DETECÇÃO DE TIMES
    -- ═══════════════════════════════════════════════════

    local function HasMultipleTeams()
        local teamCount = 0
        for _, team in pairs(Teams:GetTeams()) do
            teamCount = teamCount + 1
        end
        return teamCount > 1
    end

    local function IsEnemy(player)
        if not Settings.Aimbot.TeamCheck then
            return true
        end
        
        if not HasMultipleTeams() then
            return true
        end
        
        if LocalPlayer.Team and player.Team then
            return LocalPlayer.Team ~= player.Team
        end
        
        return true
    end

    -- ═══════════════════════════════════════════════════
    --                  FUNÇÕES ÚTEIS
    -- ═══════════════════════════════════════════════════

    local function IsVisible(targetChar)
        if not Settings.Aimbot.WallCheck then return true end
        
        local char = LocalPlayer.Character
        if not char then return false end
        
        local origin = char:FindFirstChild("HumanoidRootPart")
        local target = targetChar:FindFirstChild(Settings.Aimbot.TargetPart)
        
        if not origin or not target then return false end
        
        local ray = Ray.new(origin.Position, (target.Position - origin.Position).Unit * 1000)
        local hit = workspace:FindPartOnRayWithIgnoreList(ray, {char, Camera})
        
        return hit and hit:IsDescendantOf(targetChar)
    end

    local function GetClosestPlayerInFOV()
        local closestPlayer = nil
        local shortestDistance = Settings.Aimbot.FOV
        
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                if IsEnemy(player) then
                    local char = player.Character
                    local humanoid = char:FindFirstChild("Humanoid")
                    local targetPart = char:FindFirstChild(Settings.Aimbot.TargetPart)
                    
                    if humanoid and humanoid.Health > 0 and targetPart then
                        local screenPos, onScreen = Camera:WorldToViewportPoint(targetPart.Position)
                        
                        if onScreen then
                            local mousePos = UserInputService:GetMouseLocation()
                            local distance = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                            
                            if distance < shortestDistance then
                                if IsVisible(char) then
                                    closestPlayer = player
                                    shortestDistance = distance
                                end
                            end
                        end
                    end
                end
            end
        end
        
        return closestPlayer
    end

    -- ═══════════════════════════════════════════════════
    --                    AIMBOT
    -- ═══════════════════════════════════════════════════

    RunService.RenderStepped:Connect(function()
        if Settings.Aimbot.Enabled then
            local target = GetClosestPlayerInFOV()
            
            if target and target.Character then
                local targetPart = target.Character:FindFirstChild(Settings.Aimbot.TargetPart)
                
                if targetPart then
                    Camera.CFrame = CFrame.new(Camera.CFrame.Position, targetPart.Position)
                end
            end
        end
    end)

    -- ═══════════════════════════════════════════════════
    --                     ESP
    -- ═══════════════════════════════════════════════════

    local ESPObjects = {}

    local function CreateESP(player)
        if ESPObjects[player] then return end
        
        local esp = {
            Box = Drawing.new("Square"),
            Name = Drawing.new("Text"),
            Distance = Drawing.new("Text"),
            HealthBar = Drawing.new("Line"),
            HealthBarBG = Drawing.new("Line")
        }
        
        esp.Box.Thickness = 2
        esp.Box.Filled = false
        esp.Box.Color = Settings.ESP.BoxColor
        esp.Box.Visible = false
        esp.Box.ZIndex = 2
        
        esp.Name.Size = 14
        esp.Name.Center = true
        esp.Name.Outline = true
        esp.Name.Color = Settings.ESP.NameColor
        esp.Name.Visible = false
        esp.Name.ZIndex = 2
        
        esp.Distance.Size = 12
        esp.Distance.Center = true
        esp.Distance.Outline = true
        esp.Distance.Color = Settings.ESP.DistanceColor
        esp.Distance.Visible = false
        esp.Distance.ZIndex = 2
        
        esp.HealthBarBG.Thickness = 3
        esp.HealthBarBG.Color = Color3.fromRGB(0, 0, 0)
        esp.HealthBarBG.Visible = false
        esp.HealthBarBG.ZIndex = 1
        
        esp.HealthBar.Thickness = 3
        esp.HealthBar.Color = Color3.fromRGB(0, 255, 0)
        esp.HealthBar.Visible = false
        esp.HealthBar.ZIndex = 2
        
        ESPObjects[player] = esp
    end

    local function UpdateESP()
        for player, esp in pairs(ESPObjects) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChild("Humanoid") then
                local char = player.Character
                local hrp = char.HumanoidRootPart
                local humanoid = char.Humanoid
                
                local screenPos, onScreen = Camera:WorldToViewportPoint(hrp.Position)
                
                if onScreen and Settings.ESP.Enabled then
                    local headPos = Camera:WorldToViewportPoint(char.Head.Position + Vector3.new(0, 0.5, 0))
                    local legPos = Camera:WorldToViewportPoint(hrp.Position - Vector3.new(0, 3, 0))
                    
                    local height = math.abs(headPos.Y - legPos.Y)
                    local width = height / 2
                    
                    local boxColor = Settings.ESP.BoxColor
                    if HasMultipleTeams() and player.Team then
                        if player.Team == LocalPlayer.Team then
                            boxColor = Color3.fromRGB(0, 255, 0)
                        else
                            boxColor = Color3.fromRGB(255, 0, 0)
                        end
                    end
                    
                    esp.Box.Size = Vector2.new(width, height)
                    esp.Box.Position = Vector2.new(screenPos.X - width / 2, screenPos.Y - height / 2)
                    esp.Box.Color = boxColor
                    esp.Box.Visible = true
                    
                    esp.Name.Text = player.Name
                    esp.Name.Position = Vector2.new(screenPos.X, headPos.Y - 20)
                    esp.Name.Visible = true
                    
                    local distance = math.floor((hrp.Position - LocalPlayer.Character.HumanoidRootPart.Position).Magnitude)
                    esp.Distance.Text = tostring(distance) .. "m"
                    esp.Distance.Position = Vector2.new(screenPos.X, legPos.Y + 5)
                    esp.Distance.Visible = true
                    
                    if Settings.ESP.HealthBarEnabled then
                        local healthPercent = humanoid.Health / humanoid.MaxHealth
                        
                        esp.HealthBarBG.From = Vector2.new(screenPos.X - width / 2 - 6, screenPos.Y - height / 2)
                        esp.HealthBarBG.To = Vector2.new(screenPos.X - width / 2 - 6, screenPos.Y + height / 2)
                        esp.HealthBarBG.Visible = true
                        
                        esp.HealthBar.From = Vector2.new(screenPos.X - width / 2 - 6, screenPos.Y - height / 2)
                        esp.HealthBar.To = Vector2.new(screenPos.X - width / 2 - 6, screenPos.Y - height / 2 + height * healthPercent)
                        esp.HealthBar.Color = Color3.fromRGB(255 * (1 - healthPercent), 255 * healthPercent, 0)
                        esp.HealthBar.Visible = true
                    end
                else
                    esp.Box.Visible = false
                    esp.Name.Visible = false
                    esp.Distance.Visible = false
                    esp.HealthBar.Visible = false
                    esp.HealthBarBG.Visible = false
                end
            else
                esp.Box.Visible = false
                esp.Name.Visible = false
                esp.Distance.Visible = false
                esp.HealthBar.Visible = false
                esp.HealthBarBG.Visible = false
            end
        end
    end

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            CreateESP(player)
        end
    end

    Players.PlayerAdded:Connect(function(player)
        CreateESP(player)
    end)

    Players.PlayerRemoving:Connect(function(player)
        if ESPObjects[player] then
            for _, drawing in pairs(ESPObjects[player]) do
                drawing:Remove()
            end
            ESPObjects[player] = nil
        end
    end)

    RunService.RenderStepped:Connect(UpdateESP)

    -- ═══════════════════════════════════════════════════
    --                  FOV CIRCLE
    -- ═══════════════════════════════════════════════════

    local FOVCircle = Drawing.new("Circle")
    FOVCircle.Thickness = 3
    FOVCircle.NumSides = 64
    FOVCircle.Radius = Settings.Aimbot.FOV
    FOVCircle.Filled = false
    FOVCircle.Visible = true
    FOVCircle.ZIndex = 999
    FOVCircle.Transparency = 1
    FOVCircle.Color = Color3.fromRGB(255, 0, 255)

    local hue = 0
    RunService.RenderStepped:Connect(function()
        local mousePos = UserInputService:GetMouseLocation()
        FOVCircle.Position = mousePos
        FOVCircle.Radius = Settings.Aimbot.FOV
        
        hue = (hue + 1) % 360
        local r = math.floor(math.sin(math.rad(hue)) * 127 + 128)
        local g = math.floor(math.sin(math.rad(hue + 120)) * 127 + 128)
        local b = math.floor(math.sin(math.rad(hue + 240)) * 127 + 128)
        
        FOVCircle.Color = Color3.fromRGB(r, g, b)
    end)

    -- ═══════════════════════════════════════════════════
    --                      GUI DO HUB
    -- ═══════════════════════════════════════════════════

    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "KakaHubV4"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    ScreenGui.Parent = LocalPlayer.PlayerGui

    local MainFrame = Instance.new("Frame")
    MainFrame.Name = "MainFrame"
    MainFrame.Size = UDim2.new(0, 450, 0, 580)
    MainFrame.Position = UDim2.new(0.5, -225, 0.5, -290)
    MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    MainFrame.BorderSizePixel = 0
    MainFrame.Active = true
    MainFrame.Draggable = true
    MainFrame.Visible = false
    MainFrame.Parent = ScreenGui

    local MainCorner = Instance.new("UICorner")
    MainCorner.CornerRadius = UDim.new(0, 15)
    MainCorner.Parent = MainFrame

    local Header = Instance.new("Frame")
    Header.Size = UDim2.new(1, 0, 0, 60)
    Header.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
    Header.BorderSizePixel = 0
    Header.Parent = MainFrame

    local HeaderCorner = Instance.new("UICorner")
    HeaderCorner.CornerRadius = UDim.new(0, 15)
    HeaderCorner.Parent = Header

    local HeaderFix = Instance.new("Frame")
    HeaderFix.Size = UDim2.new(1, 0, 0, 15)
    HeaderFix.Position = UDim2.new(0, 0, 1, -15)
    HeaderFix.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
    HeaderFix.BorderSizePixel = 0
    HeaderFix.Parent = Header

    local Title = Instance.new("TextLabel")
    Title.Size = UDim2.new(1, -20, 1, 0)
    Title.Position = UDim2.new(0, 10, 0, 0)
    Title.BackgroundTransparency = 1
    Title.Text = "🔥 KAKA HUB V4"
    Title.TextColor3 = Color3.fromRGB(255, 255, 255)
    Title.TextSize = 28
    Title.Font = Enum.Font.GothamBold
    Title.TextXAlignment = Enum.TextXAlignment.Left
    Title.Parent = Header

    local CloseButton = Instance.new("TextButton")
    CloseButton.Size = UDim2.new(0, 40, 0, 40)
    CloseButton.Position = UDim2.new(1, -50, 0, 10)
    CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    CloseButton.Text = "X"
    CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    CloseButton.TextSize = 20
    CloseButton.Font = Enum.Font.GothamBold
    CloseButton.Parent = Header

    Instance.new("UICorner", CloseButton).CornerRadius = UDim.new(0, 10)

    local ContentFrame = Instance.new("ScrollingFrame")
    ContentFrame.Size = UDim2.new(1, -20, 1, -80)
    ContentFrame.Position = UDim2.new(0, 10, 0, 70)
    ContentFrame.BackgroundTransparency = 1
    ContentFrame.BorderSizePixel = 0
    ContentFrame.ScrollBarThickness = 6
    ContentFrame.Parent = MainFrame

    local UIListLayout = Instance.new("UIListLayout")
    UIListLayout.Padding = UDim.new(0, 10)
    UIListLayout.Parent = ContentFrame

    local function CreateSection(title)
        local section = Instance.new("Frame")
        section.Size = UDim2.new(1, -10, 0, 40)
        section.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        section.BorderSizePixel = 0
        section.Parent = ContentFrame
        
        Instance.new("UICorner", section).CornerRadius = UDim.new(0, 8)
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, -10, 1, 0)
        label.Position = UDim2.new(0, 10, 0, 0)
        label.BackgroundTransparency = 1
        label.Text = title
        label.TextColor3 = Color3.fromRGB(255, 200, 0)
        label.TextSize = 16
        label.Font = Enum.Font.GothamBold
        label.TextXAlignment = Enum.TextXAlignment.Left
        label.Parent = section
        
        return section
    end

    local function CreateToggle(name, default, callback)
        local toggle = Instance.new("Frame")
        toggle.Size = UDim2.new(1, -10, 0, 40)
        toggle.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        toggle.BorderSizePixel = 0
        toggle.Parent = ContentFrame
        
        Instance.new("UICorner", toggle).CornerRadius = UDim.new(0, 8)
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(0.7, 0, 1, 0)
        label.Position = UDim2.new(0, 10, 0, 0)
        label.BackgroundTransparency = 1
        label.Text = name
        label.TextColor3 = Color3.fromRGB(255, 255, 255)
        label.TextSize = 14
        label.Font = Enum.Font.Gotham
        label.TextXAlignment = Enum.TextXAlignment.Left
        label.Parent = toggle
        
        local button = Instance.new("TextButton")
        button.Size = UDim2.new(0, 60, 0, 30)
        button.Position = UDim2.new(1, -70, 0.5, -15)
        button.BackgroundColor3 = default and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
        button.Text = default and "ON" or "OFF"
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
        button.TextSize = 14
        button.Font = Enum.Font.GothamBold
        button.Parent = toggle
        
        Instance.new("UICorner", button).CornerRadius = UDim.new(0, 8)
        
        local enabled = default
        
        button.MouseButton1Click:Connect(function()
            enabled = not enabled
            button.BackgroundColor3 = enabled and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
            button.Text = enabled and "ON" or "OFF"
            callback(enabled)
        end)
        
        return toggle
    end

    local function CreateSlider(name, min, max, default, callback)
        local slider = Instance.new("Frame")
        slider.Size = UDim2.new(1, -10, 0, 60)
        slider.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        slider.BorderSizePixel = 0
        slider.Parent = ContentFrame
        
        Instance.new("UICorner", slider).CornerRadius = UDim.new(0, 8)
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, -20, 0, 20)
        label.Position = UDim2.new(0, 10, 0, 5)
        label.BackgroundTransparency = 1
        label.Text = name .. ": " .. default
        label.TextColor3 = Color3.fromRGB(255, 255, 255)
        label.TextSize = 14
        label.Font = Enum.Font.Gotham
        label.TextXAlignment = Enum.TextXAlignment.Left
        label.Parent = slider
        
        local sliderBar = Instance.new("Frame")
        sliderBar.Size = UDim2.new(0.9, 0, 0, 8)
        sliderBar.Position = UDim2.new(0.05, 0, 0, 35)
        sliderBar.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        sliderBar.BorderSizePixel = 0
        sliderBar.Parent = slider
        
        Instance.new("UICorner", sliderBar).CornerRadius = UDim.new(1, 0)
        
        local sliderFill = Instance.new("Frame")
        sliderFill.Size = UDim2.new((default - min) / (max - min), 0, 1, 0)
        sliderFill.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
        sliderFill.BorderSizePixel = 0
        sliderFill.Parent = sliderBar
        
        Instance.new("UICorner", sliderFill).CornerRadius = UDim.new(1, 0)
        
        local sliderButton = Instance.new("TextButton")
        sliderButton.Size = UDim2.new(1, 0, 1, 0)
        sliderButton.BackgroundTransparency = 1
        sliderButton.Text = ""
        sliderButton.Parent = sliderBar
        
        local dragging = false
        
        sliderButton.MouseButton1Down:Connect(function()
            dragging = true
        end)
        
        UserInputService.InputEnded:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                dragging = false
            end
        end)
        
        sliderButton.MouseMoved:Connect(function(x, y)
            if dragging then
                local mousePos = UserInputService:GetMouseLocation().X
                local sliderPos = sliderBar.AbsolutePosition.X
                local sliderSize = sliderBar.AbsoluteSize.X
                
                local value = math.clamp((mousePos - sliderPos) / sliderSize, 0, 1)
                local actualValue = math.floor(min + (max - min) * value)
                
                sliderFill.Size = UDim2.new(value, 0, 1, 0)
                label.Text = name .. ": " .. actualValue
                
                callback(actualValue)
            end
        end)
        
        return slider
    end

    local function CreateDropdown(name, options, callback)
        local dropdown = Instance.new("Frame")
        dropdown.Size = UDim2.new(1, -10, 0, 40)
        dropdown.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        dropdown.BorderSizePixel = 0
        dropdown.Parent = ContentFrame
        
        Instance.new("UICorner", dropdown).CornerRadius = UDim.new(0, 8)
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(0.4, 0, 1, 0)
        label.Position = UDim2.new(0, 10, 0, 0)
        label.BackgroundTransparency = 1
        label.Text = name
        label.TextColor3 = Color3.fromRGB(255, 255, 255)
        label.TextSize = 14
        label.Font = Enum.Font.Gotham
        label.TextXAlignment = Enum.TextXAlignment.Left
        label.Parent = dropdown
        
        local button = Instance.new("TextButton")
        button.Size = UDim2.new(0.5, -20, 0, 30)
        button.Position = UDim2.new(0.5, 10, 0.5, -15)
        button.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        button.Text = "Selecionar"
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
        button.TextSize = 13
        button.Font = Enum.Font.Gotham
        button.Parent = dropdown
        
        Instance.new("UICorner", button).CornerRadius = UDim.new(0, 6)
        
        local dropdownList = Instance.new("Frame")
        dropdownList.Size = UDim2.new(1, 0, 0, #options * 35)
        dropdownList.Position = UDim2.new(0, 0, 1, 5)
        dropdownList.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        dropdownList.BorderSizePixel = 0
        dropdownList.Visible = false
        dropdownList.ZIndex = 10
        dropdownList.Parent = dropdown
        
        Instance.new("UICorner", dropdownList).CornerRadius = UDim.new(0, 8)
        
        local listLayout = Instance.new("UIListLayout")
        listLayout.Padding = UDim.new(0, 5)
        listLayout.Parent = dropdownList
        
        button.MouseButton1Click:Connect(function()
            dropdownList.Visible = not dropdownList.Visible
        end)
        
        for _, option in pairs(options) do
            local optionButton = Instance.new("TextButton")
            optionButton.Size = UDim2.new(1, -10, 0, 30)
            optionButton.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
            optionButton.Text = option
            optionButton.TextColor3 = Color3.fromRGB(255, 255, 255)
            optionButton.TextSize = 13
            optionButton.Font = Enum.Font.Gotham
            optionButton.Parent = dropdownList
            
            Instance.new("UICorner", optionButton).CornerRadius = UDim.new(0, 6)
            
            optionButton.MouseButton1Click:Connect(function()
                button.Text = option
                dropdownList.Visible = false
                callback(option)
            end)
        end
        
        return dropdown
    end

    -- Criar GUI do Hub
    CreateSection("🎯 AIMBOT")

    CreateToggle("Aimbot", false, function(enabled)
        Settings.Aimbot.Enabled = enabled
    end)

    CreateToggle("Team Check (Anti-Aliado)", true, function(enabled)
        Settings.Aimbot.TeamCheck = enabled
    end)

    CreateSlider("FOV Circle", 50, 500, 150, function(value)
        Settings.Aimbot.FOV = value
    end)

    CreateSection("👁️ ESP")

    CreateToggle("ESP", false, function(enabled)
        Settings.ESP.Enabled = enabled
    end)

    CreateSection("🚀 TELEPORT")

    local playerNames = {}
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(playerNames, player.Name)
        end
    end

    CreateDropdown("Teleportar para", playerNames, function(selectedName)
        for _, player in pairs(Players:GetPlayers()) do
            if player.Name == selectedName then
                Settings.Teleport.SelectedPlayer = player
                
                if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                        LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
                    end
                end
                break
            end
        end
    end)

    CloseButton.MouseButton1Click:Connect(function()
        MainFrame.Visible = false
    end)

    -- ═══════════════════════════════════════════════════
    --      🖐️ SISTEMA DE 3 DEDOS SIMULTÂNEOS (CORRIGIDO)
    -- ═══════════════════════════════════════════════════

    local activeTouches = {}
    local touchDebounce = false

    local function countActiveTouches()
        local count = 0
        for touch, active in pairs(activeTouches) do
            if active then
                count = count + 1
            end
        end
        return count
    end

    -- Detectar quando toca na tela
    UserInputService.TouchStarted:Connect(function(touch, gameProcessed)
        -- Marcar toque como ativo
        activeTouches[touch] = true
        
        -- Verificar se tem 3 ou mais dedos
        if countActiveTouches() >= 3 and not touchDebounce then
            touchDebounce = true
            MainFrame.Visible = not MainFrame.Visible
            
            print("✅ Hub " .. (MainFrame.Visible and "aberto" or "fechado") .. " com 3 dedos!")
            
            -- Resetar após 1 segundo
            task.spawn(function()
                task.wait(1)
                touchDebounce = false
            end)
        end
    end)

    -- Detectar quando tira o dedo da tela
    UserInputService.TouchEnded:Connect(function(touch, gameProcessed)
        activeTouches[touch] = false
    end)

    -- Limpar toques inativos periodicamente
    task.spawn(function()
        while true do
            task.wait(2)
            for touch, active in pairs(activeTouches) do
                if not active then
                    activeTouches[touch] = nil
                end
            end
        end
    end)

    -- ═══════════════════════════════════════════════════
    --                 MENSAGENS NO CONSOLE
    -- ═══════════════════════════════════════════════════

    print("✅ KAKA HUB V4 carregado!")
    print("🎯 Aimbot: OFF (ative no hub)")
    print("👁️ ESP: OFF (ative no hub)")
    print("🖐️ Use 3 dedos simultâneos para abrir o hub!")
    print("⚡ Team Check: " .. (HasMultipleTeams() and "Múltiplos times detectados!" or "Modo FFA detectado!"))
end)
