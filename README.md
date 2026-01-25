-- 🔥 FEATURES HUB V1
-- Criado com ❤️
-- ✨ Hub completo com todas as features!

print("🔥 FEATURES HUB V1 carregando...")

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

-- ═══════════════════════════════════════════════════
--                  SPIN TO FLY
-- ═══════════════════════════════════════════════════

local SpinToFly = {
    Enabled = false,
    Speed = 50,
    Power = 100
}

local function ToggleSpinToFly()
    SpinToFly.Enabled = not SpinToFly.Enabled
    
    if SpinToFly.Enabled then
        spawn(function()
            while SpinToFly.Enabled and LocalPlayer.Character do
                local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if hrp then
                    -- Cria força de rotação
                    local bodyGyro = hrp:FindFirstChild("SpinGyro") or Instance.new("BodyGyro")
                    bodyGyro.Name = "SpinGyro"
                    bodyGyro.MaxTorque = Vector3.new(0, math.huge, 0)
                    bodyGyro.P = SpinToFly.Power * 1000
                    bodyGyro.Parent = hrp
                    
                    -- Rotaciona
                    bodyGyro.CFrame = bodyGyro.CFrame * CFrame.Angles(0, math.rad(SpinToFly.Speed), 0)
                    
                    -- Empurra outros jogadores
                    for _, player in pairs(Players:GetPlayers()) do
                        if player ~= LocalPlayer and player.Character then
                            local targetHrp = player.Character:FindFirstChild("HumanoidRootPart")
                            if targetHrp then
                                local distance = (hrp.Position - targetHrp.Position).Magnitude
                                if distance < 20 then
                                    -- Aplica força para cima
                                    local bodyVelocity = targetHrp:FindFirstChild("SpinForce") or Instance.new("BodyVelocity")
                                    bodyVelocity.Name = "SpinForce"
                                    bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                                    bodyVelocity.Velocity = Vector3.new(0, SpinToFly.Power, 0)
                                    bodyVelocity.Parent = targetHrp
                                    
                                    game:GetService("Debris"):AddItem(bodyVelocity, 0.1)
                                end
                            end
                        end
                    end
                else
                    break
                end
                task.wait(0.03)
            end
            
            -- Limpa ao desativar
            if LocalPlayer.Character then
                local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                if hrp then
                    local gyro = hrp:FindFirstChild("SpinGyro")
                    if gyro then gyro:Destroy() end
                end
            end
        end)
    end
end

-- ═══════════════════════════════════════════════════
--                  JERK OFF ANIMATION
-- ═══════════════════════════════════════════════════

local JerkOff = {
    Active = false,
    AnimationId = "rbxassetid://148840371" -- ID genérico, ajuste conforme necessário
}

local function ToggleJerkOff()
    JerkOff.Active = not JerkOff.Active
    
    if JerkOff.Active then
        spawn(function()
            while JerkOff.Active and LocalPlayer.Character do
                local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
                if humanoid then
                    -- Animação customizada
                    local animator = humanoid:FindFirstChildOfClass("Animator")
                    if animator then
                        local anim = Instance.new("Animation")
                        anim.AnimationId = JerkOff.AnimationId
                        local track = animator:LoadAnimation(anim)
                        track:Play()
                        task.wait(track.Length or 2)
                    else
                        task.wait(2)
                    end
                else
                    break
                end
            end
        end)
    end
end

-- ═══════════════════════════════════════════════════
--              ATTACH TO PLAYER (POSIÇÕES)
-- ═══════════════════════════════════════════════════

local AttachSystem = {
    Enabled = false,
    TargetPlayer = nil,
    Position = "Head", -- Head, Torso, Back, Side
    Offset = Vector3.new(0, 2, 0)
}

local AttachPositions = {
    Head = Vector3.new(0, 2, 0),
    Torso = Vector3.new(0, 0, 2),
    Back = Vector3.new(0, 0, -2),
    Side = Vector3.new(2, 0, 0),
    Sit = Vector3.new(0, 1, 0)
}

