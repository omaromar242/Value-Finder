local player = game:GetService("Players").LocalPlayer

-- Create the ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "EquippedValuesGui"
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Create the main frame
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0.3, 0, 0.4, 0)
mainFrame.Position = UDim2.new(0.35, 0, 0.3, 0)
mainFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui

-- Add the title label
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0.2, 0)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "Equipped Values"
titleLabel.TextScaled = true
titleLabel.TextColor3 = Color3.new(1, 1, 1)
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.Parent = mainFrame

-- Add the "X" button to close the frame
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0.1, 0, 0.1, 0)
closeButton.Position = UDim2.new(0.9, 0, 0, 0)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.TextScaled = true
closeButton.Font = Enum.Font.SourceSansBold
closeButton.Parent = mainFrame

-- Close the main frame when the "X" button is clicked
closeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
end)

-- Function to create buttons for each value
local function createEquippedValueButton(name, value, positionY)
    local valueButton = Instance.new("TextButton")
    valueButton.Size = UDim2.new(0.8, 0, 0.15, 0)
    valueButton.Position = UDim2.new(0.1, 0, positionY, 0)
    valueButton.BackgroundColor3 = Color3.fromRGB(75, 75, 75)
    valueButton.Text = name .. ": " .. tostring(value.Value)
    valueButton.TextColor3 = Color3.new(1, 1, 1)
    valueButton.TextScaled = true
    valueButton.Font = Enum.Font.SourceSansBold
    valueButton.Parent = mainFrame

    -- Update the button text when the value changes
    value:GetPropertyChangedSignal("Value"):Connect(function()
        valueButton.Text = name .. ": " .. tostring(value.Value)
    end)

    -- Copy the value when the button is clicked
    valueButton.MouseButton1Click:Connect(function()
        setclipboard(tostring(value.Value)) -- Copies the value to the clipboard
        print(name .. " value copied: " .. tostring(value.Value))
    end)
end

-- Access the player's Equipped1, Equipped2, Equipped3, and Equipped4 values
local equipped1 = player:WaitForChild("Equipped1") 
local equipped2 = player:WaitForChild("Equipped2") 
local equipped3 = player:WaitForChild("Equipped3") 
local equipped4 = player:WaitForChild("Equipped4") 

-- Add buttons for each equipped value
createEquippedValueButton("Equipped1", equipped1, 0.25)
createEquippedValueButton("Equipped2", equipped2, 0.45)
createEquippedValueButton("Equipped3", equipped3, 0.65)
createEquippedValueButton("Equipped4", equipped4, 0.85)
