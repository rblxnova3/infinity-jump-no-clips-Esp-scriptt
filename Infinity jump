-- NOVA_HUB | PREMIUM BLUE + RED ESP
-- For your own Roblox Studio experience
-- StarterPlayer > StarterPlayerScripts > LocalScript

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local BLUE = Color3.fromRGB(0, 170, 255)
local RED = Color3.fromRGB(255, 0, 0)
local WHITE = Color3.fromRGB(245, 245, 255)
local BLACK = Color3.fromRGB(8, 14, 28)
local DARK = Color3.fromRGB(17, 32, 55)
local HEADER = Color3.fromRGB(12, 24, 45)
local DISCORD = Color3.fromRGB(88, 101, 242)
local INVITE = "https://discord.gg/Sb8qYPrD8m"

local old = playerGui:FindFirstChild("NOVA_HUB")
if old then old:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "NOVA_HUB"
gui.ResetOnSpawn = false
gui.DisplayOrder = 999
gui.Parent = playerGui

local panel = Instance.new("Frame")
panel.Name = "MainPanel"
panel.Size = UDim2.fromOffset(280, 344)
panel.Position = UDim2.new(0.5, -140, 0.5, -172)
panel.BackgroundColor3 = BLACK
panel.BorderSizePixel = 0
panel.ClipsDescendants = true
panel.Parent = gui

Instance.new("UICorner", panel).CornerRadius = UDim.new(0, 14)

local stroke = Instance.new("UIStroke")
stroke.Color = BLUE
stroke.Thickness = 2
stroke.Parent = panel

-- Header
local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 48)
header.BackgroundColor3 = HEADER
header.BorderSizePixel = 0
header.Active = true
header.Parent = panel

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -150, 1, 0)
title.Position = UDim2.fromOffset(10, 0)
title.BackgroundTransparency = 1
title.Text = "NOVA_HUB"
title.TextColor3 = BLUE
title.Font = Enum.Font.GothamBlack
title.TextSize = 19
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = header

local toggle = Instance.new("TextButton")
toggle.Size = UDim2.fromOffset(78, 28)
toggle.Position = UDim2.new(1, -120, 0, 10)
toggle.BackgroundColor3 = BLUE
toggle.TextColor3 = WHITE
toggle.Font = Enum.Font.GothamBold
toggle.TextSize = 12
toggle.Text = "MINIMIZE"
toggle.Parent = header
Instance.new("UICorner", toggle).CornerRadius = UDim.new(0, 7)

local close = Instance.new("TextButton")
close.Size = UDim2.fromOffset(30, 28)
close.Position = UDim2.new(1, -36, 0, 10)
close.BackgroundColor3 = Color3.fromRGB(190, 45, 65)
close.TextColor3 = WHITE
close.Font = Enum.Font.GothamBold
close.TextSize = 14
close.Text = "X"
close.Parent = header
Instance.new("UICorner", close).CornerRadius = UDim.new(0, 7)

close.Activated:Connect(function()
    gui:Destroy()
end)

-- Content
local content = Instance.new("Frame")
content.Position = UDim2.fromOffset(0, 48)
content.Size = UDim2.new(1, 0, 1, -48)
content.BackgroundTransparency = 1
content.Parent = panel

local function makeButton(label, y, height, color)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -20, 0, height)
    button.Position = UDim2.fromOffset(10, y)
    button.BackgroundColor3 = color or DARK
    button.TextColor3 = WHITE
    button.Text = label .. ": OFF"
    button.Font = Enum.Font.GothamBold
    button.TextSize = 14
    button.Parent = content

    Instance.new("UICorner", button).CornerRadius = UDim.new(0, 8)

    local border = Instance.new("UIStroke")
    border.Color = BLUE
    border.Thickness = 1
    border.Parent = button

    return button
end

local jumpButton = makeButton("Infinite Jump", 10, 46)
local clipButton = makeButton("No Clip", 64, 46)
local espButton = makeButton("Red Player ESP", 118, 46)

local discordButton = Instance.new("TextButton")
discordButton.Size = UDim2.new(1, -20, 0, 42)
discordButton.Position = UDim2.fromOffset(10, 172)
discordButton.BackgroundColor3 = DISCORD
discordButton.Text = "SCRIPT EMPIRE DISCORD"
discordButton.TextColor3 = WHITE
discordButton.Font = Enum.Font.GothamBold
discordButton.TextSize = 13
discordButton.Parent = content
Instance.new("UICorner", discordButton).CornerRadius = UDim.new(0, 8)

local function setButton(button, label, enabled)
    button.Text = label .. ": " .. (enabled and "ON" or "OFF")
    button.BackgroundColor3 = enabled and BLUE or DARK
end

