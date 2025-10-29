# NANANA-HUB01
-- IMBOT UNIVERSAL MOBILE - SLIDER FOV CORRIGIDO
-- Por: Sua Assistente

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

-- Sistema de KEY
local CORRECT_KEY = "NANANABETA1.0"
local KEY_VERIFIED = false

-- Configurações do IMBOT
local IMBOT_ENABLED = false
local FOV = 80
local TEAM_CHECK = false
local WALL_CHECK = false
local KILL_CHECK = false
local SMOOTHNESS = 0.5
local AIM_PART = "Head"

-- Criar a GUI PRINCIPAL
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ImbotMobile"
ScreenGui.Parent = CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- Tela de KEY
local KeyFrame = Instance.new("Frame")
KeyFrame.Name = "KeyFrame"
KeyFrame.Size = UDim2.new(0, 350, 0, 200)
KeyFrame.Position = UDim2.new(0.5, -175, 0.5, -100)
KeyFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
KeyFrame.BorderSizePixel = 0
KeyFrame.Parent = ScreenGui

local KeyTitle = Instance.new("TextLabel")
KeyTitle.Size = UDim2.new(1, 0, 0, 40)
KeyTitle.Position = UDim2.new(0, 0, 0, 30)
KeyTitle.BackgroundTransparency = 1
KeyTitle.Text = "🎯 AIMBOT MOBILE"
KeyTitle.TextColor3 = Color3.fromRGB(255, 200, 0)
KeyTitle.TextSize = 20
KeyTitle.Font = Enum.Font.GothamBold
KeyTitle.Parent = KeyFrame

local KeyInput = Instance.new("TextBox")
KeyInput.Size = UDim2.new(0, 250, 0, 35)
KeyInput.Position = UDim2.new(0.5, -125, 0, 80)
KeyInput.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
KeyInput.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyInput.PlaceholderText = "Digite a KEY..."
KeyInput.Text = ""
KeyInput.TextSize = 14
KeyInput.Font = Enum.Font.Gotham
KeyInput.Parent = KeyFrame

local InputCorner = Instance.new("UICorner")
InputCorner.CornerRadius = UDim.new(0, 8)
InputCorner.Parent = KeyInput

local VerifyButton = Instance.new("TextButton")
VerifyButton.Size = UDim2.new(0, 120, 0, 35)
VerifyButton.Position = UDim2.new(0.5, -60, 0, 125)
VerifyButton.BackgroundColor3 = Color3.fromRGB(255, 180, 0)
VerifyButton.Text = "VERIFICAR"
VerifyButton.TextColor3 = Color3.fromRGB(0, 0, 0)
VerifyButton.TextSize = 14
VerifyButton.Font = Enum.Font.GothamBold
VerifyButton.Parent = KeyFrame

local VerifyCorner = Instance.new("UICorner")
VerifyCorner.CornerRadius = UDim.new(0, 8)
VerifyCorner.Parent = VerifyButton

local KeyError = Instance.new("TextLabel")
KeyError.Size = UDim2.new(1, 0, 0, 20)
KeyError.Position = UDim2.new(0, 0, 0, 165)
KeyError.BackgroundTransparency = 1
KeyError.Text = ""
KeyError.TextColor3 = Color3.fromRGB(255, 50, 50)
KeyError.TextSize = 12
KeyError.Font = Enum.Font.Gotham
KeyError.Visible = false
KeyError.Parent = KeyFrame

-- BOTÃO REDONDO DA BANANA
local BananaButton = Instance.new("TextButton")
BananaButton.Name = "BananaButton"
BananaButton.Size = UDim2.new(0, 60, 0, 60)
BananaButton.Position = UDim2.new(0, 20, 0.5, -30)
BananaButton.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
BananaButton.Text = "🍌"
BananaButton.TextColor3 = Color3.fromRGB(0, 0, 0)
BananaButton.TextSize = 24
BananaButton.Font = Enum.Font.GothamBold
BananaButton.Visible = false
BananaButton.Active = true
BananaButton.Draggable = true
BananaButton.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(1, 0)
UICorner.Parent = BananaButton

