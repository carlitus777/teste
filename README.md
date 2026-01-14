-- 🧠 BRAINROTS HUB - FUJA DO TSUNAMI 🧠
-- Script feito por Carlos ❤️


-- =========================
-- GUI DE KEY - BRAINROTS HUB
-- =========================
 
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer
 
local VERIFY_URL = "https://a5d33e79-eeee-48d9-930f-9ce66213b166-00-9dep1zxqcpf8.janeway.replit.dev/verify?key="
 
-- GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "KeySystem"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = player:WaitForChild("PlayerGui")
 
local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 350, 0, 200)
Frame.Position = UDim2.new(0.5, -175, 0.5, -100)
Frame.BackgroundColor3 = Color3.fromRGB(25,25,35)
Frame.Active = true
Frame.Draggable = true
 
Instance.new("UICorner", Frame).CornerRadius = UDim.new(0,12)
 
local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1,0,0,40)
Title.BackgroundTransparency = 1
Title.Text = "🔑 INSIRA SUA KEY"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
 
local Box = Instance.new("TextBox", Frame)
Box.Size = UDim2.new(0.9,0,0,40)
Box.Position = UDim2.new(0.05,0,0.4,0)
Box.PlaceholderText = "Cole sua key aqui"
Box.Text = ""
Box.TextColor3 = Color3.new(1,1,1)
Box.BackgroundColor3 = Color3.fromRGB(35,35,50)
Box.Font = Enum.Font.Gotham
Box.TextSize = 14
Box.ClearTextOnFocus = false
 
Instance.new("UICorner", Box).CornerRadius = UDim.new(0,8)
 
local Button = Instance.new("TextButton", Frame)
Button.Size = UDim2.new(0.9,0,0,40)
Button.Position = UDim2.new(0.05,0,0.7,0)
Button.Text = "VERIFICAR KEY"
Button.BackgroundColor3 = Color3.fromRGB(255,0,150)
Button.TextColor3 = Color3.new(1,1,1)
Button.Font = Enum.Font.GothamBold
Button.TextSize = 15
 
Instance.new("UICorner", Button).CornerRadius = UDim.new(0,8)
 
-- VERIFICAÇÃO
local verified = false
 
Button.MouseButton1Click:Connect(function()
    if Box.Text == "" then
        Button.Text = "Digite uma key"
        return
    end
 
    Button.Text = "Verificando..."
 
    local success, response = pcall(function()
        return game:HttpGet(VERIFY_URL .. Box.Text)
    end)
 
    if not success then
        Button.Text = "Erro de conexão"
        return
    end
 
    local data = HttpService:JSONDecode(response)
 
    if data.status == "ok" then
        verified = true
        ScreenGui:Destroy()
        print("✅ Key válida, script liberado")
    else
        Button.Text = "Key inválida"
    end
end)
 
-- BLOQUEIA O SCRIPT ATÉ VALIDAR
repeat task.wait() until verified


print("🧠 BRAINROTS HUB carregando...")

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local RunService = game:GetService("RunService")

-- Aguardar o PlayerGui carregar
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- ═══════════════════════════════════════════════════
--                  CONFIGURAÇÕES
-- ═══════════════════════════════════════════════════

local Settings = {
    AutoCollect = {
        Enabled = false,
        Interval = 2
    },
    AutoUpgradeBrainrots = {
        Enabled = false,
        Interval = 2
    },
    AutoRebirth = {
        Enabled = false,
        Interval = 5
    },
    AutoSpeedUpgrade = {
        Enabled = false,
        Interval = 3
    },
    AutoBaseUpgrade = {
        Enabled = false,
        Interval = 3
    },
    CurrentTab = "Auto"
}

-- ═══════════════════════════════════════════════════
--            FUNÇÃO DE AUTO COLLECT
-- ═══════════════════════════════════════════════════

local isCollecting = false

local function CollectAllSlots()
    if isCollecting then return end
    isCollecting = true
    
    local slots = {"Slot1", "Slot2", "Slot3", "Slot4", "Slot5", "Slot6", "Slot7", "Slot8", "Slot9", "Slot10", "Slot11", "Slot12", "Slot13", "Slot14", "Slot15", "Slot16", "Slot17", "Slot18", "Slot19", "Slot20", "Slot21", "Slot22", "Slot23", "Slot24", "Slot25", "Slot26", "Slot27", "Slot28", "Slot29", "Slot30"}
    
    for _, slot in ipairs(slots) do
        pcall(function()
            local args = {slot}
            ReplicatedStorage:WaitForChild("RemoteEvents"):WaitForChild("CollectMoney"):FireServer(unpack(args))
        end)
        task.wait(0.1)
    end
    
    isCollecting = false
