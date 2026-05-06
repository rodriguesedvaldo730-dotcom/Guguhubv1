--// SERVICES
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")

--// VARIABLES
local Player = Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local Humanoid = Character:WaitForChild("Humanoid")
local RootPart = Character:WaitForChild("HumanoidRootPart")

--// SETTINGS
local MenuKey = Enum.KeyCode.RightControl

--// GUI CREATION
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MM2_HUB_ULTRA"
ScreenGui.Parent = Player.PlayerGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.ResetOnSpawn = false

-- ==============================================
-- 🖼️ IMAGEM FLUTUANTE
-- ==============================================
local FloatImage = Instance.new("ImageLabel")
FloatImage.Name = "ImagemFlutuante"
FloatImage.Size = UDim2.new(0, 140, 0, 190)
FloatImage.Position = UDim2.new(0.01, 0, 0.01, 0)
FloatImage.BackgroundTransparency = 1
FloatImage.Image = "https://i.imgur.com/EXEMPLO.png" -- COLOQUE O LINK DA SUA IMAGEM AQUI
FloatImage.Parent = ScreenGui

-- ANIMAÇÃO DE FLUTUAR
coroutine.wrap(function()
    while task.wait(0.05) do
        for i = 0, 6, 1 do FloatImage.Position = UDim2.new(0.01,0,0.01,i) task.wait(0.05) end
        for i = 6, 0, -1 do FloatImage.Position = UDim2.new(0.01,0,0.01,i) task.wait(0.05) end
    end
end)()

-- ==============================================
-- 🪟 JANELA PRINCIPAL
-- ==============================================
local Main = Instance.new("Frame")
Main.Size = UDim2.new(0, 650, 0, 500)
Main.Position = UDim2.new(0.5, -325, 0.5, -250)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
Main.BorderSizePixel = 0
Main.Visible = false
Main.Parent = ScreenGui

-- TOPO
local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 50)
TopBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
TopBar.BorderSizePixel = 0
TopBar.Parent = Main

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -10, 1, 0)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "💀 MM2 HUB MESTRE - BY DOLA 💀"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 22
Title.Parent = TopBar

-- AREA DE CONTEUDO
local Container = Instance.new("Frame")
Container.Size = UDim2.new(1, -20, 1, -60)
Container.Position = UDim2.new(0, 10, 0, 55)
Container.BackgroundTransparency = 1
Container.Parent = Main

-- ==============================================
-- ⚙️ VARIAVEIS DE FUNÇÕES
-- ==============================================
local Enabled = {
    ESP = false, Fly = false, Noclip = false,
    SpeedBoost = false, InfiniteJump = false,
    HitboxExpansive = false, FullBright = false,
    GodMode = false, NoClip = false, AntiKnife = false,
    WalkOnWater = false, Invisible = false
}

-- ==============================================
-- 🛠️ FUNÇÕES PRINCIPAIS
-- ==============================================

-- 🔍 ESP COMPLETO
local function ESPLoop()
    while Enabled.ESP do
        for _, v in pairs(Players:GetPlayers()) do
            if v ~= Player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
                local hrp = v.Character.HumanoidRootPart
                local role = "Innocent"
                local color = Color3.new(0,1,0)
                
                pcall(function()
                    role = Workspace.Game.Players[v.Name].Role.Value
                    if role == "Murderer" then color = Color3.new(1,0,0)
                    elseif role == "Sheriff" then color = Color3.new(0,0,1) end
                end)

                local box = Drawing.new("Square")
                box.Thickness = 2
                box.Filled = false
                box.Color = color
                local vec, onScreen = Workspace.CurrentCamera:WorldToViewportPoint(hrp.Position)
                if onScreen then
                    box.Size = Vector2.new(2000 / vec.Z, 2000 / vec.Z)
                    box.Position = Vector2.new(vec.X - box.Size.X/2, vec.Y - box.Size.Y/2)
                    box.Visible = true
                end
                game.Debris:AddItem(box, 0.1)

                local name = Drawing.new("Text")
                name.Color = color
                name.Size = 18
                name.Center = true
                name.Text = v.Name.." | "..role.." | "..math.floor((RootPart.Position-hrp.Position).Magnitude).."m"
                if onScreen then
                    name.Position = Vector2.new(vec.X, vec.Y - box.Size.Y/2 - 10)
                    name.Visible = true
                end
                game.Debris:AddItem(name, 0.1)
            end
        end
        RunService.Heartbeat:Wait()
    end
