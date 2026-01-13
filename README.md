-- ╔══════════════════════════════════════════════════════════╗
-- ║          🧠 BRAINROTS HUB - FUJA DO TSUNAMI 🧠          ║
-- ║              Script feito por Carlos                     ║
-- ║          Ofuscado com proteção avançada                  ║
-- ╚══════════════════════════════════════════════════════════╝

local _G = {}
_G.b64 = "QUJDREVGR0hJSktMTU5PUFFSU1RVVldYWVphYmNkZWZnaGlqa2xtbm9wcXJzdHV2d3h5ejAxMjM0NTY3ODkrLw=="

-- Anti-Decompiler
local function secure(func)
    return coroutine.wrap(function(...)
        while true do
            func(...)
            coroutine.yield()
        end
    end)
end

-- String Encryption
local function decrypt(str)
    return str:gsub(".", function(c)
        return string.char(c:byte() - 3)
    end)
end

-- Variáveis Ofuscadas
local __0x1 = game
local __0x2 = __0x1:GetService(decrypt("Sod|huv"))
local __0x3 = __0x2.LocalPlayer
local __0x4 = __0x1:GetService(decrypt("UhsolfdwhgVwrudjh"))
local __0x5 = __0x3:WaitForChild(decrypt("Sod|hu*xl"))
local __0x6 = Instance.new
local __0x7 = UDim2.new
local __0x8 = Color3.fromRGB
local __0x9 = Enum.Font.GothamBold
local __0xa = Enum.Font.Gotham
local __0xb = task.spawn
local __0xc = task.wait
local __0xd = pcall

-- Configurações Criptografadas
local __cfg = {
    [decrypt("DxwrFroohfw")] = {[decrypt("Hqdeohg")] = false, [decrypt("Lqwhuydo")] = 2},
    [decrypt("DxwrXsjudghEudlqurwv")] = {[decrypt("Hqdeohg")] = false, [decrypt("Lqwhuydo")] = 2},
    [decrypt("DxwrUheluwk")] = {[decrypt("Hqdeohg")] = false, [decrypt("Lqwhuydo")] = 5},
    [decrypt("DxwrVshhgXsjudgh")] = {[decrypt("Hqdeohg")] = false, [decrypt("Lqwhuydo")] = 3},
    [decrypt("DxwrEdvhXsjudgh")] = {[decrypt("Hqdeohg")] = false, [decrypt("Lqwhuydo")] = 3},
    [decrypt("Fxuuhqw0de")] = decrypt("Dxwr")
}

-- Funções Principais Ofuscadas
local __lock1 = false
local function __fn1()
    if __lock1 then return end
    __lock1 = true
    
    local __slots = {}
    for __i = 1, 30 do
        table.insert(__slots, decrypt("Vorw") .. tostring(__i))
    end
    
    for _, __slot in ipairs(__slots) do
        __0xd(function()
            __0x4:WaitForChild(decrypt("UhprwhHyhqwv")):WaitForChild(decrypt("FroohfwPrqh|")):FireServer(__slot)
        end)
        __0xc(0.1)
    end
    
    __lock1 = false
end

__0xb(function()
    while __0xc(__cfg[decrypt("DxwrFroohfw")][decrypt("Lqwhuydo")]) do
        if __cfg[decrypt("DxwrFroohfw")][decrypt("Hqdeohg")] then
            __fn1()
        end
    end
end)

local __lock2 = false
local function __fn2()
    if __lock2 then return end
    __lock2 = true
    
    local __order = {2,3,4,5,1,7,8,9,10,6}
    for __i = 11, 30 do table.insert(__order, __i) end
    
    for _, __idx in ipairs(__order) do
        __0xd(function()
            local __slot = decrypt("Vorw") .. tostring(__idx)
            __0x4:WaitForChild(decrypt("UhprwhIxqfwlrqv")):WaitForChild(decrypt("XsjudghEudlqurw")):InvokeServer(__slot)
        end)
        __0xc(0.1)
    end
    
    __lock2 = false
end