local UIStroke = Instance.new("UIStroke")
UIStroke.Color = Color3.fromRGB(200, 150, 0)
UIStroke.Thickness = 3
UIStroke.Parent = BananaButton

-- HUB Principal
local MainHub = Instance.new("Frame")
MainHub.Name = "MainHub"
MainHub.Size = UDim2.new(0, 300, 0, 350)
MainHub.Position = UDim2.new(0.5, -150, 0.5, -175)
MainHub.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainHub.BorderSizePixel = 0
MainHub.Visible = false
MainHub.Active = true
MainHub.Draggable = true
MainHub.Parent = ScreenGui

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 40)
Header.BackgroundColor3 = Color3.fromRGB(255, 180, 0)
Header.BorderSizePixel = 0
Header.Parent = MainHub

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 1, 0)
Title.BackgroundTransparency = 1
Title.Text = "🎯 AIMBOT MOBILE"
Title.TextColor3 = Color3.fromRGB(0, 0, 0)
Title.TextSize = 16
Title.Font = Enum.Font.GothamBold
Title.Parent = Header

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -20, 1, -60)
Content.Position = UDim2.new(0, 10, 0, 50)
Content.BackgroundTransparency = 1
Content.Parent = MainHub

-- Botão Ativar/Desativar Aimbot
local ToggleAimbot = Instance.new("TextButton")
ToggleAimbot.Size = UDim2.new(1, 0, 0, 50)
ToggleAimbot.Position = UDim2.new(0, 0, 0, 10)
ToggleAimbot.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
ToggleAimbot.Text = "Ativar Aimbot OFF"
ToggleAimbot.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleAimbot.TextSize = 16
ToggleAimbot.Font = Enum.Font.GothamBold
ToggleAimbot.Parent = Content

-- FOV - SLIDER TOTALMENTE CORRIGIDO
local FovFrame = Instance.new("Frame")
FovFrame.Size = UDim2.new(1, 0, 0, 80)
FovFrame.Position = UDim2.new(0, 0, 0, 70)
FovFrame.BackgroundTransparency = 1
FovFrame.Parent = Content

local FovLabel = Instance.new("TextLabel")
FovLabel.Size = UDim2.new(1, 0, 0, 25)
FovLabel.BackgroundTransparency = 1
FovLabel.Text = "FOV: 80"
FovLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
FovLabel.TextSize = 16
FovLabel.Font = Enum.Font.GothamBold
FovLabel.TextXAlignment = Enum.TextXAlignment.Center
FovLabel.Parent = FovFrame

-- SLIDER DO FOV - AGORA FUNCIONA PERFEITAMENTE
local FovSliderBackground = Instance.new("TextButton") -- Mudei para TextButton
FovSliderBackground.Size = UDim2.new(1, 0, 0, 30)
FovSliderBackground.Position = UDim2.new(0, 0, 0, 30)
FovSliderBackground.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
FovSliderBackground.BorderSizePixel = 0
FovSliderBackground.Text = ""
FovSliderBackground.AutoButtonColor = false
FovSliderBackground.Parent = FovFrame

local SliderCorner = Instance.new("UICorner")
SliderCorner.CornerRadius = UDim.new(0, 15)
SliderCorner.Parent = FovSliderBackground

-- Barra de progresso do FOV
local FovFill = Instance.new("Frame")
FovFill.Size = UDim2.new(0.4, 0, 1, 0)
FovFill.BackgroundColor3 = Color3.fromRGB(255, 180, 0)
FovFill.BorderSizePixel = 0
FovFill.Parent = FovSliderBackground

local FillCorner = Instance.new("UICorner")
FillCorner.CornerRadius = UDim.new(0, 15)
FillCorner.Parent = FovFill

-- Botão de arraste do slider - MAIOR E MAIS FÁCIL DE CLICAR
local SliderButton = Instance.new("TextButton")
SliderButton.Size = UDim2.new(0, 50, 0, 50) -- Aumentei para 50x50
SliderButton.Position = UDim2.new(0.4, -25, 0.5, -25) -- Ajuste da posição
SliderButton.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
SliderButton.Text = "●" -- Bolinha para indicar arraste
SliderButton.TextColor3 = Color3.fromRGB(0, 0, 0)
SliderButton.TextSize = 20
SliderButton.AutoButtonColor = false
SliderButton.ZIndex = 3
SliderButton.Parent = FovSliderBackground

