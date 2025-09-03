-- GUI + زر
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 150, 0, 50)
Button.Position = UDim2.new(1, -170, 0.5, -25)
Button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
Button.Text = "GOTPBASE"
Button.TextColor3 = Color3.fromRGB(255,255,255)
Button.Parent = ScreenGui

-- متغيرات
local running = false
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hum = char:WaitForChild("Humanoid")

-- God Mode
local function enableGodMode()
    hum.Health = math.huge
    hum:GetPropertyChangedSignal("Health"):Connect(function()
        hum.Health = math.huge
    end)
end

-- تشغيل/إيقاف
Button.MouseButton1Click:Connect(function()
    running = not running
    if running then
        Button.BackgroundColor3 = Color3.fromRGB(0,255,0)
        enableGodMode()
        -- لووب البناء
        task.spawn(function()
            while running do
                local root = char:FindFirstChild("HumanoidRootPart")
                if root then
                    local part = Instance.new("Part")
                    part.Size = Vector3.new(10,1,10)
                    part.Anchored = true
                    part.CanCollide = true
                    part.Position = root.Position - Vector3.new(0,3,0)
                    part.Parent = workspace
                    
                    game:GetService("Debris"):AddItem(part,1) -- يختفي بعد 1 ثانية
                end
                task.wait(0.2) -- كل 0.2 ثانية يطلع بلوك جديد
            end
        end)
    else
        Button.BackgroundColor3 = Color3.fromRGB(255,0,0)
    end
end)