__0xb(function()
    while __0xc(__cfg[decrypt("DxwrXsjudghEudlqurwv")][decrypt("Lqwhuydo")]) do
        if __cfg[decrypt("DxwrXsjudghEudlqurwv")][decrypt("Hqdeohg")] then
            __fn2()
        end
    end
end)

local function __fn3()
    return __0xd(function()
        __0x4:WaitForChild(decrypt("UhprwhIxqfwlrqv")):WaitForChild(decrypt("XsjudghFduu|")):InvokeServer()
    end)
end

local function __fn4()
    return __0xd(function()
        __0x4:WaitForChild(decrypt("UhprwhIxqfwlrqv")):WaitForChild(decrypt("Uheluwk")):InvokeServer()
    end)
end

__0xb(function()
    while __0xc(__cfg[decrypt("DxwrUheluwk")][decrypt("Lqwhuydo")]) do
        if __cfg[decrypt("DxwrUheluwk")][decrypt("Hqdeohg")] then
            __fn4()
        end
    end
end)

local function __fn5()
    return __0xd(function()
        __0x4:WaitForChild(decrypt("UhprwhIxqfwlrqv")):WaitForChild(decrypt("XsjudghVshhg")):InvokeServer(10)
    end)
end

__0xb(function()
    while __0xc(__cfg[decrypt("DxwrVshhgXsjudgh")][decrypt("Lqwhuydo")]) do
        if __cfg[decrypt("DxwrVshhgXsjudgh")][decrypt("Hqdeohg")] then
            __fn5()
        end
    end
end)

local function __fn6()
    return __0xd(function()
        __0x4:WaitForChild(decrypt("UhprwhIxqfwlrqv")):WaitForChild(decrypt("XsjudghEdvh")):InvokeServer()
    end)
end

__0xb(function()
    while __0xc(__cfg[decrypt("DxwrEdvhXsjudgh")][decrypt("Lqwhuydo")]) do
        if __cfg[decrypt("DxwrEdvhXsjudgh")][decrypt("Hqdeohg")] then
            __fn6()
        end
    end
end)

-- GUI Ofuscada
local __gui = __0x6(decrypt("VfuhhqJxl"))
__gui.Name = decrypt("EudlqurwvKxeYU")
__gui.ResetOnSpawn = false
__gui.Parent = __0x5

local __main = __0x6(decrypt("Iudph"))
__main.Size = __0x7(0, 450, 0, 600)
__main.Position = __0x7(0.5, -225, 0.5, -300)
__main.BackgroundColor3 = __0x8(25, 25, 35)
__main.BorderSizePixel = 0
__main.Active = true
__main.Draggable = true
__main.Parent = __gui

__0x6(decrypt("XLFruqhu"), __main).CornerRadius = UDim.new(0, 15)

-- Header
local __header = __0x6(decrypt("Iudph"))
__header.Size = __0x7(1, 0, 0, 60)
__header.BackgroundColor3 = __0x8(255, 0, 150)
__header.BorderSizePixel = 0
__header.Parent = __main

__0x6(decrypt("XLFruqhu"), __header).CornerRadius = UDim.new(0, 15)

local __hfix = __0x6(decrypt("Iudph"))
__hfix.Size = __0x7(1, 0, 0, 15)
__hfix.Position = __0x7(0, 0, 1, -15)
__hfix.BackgroundColor3 = __0x8(255, 0, 150)
__hfix.BorderSizePixel = 0
__hfix.Parent = __header

local __title = __0x6(decrypt("Wh{w0deho"))
__title.Size = __0x7(1, -20, 0.5, 0)
__title.Position = __0x7(0, 10, 0, 5)
__title.BackgroundTransparency = 1
__title.Text = "🧠 " .. decrypt("EUDLQURWV#KXE")
__title.TextColor3 = __0x8(255, 255, 255)
__title.TextSize = 22
__title.Font = __0x9
__title.TextXAlignment = Enum.TextXAlignment.Left
__title.Parent = __header

local __game = __0x6(decrypt("Wh{w0deho"))
__game.Size = __0x7(1, -20, 0.3, 0)
__game.Position = __0x7(0, 10, 0.45, 0)
__game.BackgroundTransparency = 1
__game.Text = decrypt("Ixmd#gr#Wvxqdpl")
__game.TextColor3 = __0x8(200, 200, 255)
__game.TextSize = 13
__game.Font = __0x9
__game.TextXAlignment = Enum.TextXAlignment.Left
__game.Parent = __header

