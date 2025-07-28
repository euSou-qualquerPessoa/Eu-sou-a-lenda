-- Script de voo
local player = game.Players.LocalPlayer
local character = player.Character
local humanoid = character:WaitForChild("Humanoid")

-- Função para voar
local function fly()
    humanoid.PlatformStand = true
    character.HumanoidRootPart.Anchored = true
    local bodyGyro = Instance.new("BodyGyro")
    bodyGyro.Parent = character.HumanoidRootPart
    local bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.Parent = character.HumanoidRootPart
    bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
    
    -- Função para controlar o voo
    local function onInputBegan(input)
        if input.KeyCode == Enum.KeyCode.W then
            bodyVelocity.Velocity = character.HumanoidRootPart.CFrame.LookVector * 50
        elseif input.KeyCode == Enum.KeyCode.S then
            bodyVelocity.Velocity = -character.HumanoidRootPart.CFrame.LookVector * 50
        elseif input.KeyCode == Enum.KeyCode.A then
            bodyVelocity.Velocity = -character.HumanoidRootPart.CFrame.RightVector * 50
        elseif input.KeyCode == Enum.KeyCode.D then
            bodyVelocity.Velocity = character.HumanoidRootPart.CFrame.RightVector * 50
        elseif input.KeyCode == Enum.KeyCode.Space then
            bodyVelocity.Velocity = Vector3.new(bodyVelocity.Velocity.X, 50, bodyVelocity.Velocity.Z)
        elseif input.KeyCode == Enum.KeyCode.LeftShift then
            bodyVelocity.Velocity = Vector3.new(bodyVelocity.Velocity.X, -50, bodyVelocity.Velocity.Z)
        end
    end
    
    -- Função para parar o voo
    local function onInputEnded(input)
        if input.KeyCode == Enum.KeyCode.W or input.KeyCode == Enum.KeyCode.S or input.KeyCode == Enum.KeyCode.A or input.KeyCode == Enum.KeyCode.D then
            bodyVelocity.Velocity = Vector3.new(0, bodyVelocity.Velocity.Y, 0)
        end
    end
    
    game:GetService("UserInputService").InputBegan:Connect(onInputBegan)
    game:GetService("UserInputService").InputEnded:Connect(onInputEnded)
end

-- Ativar o voo
fly()
