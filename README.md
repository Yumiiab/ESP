-- Cria um GUI para ESP
local ESP = Instance.new("ScreenGui")
ESP.Name = "ESP"
ESP.Parent = game.CoreGui

-- Função para criar um Box ESP em torno de um jogador
local function CreateESPBox(player)
    local Box = Instance.new("BoxHandleAdornment")
    Box.Name = "ESPBox"
    Box.Size = Vector3.new(4, 5, 1)
    Box.Adornee = player.Character:FindFirstChild("HumanoidRootPart")
    Box.Parent = ESP
    Box.AlwaysOnTop = true
    Box.ZIndex = 10
    Box.Transparency = 0.5
    Box.Color3 = Color3.new(1, 0, 0)
end

-- Adiciona ESP para todos os jogadores atuais
for _, player in pairs(game.Players:GetPlayers()) do
    if player ~= game.Players.LocalPlayer then
        CreateESPBox(player)
    end
end

-- Adiciona ESP para novos jogadores que entrarem no jogo
game.Players.PlayerAdded:Connect(function(player)
    if player ~= game.Players.LocalPlayer then
        player.CharacterAdded:Connect(function()
            CreateESPBox(player)
        end)
    end
end)

-- Remove ESP quando os jogadores saem do jogo
game.Players.PlayerRemoving:Connect(function(player)
    if ESP:FindFirstChild(player.Name) then
        ESP[player.Name]:Destroy()
    end
end)
