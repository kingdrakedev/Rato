-- Interface simples
local ScreenGui = Instance.new("ScreenGui")
local Button = Instance.new("TextButton")

ScreenGui.Name = "AutoWin_GUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.CoreGui

Button.Name = "AutoWinButton"
Button.Parent = ScreenGui
Button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Button.Position = UDim2.new(0, 20, 0, 200)
Button.Size = UDim2.new(0, 160, 0, 40)
Button.Text = "Ganhar Win"
Button.TextColor3 = Color3.fromRGB(255, 255, 255)
Button.TextScaled = true

-- Função para dar win
local function darWin()
    -- Tente encontrar um RemoteEvent que controla as wins
    -- Nome comum em muitos jogos: "RemoteEvent", "AddWin", "WinRemote", etc

    -- EXEMPLO 1: Se o jogo tiver um Remote chamado "AddWin"
    local remote = game:GetService("ReplicatedStorage"):FindFirstChild("AddWin")
    if remote and remote:IsA("RemoteEvent") then
        remote:FireServer()
        print("✔️ Win enviada via RemoteEvent")
    end

    -- EXEMPLO 2: Se a Win for armazenada no Leaderstats e puder ser manipulada localmente (muito raro e só em jogos mal protegidos)
    local player = game:GetService("Players").LocalPlayer
    local stats = player:FindFirstChild("leaderstats")
    if stats and stats:FindFirstChild("Wins") then
        stats.Wins.Value = stats.Wins.Value + 1
        print("⚠️ Win alterada localmente (visual apenas)")
    end
end

-- Ação do botão
Button.MouseButton1Click:Connect(function()
    darWin()
end)
