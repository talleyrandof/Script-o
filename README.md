-- Trash Brainrot UGC Auto Lite (Grok xAI) - Bypass Tempo + Anti-Kick
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootpart = character:WaitForChild("HumanLite")

-- Anti-Kick
hookmetamethod(game, "__namecall", function(self, ...)
    if getnamecallmethod() == "Kick" then return end
    return hookmetamethod(game, "__namecall", self, ...)
end)

-- Cheats Básicos
humanoid.WalkSpeed = 100
humanoid.JumpPower = 100

-- Noclip
RunService.Stepped:Connect(function()
    for _, part in pairs(character:GetDescendants()) do
        if part:IsA("BasePart") then part.CanCollide = false end
    end
end)

-- Fly Simples
local bv = Instance.new("BodyVelocity", rootpart)
bv.MaxForce = Vector3.new(4000,4000,4000)
RunService.Heartbeat:Connect(function()
    local cam = workspace.CurrentCamera
    bv.Velocity = cam.CFrame:VectorToWorldSpace(humanoid.MoveDirection) * 50
end)

-- TP Inicial
rootpart.CFrame = CFrame.new(0, 50, 0)

-- Zero Cooldowns (leve)
spawn(function()
    while wait(0.5) do
        for _, v in pairs(game:GetDescendants()) do
            if (v:IsA("NumberValue") or v:IsA("IntValue")) and (v.Name:lower():find("cooldown") or v.Name:lower():find("debounce") or v.Name:lower():find("hold")) then
                v.Value = 0
            end
        end
    end
end)

-- Auto-Fire Prompts/Clicks
RunService.Heartbeat:Connect(function()
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("ProximityPrompt") then
            obj.HoldDuration = 0
            obj.MaxActivationDistance = math.huge
            local txt = (obj.ActionText .. obj.ObjectText):lower()
            if txt:find("buy") or txt:find("claim") or txt:find("get") or txt:find("hair") or txt:find("green") then
                fireproximityprompt(obj)
            end
        elseif obj:IsA("ClickDetector") then
            fireclickdetector(obj)
        end
    end
end)

-- Remotes Spam Leve
spawn(function()
    while wait(0.5) do
        for _, rem in pairs(game:GetDescendants()) do
            if rem:IsA("RemoteEvent") and (rem.Name:lower():find("claim") or rem.Name:lower():find("buy") or rem.Name:lower():find("get")) then
                pcall(rem.FireServer, rem)
            end
        end
    end
end)

print("🟢 Lite ATIVO! 6/10 stock - Fly/Noclip ON")
