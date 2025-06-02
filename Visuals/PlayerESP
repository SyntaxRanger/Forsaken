local SurvivorsFolder = workspace.Players.Survivors
local KillersFolder = workspace.Players.Killers

local HighlightSettings = {
    FillTransparency = 0.9,
    OutlineColor = Color3.fromRGB(255, 255, 255),
    OutlineTransparency = 0.7,
    DepthMode = Enum.HighlightDepthMode.AlwaysOnTop,
    Enabled = true
}

local function ApplyHighlight(Target, FillColor, HighlightName)
    local ExistingHighlight = Target:FindFirstChild(HighlightName)
    if not ExistingHighlight then
        local NewHighlight = Instance.new("Highlight")
        NewHighlight.Name = HighlightName
        NewHighlight.Adornee = Target
        NewHighlight.FillColor = FillColor
        NewHighlight.FillTransparency = HighlightSettings.FillTransparency
        NewHighlight.OutlineColor = HighlightSettings.OutlineColor
        NewHighlight.OutlineTransparency = HighlightSettings.OutlineTransparency
        NewHighlight.DepthMode = HighlightSettings.DepthMode
        NewHighlight.Enabled = HighlightSettings.Enabled
        NewHighlight.Parent = Target
    end
end

local function UpdateHighlights()
    for _, Character in ipairs(SurvivorsFolder:GetChildren()) do
        local Highlight = Character:FindFirstChild("SurvivorHighlight")
        if Highlight then
            Highlight.FillColor = Color3.fromRGB(48, 227, 255)
            Highlight.FillTransparency = HighlightSettings.FillTransparency
            Highlight.OutlineColor = HighlightSettings.OutlineColor
            Highlight.OutlineTransparency = HighlightSettings.OutlineTransparency
            Highlight.DepthMode = HighlightSettings.DepthMode
            Highlight.Enabled = HighlightSettings.Enabled
        else
            ApplyHighlight(Character, Color3.fromRGB(48, 227, 255), "SurvivorHighlight")
        end
    end
    for _, Character in ipairs(KillersFolder:GetChildren()) do
        local Highlight = Character:FindFirstChild("KillerHighlight")
        if Highlight then
            Highlight.FillColor = Color3.fromRGB(255, 0, 0)
            Highlight.FillTransparency = HighlightSettings.FillTransparency
            Highlight.OutlineColor = HighlightSettings.OutlineColor
            Highlight.OutlineTransparency = HighlightSettings.OutlineTransparency
            Highlight.DepthMode = HighlightSettings.DepthMode
            Highlight.Enabled = HighlightSettings.Enabled
        else
            ApplyHighlight(Character, Color3.fromRGB(255, 0, 0), "KillerHighlight")
        end
    end
end

local function MonitorFolder(Folder, FillColor, HighlightName)
    Folder.ChildAdded:Connect(function(Character)
        ApplyHighlight(Character, FillColor, HighlightName)
    end)
    Folder.ChildRemoved:Connect(function()
        UpdateHighlights()
    end)
    for _, Character in ipairs(Folder:GetChildren()) do
        ApplyHighlight(Character, FillColor, HighlightName)
    end
end

MonitorFolder(SurvivorsFolder, Color3.fromRGB(48, 227, 255), "SurvivorHighlight")
MonitorFolder(KillersFolder, Color3.fromRGB(255, 0, 0), "KillerHighlight")

task.spawn(function()
    while true do
        UpdateHighlights()
        task.wait(1)
    end
end)