local ButtonCorner = Instance.new("UICorner")
ButtonCorner.CornerRadius = UDim.new(1, 0)
ButtonCorner.Parent = SliderButton

local ButtonStroke = Instance.new("UIStroke")
ButtonStroke.Color = Color3.fromRGB(200, 150, 0)
ButtonStroke.Thickness = 3
ButtonStroke.Parent = SliderButton

-- Linha divisória
local Divider = Instance.new("Frame")
Divider.Size = UDim2.new(1, 0, 0, 2)
Divider.Position = UDim2.new(0, 0, 0, 160)
Divider.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
Divider.BorderSizePixel = 0
Divider.Parent = Content

-- Toggles (mantidos iguais)
local TeamToggleFrame = Instance.new("Frame")
TeamToggleFrame.Size = UDim2.new(1, 0, 0, 30)
TeamToggleFrame.Position = UDim2.new(0, 0, 0, 170)
TeamToggleFrame.BackgroundTransparency = 1
TeamToggleFrame.Parent = Content

local TeamLabel = Instance.new("TextLabel")
TeamLabel.Size = UDim2.new(0.7, 0, 1, 0)
TeamLabel.BackgroundTransparency = 1
TeamLabel.Text = "Team Check: OFF"
TeamLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TeamLabel.TextSize = 14
TeamLabel.Font = Enum.Font.Gotham
TeamLabel.TextXAlignment = Enum.TextXAlignment.Left
TeamLabel.Parent = TeamToggleFrame

local TeamButton = Instance.new("TextButton")
TeamButton.Size = UDim2.new(0, 50, 0, 25)
TeamButton.Position = UDim2.new(0.8, 0, 0.08, 0)
TeamButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
TeamButton.Text = "OFF"
TeamButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TeamButton.TextSize = 12
TeamButton.Font = Enum.Font.GothamBold
TeamButton.Parent = TeamToggleFrame

local KillToggleFrame = Instance.new("Frame")
KillToggleFrame.Size = UDim2.new(1, 0, 0, 30)
KillToggleFrame.Position = UDim2.new(0, 0, 0, 210)
KillToggleFrame.BackgroundTransparency = 1
KillToggleFrame.Parent = Content

local KillLabel = Instance.new("TextLabel")
KillLabel.Size = UDim2.new(0.7, 0, 1, 0)
KillLabel.BackgroundTransparency = 1
KillLabel.Text = "Kill Check: OFF"
KillLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
KillLabel.TextSize = 14
KillLabel.Font = Enum.Font.Gotham
KillLabel.TextXAlignment = Enum.TextXAlignment.Left
KillLabel.Parent = KillToggleFrame

local KillButton = Instance.new("TextButton")
KillButton.Size = UDim2.new(0, 50, 0, 25)
KillButton.Position = UDim2.new(0.8, 0, 0.08, 0)
KillButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
KillButton.Text = "OFF"
KillButton.TextColor3 = Color3.fromRGB(255, 255, 255)
KillButton.TextSize = 12
KillButton.Font = Enum.Font.GothamBold
KillButton.Parent = KillToggleFrame

local WallToggleFrame = Instance.new("Frame")
WallToggleFrame.Size = UDim2.new(1, 0, 0, 30)
WallToggleFrame.Position = UDim2.new(0, 0, 0, 250)
WallToggleFrame.BackgroundTransparency = 1
WallToggleFrame.Parent = Content

local WallLabel = Instance.new("TextLabel")
WallLabel.Size = UDim2.new(0.7, 0, 1, 0)
WallLabel.BackgroundTransparency = 1
WallLabel.Text = "Wall Check: OFF"
WallLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
WallLabel.TextSize = 14
WallLabel.Font = Enum.Font.Gotham
WallLabel.TextXAlignment = Enum.TextXAlignment.Left
WallLabel.Parent = WallToggleFrame