-- Minimize to top / reopen
local minimized = false
local expandedPosition = panel.Position
local expandedSize = UDim2.fromOffset(280, 344)
local compactSize = UDim2.fromOffset(280, 48)

toggle.Activated:Connect(function()
    minimized = not minimized
    toggle.Text = minimized and "OPEN" or "MINIMIZE"
    content.Visible = not minimized

    local targetPosition
    local targetSize

    if minimized then
        expandedPosition = panel.Position
        targetPosition = UDim2.new(
            expandedPosition.X.Scale,
            expandedPosition.X.Offset,
            0, 12
        )
        targetSize = compactSize
    else
        targetPosition = expandedPosition
        targetSize = expandedSize
    end

    TweenService:Create(
        panel,
        TweenInfo.new(0.3, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),
        {Position = targetPosition, Size = targetSize}
    ):Play()
end)

-- Drag with mouse or touch
local dragging = false
local dragStart
local startPosition
local activeTouch

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        activeTouch = input
        dragStart = input.Position
        startPosition = panel.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
                activeTouch = nil
            end
        end)
    elseif input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPosition = panel.Position
    end
end)

UIS.InputChanged:Connect(function(input)
    if not dragging then return end

    if input.UserInputType == Enum.UserInputType.MouseMovement
        or input == activeTouch then
        local delta = input.Position - dragStart
        panel.Position = UDim2.new(
            startPosition.X.Scale,
            startPosition.X.Offset + delta.X,
            startPosition.Y.Scale,
            startPosition.Y.Offset + delta.Y
        )
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

-- Infinite Jump
local infiniteJump = false

jumpButton.Activated:Connect(function()
    infiniteJump = not infiniteJump
    setButton(jumpButton, "Infinite Jump", infiniteJump)
end)

UIS.JumpRequest:Connect(function()
    if not infiniteJump then return end

    local character = player.Character
    local humanoid = character and character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

-- No Clip
local noClip = false
local clipConnection
local originalCollisions = {}

local function updateNoClip()
    local character = player.Character
    if not character then return end

    for _, part in ipairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            if noClip then
                if originalCollisions[part] == nil then
                    originalCollisions[part] = part.CanCollide
                end
                part.CanCollide = false
            elseif originalCollisions[part] ~= nil then
                part.CanCollide = originalCollisions[part]
                originalCollisions[part] = nil
            end
        end
    end
end

clipButton.Activated:Connect(function()
    noClip = not noClip
    setButton(clipButton, "No Clip", noClip)

    if clipConnection then
        clipConnection:Disconnect()
        clipConnection = nil
    end

    if noClip then
        clipConnection = RunService.Stepped:Connect(updateNoClip)
        updateNoClip()
    else
        updateNoClip()
        table.clear(originalCollisions)
    end
end)

player.CharacterAdded:Connect(function()
    table.clear(originalCollisions)
    if noClip then
        task.wait(0.5)
        updateNoClip()
    end
end)

-- RED ESP: no player names
local esp = false
local highlights = {}
local characterConnections = {}

local function removeHighlight(other)
    if highlights[other] then
        highlights[other]:Destroy()
        highlights[other] = nil
    end
end

local function addHighlight(other)
    removeHighlight(other)

    if not esp or other == player or not other.Character then
        return
    end

    local highlight = Instance.new("Highlight")
    highlight.Name = "NOVA_RedESP"
    highlight.Adornee = other.Character
    highlight.FillColor = RED
    highlight.OutlineColor = Color3.fromRGB(255, 50, 50)
    highlight.FillTransparency = 0.65
    highlight.OutlineTransparency = 0
    highlight.Parent = other.Character

    highlights[other] = highlight
end

local function watchPlayer(other)
    if characterConnections[other] then
        characterConnections[other]:Disconnect()
    end

    characterConnections[other] = other.CharacterAdded:Connect(function()
        task.wait(0.5)
        addHighlight(other)
    end)

    addHighlight(other)
end

espButton.Activated:Connect(function()
    esp = not esp
    setButton(espButton, "Red Player ESP", esp)

    for _, other in ipairs(Players:GetPlayers()) do
        if other ~= player then
            if esp then
                watchPlayer(other)
            else
                removeHighlight(other)
            end
        end
    end
end)

Players.PlayerAdded:Connect(function(other)
    if esp then watchPlayer(other) end
end)

Players.PlayerRemoving:Connect(function(other)
    removeHighlight(other)

    if characterConnections[other] then
        characterConnections[other]:Disconnect()
        characterConnections[other] = nil
    end
end)

-- Discord invite button
discordButton.Activated:Connect(function()
    if typeof(setclipboard) == "function" then
        setclipboard(INVITE)
    else
        discordButton.Text = INVITE
        discordButton.TextSize = 10
    end
end)
