# Scriptalex
Scriptalex
-- Criação do painel de interface
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local ColorPickerButton = Instance.new("TextButton")
local ToggleESPButton = Instance.new("TextButton")
local ESP_Ativado = false
local ESP = {}
local HighlightColor = Color3.fromRGB(255, 0, 0) -- Cor inicial do destaque (Vermelho)

-- Painel
ScreenGui.Parent = game.Players.LocalPlayer.PlayerGui
ScreenGui.ResetOnSpawn = false

MainFrame.Parent = ScreenGui
MainFrame.Size = UDim2.new(0, 250, 0, 150)
MainFrame.Position = UDim2.new(0.5, -125, 0.5, -75)
MainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MainFrame.BackgroundTransparency = 0.3

Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.Text = "Painel ESP"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

-- Botão para ativar/desativar ESP
ToggleESPButton.Parent = MainFrame
ToggleESPButton.Size = UDim2.new(0.8, 0, 0.2, 0)
ToggleESPButton.Position = UDim2.new(0.1, 0, 0.3, 0)
ToggleESPButton.Text = "Ativar ESP"
ToggleESPButton.TextColor3 = Color3.fromRGB(0, 255, 0)
ToggleESPButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
ToggleESPButton.Font = Enum.Font.SourceSansBold
ToggleESPButton.TextSize = 18

-- Botão para escolher a cor
ColorPickerButton.Parent = MainFrame
ColorPickerButton.Size = UDim2.new(0.8, 0, 0.2, 0)
ColorPickerButton.Position = UDim2.new(0.1, 0, 0.6, 0)
ColorPickerButton.Text = "Mudar Cor"
ColorPickerButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ColorPickerButton.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
ColorPickerButton.Font = Enum.Font.SourceSansBold
ColorPickerButton.TextSize = 18

-- Função para destacar o jogador
function ESP:HighlightPlayer(player)
    if not ESP_Ativado then return end
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local highlight = Instance.new("Highlight")
        highlight.Adornee = player.Character
        highlight.FillColor = HighlightColor
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255) -- Branco
        highlight.Parent = game.CoreGui
    end
end

-- Função para ativar/desativar ESP
ToggleESPButton.MouseButton1Click:Connect(function()
    ESP_Ativado = not ESP_Ativado
    if ESP_Ativado then
        ToggleESPButton.Text = "Desativar ESP"
        ToggleESPButton.TextColor3 = Color3.fromRGB(255, 0, 0)
        for _, player in pairs(game.Players:GetPlayers()) do
            ESP:HighlightPlayer(player)
        end
    else
        ToggleESPButton.Text = "Ativar ESP"
        ToggleESPButton.TextColor3 = Color3.fromRGB(0, 255, 0)
        -- Remove o highlight de todos os jogadores
        for _, v in pairs(game.CoreGui:GetChildren()) do
            if v:IsA("Highlight") then
                v:Destroy()
            end
        end
    end
end)

-- Função para mudar a cor do destaque
ColorPickerButton.MouseButton1Click:Connect(function()
    -- Exemplo de um prompt de cor (no caso, estamos usando um número de cores predefinido)
    local colorOptions = {
        Color3.fromRGB(255, 0, 0), -- Vermelho
        Color3.fromRGB(0, 255, 0), -- Verde
        Color3.fromRGB(0, 0, 255), -- Azul
        Color3.fromRGB(255, 255, 0), -- Amarelo
        Color3.fromRGB(255, 165, 0), -- Laranja
    }
    
    -- Aleatoriamente escolhe uma cor da lista
    HighlightColor = colorOptions[math.random(1, #colorOptions)]
    
    -- Exibe a cor escolhida no botão
    ColorPickerButton.Text = "Cor Selecionada"
    ColorPickerButton.BackgroundColor3 = HighlightColor
end)

-- Função para limpar o highlight ao sair do jogo
game.Players.PlayerRemoving:Connect(function(player)
    for _, v in pairs(game.CoreGui:GetChildren()) do
        if v:IsA("Highlight") and v.Adornee == player.Character then
            v:Destroy()
        end
    end
end)