local __sub = __0x6(decrypt("Wh{w0deho"))
__sub.Size = __0x7(1, -20, 0, 15)
__sub.Position = __0x7(0, 10, 1, -20)
__sub.BackgroundTransparency = 1
__sub.Text = decrypt("Vfulvw#ihlwr#sru#Fduorv")
__sub.TextColor3 = __0x8(200, 200, 200)
__sub.TextSize = 11
__sub.Font = __0xa
__sub.TextXAlignment = Enum.TextXAlignment.Left
__sub.Parent = __header

local __close = __0x6(decrypt("Wh{wExwwrq"))
__close.Size = __0x7(0, 40, 0, 40)
__close.Position = __0x7(1, -50, 0, 10)
__close.BackgroundColor3 = __0x8(255, 50, 50)
__close.Text = "X"
__close.TextColor3 = __0x8(255, 255, 255)
__close.TextSize = 20
__close.Font = __0x9
__close.Parent = __header

__0x6(decrypt("XLFruqhu"), __close).CornerRadius = UDim.new(0, 10)

__close.MouseButton1Click:Connect(function()
    __gui:Destroy()
end)

-- Tabs
local __tabs = __0x6(decrypt("Iudph"))
__tabs.Size = __0x7(1, -20, 0, 45)
__tabs.Position = __0x7(0, 10, 0, 70)
__tabs.BackgroundColor3 = __0x8(35, 35, 50)
__tabs.BorderSizePixel = 0
__tabs.Parent = __main

__0x6(decrypt("XLFruqhu"), __tabs).CornerRadius = UDim.new(0, 10)

local __auto = __0x6(decrypt("Wh{wExwwrq"))
__auto.Size = __0x7(0.48, 0, 0, 35)
__auto.Position = __0x7(0.02, 0, 0.5, -17.5)
__auto.BackgroundColor3 = __0x8(255, 0, 150)
__auto.Text = "🔄 " .. decrypt("DXWR")
__auto.TextColor3 = __0x8(255, 255, 255)
__auto.TextSize = 16
__auto.Font = __0x9
__auto.Parent = __tabs

__0x6(decrypt("XLFruqhu"), __auto).CornerRadius = UDim.new(0, 8)

local __manual = __0x6(decrypt("Wh{wExwwrq"))
__manual.Size = __0x7(0.48, 0, 0, 35)
__manual.Position = __0x7(0.5, 0, 0.5, -17.5)
__manual.BackgroundColor3 = __0x8(50, 50, 70)
__manual.Text = "✋ " .. decrypt("PDQXDO")
__manual.TextColor3 = __0x8(200, 200, 200)
__manual.TextSize = 16
__manual.Font = __0x9
__manual.Parent = __tabs

__0x6(decrypt("XLFruqhu"), __manual).CornerRadius = UDim.new(0, 8)

-- Content
local __scroll = __0x6(decrypt("VfuroIudph"))
__scroll.Size = __0x7(1, -20, 1, -135)
__scroll.Position = __0x7(0, 10, 0, 125)
__scroll.BackgroundTransparency = 1
__scroll.BorderSizePixel = 0
__scroll.ScrollBarThickness = 6
__scroll.Parent = __main

local __autoC = __0x6(decrypt("Iudph"))
__autoC.Name = decrypt("DxwrFrqwhqw")
__autoC.Size = __0x7(1, 0, 0, 900)
__autoC.BackgroundTransparency = 1
__autoC.Visible = true
__autoC.Parent = __scroll

__0x6(decrypt("XL0lvw0d|rxw"), __autoC).Padding = UDim.new(0, 10)

local __manualC = __0x6(decrypt("Iudph"))
__manualC.Name = decrypt("PdqxdoFrqwhqw")
__manualC.Size = __0x7(1, 0, 0, 600)
__manualC.BackgroundTransparency = 1
__manualC.Visible = false
__manualC.Parent = __scroll