end

-- 🚀 VOAR
local function FlyLoop()
    local Speed = 80
    while Enabled.Fly do
        RootPart.Velocity = Vector3.new()
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then RootPart.Velocity += Workspace.CurrentCamera.CFrame.LookVector * Speed end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then RootPart.Velocity -= Workspace.CurrentCamera.CFrame.LookVector * Speed end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then RootPart.Velocity -= Workspace.CurrentCamera.CFrame.RightVector * Speed end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then RootPart.Velocity += Workspace.CurrentCamera.CFrame.RightVector * Speed end
        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then RootPart.Velocity += Vector3.new(0,Speed,0) end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then RootPart.Velocity -= Vector3.new(0,Speed,0) end
        RunService.Heartbeat:Wait()
    end
end

-- 🌫️ NOCLIP
RunService.Stepped:Connect(function()
    if Enabled.Noclip then
        for _, part in pairs(Character:GetChildren()) do
            if part:IsA("BasePart") then part.CanCollide = false end
        end
    end
end)

-- ⚡ VELOCIDADE
RunService.Heartbeat:Connect(function()
    if Enabled.SpeedBoost then Humanoid.WalkSpeed = 150 else Humanoid.WalkSpeed = 16 end
end)

-- 🦘 PULO INFINITO
UserInputService.JumpRequest:Connect(function()
    if Enabled.InfiniteJump then Humanoid.Jump = true end
end)

-- 🎯 HITBOX
RunService.Heartbeat:Connect(function()
    if Enabled.HitboxExpansive then
        pcall(function()
            for _, part in pairs(Character:GetChildren()) do
                if part:IsA("BasePart") then part.Size = Vector3.new(10,10,10) end
            end
        end)
    end
end)

-- 💡 LUZ TOTAL
RunService.Heartbeat:Connect(function()
    if Enabled.FullBright then
        game:GetService("Lighting").Brightness = 10
        game:GetService("Lighting").FogEnd = 100000
    else
        game:GetService("Lighting").Brightness = 1
        game:GetService("Lighting").FogEnd = 100
    end
end)

-- 🛡️ VIDA INFINITA
RunService.Heartbeat:Connect(function()
    if Enabled.GodMode then
        Humanoid.MaxHealth = math.huge
        Humanoid.Health = math.huge
    end
end)

-- 🥷 FICAR INVISIVEL
RunService.Heartbeat:Connect(function()
    if Enabled.Invisible then
        for _, part in pairs(Character:GetChildren()) do
            if part:IsA("BasePart") then part.Transparency = 1 end
        end
        Humanoid.DisplayDistanceType = "None"
    else
        for _, part in pairs(Character:GetChildren()) do
            if part:IsA("BasePart") then part.Transparency = 0 end
        end
        Humanoid.DisplayDistanceType = "Automatic"
    end
end)

-- ==============================================
-- 🎛️ CRIANDO BOTÕES
-- ==============================================

local yPos = 10
local xPos = 10

local function AddButton(text, func)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 180, 0, 45)
    btn.Position = UDim2.new(0, xPos, 0, yPos)
    btn.BackgroundColor3 = Color3.fromRGB(35,35,35)
    btn.Text = text
    btn.TextColor3 = Color3.new(1,1,1)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 13
    btn.Parent = Container
    
    btn.MouseButton1Click:Connect(func)
    
    xPos += 190
    if xPos > 600 then
        xPos = 10
        yPos += 55
    end
    
    return btn
end

-- ==============================================
-- 👁️ VISAO
-- ==============================================
local ESPBtn = AddButton("🔍 ATIVAR ESP", function()
    Enabled.ESP = not Enabled.ESP
    ESPBtn.BackgroundColor3 = Enabled.ESP and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
    if Enabled.ESP then coroutine.wrap(ESPLoop)() end
end)

