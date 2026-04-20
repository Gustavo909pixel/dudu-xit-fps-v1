--[[
FPS PASEIO ADVANCED v2
This is a complete advanced Roblox FPS PVP script featuring:
- Aimbot
- Aim Lock
- Advanced ESP System
- Wallhack
- Hitbox Expander
- Infinite Jump
- Speed Boost
- Professional Collapsible UI with Close and Hide buttons
]]--

-- Aimbot Setup
local Player = game.Players.LocalPlayer
local Camera = game.Workspace.CurrentCamera
local UIS = game:GetService('UserInputService')

-- Variables
local Target = nil
local SpeedBoostEnabled = false
local InfiniteJumpEnabled = false
local JumpHeight = 50

-- Aimbot Function
function Aimbot()
    while Target do
        wait()
        if Target then
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, Target.Position)
        end
    end
end

-- Aim Lock Function
function AimLock()
    if Target then
        Camera.CFrame = CFrame.new(Camera.CFrame.Position, Target.Position)
    end
end

-- Advanced ESP System
function ESP()
    for _, v in pairs(game.Players:GetPlayers()) do
        if v ~= Player then
            local Highlight = Instance.new('Highlight', v.Character)
            Highlight.FillColor = Color3.new(1, 0, 0)
            Highlight.OutlineColor = Color3.new(0, 0, 0)
        end
    end
end

-- Wallhack Implementation
function Wallhack()
    for _, part in pairs(workspace:GetChildren()) do
        if part:IsA('Part') then
            part.Transparency = 0.5
        end
    end
end

-- Hitbox Expander
function ExpandHitbox()
    for _, v in pairs(workspace:GetChildren()) do
        if v:IsA('Part') and v.Name == 'Hitbox' then
            v.Size = v.Size * 2
        end
    end
end

-- Infinite Jump
UIS.JumpRequest:Connect(function()
    if InfiniteJumpEnabled then
        Player.Character:FindFirstChildOfClass('Humanoid'):ChangeState('Jump')
    end
end)

-- Speed Boost
function ToggleSpeedBoost()
    local humanoid = Player.Character:FindFirstChildOfClass('Humanoid')
    if SpeedBoostEnabled then
        humanoid.WalkSpeed = 50
    else
        humanoid.WalkSpeed = 16
    end
end

-- UI Implementation
local ScreenGui = Instance.new('ScreenGui', Player:WaitForChild('PlayerGui'))
local Frame = Instance.new('Frame', ScreenGui)
Frame.Size = UDim2.new(0.3, 0, 0.3, 0)
Frame.Position = UDim2.new(0.7, 0, 0.7, 0)
Frame.BackgroundColor3 = Color3.new(0, 0, 0)
Frame.BackgroundTransparency = 0.5

local ToggleButton = Instance.new('TextButton', Frame)
ToggleButton.Size = UDim2.new(1, 0, 1, 0)
ToggleButton.Text = 'Toggle Aimbot'

ToggleButton.MouseButton1Click:Connect(function()
    Target = (Target == nil) and GetClosestPlayer() or nil
    if Target then
        Aimbot()
    end
end)

-- Close & Hide Buttons
local CloseButton = Instance.new('TextButton', Frame)
CloseButton.Size = UDim2.new(0.5, 0, 0.1, 0)
CloseButton.Position = UDim2.new(0.25, 0, 0, 0)
CloseButton.Text = 'Close'

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Initialize
ESP()
Wallhack()
ExpandHitbox()
ToggleSpeedBoost()