__0x6(decrypt("XL0lvw0d|rxw"), __manualC).Padding = UDim.new(0, 10)

-- Funções de Criação
local function __toggle(__name, __default, __callback, __parent)
    local __frame = __0x6(decrypt("Iudph"))
    __frame.Size = __0x7(1, -10, 0, 40)
    __frame.BackgroundColor3 = __0x8(35, 35, 50)
    __frame.BorderSizePixel = 0
    __frame.Parent = __parent
    
    __0x6(decrypt("XLFruqhu"), __frame).CornerRadius = UDim.new(0, 8)
    
    local __label = __0x6(decrypt("Wh{w0deho"))
    __label.Size = __0x7(0.7, 0, 1, 0)
    __label.Position = __0x7(0, 10, 0, 0)
    __label.BackgroundTransparency = 1
    __label.Text = __name
    __label.TextColor3 = __0x8(255, 255, 255)
    __label.TextSize = 14
    __label.Font = __0xa
    __label.TextXAlignment = Enum.TextXAlignment.Left
    __label.Parent = __frame
    
    local __btn = __0x6(decrypt("Wh{wExwwrq"))
    __btn.Size = __0x7(0, 60, 0, 30)
    __btn.Position = __0x7(1, -70, 0.5, -15)
    __btn.BackgroundColor3 = __default and __0x8(0, 200, 0) or __0x8(200, 0, 0)
    __btn.Text = __default and "ON" or "OFF"
    __btn.TextColor3 = __0x8(255, 255, 255)
    __btn.TextSize = 14
    __btn.Font = __0x9
    __btn.Parent = __frame
    
    __0x6(decrypt("XLFruqhu"), __btn).CornerRadius = UDim.new(0, 8)
    
    local __state = __default
    
    __btn.MouseButton1Click:Connect(function()
        __state = not __state
        __btn.BackgroundColor3 = __state and __0x8(0, 200, 0) or __0x8(200, 0, 0)
        __btn.Text = __state and "ON" or "OFF"
        __callback(__state)
    end)
end

local function __button(__name, __callback, __parent)
    local __frame = __0x6(decrypt("Iudph"))
    __frame.Size = __0x7(1, -10, 0, 45)
    __frame.BackgroundColor3 = __0x8(35, 35, 50)
    __frame.BorderSizePixel = 0
    __frame.Parent = __parent
    
    __0x6(decrypt("XLFruqhu"), __frame).CornerRadius = UDim.new(0, 8)
    
    local __btn = __0x6(decrypt("Wh{wExwwrq"))
    __btn.Size = __0x7(0.9, 0, 0, 35)
    __btn.Position = __0x7(0.05, 0, 0.5, -17.5)
    __btn.BackgroundColor3 = __0x8(255, 0, 150)
    __btn.Text = __name
    __btn.TextColor3 = __0x8(255, 255, 255)
    __btn.TextSize = 15
    __btn.Font = __0x9
    __btn.Parent = __frame
    
    __0x6(decrypt("XLFruqhu"), __btn).CornerRadius = UDim.new(0, 8)
    
    __btn.MouseButton1Click:Connect(__callback)
end

-- Criar Elementos AUTO
__toggle("💰 " .. decrypt("Dxwr#Froohfw#+63#Vorwv,"), false, function(__v)
    __cfg[decrypt("DxwrFroohfw")][decrypt("Hqdeohg")] = __v
    print(__v and "✅ Auto Collect ATIVADO!" or "❌ Auto Collect DESATIVADO!")
end, __autoC)

__toggle("🧠 " .. decrypt("Dxwr#Xsjudgh#Eudlqurwv#+ 63#Vorwv,"), false, function(__v)
    __cfg[decrypt("DxwrXsjudghEudlqurwv")][decrypt("Hqdeohg")] = __v
    print(__v and "✅ Auto Upgrade Brainrots ATIVADO!" or "❌ Auto Upgrade Brainrots DESATIVADO!")
end, __autoC)

__toggle("🔄 " .. decrypt("Dxwr#Uheluwk"), false, function(__v)
    __cfg[decrypt("DxwrUheluwk")][decrypt("Hqdeohg")] = __v
    print(__v and "✅ Auto Rebirth ATIVADO!" or "❌ Auto Rebirth DESATIVADO!")
end, __autoC)

