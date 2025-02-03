local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local workspace = game:GetService("Workspace")

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local RevealButton = Instance.new("TextButton")
local HideButton = Instance.new("TextButton")

ScreenGui.Name = "GlassBridgeUI"
ScreenGui.Parent = Player:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false -- Impede que o UI seja reiniciado ao reaparecer

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Position = UDim2.new(0.1, 0, 0.1, 0)
MainFrame.Size = UDim2.new(0, 200, 0, 100)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = true -- Garante que o frame é visível

-- Adiciona um ZIndex para garantir que os botões fiquem visíveis
MainFrame.ZIndex = 10

RevealButton.Name = "RevealButton"
RevealButton.Parent = MainFrame
RevealButton.BackgroundColor3 = Color3.fromRGB(50, 200, 50)
RevealButton.Size = UDim2.new(0, 180, 0, 40)
RevealButton.Position = UDim2.new(0, 10, 0, 10)
RevealButton.Font = Enum.Font.SourceSans
RevealButton.Text = "Revelar"
RevealButton.TextColor3 = Color3.fromRGB(255, 255, 255)
RevealButton.TextSize = 24
RevealButton.ZIndex = 20 -- ZIndex maior para garantir visibilidade

HideButton.Name = "HideButton"
HideButton.Parent = MainFrame
HideButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
HideButton.Size = UDim2.new(0, 180, 0, 40)
HideButton.Position = UDim2.new(0, 10, 0, 60)
HideButton.Font = Enum.Font.SourceSans
HideButton.Text = "Esconder"
HideButton.TextColor3 = Color3.fromRGB(255, 255, 255)
HideButton.TextSize = 24
HideButton.ZIndex = 20 -- ZIndex maior para garantir visibilidade

local function revealParts()
    local glassBridgeModel = workspace:FindFirstChild("GlassBridge")

    if not glassBridgeModel then
        warn("Modelo 'Squid Game Glass Bridge' não encontrado no Workspace.")
        return
    end

    local glassGroup = glassBridgeModel:FindFirstChild("Bridge")

    if not glassGroup then
        warn("Grupo 'glass' não encontrado dentro do modelo.")
        return
    end

    for _, pairGroup in ipairs(glassGroup:GetChildren()) do
        if pairGroup:IsA("Model") or pairGroup:IsA("Folder") then
            for _, part in ipairs(pairGroup:GetChildren()) do
                if part:IsA("Part") and part:FindFirstChild("TouchInterest") then
                    part.BrickColor = BrickColor.new("Bright red")
                    part.Material = Enum.Material.Neon
                end
            end
        end
    end

    print("Partes reveladas.")
end

local function hideParts()
    local glassBridgeModel = workspace:FindFirstChild("Squid Game Glass Bridge")

    if not glassBridgeModel then
        warn("Modelo 'Squid Game Glass Bridge' não encontrado no Workspace.")
        return
    end

    local glassGroup = glassBridgeModel:FindFirstChild("glass")

    if not glassGroup then
        warn("Grupo 'glass' não encontrado dentro do modelo.")
        return
    end

    for _, pairGroup in ipairs(glassGroup:GetChildren()) do
        if pairGroup:IsA("Model") or pairGroup:IsA("Folder") then
            for _, part in ipairs(pairGroup:GetChildren()) do
                if part:IsA("Part") then
                    part.BrickColor = BrickColor.new("Medium stone grey")
                    part.Material = Enum.Material.SmoothPlastic
                end
            end
        end
    end

    print("Partes escondidas.")
end

RevealButton.MouseButton1Click:Connect(revealParts)
HideButton.MouseButton1Click:Connect(hideParts)

print("UI criada com sucesso.")