end

task.spawn(function()
    while task.wait(Settings.AutoCollect.Interval) do
        if Settings.AutoCollect.Enabled then
            CollectAllSlots()
        end
    end
end)

-- ═══════════════════════════════════════════════════
--        FUNÇÃO DE AUTO UPGRADE BRAINROTS
-- ═══════════════════════════════════════════════════

local isUpgradingBrainrots = false

local function UpgradeAllBrainrots()
    if isUpgradingBrainrots then return end
    isUpgradingBrainrots = true
    
    local slots = {"Slot2", "Slot3", "Slot4", "Slot5", "Slot1", "Slot7", "Slot8", "Slot9", "Slot10", "Slot6", "Slot11", "Slot12", "Slot13", "Slot14", "Slot15", "Slot16", "Slot17", "Slot18", "Slot19", "Slot20", "Slot21", "Slot22", "Slot23", "Slot24", "Slot25", "Slot26", "Slot27", "Slot28", "Slot29", "Slot30"}
    
    for _, slot in ipairs(slots) do
        pcall(function()
            local args = {slot}
            ReplicatedStorage:WaitForChild("RemoteFunctions"):WaitForChild("UpgradeBrainrot"):InvokeServer(unpack(args))
        end)
        task.wait(0.1)
    end
    
    isUpgradingBrainrots = false
end

task.spawn(function()
    while task.wait(Settings.AutoUpgradeBrainrots.Interval) do
        if Settings.AutoUpgradeBrainrots.Enabled then
            UpgradeAllBrainrots()
        end
    end
end)

-- ═══════════════════════════════════════════════════
--            FUNÇÃO DE UPGRADE CARRY
-- ═══════════════════════════════════════════════════

local function UpgradeCarry()
    local success, err = pcall(function()
        ReplicatedStorage:WaitForChild("RemoteFunctions"):WaitForChild("UpgradeCarry"):InvokeServer()
    end)
    
    if success then
        return true, "✅ Upgrade Carry executado!"
    else
        return false, "❌ Erro: " .. tostring(err)
    end
end

-- ═══════════════════════════════════════════════════
--            FUNÇÃO DE AUTO REBIRTH
-- ═══════════════════════════════════════════════════

local function AutoRebirth()
    local success, err = pcall(function()
        ReplicatedStorage:WaitForChild("RemoteFunctions"):WaitForChild("Rebirth"):InvokeServer()
    end)
    
    if success then
        return true, "✅ Rebirth executado!"
    else
        return false, "❌ Erro: " .. tostring(err)
    end
end

task.spawn(function()
    while task.wait(Settings.AutoRebirth.Interval) do
        if Settings.AutoRebirth.Enabled then
            AutoRebirth()
        end
    end
end)

-- ═══════════════════════════════════════════════════
--          FUNÇÃO DE UPGRADE SPEED
-- ═══════════════════════════════════════════════════

local function UpgradeSpeed()
    local success, err = pcall(function()
        local args = {10}
        ReplicatedStorage:WaitForChild("RemoteFunctions"):WaitForChild("UpgradeSpeed"):InvokeServer(unpack(args))
    end)
    
    if success then
        return true, "✅ Speed Upgrade executado!"
    else
        return false, "❌ Erro: " .. tostring(err)
    end
end

task.spawn(function()
    while task.wait(Settings.AutoSpeedUpgrade.Interval) do
        if Settings.AutoSpeedUpgrade.Enabled then
            UpgradeSpeed()
        end
    end
end)

-- ═══════════════════════════════════════════════════
--            FUNÇÃO DE UPGRADE BASE
-- ═══════════════════════════════════════════════════

local function UpgradeBase()
    local success, err = pcall(function()
        ReplicatedStorage:WaitForChild("RemoteFunctions"):WaitForChild("UpgradeBase"):InvokeServer()
    end)
    
    if success then
        return true, "✅ Base Upgrade executado!"
    else
        return false, "❌ Erro: " .. tostring(err)
    end
end

task.spawn(function()
    while task.wait(Settings.AutoBaseUpgrade.Interval) do
        if Settings.AutoBaseUpgrade.Enabled then
            UpgradeBase()
        end
    end
end)

-- ═══════════════════════════════════════════════════
--                      GUI
-- ═══════════════════════════════════════════════════

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BrainrotsHub"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 450, 0, 600)
MainFrame.Position = UDim2.new(0.5, -225, 0.5, -300)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 15)