local WallButton = Instance.new("TextButton")
WallButton.Size = UDim2.new(0, 50, 0, 25)
WallButton.Position = UDim2.new(0.8, 0, 0.08, 0)
WallButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
WallButton.Text = "OFF"
WallButton.TextColor3 = Color3.fromRGB(255, 255, 255)
WallButton.TextSize = 12
WallButton.Font = Enum.Font.GothamBold
WallButton.Parent = WallToggleFrame

-- Status
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(1, 0, 0, 40)
StatusLabel.Position = UDim2.new(0, 0, 0, 290)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = "Status: Aguardando KEY..."
StatusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
StatusLabel.TextSize = 12
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.TextWrapped = true
StatusLabel.Parent = Content

-- FOV Circle visual
local FovCircle = Instance.new("Frame")
FovCircle.Size = UDim2.new(0, FOV * 2, 0, FOV * 2)
FovCircle.Position = UDim2.new(0.5, -FOV, 0.5, -FOV)
FovCircle.BackgroundColor3 = Color3.fromRGB(255, 180, 0)
FovCircle.BackgroundTransparency = 0.9
FovCircle.BorderSizePixel = 0
FovCircle.Visible = false
FovCircle.Parent = ScreenGui

local CircleCorner = Instance.new("UICorner")
CircleCorner.CornerRadius = UDim.new(1, 0)
CircleCorner.Parent = FovCircle

local CircleStroke = Instance.new("UIStroke")
CircleStroke.Color = Color3.fromRGB(255, 200, 0)
CircleStroke.Thickness = 2
CircleStroke.Parent = FovCircle

-- FUNÇÃO VERIFICAR KEY
local function VerifyKey()
    local inputKey = KeyInput.Text
    
    if inputKey == CORRECT_KEY then
        KEY_VERIFIED = true
        KeyFrame.Visible = false
        BananaButton.Visible = true
        KeyError.Visible = false
        StatusLabel.Text = "Obrigado pela preferência 🍌🍌"
        
        local ThanksLabel = Instance.new("TextLabel")
        ThanksLabel.Size = UDim2.new(0, 300, 0, 60)
        ThanksLabel.Position = UDim2.new(0.5, -150, 0.3, -30)
        ThanksLabel.BackgroundColor3 = Color3.fromRGB(255, 200, 0)
        ThanksLabel.BackgroundTransparency = 0.1
        ThanksLabel.Text = "Obrigado pela preferência 🍌🍌"
        ThanksLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        ThanksLabel.TextSize = 18
        ThanksLabel.Font = Enum.Font.GothamBold
        ThanksLabel.TextWrapped = true
        ThanksLabel.Parent = ScreenGui
        
        local ThanksCorner = Instance.new("UICorner")
        ThanksCorner.CornerRadius = UDim.new(0, 15)
        ThanksCorner.Parent = ThanksLabel
        
        wait(3)
        ThanksLabel:Destroy()
        
    else
        KeyError.Text = "KEY incorreta! Use: NANANABETA1.0"
        KeyError.Visible = true
        KeyInput.Text = ""
    end
end

-- CONEXÕES DA KEY
VerifyButton.MouseButton1Click:Connect(VerifyKey)
KeyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then VerifyKey() end
end)

-- TOGGLE DO HUB
local hubVisible = false
BananaButton.MouseButton1Click:Connect(function()
    if not KEY_VERIFIED then return end
    hubVisible = not hubVisible
    MainHub.Visible = hubVisible
    if hubVisible then
        StatusLabel.Text = "Obrigado pela preferência 🍌🍌"
    end
end)

-- TOGGLE DO AIMBOT
ToggleAimbot.MouseButton1Click:Connect(function()
    if not KEY_VERIFIED then return end
    IMBOT_ENABLED = not IMBOT_ENABLED
    FovCircle.Visible = IMBOT_ENABLED
    if IMBOT_ENABLED then
        ToggleAimbot.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
        ToggleAimbot.Text = "Ativar Aimbot ON"
        StatusLabel.Text = "🎯 AIMBOT ATIVADO - FOV: " .. FOV
    else
        ToggleAimbot.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        ToggleAimbot.Text = "Ativar Aimbot OFF"
        StatusLabel.Text = "Obrigado pela preferência 🍌🍌"
    end
end)