local FullBrightBtn = AddButton("💡 LUZ TOTAL", function()
    Enabled.FullBright = not Enabled.FullBright
    FullBrightBtn.BackgroundColor3 = Enabled.FullBright and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

-- ==============================================
-- 🚀 MOVIMENTO
-- ==============================================
local FlyBtn = AddButton("🚀 VOAR (FLY)", function()
    Enabled.Fly = not Enabled.Fly
    FlyBtn.BackgroundColor3 = Enabled.Fly and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
    Humanoid.PlatformStand = Enabled.Fly
    if Enabled.Fly then coroutine.wrap(FlyLoop)() end
end)

local NoclipBtn = AddButton("🌫️ ATRAVESSAR", function()
    Enabled.Noclip = not Enabled.Noclip
    NoclipBtn.BackgroundColor3 = Enabled.Noclip and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

local SpeedBtn = AddButton("⚡ VELOCIDADE MAX", function()
    Enabled.SpeedBoost = not Enabled.SpeedBoost
    SpeedBtn.BackgroundColor3 = Enabled.SpeedBoost and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

local JumpBtn = AddButton("🦘 PULO INFINITO", function()
    Enabled.InfiniteJump = not Enabled.InfiniteJump
    JumpBtn.BackgroundColor3 = Enabled.InfiniteJump and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

-- ==============================================
-- 🛡️ SEGURANÇA
-- ==============================================
local GodBtn = AddButton("🛡️ VIDA INFINITA", function()
    Enabled.GodMode = not Enabled.GodMode
    GodBtn.BackgroundColor3 = Enabled.GodMode and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

local InvisBtn = AddButton("🥷 FICAR INVISIVEL", function()
    Enabled.Invisible = not Enabled.Invisible
    InvisBtn.BackgroundColor3 = Enabled.Invisible and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

-- ==============================================
-- ⚔️ COMBATE
-- ==============================================
local HitboxBtn = AddButton("🎯 HITBOX GIGANTE", function()
    Enabled.HitboxExpansive = not Enabled.HitboxExpansive
    HitboxBtn.BackgroundColor3 = Enabled.HitboxExpansive and Color3.fromRGB(0,150,0) or Color3.fromRGB(35,35,35)
end)

local KnifeBtn = AddButton("🔪 PEGAR TODAS FACAS", function()
    pcall(function()
        game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("Knife"):FireServer("Equip", "Chroma")
        game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("Knife"):FireServer("Equip", "Ghost")
        game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("Knife"):FireServer("Equip", "Pixel")
    end)
end)

local GunBtn = AddButton("🔫 PEGAR ARMAS", function()
    pcall(function()
        game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("Gun"):FireServer("Equip", "Chroma")
    end)
end)

-- ==============================================
-- 💀 DESTRUIÇÃO TOTAL
-- ==============================================
AddButton("💀 MATAR TODOS", function()
    for _,v in pairs(Players:GetPlayers()) do
        if v.Character and v.Character:FindFirstChild("Humanoid") then
            v.Character.Humanoid.Health = 0
        end
    end
end)

AddButton("🧨 EXPLODIR MAPA", function()
    for _, part in pairs(Workspace:GetDescendants()) do
        if part:IsA("BasePart") and part.Anchored == false then
            part:Destroy()
        end
    end
end)

AddButton("🚪 TELEPORTE INICIO", function()
    RootPart.CFrame = CFrame.new(0, 50, 0)
end)

AddButton("🎨 COR RAINBOW", function()
    while true do
        for _, part in pairs(Character:GetChildren()) do
            if part:IsA("BasePart") then
                part.Color = Color3.new(math.random(), math.random(), math.random())
            end
        end
        task.wait(0.1)
    end
end)

AddButton("👻 ANDAR NA AGUA", function()
    while true do
        RootPart.CFrame += Vector3.new(0,0.1,0)
        task.wait()
    end
end)

AddButton("💥 FORÇA GRAVIDADE", function()
    Workspace.Gravity = 0
end)

AddButton("🔊 SOM ALTO", function()
    local s = Instance.new("Sound")
    s.SoundId = "rbxassetid://122220768"
    s.Volume = 10
    s.Parent = RootPart
    s:Play()
end)

-- ==============================================
-- ABRIR / FECHAR MENU
-- ==============================================
UserInputService.InputBegan:Connect(function(input)
    if input.Key
    
