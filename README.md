-- Script Lua para Roblox - Interface de Teleporte Simples

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local savedPosition = nil

-- Função para criar a interface
local function createUI()
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "TeleportGui"
    screenGui.Parent = player:WaitForChild("PlayerGui")

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 250, 0, 150)
    frame.Position = UDim2.new(0.5, -125, 0.5, -75)
    frame.BackgroundColor3 = Color3.fromRGB(50, 100, 200)
    frame.Visible = false
    frame.Parent = screenGui

    local saveButton = Instance.new("TextButton")
    saveButton.Size = UDim2.new(0, 220, 0, 40)
    saveButton.Position = UDim2.new(0, 15, 0, 20)
    saveButton.Text = "Salvar Local Atual"
    saveButton.BackgroundColor3 = Color3.fromRGB(100, 200, 100)
    saveButton.Parent = frame

    local teleportButton = Instance.new("TextButton")
    teleportButton.Size = UDim2.new(0, 220, 0, 40)
    teleportButton.Position = UDim2.new(0, 15, 0, 75)
    teleportButton.Text = "Teleportar para Local Salvo"
    teleportButton.BackgroundColor3 = Color3.fromRGB(200, 100, 100)
    teleportButton.Parent = frame

    -- Salvar posição atual
    saveButton.MouseButton1Click:Connect(function()
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            savedPosition = player.Character.HumanoidRootPart.Position
            saveButton.Text = "Local Salvo!"
        end
    end)

    -- Teleportar para posição salva
    teleportButton.MouseButton1Click:Connect(function()
        if savedPosition and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(savedPosition)
        end
    end)

    -- Abrir interface com tecla G
    game:GetService("UserInputService").InputBegan:Connect(function(input, processed)
        if processed then return end
        if input.KeyCode == Enum.KeyCode.G then
            frame.Visible = not frame.Visible
            -- Resetar texto do botão de salvar ao abrir a interface
            saveButton.Text = "Salvar Local Atual"
        end
    end)
end

createUI()