-- Header
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
Title.Size = UDim2.new(1, -20, 0.5, 0)
Title.Position = UDim2.new(0, 10, 0, 5)
Title.BackgroundTransparency = 1
Title.Text = "🧠 BRAINROTS HUB"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 22
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

local GameName = Instance.new("TextLabel")
GameName.Size = UDim2.new(1, -20, 0.3, 0)
GameName.Position = UDim2.new(0, 10, 0.45, 0)
GameName.BackgroundTransparency = 1
GameName.Text = "Fuja do Tsunami"
GameName.TextColor3 = Color3.fromRGB(200, 200, 255)
GameName.TextSize = 13
GameName.Font = Enum.Font.GothamBold
GameName.TextXAlignment = Enum.TextXAlignment.Left
GameName.Parent = Header

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(1, -20, 0, 15)
Subtitle.Position = UDim2.new(0, 10, 1, -20)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = "Script feito por Carlos"
Subtitle.TextColor3 = Color3.fromRGB(200, 200, 200)
Subtitle.TextSize = 11
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextXAlignment = Enum.TextXAlignment.Left
Subtitle.Parent = Header

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

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Tabs
local TabFrame = Instance.new("Frame")
TabFrame.Size = UDim2.new(1, -20, 0, 45)
TabFrame.Position = UDim2.new(0, 10, 0, 70)
TabFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
TabFrame.BorderSizePixel = 0
TabFrame.Parent = MainFrame

Instance.new("UICorner", TabFrame).CornerRadius = UDim.new(0, 10)

local AutoTab = Instance.new("TextButton")
AutoTab.Size = UDim2.new(0.48, 0, 0, 35)
AutoTab.Position = UDim2.new(0.02, 0, 0.5, -17.5)
AutoTab.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
AutoTab.Text = "🔄 AUTO"
AutoTab.TextColor3 = Color3.fromRGB(255, 255, 255)
AutoTab.TextSize = 16
AutoTab.Font = Enum.Font.GothamBold
AutoTab.Parent = TabFrame

Instance.new("UICorner", AutoTab).CornerRadius = UDim.new(0, 8)

local ManualTab = Instance.new("TextButton")
ManualTab.Size = UDim2.new(0.48, 0, 0, 35)
ManualTab.Position = UDim2.new(0.5, 0, 0.5, -17.5)
ManualTab.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
ManualTab.Text = "✋ MANUAL"
ManualTab.TextColor3 = Color3.fromRGB(200, 200, 200)
ManualTab.TextSize = 16
ManualTab.Font = Enum.Font.GothamBold
ManualTab.Parent = TabFrame

Instance.new("UICorner", ManualTab).CornerRadius = UDim.new(0, 8)

-- Content
local ContentFrame = Instance.new("ScrollingFrame")
ContentFrame.Size = UDim2.new(1, -20, 1, -135)
ContentFrame.Position = UDim2.new(0, 10, 0, 125)
ContentFrame.BackgroundTransparency = 1
ContentFrame.BorderSizePixel = 0
ContentFrame.ScrollBarThickness = 6
ContentFrame.Parent = MainFrame

local AutoContent = Instance.new("Frame")
AutoContent.Name = "AutoContent"
AutoContent.Size = UDim2.new(1, 0, 0, 900)
AutoContent.BackgroundTransparency = 1
AutoContent.Visible = true
AutoContent.Parent = ContentFrame

local AutoLayout = Instance.new("UIListLayout")
AutoLayout.Padding = UDim.new(0, 10)
AutoLayout.Parent = AutoContent

local ManualContent = Instance.new("Frame")
ManualContent.Name = "ManualContent"
ManualContent.Size = UDim2.new(1, 0, 0, 600)
ManualContent.BackgroundTransparency = 1
ManualContent.Visible = false
ManualContent.Parent = ContentFrame

local ManualLayout = Instance.new("UIListLayout")
ManualLayout.Padding = UDim.new(0, 10)
ManualLayout.Parent = ManualContent

-- Função para criar elementos
local function CreateToggle(name, default, callback, parent)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -10, 0, 40)
    frame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    frame.BorderSizePixel = 0
    frame.Parent = parent
    
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 8)
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(0.7, 0, 1, 0)
    label.Position = UDim2.new(0, 10, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = name
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame
    
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 60, 0, 30)
    button.Position = UDim2.new(1, -70, 0.5, -15)
    button.BackgroundColor3 = default and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
    button.Text = default and "ON" or "OFF"
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 14
    button.Font = Enum.Font.GothamBold
    button.Parent = frame
    
    Instance.new("UICorner", button).CornerRadius = UDim.new(0, 8)
    
    local enabled = default
    
    button.MouseButton1Click:Connect(function()
        enabled = not enabled
        button.BackgroundColor3 = enabled and Color3.fromRGB(0, 200, 0) or Color3.fromRGB(200, 0, 0)
        button.Text = enabled and "ON" or "OFF"
        callback(enabled)
    end)
