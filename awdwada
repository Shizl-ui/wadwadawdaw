--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]
local AztechTeam = {}

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local humanoid, character = nil, nil

function AztechTeam.initializeCharacter()
    character = player.Character or player.CharacterAdded:Wait()
    humanoid = character:WaitForChild("Humanoid")
end

AztechTeam.initializeCharacter()
player.CharacterAdded:Connect(AztechTeam.initializeCharacter) -- Reinitialize on character respawn

function AztechTeam.setToolName(hotbarIndex, moveName)
    local hotbar = playerGui:FindFirstChild("Hotbar")
    if hotbar then
        local backpack = hotbar:FindFirstChild("Backpack")
        local hotbarFrame = backpack and backpack:FindFirstChild("Hotbar")
        local baseButton = hotbarFrame and hotbarFrame:FindFirstChild(tostring(hotbarIndex))
        if baseButton then
            local toolNameLabel = baseButton:FindFirstChild("Base") and baseButton.Base:FindFirstChild("ToolName")
            if toolNameLabel then
                toolNameLabel.Text = moveName
            end
        end
    end
end

-- Set move names
AztechTeam.setToolName(1, "Hulk PUNCH")
AztechTeam.setToolName(2, "Fearsome barrage")
AztechTeam.setToolName(3, "Hulk Push")
AztechTeam.setToolName(4, "Hulk Smash")

-- Create Hulk Leap Tool
local function createHulkLeapTool()
    local tool = Instance.new("Tool")
    tool.Name = "Hulk Leap"
    tool.RequiresHandle = false
    tool.Parent = player.Backpack
end

createHulkLeapTool() -- Create the tool when the script starts

-- Hulk Leap Function
function AztechTeam.hulkLeap()
    local randomPlayer = nil
    local players = game.Players:GetPlayers()
    
    -- Filter out the local player to avoid teleporting to themselves
    local otherPlayers = {}
    for _, p in ipairs(players) do
        if p ~= player then
            table.insert(otherPlayers, p)
        end
    end

    -- Select a random player
    if #otherPlayers > 0 then
        randomPlayer = otherPlayers[math.random(1, #otherPlayers)]
    end

    if randomPlayer then
        -- Get the random player's position and add 100 to the Y-coordinate
        local targetPosition = randomPlayer.Character and randomPlayer.Character.HumanoidRootPart.Position
        if targetPosition then
            character:SetPrimaryPartCFrame(CFrame.new(targetPosition.X, targetPosition.Y + 100, targetPosition.Z))
        end
    end
end

-- Bind the Hulk Leap action to the tool's activation
local hulkLeapTool = player.Backpack:WaitForChild("Hulk Leap")
hulkLeapTool.Activated:Connect(function()
    AztechTeam.hulkLeap()  -- Activate Hulk Leap when the tool is used
end)

-- change their speed and things
local birdUSuck = {
    -- M1 replacements(bird sending hentai 4k) 
    [10469493270] = {replacementId = "17889458563", startTime = 0, speed = 1},  -- 1st M1
    [10469630950] = {replacementId = "17889461810", startTime = 0, speed = 1},  -- 2nd M1
    [10469639222] = {replacementId = "17889471098", startTime = 0, speed = 1},  -- 3rd M1
    [10469643643] = {replacementId = "17889290569", startTime = 0, speed = 1},  -- 4th M1

    -- Moves
    [10468665991] = {replacementId = "18896127525", startTime = 0.2, speed = 1}, -- Move 1
    [10466974800] = {replacementId = "12534735382", startTime = 0, speed = 1.3},  -- Move 2
    [10471336737] = {replacementId = "17838006839", startTime = 0.5, speed = 1},  -- Move 3
    [12510170988] = {replacementId = "18464372850", startTime = 2, speed = 1},    -- Move 4

    -- moves like downslam etc...
    [10470104242] = {replacementId = "12684185971", startTime = 0, speed = 1},    -- Downslam
    [10503381238] = {replacementId = "14900168720", startTime = 1.3, speed = 1},  -- Mini Uppercut
    [10479335397] = {replacementId = "14046756619", startTime = 0, speed = 0.7},  -- Front Dash
}

function AztechTeam.stopAllAnimations()
    for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do
        track:Stop()
    end
end

function AztechTeam.playReplacementAnimation(config)
    local anim = Instance.new("Animation")
    anim.AnimationId = "rbxassetid://" .. config.replacementId
    local track = humanoid:LoadAnimation(anim)
    track:Play()
    track:AdjustSpeed(0)
    track.TimePosition = config.startTime
    track:AdjustSpeed(config.speed)
end

humanoid.AnimationPlayed:Connect(function(animationTrack)
    local animId = tonumber(animationTrack.Animation.AnimationId:match("%d+"))
    local config = birdUSuck[animId]
    if config then
        AztechTeam.stopAllAnimations()
        AztechTeam.playReplacementAnimation(config)
    end
end)

character.DescendantAdded:Connect(function(descendant)
    if descendant:IsA("BodyVelocity") then
        descendant.Velocity = Vector3.new(descendant.Velocity.X, 0, descendant.Velocity.Z)
    end
end)

-- ult moves and name soon...