local function AttachToPlayer(targetPlayer, position)
    if not targetPlayer or not targetPlayer.Character then return end
    
    AttachSystem.TargetPlayer = targetPlayer
    AttachSystem.Position = position
    AttachSystem.Offset = AttachPositions[position] or Vector3.new(0, 2, 0)
    AttachSystem.Enabled = true
    
    spawn(function()
        while AttachSystem.Enabled and LocalPlayer.Character and AttachSystem.TargetPlayer.Character do
            local myHrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            local targetHrp = AttachSystem.TargetPlayer.Character:FindFirstChild("HumanoidRootPart")
            
            if myHrp and targetHrp then
                myHrp.CFrame = targetHrp.CFrame * CFrame.new(AttachSystem.Offset)
                
                -- Força a posição
                local bodyPos = myHrp:FindFirstChild("AttachPos") or Instance.new("BodyPosition")
                bodyPos.Name = "AttachPos"
                bodyPos.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                bodyPos.Position = targetHrp.Position + AttachSystem.Offset
                bodyPos.Parent = myHrp
                
                -- Se for "Sit", muda a pose
                if position == "Sit" then
                    local humanoid = LocalPlayer.Character:FindFirstChild("Humanoid")
                    if humanoid then
                        humanoid.Sit = true
                    end
                end
            else
                break
            end
            task.wait()
        end
        
        -- Limpa
        if LocalPlayer.Character then
            local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if hrp then
                local bp = hrp:FindFirstChild("AttachPos")
                if bp then bp:Destroy() end
            end
        end
    end)
end

local function DetachFromPlayer()
    AttachSystem.Enabled = false
end

-- ═══════════════════════════════════════════════════
--              SPECTATE CAMERA (ESPIAR)
-- ═══════════════════════════════════════════════════

local SpectateMode = {
    Active = false,
    TargetPlayer = nil,
    OriginalCFrame = nil
}

local function SpectatePlayer(targetPlayer)
    if not targetPlayer or not targetPlayer.Character then return end
    
    local camera = workspace.CurrentCamera
    SpectateMode.OriginalCFrame = camera.CFrame
    SpectateMode.TargetPlayer = targetPlayer
    SpectateMode.Active = true
    
    camera.CameraSubject = targetPlayer.Character:FindFirstChild("Humanoid")
    
    print("👁️ Especando: " .. targetPlayer.Name)
end

local function StopSpectate()
    if not SpectateMode.Active then return end
    
    local camera = workspace.CurrentCamera
    camera.CameraSubject = LocalPlayer.Character:FindFirstChild("Humanoid")
    
    SpectateMode.Active = false
    SpectateMode.TargetPlayer = nil
    
    print("👁️ Spectate desativado")
end

-- ═══════════════════════════════════════════════════
--                  INVISIBILIDADE
-- ═══════════════════════════════════════════════════

local Invisible = {
    Active = false,
    OriginalTransparency = {}
}