end

local function CreateButton(name, callback, parent)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -10, 0, 45)
    frame.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
    frame.BorderSizePixel = 0
    frame.Parent = parent
    
    Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 8)
    
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.9, 0, 0, 35)
    button.Position = UDim2.new(0.05, 0, 0.5, -17.5)
    button.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
    button.Text = name
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 15
    button.Font = Enum.Font.GothamBold
    button.Parent = frame
    
    Instance.new("UICorner", button).CornerRadius = UDim.new(0, 8)
    
    button.MouseButton1Click:Connect(callback)
end

-- AUTO TAB
CreateToggle("💰 Auto Collect (30 Slots)", false, function(v)
    Settings.AutoCollect.Enabled = v
    print(v and "✅ Auto Collect ATIVADO!" or "❌ Auto Collect DESATIVADO!")
end, AutoContent)

CreateToggle("🧠 Auto Upgrade Brainrots (30 Slots)", false, function(v)
    Settings.AutoUpgradeBrainrots.Enabled = v
    print(v and "✅ Auto Upgrade Brainrots ATIVADO!" or "❌ Auto Upgrade Brainrots DESATIVADO!")
end, AutoContent)

CreateToggle("🔄 Auto Rebirth", false, function(v)
    Settings.AutoRebirth.Enabled = v
    print(v and "✅ Auto Rebirth ATIVADO!" or "❌ Auto Rebirth DESATIVADO!")
end, AutoContent)

CreateToggle("⚡ Auto Speed Upgrade", false, function(v)
    Settings.AutoSpeedUpgrade.Enabled = v
    print(v and "✅ Auto Speed Upgrade ATIVADO!" or "❌ Auto Speed Upgrade DESATIVADO!")
end, AutoContent)

CreateToggle("🏠 Auto Base Upgrade", false, function(v)
    Settings.AutoBaseUpgrade.Enabled = v
    print(v and "✅ Auto Base Upgrade ATIVADO!" or "❌ Auto Base Upgrade DESATIVADO!")
end, AutoContent)

-- MANUAL TAB
CreateButton("💰 Coletar Agora", function()
    print("💰 Coletando manualmente...")
    CollectAllSlots()
end, ManualContent)

CreateButton("📦 Upgrade Carry", function()
    local s, m = UpgradeCarry()
    print(m)
end, ManualContent)

CreateButton("🧠 Upgrade Brainrots", function()
    print("🧠 Fazendo upgrade...")
    UpgradeAllBrainrots()
end, ManualContent)

CreateButton("🔄 Rebirth Agora", function()
    local s, m = AutoRebirth()
    print(m)
end, ManualContent)

CreateButton("⚡ Speed Upgrade", function()
    local s, m = UpgradeSpeed()
    print(m)
end, ManualContent)

CreateButton("🏠 Base Upgrade", function()
    local s, m = UpgradeBase()
    print(m)
end, ManualContent)

-- Tab System
local function SwitchTab(tab)
    if tab == "Auto" then
        AutoContent.Visible = true
        ManualContent.Visible = false
        AutoTab.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
        AutoTab.TextColor3 = Color3.fromRGB(255, 255, 255)
        ManualTab.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        ManualTab.TextColor3 = Color3.fromRGB(200, 200, 200)
    else
        AutoContent.Visible = false
        ManualContent.Visible = true
        ManualTab.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
        ManualTab.TextColor3 = Color3.fromRGB(255, 255, 255)
        AutoTab.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
        AutoTab.TextColor3 = Color3.fromRGB(200, 200, 200)
    end
end

AutoTab.MouseButton1Click:Connect(function() SwitchTab("Auto") end)
ManualTab.MouseButton1Click:Connect(function() SwitchTab("Manual") end)

-- Toggle Button
local ToggleBtn = Instance.new("TextButton")
ToggleBtn.Size = UDim2.new(0, 50, 0, 50)
ToggleBtn.Position = UDim2.new(0, 10, 0.5, -25)
ToggleBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 150)
ToggleBtn.Text = "B"
ToggleBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleBtn.TextSize = 28
ToggleBtn.Font = Enum.Font.GothamBold
ToggleBtn.Parent = ScreenGui

Instance.new("UICorner", ToggleBtn).CornerRadius = UDim.new(1, 0)

ToggleBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

print("✅ BRAINROTS HUB carregado!")
print("👤 Script feito por Carlos")
