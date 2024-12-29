
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Função para criar uma etiqueta de nome para o jogador
local function createESP(player)
    -- Verifica se o jogador está vivo
    local character = player.Character
    if not character then return end

    -- Cria a caixa de texto para o nome
    local billboardGui = Instance.new("BillboardGui")
    billboardGui.Adornee = character:WaitForChild("Head")
    billboardGui.Size = UDim2.new(0, 100, 0, 50)
    billboardGui.StudsOffset = Vector3.new(0, 3, 0)  -- Posiciona o nome um pouco acima da cabeça

    -- Cria o texto para o nome
    local textLabel = Instance.new("TextLabel")
    textLabel.Parent = billboardGui
    textLabel.Text = player.Name
    textLabel.TextColor3 = Color3.fromRGB(255, 0, 0)  -- Cor vermelha
    textLabel.TextSize = 20
    textLabel.BackgroundTransparency = 1
    textLabel.TextStrokeTransparency = 0.5  -- Para adicionar uma borda ao texto

    -- Adiciona a GUI ao jogador
    billboardGui.Parent = game.CoreGui
end

-- Função para atualizar os ESPs enquanto o jogo está em andamento
RunService.Heartbeat:Connect(function()
    for _, player in ipairs(Players:GetPlayers()) do
        -- Evita que a ESP seja criada para o próprio jogador
        if player ~= Players.LocalPlayer then
            -- Verifica se a ESP já foi criada para este jogador
            if not player:FindFirstChild("ESP") then
                -- Cria o ESP para o jogador
                createESP(player)
                -- Marca o jogador para saber que já foi feito
                local espTag = Instance.new("BoolValue")
                espTag.Name = "ESP"
                espTag.Parent = player
            end
        end
    end
end)
