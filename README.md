# Scriptalex
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local ToggleESPButton = Instance.new("TextButton")
local ToggleHitboxButton = Instance.new("TextButton")
local ToggleDistanceESPButton = Instance.new("TextButton")
local ToggleNameESPButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 300, 0, 300)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -150)
MainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MainFrame.BackgroundTransparency = 0.5

-- Função para criar os botões
local function createButton(name, position, text, func)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Size = UDim2.new(0, 260, 0, 40)
    button.Position = position
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.Parent = MainFrame
    button.MouseButton1Click:Connect(func)
end

-- Variáveis para controle
local ESP_Ativado = false
local Hitbox_Ativado = false
local DistanceESP_Ativado = false
local NameESP_Ativado = false

-- Funções para ativar/desativar as funcionalidades

local function toggleESP()
    ESP_Ativado = not ESP_Ativado
    if ESP_Ativado then
        ToggleESPButton.Text = "Desativar ESP"
        -- Lógica para ativar o ESP
        print("ESP Ativado")
    else
        ToggleESPButton.Text = "Ativar ESP"
        -- Lógica para desativar o ESP
        print("ESP Desativado")
    end
end

local function toggleHitbox()
    Hitbox_Ativado = not Hitbox_Ativado
    if Hitbox_Ativado then
        ToggleHitboxButton.Text = "Desativar Hitbox"
        -- Lógica para ativar a Hitbox
        print("Hitbox Ativada")
    else
        ToggleHitboxButton.Text = "Ativar Hitbox"
        -- Lógica para desativar a Hitbox
        print("Hitbox Desativada")
    end
end

local function toggleDistanceESP()
    DistanceESP_Ativado = not DistanceESP_Ativado
    if DistanceESP_Ativado then
        ToggleDistanceESPButton.Text = "Desativar Distância ESP"
        -- Lógica para ativar a Distância ESP
        print("Distância ESP Ativada")
    else
        ToggleDistanceESPButton.Text = "Ativar Distância ESP"
        -- Lógica para desativar a Distância ESP
        print("Distância ESP Desativada")
    end
end

local function toggleNameESP()
    NameESP_Ativado = not NameESP_Ativado
    if NameESP_Ativado then
        ToggleNameESPButton.Text = "Desativar Name ESP"
        -- Lógica para ativar o Name ESP
        print("Name ESP Ativado")
    else
        ToggleNameESPButton.Text = "Ativar Name ESP"
        -- Lógica para desativar o Name ESP
        print("Name ESP Desativado")
    end
end

-- Criando os botões do painel
createButton("ToggleESPButton", UDim2.new(0, 20, 0, 20), "Ativar ESP", toggleESP)
createButton("ToggleHitboxButton", UDim2.new(0, 20, 0, 70), "Ativar Hitbox", toggleHitbox)
createButton("ToggleDistanceESPButton", UDim2.new(0, 20, 0, 120), "Ativar Distância ESP", toggleDistanceESP)
createButton("ToggleNameESPButton", UDim2.new(0, 20, 0, 170), "Ativar Name ESP", toggleNameESP)

-- Funções de ESP, Hitbox, Distância ESP e Name ESP
-- Estas funções irão gerenciar a ativação/desativação dos efeitos.

local function updateESP()
    -- Lógica para atualizar o ESP
    if ESP_Ativado then
        -- Código para ativar o ESP
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local highlight = Instance.new("Highlight")
                highlight.Adornee = player.Character
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.Parent = player.Character
            end
        end
    end
end

local function updateHitbox()
    -- Lógica para ativar a Hitbox (aumentar área de detecção de colisão)
    if Hitbox_Ativado then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                -- Adicionar hitbox visual ou de detecção para o personagem
                local hitbox = Instance.new("Part")
                hitbox.Size = Vector3.new(5, 5, 5) -- Ajuste conforme necessário
                hitbox.Position = player.Character.HumanoidRootPart.Position
                hitbox.Anchored = true
                hitbox.CanCollide = false
                hitbox.Parent = player.Character
            end
        end
    end
end

local function updateDistanceESP()
    -- Lógica para ativar o Distance ESP
    if DistanceESP_Ativado then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (player.Character.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude
                local distanceLabel = Instance.new("BillboardGui")
                distanceLabel.Adornee = player.Character.HumanoidRootPart
                distanceLabel.Size = UDim2.new(0, 100, 0, 50)
                distanceLabel.StudsOffset = Vector3.new(0, 2, 0)
                distanceLabel.AlwaysOnTop = true
                distanceLabel.Parent = game.CoreGui
                local label = Instance.new("TextLabel")
                label.Size = UDim2.new(1, 0, 1, 0)
                label.Text = math.floor(distance) .. " studs"
                label.BackgroundTransparency = 1
                label.TextColor3 = Color3.fromRGB(255, 255, 255)
                label.Font = Enum.Font.SourceSans
                label.TextSize = 18
                label.Parent = distanceLabel
            end
        end
    end
end

local function updateNameESP()
    -- Lógica para ativar o Name ESP
    if NameESP_Ativado then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character and player.Character:FindFirstChild("Head") then
                local nameLabel = Instance.new("BillboardGui")
                nameLabel.Adornee = player.Character.Head
                nameLabel.Size = UDim2.new(0, 100, 0, 50)
                nameLabel.StudsOffset = Vector3.new(0, 2, 0)
                nameLabel.AlwaysOnTop = true
                nameLabel.Parent = game.CoreGui
                local label = Instance.new("TextLabel")
                label.Size = UDim2.new(1, 0, 1, 0)
                label.Text = player.Name
                label.BackgroundTransparency = 1
                label.TextColor3 = Color3.fromRGB(255, 255, 255)
                label.Font = Enum.Font.SourceSans
                label.TextSize = 18
                label.Parent = nameLabel
            end
        end
    end
end

-- Atualizando o painel continuamente
while true do
    wait(0.1)
    updateESP()
    updateHitbox()
    updateDistanceESP()
    updateNameESP()
end
