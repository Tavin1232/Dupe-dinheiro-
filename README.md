local player = game.Players.LocalPlayer
local humanoidRootPart = player.Character:WaitForChild("HumanoidRootPart")
local running = true  -- O Auto Farm começa imediatamente

-- Coordenadas dos três locais de entrega fornecidos
local locations = {
    Vector3.new(-246.2454833984375, 6.7608842849731445, -103.72569274902344),  -- Primeiro local de entrega
    Vector3.new(60.48515319824219, 5.763455390930176, 656.7576904296875),    -- Segundo local de entrega
    Vector3.new(807.6621704101562, 6.728733062744141, 49.6536865234375)      -- Terceiro local de entrega
}

-- Função para teleportar o jogador
local function teleportTo(position)
    if humanoidRootPart then
        humanoidRootPart.CFrame = CFrame.new(position)  -- Atualizando o CFrame diretamente
    end
end

-- Função para pressionar uma tecla por um tempo
local function pressKey(key, duration)
    local virtualInput = game:GetService("VirtualInputManager")
    virtualInput:SendKeyEvent(true, key, false, game)
    task.wait(duration)
    virtualInput:SendKeyEvent(false, key, false, game)
end

-- Função para coletar o gás
local function collectGas()
    teleportTo(Vector3.new(-496.87, 4.77, -47.41)) -- Posição do botijão
    task.wait(1)
    pressKey(Enum.KeyCode.E, 4) -- Segura a tecla E para pegar o botijão
    local gasCollected = false
    -- Verifica se o botijão foi coletado
    while not gasCollected do
        if player.Character:FindFirstChild("HumanoidRootPart") then
            gasCollected = true
        end
        task.wait(0.1)
    end
end

-- Função para entregar o gás (vai para uma das coordenadas)
local function deliverGas()
    -- Escolhe um local de entrega aleatório das coordenadas fornecidas
    local deliveryLocation = locations[math.random(1, #locations)]
    teleportTo(deliveryLocation) -- Teletransporta para o local de entrega
    task.wait(1) -- Aguarda o teletransporte
    -- Verifica se o jogador chegou ao local de entrega correto
    if (humanoidRootPart.Position - deliveryLocation).magnitude < 5 then
        pressKey(Enum.KeyCode.E, 4) -- Pressiona E para entregar o botijão
    else
        warn("Erro: Jogador não chegou ao local de entrega!")
    end
end

-- Função para ativar e desativar o Auto Farm Gas
local function autoFarmGas()
    while running do
        collectGas()    -- Pega o botijão
        deliverGas()    -- Entrega o gás
        task.wait(2)    -- Espera antes de repetir
    end
end

-- Inicia o Auto Farm assim que o código for executado
autoFarmGas()
