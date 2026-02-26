-- MENU COMPACTO + RÁPIDO - Mage Cattie Claim

local RS = game:GetService("ReplicatedStorage")
local MS = game:GetService("MarketplaceService")
local SG = game:GetService("StarterGui")
local UIS = game:GetService("UserInputService")
local player = game.Players.LocalPlayer
local item = 118301816068198

local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.IgnoreGuiInset = true
gui.ResetOnSpawn = false

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,220,0,180)
frame.Position = UDim2.new(0.5,-110,0.5,-90)
frame.BackgroundColor3 = Color3.fromRGB(30,30,35)
frame.BorderSizePixel = 0
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,0,0,30)
title.BackgroundColor3 = Color3.fromRGB(45,45,55)
title.Text = "Mage Cattie"
title.TextColor3 = Color3.fromRGB(200,200,255)
title.Font = Enum.Font.GothamBold
title.TextSize = 16

local close = Instance.new("TextButton", frame)
close.Size = UDim2.new(0,26,0,26)
close.Position = UDim2.new(1,-30,0,2)
close.BackgroundColor3 = Color3.fromRGB(180,50,50)
close.Text = "X"
close.TextColor3 = Color3.new(1,1,1)
close.Font = Enum.Font.Gotham
close.TextSize = 14

close.MouseButton1Click:Connect(function() gui:Destroy() end)

local function fire(r, a)
    pcall(function()
        if r:IsA("RemoteEvent") then r:FireServer(a or nil)
        elseif r:IsA("RemoteFunction") then r:InvokeServer(a or nil) end
    end)
end

local function claimAll(code)
    MS:PromptProductPurchase(player, item)
    
    local args = code and {item, code} or {item, nil}
    
    for _,v in ipairs(RS:GetDescendants()) do
        if v:IsA("RemoteEvent") or v:IsA("RemoteFunction") then
            local n = v.Name:lower()
            if n:find("code") or n:find("claim") or n:find("redeem") or n:find("ugc") then
                for _,a in ipairs(args) do fire(v, a) end
            end
        end
    end
    
    -- Knit rápidos
    local paths = {
        "Packages._Index.sleitnick_knit@1.7.0.knit.Services.UGCService.RE.UGCClaimed",
        "Packages._Index.sleitnick_knit@1.7.0.knit.Services.DataService.RP.ClaimedUGC"
    }
    for _,p in ipairs(paths) do
        local cur = game
        for part in p:gmatch("[^.]+") do cur = cur:FindFirstChild(part) or break end
        if cur then for _,a in ipairs(args) do fire(cur, a) end end
    end
    
    SG:SetCore("SendNotification",{Title="Enviado",Text="Tentando claim...",Duration=2.5})
end

local function debugFTUE()
    local rf = RS:FindFirstChild("DebugCompleteOriginalFTUE", true)
    if rf and rf:IsA("RemoteFunction") then pcall(rf.InvokeServer, rf) end
    SG:SetCore("SendNotification",{Title="Debug",Text="Tentado (1x)",Duration=3})
end

-- Botões compactos
local y = 35
local function btn(txt, callback)
    local b = Instance.new("TextButton", frame)
    b.Size = UDim2.new(0.92,0,0,34)
    b.Position = UDim2.new(0.04,0,0,y)
    b.BackgroundColor3 = Color3.fromRGB(55,55,75)
    b.TextColor3 = Color3.fromRGB(220,220,255)
    b.Font = Enum.Font.GothamSemibold
    b.TextSize = 14
    b.Text = txt
    b.MouseButton1Click:Connect(callback)
    y = y + 38
end

btn("Claim (com código)", function()
    claimAll(input.Text ~= "" and input.Text or nil)
end)

btn("Claim básico", function() claimAll() end)

btn("Debug FTUE (risco)", debugFTUE)

-- Campo código
local input = Instance.new("TextBox", frame)
input.Size = UDim2.new(0.92,0,0,28)
input.Position = UDim2.new(0.04,0,0,38)
input.BackgroundColor3 = Color3.fromRGB(40,40,50)
input.TextColor3 = Color3.new(1,1,1)
input.PlaceholderText = "Código (opcional)"
input.TextSize = 14
input.Font = Enum.Font.Gotham

-- Toggle F6
local visible = true
UIS.InputBegan:Connect(function(i)
    if i.KeyCode == Enum.KeyCode.F6 then
        visible = not visible
        frame.Visible = visible
    end
end)

print("Menu compacto carregado | F6 toggle")# Script-
Jdjd