-- TOGGLE DOS CHECKS
TeamButton.MouseButton1Click:Connect(function()
    if not KEY_VERIFIED then return end
    TEAM_CHECK = not TEAM_CHECK
    TeamButton.BackgroundColor3 = TEAM_CHECK and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
    TeamButton.Text = TEAM_CHECK and "ON" or "OFF"
    TeamLabel.Text = "Team Check: " .. (TEAM_CHECK and "ON" or "OFF")
end)

KillButton.MouseButton1Click:Connect(function()
    if not KEY_VERIFIED then return end
    KILL_CHECK = not KILL_CHECK
    KillButton.BackgroundColor3 = KILL_CHECK and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
    KillButton.Text = KILL_CHECK and "ON" or "OFF"
    KillLabel.Text = "Kill Check: " .. (KILL_CHECK and "ON" or "OFF")
end)

WallButton.MouseButton1Click:Connect(function()
    if not KEY_VERIFIED then return end
    WALL_CHECK = not WALL_CHECK
    WallButton.BackgroundColor3 = WALL_CHECK and Color3.fromRGB(0, 255, 0) or Color3.fromRGB(255, 50, 50)
    WallButton.Text = WALL_CHECK and "ON" or "OFF"
    WallLabel.Text = "Wall Check: " .. (WALL_CHECK and "ON" or "OFF")
end)

-- SLIDER DO FOV - TOTALMENTE CORRIGIDO E FUNCIONAL
local draggingFov = false

local function UpdateFov(value)
    FOV = math.clamp(value, 10, 200)
    FovLabel.Text = "FOV: " .. FOV
    local ratio = (FOV - 10) / 190
    
    -- Atualizar barra de progresso
    FovFill.Size = UDim2.new(ratio, 0, 1, 0)
    
    -- Atualizar posição do botão do slider
    SliderButton.Position = UDim2.new(ratio, -25, 0.5, -25)
    
    -- Atualizar círculo FOV
    FovCircle.Size = UDim2.new(0, FOV * 2, 0, FOV * 2)
    FovCircle.Position = UDim2.new(0.5, -FOV, 0.5, -FOV)
    
    if IMBOT_ENABLED then
        StatusLabel.Text = "🎯 AIMBOT ATIVADO - FOV: " .. FOV
    end
end

-- SISTEMA DE ARRASTE DO SLIDER CORRIGIDO
local function onSliderInputBegan(input)
    if not KEY_VERIFIED then return end
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        draggingFov = true
        -- Atualizar imediatamente na posição do clique
        local mouse = UserInputService:GetMouseLocation()
        local sliderAbsPos = FovSliderBackground.AbsolutePosition
        local sliderAbsSize = FovSliderBackground.AbsoluteSize.X
        
        local relativeX = math.clamp(mouse.X - sliderAbsPos.X, 0, sliderAbsSize)
        local ratio = relativeX / sliderAbsSize
        local newFov = math.floor(10 + (190 * ratio))
        
        UpdateFov(newFov)
    end
end

local function onSliderInputChanged(input)
    if draggingFov and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local mouse = input.Position
        local sliderAbsPos = FovSliderBackground.AbsolutePosition
        local sliderAbsSize = FovSliderBackground.AbsoluteSize.X
        
        local relativeX = math.clamp(mouse.X - sliderAbsPos.X, 0, sliderAbsSize)
        local ratio = relativeX / sliderAbsSize
        local newFov = math.floor(10 + (190 * ratio))
        
        UpdateFov(newFov)
    end
end

