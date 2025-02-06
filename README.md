# Scriptalex
Scriptalex
-- Criando o painel e as funcionalidades
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Configuração inicial do painel
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local ESPButton = Instance.new("TextButton")
local HitboxButton = Instance.new("TextButton")
local DistanceESPButton = Instance.new("TextButton")
local NameESPButton = Instance.new("TextButton")
local ToggleESPButton = Instance.new("TextButton")
local ToggleHitboxButton = Instance.new("TextButton")
local ToggleDistanceESPButton = Instance.new("TextButton")
local ToggleNameESPButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui

-- Configuração do Frame
MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MainFrame.BackgroundTransparency = 0.5

-- Função de Criar Botões no Painel
local function createButton(name, position, text, func)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Size = UDim2.new(0, 260, 0, 50)
    button.Position = position
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.Parent = MainFrame
    button.MouseButton1Click:Connect(func)
    return button
end

-- Variáveis para ESP, Hitbox e outras funções
local ESP_Ativado = false
local Hitbox_Ativado = false
local DistanceESP_Ativado = false
local NameESP_Ativado = false

-- Função para ativar/desativar o ESP
local function toggleESP()
    ESP_Ativado = not ESP_Ativado
    if ESP_Ativado then
        ToggleESPButton.Text = "Desativar ESP"
        -- Lógica de ativação do ESP (mostrando caixas ou outras marcas)
    else
        ToggleESPButton.Text = "Ativar ESP"
        -- Lógica de desativação do ESP
    end
end

-- Função para ativar/desativar a Hitbox
local function toggleHitbox()
    Hitbox_Ativado = not Hitbox_Ativado
    if Hitbox_Ativado then
        ToggleHitboxButton.Text = "Desativar Hitbox"
        -- Lógica para adicionar a hitbox
    else
        ToggleHitboxButton.Text = "Ativar Hitbox"
        -- Lógica para remover a hitbox
    end
end

-- Função para ativar/desativar o Distance ESP
local function toggleDistanceESP()
    DistanceESP_Ativado = not DistanceESP_Ativado
    if DistanceESP_Ativado then
        ToggleDistanceESPButton.Text = "Desativar Distance ESP"
        -- Lógica para ativar a visualização de distância
    else
        ToggleDistanceESPButton.Text = "Ativar Distance ESP"
        -- Lógica para desativar a visualização de distância
    end
end

-- Função para ativar/desativar o Name ESP
local function toggleNameESP()
    NameESP_Ativado = not NameESP_Ativado
    if NameESP_Ativado then
        ToggleNameESPButton.Text = "Desativar Name ESP"
        -- Lógica para mostrar os nomes dos jogadores
    else
        ToggleNameESPButton.Text = "Ativar Name ESP"
        -- Lógica para desativar os nomes
    end
end

-- Criar botões
createButton("ESPButton", UDim2.new(0, 20, 0, 20), "Ativar ESP", toggleESP)
createButton("HitboxButton", UDim2.new(0, 20, 0, 80), "Ativar Hitbox", toggleHitbox)
createButton("DistanceESPButton", UDim2.new(0, 20, 0, 140), "Ativar Distance ESP", toggleDistanceESP)
createButton("NameESPButton", UDim2.new(0, 20, 0, 200), "Ativar Name ESP", toggleNameESP)

-- Função para a lógica de ESP (simples)
local function createESP(player)
    if ESP_Ativado then
        local box = Instance.new("BillboardGui")
        box.Adornee = player.Character.HumanoidRootPart
        box.Size = UDim2.new(0, 100, 0, 100)
        box.StudsOffset = Vector3.new(0, 2, 0)
        box.AlwaysOnTop = true
        box.Parent = game.CoreGui

        local frame = Instance.new("Frame")
        frame.Size = UDim2.new(1, 0, 1, 0)
        frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        frame.BackgroundTransparency = 0.5
        frame.Parent = box
    end
end

-- Função para a lógica de Name ESP
local function createNameESP(player)
    if NameESP_Ativado and player.Character and player.Character:FindFirstChild("Head") then
        local nameTag = Instance.new("BillboardGui")
        nameTag.Adornee = player.Character.Head
        nameTag.Size = UDim2.new(0, 100, 0, 50)
        nameTag.StudsOffset = Vector3.new(0, 2, 0)
        nameTag.AlwaysOnTop = true
        nameTag.Parent = game.CoreGui

        local nameLabel = Instance.new("TextLabel")
        nameLabel.Size = UDim2.new(1, 0, 1, 0)
        nameLabel.Text = player.Name
        nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        nameLabel.BackgroundTransparency = 1
        nameLabel.Font = Enum.Font.SourceSans
        nameLabel.TextSize = 18
        nameLabel.Parent = nameTag
    end
end

-- Função para a lógica de Distance ESP
local function createDistanceESP(player)
    if DistanceESP_Ativado then
        local distanceText = Instance.new("BillboardGui")
        distanceText.Adornee = player.Character.HumanoidRootPart
        distanceText.Size = UDim2.new(0, 100, 0, 50)
        distanceText.StudsOffset = Vector3.new(0, 3, 0)
        distanceText.AlwaysOnTop = true
        distanceText.Parent = game.CoreGui

        local distanceLabel = Instance.new("TextLabel")
        distanceLabel.Size = UDim2.new(1, 0, 1, 0)
        distanceLabel.BackgroundTransparency = 1
        distanceLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        distanceLabel.Font = Enum.Font.SourceSans
        distanceLabel.TextSize = 18
        distanceLabel.Parent = distanceText

        -- Atualiza a distância
        local function updateDistance()
            while player.Character and player.Character:FindFirstChild("HumanoidRootPart") do
                local distance = (player.Character.HumanoidRootPart.Position - character.HumanoidRootPart.Position).magnitude
                distanceLabel.Text = math.floor(distance) .. " studs"
                wait(0.5)
            end
        end

        updateDistance()
    end
end

-- Conectar os eventos de jogador
game.Players.PlayerAdded:Connect(function(player)
    -- Adicionar funcionalidades ao jogador
    player.CharacterAdded:Connect(function()
        createESP(player)
        createNameESP(player)
        createDistanceESP(player)
    end)
end)
