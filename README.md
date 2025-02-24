-- Certifique-se de executar isso no executor Delta ou Xeno
local player = game.Players.LocalPlayer
local starterGui = game:GetService("StarterGui")

-- Criar GUI principal
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
screenGui.Name = "ExploitGUI"

local mainFrame = Instance.new("Frame", screenGui)
mainFrame.Size = UDim2.new(0, 250, 0, 150)
mainFrame.Position = UDim2.new(0.5, -125, 0.4, -75)
mainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
mainFrame.BorderSizePixel = 2
mainFrame.Draggable = true -- Permite arrastar a interface
mainFrame.Active = true

-- Criar os botões
local function createButton(text, position)
    local button = Instance.new("TextButton", mainFrame)
    button.Size = UDim2.new(0, 200, 0, 30)
    button.Position = UDim2.new(0.5, -100, 0, position)
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextScaled = true
    return button
end

local bypassButton = createButton("Ativar Bypass", 10)
local dupeButton1 = createButton("Dupe Function 1", 50)
local dupeButton2 = createButton("Dupe Function 2", 90)

-- Variáveis de controle
local dupe1Active = false
local dupe2Active = false

local dupe1Coroutine
local dupe2Coroutine

-- Funções específicas para os botões
bypassButton.MouseButton1Click:Connect(function()
    -- Exemplo de código de bypass
    local mt = getrawmetatable(game)
    setreadonly(mt, false)
    local old = mt.__namecall
    mt.__namecall = newcclosure(function(...)
        -- Coloque a lógica do bypass aqui
        return old(...)
    end)
    print("Bypass ativado")
end)

local function generateMoney(player, amount, dupeActive)
    while dupeActive do
        wait(1) -- Intervalo de 1 segundo
        local playerData = player:FindFirstChild("PlayerData")
        if playerData and playerData:FindFirstChild("Money") then
            playerData.Money.Value = playerData.Money.Value + amount
            print("Dinheiro gerado:", amount)
            amount = amount * 1.1 -- Aumenta a quantia em 10%
        end
    end
end

dupeButton1.MouseButton1Click:Connect(function()
    if not dupe1Active then
        dupe1Active = true
        dupe1Coroutine = coroutine.wrap(generateMoney)
        dupe1Coroutine(player, 1000, dupe1Active)
        print("Dupe Function 1 ativada")
    else
        dupe1Active = false
        if dupe1Coroutine then
            coroutine.close(dupe1Coroutine)
        end
        print("Dupe Function 1 desativada")
    end
end)

dupeButton2.MouseButton1Click:Connect(function()
    if not dupe2Active then
        dupe2Active = true
        dupe2Coroutine = coroutine.wrap(generateMoney)
        dupe2Coroutine(player, 1000, dupe2Active)
        print("Dupe Function 2 ativada")
    else
        dupe2Active = false
        if dupe2Coroutine then
            coroutine.close(dupe2Coroutine)
        end
        print("Dupe Function 2 desativada")
    end
end)