local function onSliderInputEnded(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        draggingFov = false
    end
end

-- Conectar eventos ao slider background (área inteira)
FovSliderBackground.InputBegan:Connect(onSliderInputBegan)
FovSliderBackground.InputChanged:Connect(onSliderInputChanged)
FovSliderBackground.InputEnded:Connect(onSliderInputEnded)

-- Conectar eventos ao botão do slider também
SliderButton.InputBegan:Connect(onSliderInputBegan)
SliderButton.InputChanged:Connect(onSliderInputChanged)
SliderButton.InputEnded:Connect(onSliderInputEnded)

-- FUNÇÃO WALL CHECK
local function IsVisible(targetPart)
    if not targetPart then return false end
    local character = LocalPlayer.Character
    if not character then return false end
    local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
    if not humanoidRootPart then return false end
    
    local origin = humanoidRootPart.Position
    local target = targetPart.Position
    local direction = (target - origin).Unit
    local distance = (target - origin).Magnitude
    
    local ignoreList = {character, targetPart.Parent}
    local raycastParams = RaycastParams.new()
    raycastParams.FilterDescendantsInstances = ignoreList
    raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
    
    local raycastResult = workspace:Raycast(origin, direction * distance, raycastParams)
    
    if not raycastResult then return true end
    if raycastResult.Instance:IsDescendantOf(targetPart.Parent) then return true end
    return false
end

-- FUNÇÃO DO AIMBOT
local function GetClosestPlayer()
    if not KEY_VERIFIED then return nil end
    local closestPlayer = nil
    local closestDistance = FOV
    
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local character = player.Character
            local humanoid = character:FindFirstChild("Humanoid")
            local rootPart = character:FindFirstChild("HumanoidRootPart")
            
            if humanoid and humanoid.Health > 0 and rootPart then
                if TEAM_CHECK and player.Team and LocalPlayer.Team and player.Team == LocalPlayer.Team then
                    continue
                end
                if KILL_CHECK and humanoid.Health <= 0 then
                    continue
                end
                if WALL_CHECK then
                    local targetPart = character:FindFirstChild(AIM_PART) or rootPart
                    if not IsVisible(targetPart) then
                        continue
                    end
                end
                
                local screenPoint, onScreen = Camera:WorldToViewportPoint(rootPart.Position)
                local distance = (Vector2.new(screenPoint.X, screenPoint.Y) - Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)).Magnitude
                
                if onScreen and distance < closestDistance then
                    closestDistance = distance
                    closestPlayer = player
                end
            end
        end
    end
    return closestPlayer
end

-- LOOP DO AIMBOT
RunService.RenderStepped:Connect(function()
    if IMBOT_ENABLED and KEY_VERIFIED then
        local closestPlayer = GetClosestPlayer()
        if closestPlayer and closestPlayer.Character then
            local targetPart = closestPlayer.Character:FindFirstChild(AIM_PART) or closestPlayer.Character:FindFirstChild("HumanoidRootPart")
            if targetPart then
                local currentCamera = workspace.CurrentCamera
                local currentLook = currentCamera.CFrame.LookVector
                local direction = (targetPart.Position - currentCamera.CFrame.Position).Unit
                local smoothDirection = currentLook:Lerp(direction, 1 - SMOOTHNESS)
                currentCamera.CFrame = CFrame.new(currentCamera.CFrame.Position, currentCamera.CFrame.Position + smoothDirection)
            end
        end
    end
end)

-- HOTKEY ALT
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed or not KEY_VERIFIED then return end
    if input.KeyCode == Enum.KeyCode.LeftAlt or input.KeyCode == Enum.KeyCode.RightAlt then
        IMBOT_ENABLED = not IMBOT_ENABLED
        FovCircle.Visible = IMBOT_ENABLED
        if IMBOT_ENABLED then
            ToggleAimbot.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
            ToggleAimbot.Text = "Ativar Aimbot ON"
            StatusLabel.Text = "🎯 AIMBOT ATIVADO - FOV: " .. FOV
        else
            ToggleAimbot.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
            ToggleAimbot.Text = "Ativar Aimbot OFF"
            StatusLabel.Text = "Obrigado pela preferência 🍌🍌"
        end
    end
end)

-- INICIALIZAR
KeyFrame.Visible = true
BananaButton.Visible = false
MainHub.Visible = false
FovCircle.Visible = false

print("🎯 AIMBOT MOBILE INICIADO!")
print("🔑 KEY: NANANABETA1.0")
print("📱 Slider do FOV agora funciona perfeitamente!")