__toggle("⚡ " .. decrypt("Dxwr#Vshhg#Xsjudgh"), false, function(__v)
    __cfg[decrypt("DxwrVshhgXsjudgh")][decrypt("Hqdeohg")] = __v
    print(__v and "✅ Auto Speed Upgrade ATIVADO!" or "❌ Auto Speed Upgrade DESATIVADO!")
end, __autoC)

__toggle("🏠 " .. decrypt("Dxwr#Edvh#Xsjudgh"), false, function(__v)
    __cfg[decrypt("DxwrEdvhXsjudgh")][decrypt("Hqdeohg")] = __v
    print(__v and "✅ Auto Base Upgrade ATIVADO!" or "❌ Auto Base Upgrade DESATIVADO!")
end, __autoC)

-- Criar Elementos MANUAL
__button("💰 " .. decrypt("Froohwdu#Djrud"), function()
    print("💰 Coletando manualmente...")
    __fn1()
end, __manualC)

__button("📦 " .. decrypt("Xsjudgh#Fduu|"), function()
    local __s, __m = __fn3()
    print(__m or (__s and "✅ Upgrade Carry executado!" or "❌ Erro"))
end, __manualC)

__button("🧠 " .. decrypt("Xsjudgh#Eudlqurwv"), function()
    print("🧠 Fazendo upgrade...")
    __fn2()
end, __manualC)

__button("🔄 " .. decrypt("Uheluwk#Djrud"), function()
    local __s, __m = __fn4()
    print(__m or (__s and "✅ Rebirth executado!" or "❌ Erro"))
end, __manualC)

__button("⚡ " .. decrypt("Vshhg#Xsjudgh"), function()
    local __s, __m = __fn5()
    print(__m or (__s and "✅ Speed Upgrade executado!" or "❌ Erro"))
end, __manualC)

__button("🏠 " .. decrypt("Edvh#Xsjudgh"), function()
    local __s, __m = __fn6()
    print(__m or (__s and "✅ Base Upgrade executado!" or "❌ Erro"))
end, __manualC)

-- Sistema de Tabs
local function __switch(__tab)
    if __tab == decrypt("Dxwr") then
        __autoC.Visible = true
        __manualC.Visible = false
        __auto.BackgroundColor3 = __0x8(255, 0, 150)
        __auto.TextColor3 = __0x8(255, 255, 255)
        __manual.BackgroundColor3 = __0x8(50, 50, 70)
        __manual.TextColor3 = __0x8(200, 200, 200)
    else
        __autoC.Visible = false
        __manualC.Visible = true
        __manual.BackgroundColor3 = __0x8(255, 0, 150)
        __manual.TextColor3 = __0x8(255, 255, 255)
        __auto.BackgroundColor3 = __0x8(50, 50, 70)
        __auto.TextColor3 = __0x8(200, 200, 200)
    end
end

__auto.MouseButton1Click:Connect(function()
    __switch(decrypt("Dxwr"))
end)

__manual.MouseButton1Click:Connect(function()
    __switch(decrypt("Pdqxdo"))
end)

-- Toggle Button
local __toggle_btn = __0x6(decrypt("Wh{wExwwrq"))
__toggle_btn.Size = __0x7(0, 50, 0, 50)
__toggle_btn.Position = __0x7(0, 10, 0.5, -25)
__toggle_btn.BackgroundColor3 = __0x8(255, 0, 150)
__toggle_btn.Text = "B"
__toggle_btn.TextColor3 = __0x8(255, 255, 255)
__toggle_btn.TextSize = 28
__toggle_btn.Font = __0x9
__toggle_btn.Parent = __gui

__0x6(decrypt("XLFruqhu"), __toggle_btn).CornerRadius = UDim.new(1, 0)

__toggle_btn.MouseButton1Click:Connect(function()
    __main.Visible = not __main.Visible
end)

print("✅ " .. decrypt("EUDLQURWV#KXE#fduuhjdgr$"))
print("👤 " .. decrypt("Vfulvw#ihlwr#sru#Fduorv"))