local function ToggleInvisible()
    Invisible.Active = not Invisible.Active
    
    if Invisible.Active then
        -- Salva transparências originais
        for _, part in pairs(LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                Invisible.OriginalTransparency[part] = part.Transparency
                part.Transparency = 1
            elseif part:IsA("Decal") or part:IsA("Texture") then
                Invisible.OriginalTransparency[part] = part.Transparency
                part.Transparency = 1
            end
        end
        
        -- Esconde acessórios
        for _, accessory in pairs(LocalPlayer.Character:GetChildren()) do
            if accessory:IsA("Accessory") then
                accessory:Destroy()
            end
        end
        
        print("👻 Invisível ativado")
    else
        -- Restaura transparências
        for part, transparency in pairs(Invisible.OriginalTransparency) do
            if part and part.Parent then
                part.Transparency = transparency
            end
        end
        
        Invisible.OriginalTransparency = {}
        print("👁️ Visível novamente")
    end
end

-- ═══════════════════════════════════════════════════
--                  REPLAY SYSTEM
-- ═══════════════════════════════════════════════════

local ReplaySystem = {
    Recording = false,
    RecordedFrames = {},
    Playing = false,
    RecordInterval = 0.1
}

local function StartRecording()
    ReplaySystem.Recording = true
    ReplaySystem.RecordedFrames = {}
    
    spawn(function()
        while ReplaySystem.Recording and LocalPlayer.Character do
            local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if hrp then
                table.insert(ReplaySystem.RecordedFrames, {
                    CFrame = hrp.CFrame,
                    Time = tick()
                })
            end
            task.wait(ReplaySystem.RecordInterval)
        end
    end)
    
    print("🎬 Gravação iniciada")
end

local function StopRecording()
    ReplaySystem.Recording = false
    print("🎬 Gravação finalizada - " .. #ReplaySystem.RecordedFrames .. " frames")
end

local function PlayReplay()
    if #ReplaySystem.RecordedFrames == 0 then
        print("❌ Nenhuma gravação disponível")
        return
    end
    
    ReplaySystem.Playing = true
    
    spawn(function()
        for i, frame in ipairs(ReplaySystem.RecordedFrames) do
            if not ReplaySystem.Playing then break end
            
            local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
            if hrp then
                hrp.CFrame = frame.CFrame
            end
            
            task.wait(ReplaySystem.RecordInterval)
        end
        
        ReplaySystem.Playing = false
        print("🎬 Replay finalizado")
    end)
end

local function StopReplay()
    ReplaySystem.Playing = false
end

-- ═══════════════════════════════════════════════════
--              FLIP (MORTAL) ANIMATIONS
-- ═══════════════════════════════════════════════════

local function FrontFlip()
    local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    
    local startCFrame = hrp.CFrame
    
    for i = 0, 1, 0.05 do
        hrp.CFrame = startCFrame * CFrame.Angles(math.rad(360 * i), 0, 0) * CFrame.new(0, 5 * math.sin(math.pi * i), 0)
        task.wait(0.03)
    end
end

local function BackFlip()
    local hrp = LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    
    local startCFrame = hrp.CFrame
    
    for i = 0, 1, 0.05 do
        hrp.CFrame = startCFrame * CFrame.Angles(math.rad(-360 * i), 0, 0) * CFrame.new(0, 5 * math.sin(math.pi * i), 0)
        task.wait(0.03)
    end
end

-- ═══════════════════════════════════════════════════
--                      GUI
-- ═══════════════════════════════════════════════════

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FeaturesHubV1"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = LocalPlayer.PlayerGui

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 480, 0, 620)
MainFrame.Position = UDim2.new(0.5, -240, 0.5, -310)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 15)

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 60)
Header.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
Header.BorderSizePixel = 0
Header.Parent = MainFrame

Instance.new("UICorner", Header).CornerRadius = UDim.new(0, 15)

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
Title.Text = "🔥 FEATURES HUB V1"
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

local function CreateButton(name, callback)
    local button = Instance.new("Frame")
    button.Size = UDim2.new(1, -10, 0, 45)
    button.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    button.BorderSizePixel = 0
    button.Parent = ContentFrame
    
    Instance.new("UICorner", button).CornerRadius = UDim.new(0, 8)
    
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 1, -10)
    btn.Position = UDim2.new(0, 10, 0, 5)
    btn.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
    btn.Text = name
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 15
    btn.Font = Enum.Font.GothamBold
    btn.Parent = button
    
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 6)
    
    btn.MouseButton1Click:Connect(callback)
    
    return button
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

-- Criar GUI
CreateSection("🌀 SPIN TO FLY")
CreateToggle("Ativar Spin to Fly", false, function(enabled)
    if enabled then
        ToggleSpinToFly()
        if not SpinToFly.Enabled then
            ToggleSpinToFly()
        end
    else
        if SpinToFly.Enabled then
            ToggleSpinToFly()
        end
    end
end)

CreateSection("💃 ANIMAÇÕES")
CreateToggle("Jerk Off Animation", false, function(enabled)
    if enabled then
        if not JerkOff.Active then
            ToggleJerkOff()
        end
    else
        if JerkOff.Active then
            ToggleJerkOff()
        end
    end
end)
CreateButton("🤸 Mortal Frente", FrontFlip)
CreateButton("🤸 Mortal Trás", BackFlip)

CreateSection("📌 GRUDAR EM JOGADOR")

-- Função para atualizar lista de jogadores
local function GetPlayerNames()
    local names = {}
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer then
            table.insert(names, player.Name)
        end
    end
    return names
end

-- Variável para armazenar o jogador selecionado
local SelectedAttachPlayer = nil
local SelectedPosition = "Head"

