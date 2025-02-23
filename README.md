local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Button1 = Instance.new("TextButton")
local Button2 = Instance.new("TextButton")
local Button3 = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.new(1, 1, 1)
Frame.Position = UDim2.new(0.3, 0, 0.3, 0)
Frame.Size = UDim2.new(0.4, 0, 0.4, 0)

Button1.Parent = Frame
Button1.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
Button1.Position = UDim2.new(0.1, 0, 0.1, 0)
Button1.Size = UDim2.new(0.8, 0, 0.2, 0)
Button1.Text = "Dupe 1"
Button1.MouseButton1Click:Connect(function()
    game.Players.LocalPlayer.leaderstats.Money.Value = game.Players.LocalPlayer.leaderstats.Money.Value + 1000
    print("Dupe 1 selecionado")
end)

Button2.Parent = Frame
Button2.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
Button2.Position = UDim2.new(0.1, 0, 0.4, 0)
Button2.Size = UDim2.new(0.8, 0, 0.2, 0)
Button2.Text = "Dupe 2"
Button2.MouseButton1Click:Connect(function()
    game.Players.LocalPlayer.leaderstats.Money.Value = game.Players.LocalPlayer.leaderstats.Money.Value + 2000
    print("Dupe 2 selecionado")
end)

Button3.Parent = Frame
Button3.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
Button3.Position = UDim2.new(0.1, 0, 0.7, 0)
Button3.Size = UDim2.new(0.8, 0, 0.2, 0)
Button3.Text = "Gerador Dinheiro"
Button3.MouseButton1Click:Connect(function()
    while true do
        game.Players.LocalPlayer.leaderstats.Money.Value = game.Players.LocalPlayer.leaderstats.Money.Value + 100
        wait(1) -- Adiciona dinheiro a cada segundo
    end
    print("Gerador de Dinheiro selecionado")
end)
