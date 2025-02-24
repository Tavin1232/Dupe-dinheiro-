-- Certifique-se de executar isso no executor Delta ou Xeno
local player = game.Players.LocalPlayer
local starterGui = game:GetService("StarterGui")

-- Adicionar a biblioteca KavoUI
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Anti-Cheat Menu", "DarkTheme")

-- Criar aba principal
local Main = Window:NewTab("Main")
local MainSection = Main:NewSection("Features")

-- Variáveis de controle
local dupe1Active = false
local dupe2Active = false

-- Funções específicas para os botões
MainSection:NewButton("Ativar Bypass", "Ativa o bypass", function()
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

local function generateMoney(amount)
    while wait(1) do
        local playerData = player:FindFirstChild("PlayerData")
        if playerData and playerData:FindFirstChild("Money") then
            playerData.Money.Value = playerData.Money.Value + amount
            print("Dinheiro gerado:", amount)
            amount = amount * 1.1 -- Aumenta a quantia em 10%
        else
            print("PlayerData ou Money não encontrado!")
            break
        end
    end
end

MainSection:NewButton("Dupe Function 1", "Ativa a função de duplicação 1", function()
    if not dupe1Active then
        dupe1Active = true
        dupe1Coroutine = coroutine.wrap(generateMoney)
        dupe1Coroutine(1000)
        print("Dupe Function 1 ativada")
    else
        dupe1Active = false
        dupe1Coroutine = nil
        print("Dupe Function 1 desativada")
    end
end)

MainSection:NewButton("Dupe Function 2", "Ativa a função de duplicação 2", function()
    if not dupe2Active then
        dupe2Active = true
        dupe2Coroutine = coroutine.wrap(generateMoney)
        dupe2Coroutine(1000)
        print("Dupe Function 2 ativada")
    else
        dupe2Active = false
        dupe2Coroutine = nil
        print("Dupe Function 2 desativada")
    end
end)