CreateDropdown("Selecionar Jogador", GetPlayerNames(), function(selectedName)
    for _, player in pairs(Players:GetPlayers()) do
        if player.Name == selectedName then
            SelectedAttachPlayer = player
            print("✅ Jogador selecionado: " .. selectedName)
            break
        end
    end
end)

CreateDropdown("Posição", {"Head", "Torso", "Back", "Side", "Sit"}, function(position)
    SelectedPosition = position
    print("✅ Posição selecionada: " .. position)
end)

CreateButton("✅ Grudar no Jogador", function()
    if SelectedAttachPlayer then
        AttachToPlayer(SelectedAttachPlayer, SelectedPosition)
        print("✅ Grudado em " .. SelectedAttachPlayer.Name .. " na posição " .. SelectedPosition)
    else
        print("❌ Selecione um jogador primeiro!")
    end
end)

CreateButton("❌ Desgrudar", DetachFromPlayer)

CreateSection("👁️ SPECTATE (ESPIAR)")

local SelectedSpectatePlayer = nil

CreateDropdown("Espiar Jogador", GetPlayerNames(), function(selectedName)
    for _, player in pairs(Players:GetPlayers()) do
        if player.Name == selectedName then
            SelectedSpectatePlayer = player
            print("✅ Jogador para espiar selecionado: " .. selectedName)
            break
        end
    end
end)

CreateButton("👁️ Começar a Espiar", function()
    if SelectedSpectatePlayer then
        SpectatePlayer(SelectedSpectatePlayer)
    else
        print("❌ Selecione um jogador primeiro!")
    end
end)

CreateButton("👁️ Parar de Espiar", StopSpectate)

CreateSection("👻 INVISIBILIDADE")
CreateToggle("Ficar Invisível", false, function(enabled)
    if enabled then
        if not Invisible.Active then
            ToggleInvisible()
        end
    else
        if Invisible.Active then
            ToggleInvisible()
        end
    end
end)

CreateSection("🎬 REPLAY SYSTEM")
CreateButton("▶️ Iniciar Gravação", StartRecording)
CreateButton("⏹️ Parar Gravação", StopRecording)
CreateButton("🎬 Reproduzir Replay", PlayReplay)
CreateButton("⏸️ Parar Replay", StopReplay)

CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

-- Botão de toggle
local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 50, 0, 50)
ToggleButton.Position = UDim2.new(0, 10, 0.5, -25)
ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
ToggleButton.Text = "F"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.TextSize = 28
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.Parent = ScreenGui

Instance.new("UICorner", ToggleButton).CornerRadius = UDim.new(1, 0)

ToggleButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- Notificação inicial
local function ShowNotification()
    local notif = Instance.new("Frame")
    notif.Size = UDim2.new(0, 400, 0, 130)
    notif.Position = UDim2.new(0.5, -200, 0, -140)
    notif.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
    notif.BorderSizePixel = 0
    notif.Parent = ScreenGui
    
    Instance.new("UICorner", notif).CornerRadius = UDim.new(0, 15)
    
    local text = Instance.new("TextLabel")
    text.Size = UDim2.new(1, -20, 1, -20)
    text.Position = UDim2.new(0, 10, 0, 10)
    text.BackgroundTransparency = 1
    text.Text = "🔥 FEATURES HUB V1 CARREGADO!\n\n✅ Todas as features ativas!\n🎮 Pressione 'F' para abrir o menu!\n💡 Divirta-se!"
    text.TextColor3 = Color3.fromRGB(255, 255, 255)
    text.TextSize = 16
    text.Font = Enum.Font.GothamBold
    text.Parent = notif
    
    -- Animação
    notif:TweenPosition(UDim2.new(0.5, -200, 0, 20), "Out", "Elastic", 0.8, true)
    
    task.wait(4)
    
    notif:TweenPosition(UDim2.new(0.5, -200, 0, -140), "In", "Back", 0.5, true)
    task.wait(0.5)
    notif:Destroy()
end

ShowNotification()

print("✅ FEATURES HUB V1 carregado!")
print("🔥 Todas as features disponíveis!")
print("💡 Clique no botão 'F' para abrir o menu!")
