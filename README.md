--uwu
local Library = {}

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

local function create(class, properties)
    local obj = Instance.new(class)
    for i,v in pairs(properties) do
        obj[i] = v
    end
    return obj
end

local TabIcons = {
    ["Main"] = "rbxassetid://10723434711",
    ["Combate"] = "rbxassetid://10723407389",
    ["PVP"] = "rbxassetid://10723424505",
    ["Movimento"] = "rbxassetid://10747372992",
    ["Jogador"] = "rbxassetid://10734950309",
    ["Veiculos"] = "rbxassetid://10723434711",
    ["Troll"] = "rbxassetid://10723345518",
    ["OP"] = "rbxassetid://10723434771"
}

function Library:CreateWindow(config)
    local Window = {
        Tabs = {}
    }
    Window.Minimized = false
    Window.Hidden = false
    
    local ScreenGui = create("ScreenGui", {
        Name = "ModernLib",
        Parent = game:GetService("CoreGui"),
        ZIndexBehavior = Enum.ZIndexBehavior.Sibling,
        ResetOnSpawn = false
    })
    
    local MainFrame = create("Frame", {
        Name = "MainFrame",
        Parent = ScreenGui,
        BackgroundColor3 = Color3.fromRGB(15, 15, 20),
        BorderSizePixel = 0,
        Position = UDim2.new(0.5, -425, 0.5, -275),
        Size = UDim2.new(0, 850, 0, 550)
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 12),
        Parent = MainFrame
    })
    
    create("UIStroke", {
        Parent = MainFrame,
        Color = Color3.fromRGB(139, 92, 246),
        Thickness = 2
    })
    
    local MainShadow = create("ImageLabel", {
        Name = "Shadow",
        Parent = MainFrame,
        BackgroundTransparency = 1,
        Position = UDim2.new(0, -15, 0, -15),
        Size = UDim2.new(1, 30, 1, 30),
        ZIndex = 0,
        Image = "rbxassetid://5554236805",
        ImageColor3 = Color3.fromRGB(0, 0, 0),
        ImageTransparency = 0.3,
        ScaleType = Enum.ScaleType.Slice,
        SliceCenter = Rect.new(23, 23, 277, 277)
    })
    
    local TopBar = create("Frame", {
        Name = "TopBar",
        Parent = MainFrame,
        BackgroundColor3 = Color3.fromRGB(10, 10, 15),
        BorderSizePixel = 0,
        Size = UDim2.new(1, 0, 0, 50)
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 12),
        Parent = TopBar
    })
    
    local BottomCover = create("Frame", {
        Parent = TopBar,
        BackgroundColor3 = Color3.fromRGB(10, 10, 15),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 1, -10),
        Size = UDim2.new(1, 0, 0, 10)
    })
    
    local TopBarLine = create("Frame", {
        Parent = TopBar,
        BackgroundColor3 = Color3.fromRGB(139, 92, 246),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 1, -2),
        Size = UDim2.new(1, 0, 0, 2)
    })
    
    local LogoIcon = create("ImageLabel", {
        Name = "LogoIcon",
        Parent = TopBar,
        BackgroundTransparency = 1,
        Position = UDim2.new(0, 15, 0.5, -12),
        Size = UDim2.new(0, 24, 0, 24),
        Image = "rbxassetid://10723434771",
        ImageColor3 = Color3.fromRGB(139, 92, 246)
    })
    
    local Title = create("TextLabel", {
        Name = "Title",
        Parent = TopBar,
        BackgroundTransparency = 1,
        Position = UDim2.new(0, 50, 0, 0),
        Size = UDim2.new(0, 200, 1, 0),
        Font = Enum.Font.GothamBold,
        Text = config.Name or "UI LIBRARY",
        TextColor3 = Color3.fromRGB(255, 255, 255),
        TextSize = 16,
        TextXAlignment = Enum.TextXAlignment.Left
    })
    
    local MinimizeButton = create("TextButton", {
        Name = "MinimizeButton",
        Parent = TopBar,
        BackgroundColor3 = Color3.fromRGB(45, 45, 55),
        BorderSizePixel = 0,
        Position = UDim2.new(1, -75, 0.5, -15),
        Size = UDim2.new(0, 30, 0, 30),
        Font = Enum.Font.GothamBold,
        Text = "-",
        TextColor3 = Color3.fromRGB(200, 200, 200),
        TextSize = 20,
        AutoButtonColor = false
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 6),
        Parent = MinimizeButton
    })
    
    local CloseButton = create("TextButton", {
        Name = "CloseButton",
        Parent = TopBar,
        BackgroundColor3 = Color3.fromRGB(139, 92, 246),
        BorderSizePixel = 0,
        Position = UDim2.new(1, -40, 0.5, -15),
        Size = UDim2.new(0, 30, 0, 30),
        Font = Enum.Font.GothamBold,
        Text = "X",
        TextColor3 = Color3.fromRGB(255, 255, 255),
        TextSize = 14,
        AutoButtonColor = false
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 6),
        Parent = CloseButton
    })
    
    MinimizeButton.MouseEnter:Connect(function()
        TweenService:Create(MinimizeButton, TweenInfo.new(0.2), {
            BackgroundColor3 = Color3.fromRGB(60, 60, 70)
        }):Play()
    end)
    
    MinimizeButton.MouseLeave:Connect(function()
        TweenService:Create(MinimizeButton, TweenInfo.new(0.2), {
            BackgroundColor3 = Color3.fromRGB(45, 45, 55)
        }):Play()
    end)
    
    MinimizeButton.MouseButton1Click:Connect(function()
        Window:ToggleMinimize()
    end)
    
    CloseButton.MouseEnter:Connect(function()
        TweenService:Create(CloseButton, TweenInfo.new(0.2), {
            BackgroundColor3 = Color3.fromRGB(167, 139, 250)
        }):Play()
    end)
    
    CloseButton.MouseLeave:Connect(function()
        TweenService:Create(CloseButton, TweenInfo.new(0.2), {
            BackgroundColor3 = Color3.fromRGB(139, 92, 246)
        }):Play()
    end)
    
    CloseButton.MouseButton1Click:Connect(function()
        ScreenGui:Destroy()
    end)
    
    local SearchBox = create("TextBox", {
        Name = "SearchBox",
        Parent = TopBar,
        BackgroundColor3 = Color3.fromRGB(20, 20, 28),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 275, 0.5, -15),
        Size = UDim2.new(0, 220, 0, 30),
        Font = Enum.Font.Gotham,
        PlaceholderText = "Search...",
        Text = "",
        TextColor3 = Color3.fromRGB(180, 180, 180),
        TextSize = 13,
        TextXAlignment = Enum.TextXAlignment.Left
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 6),
        Parent = SearchBox
    })
    
    create("UIPadding", {
        Parent = SearchBox,
        PaddingLeft = UDim.new(0, 12)
    })
    
    local Sidebar = create("ScrollingFrame", {
        Name = "Sidebar",
        Parent = MainFrame,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 0, 50),
        Size = UDim2.new(0, 220, 1, -140),
        ScrollBarThickness = 4,
        ScrollBarImageColor3 = Color3.fromRGB(139, 92, 246),
        ScrollBarImageTransparency = 0.3,
        CanvasSize = UDim2.new(0, 0, 0, 0),
        AutomaticCanvasSize = Enum.AutomaticSize.Y
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 12),
        Parent = Sidebar
    })
    
    local SidebarCover = create("Frame", {
        Parent = Sidebar,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 0, 0),
        Size = UDim2.new(1, 0, 0, 10),
        ZIndex = 2
    })
    
    local SidebarCoverRight = create("Frame", {
        Parent = Sidebar,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(1, -10, 0, 0),
        Size = UDim2.new(0, 10, 1, 0),
        ZIndex = 2
    })
    
    local SidebarCoverBottom = create("Frame", {
        Parent = Sidebar,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 1, -10),
        Size = UDim2.new(1, 0, 0, 10),
        ZIndex = 2
    })
    
    local SidebarContainer = create("Frame", {
        Name = "SidebarContainer",
        Parent = Sidebar,
        BackgroundTransparency = 1,
        Size = UDim2.new(1, -10, 0, 0),
        Position = UDim2.new(0, 5, 0, 0),
        AutomaticSize = Enum.AutomaticSize.Y
    })
    
    local SidebarList = create("UIListLayout", {
        Parent = SidebarContainer,
        SortOrder = Enum.SortOrder.LayoutOrder,
        Padding = UDim.new(0, 6)
    })
    
    create("UIPadding", {
        Parent = SidebarContainer,
        PaddingTop = UDim.new(0, 10),
        PaddingLeft = UDim.new(0, 5),
        PaddingRight = UDim.new(0, 5),
        PaddingBottom = UDim.new(0, 10)
    })
    
    local PlayerInfoFrame = create("Frame", {
        Name = "PlayerInfo",
        Parent = MainFrame,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 1, -90),
        Size = UDim2.new(0, 220, 0, 90)
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 12),
        Parent = PlayerInfoFrame
    })
    
    local PlayerInfoCoverTop = create("Frame", {
        Parent = PlayerInfoFrame,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 0, 0, 0),
        Size = UDim2.new(1, 0, 0, 10)
    })
    
    local PlayerInfoCoverRight = create("Frame", {
        Parent = PlayerInfoFrame,
        BackgroundColor3 = Color3.fromRGB(18, 18, 25),
        BorderSizePixel = 0,
        Position = UDim2.new(1, -10, 0, 0),
        Size = UDim2.new(0, 10, 1, 0)
    })
    
    local PlayerAvatar = create("ImageLabel", {
        Name = "Avatar",
        Parent = PlayerInfoFrame,
        BackgroundColor3 = Color3.fromRGB(25, 25, 35),
        BorderSizePixel = 0,
        Position = UDim2.new(0, 10, 0, 10),
        Size = UDim2.new(0, 70, 0, 70),
        Image = Players:GetUserThumbnailAsync(Players.LocalPlayer.UserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size150x150)
    })
    
    create("UICorner", {
        CornerRadius = UDim.new(0, 10),
        Parent = PlayerAvatar
    })
    
    create("UIStroke", {
        Parent = PlayerAvatar,
        Color = Color3.fromRGB(139, 92, 246),
        Thickness = 2
    })
    
    local PlayerName = create("TextLabel", {
        Name = "PlayerName",
        Parent = PlayerInfoFrame,
        BackgroundTransparency = 1,
        Position = UDim2.new(0, 90, 0, 15),
        Size = UDim2.new(1, -100, 0, 25),
        Font = Enum.Font.GothamBold,
        Text = Players.LocalPlayer.Name,
        TextColor3 = Color3.fromRGB(255, 255, 255),
        TextSize = 14,
        TextXAlignment = Enum.TextXAlignment.Left,
        TextTruncate = Enum.TextTruncate.AtEnd
    })
    
    local PlayerDisplayName = create("TextLabel", {
        Name = "DisplayName",
        Parent = PlayerInfoFrame,
        BackgroundTransparency = 1,
        Position = UDim2.new(0, 90, 0, 40),
        Size = UDim2.new(1, -100, 0, 20),
        Font = Enum.Font.Gotham,
        Text = "@" .. Players.LocalPlayer.DisplayName,
        TextColor3 = Color3.fromRGB(139, 92, 246),
        TextSize = 12,
        TextXAlignment = Enum.TextXAlignment.Left,
        TextTruncate = Enum.TextTruncate.AtEnd
    })
    
    local ContentArea = create("Frame", {
        Name = "ContentArea",
        Parent = MainFrame,
        BackgroundTransparency = 1,
        BorderSizePixel = 0,
        Position = UDim2.new(0, 220, 0, 50),
        Size = UDim2.new(1, -220, 1, -50)
    })
    
    local NotificationContainer = create("Frame", {
        Name = "NotificationContainer",
        Parent = ScreenGui,
        BackgroundTransparency = 1,
        Position = UDim2.new(1, -320, 0, 20),
        Size = UDim2.new(0, 300, 1, -40),
        ZIndex = 100
    })
    
    local NotificationList = create("UIListLayout", {
        Parent = NotificationContainer,
        SortOrder = Enum.SortOrder.LayoutOrder,
        Padding = UDim.new(0, 10),
        VerticalAlignment = Enum.VerticalAlignment.Top
    })
    
    function Window:Notify(options)
        options = options or {}
        local title = options.Title or options.title or "Notification"
        local text = options.Text or options.text or options.Description or ""
        local duration = options.Duration or options.duration or 5
        
        local NotifFrame = create("Frame", {
            Parent = NotificationContainer,
            BackgroundColor3 = Color3.fromRGB(20, 20, 28),
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 80),
            Position = UDim2.new(1, 50, 0, 0)
        })
        
        create("UICorner", {
            CornerRadius = UDim.new(0, 8),
            Parent = NotifFrame
        })
        
        create("UIStroke", {
            Parent = NotifFrame,
            Color = Color3.fromRGB(139, 92, 246),
            Thickness = 2
        })
        
        local NotifAccent = create("Frame", {
            Parent = NotifFrame,
            BackgroundColor3 = Color3.fromRGB(139, 92, 246),
            BorderSizePixel = 0,
            Size = UDim2.new(0, 4, 1, 0)
        })
        
        create("UICorner", {
            CornerRadius = UDim.new(0, 8),
            Parent = NotifAccent
        })
        
        local NotifTitle = create("TextLabel", {
            Parent = NotifFrame,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 15, 0, 10),
            Size = UDim2.new(1, -30, 0, 20),
            Font = Enum.Font.GothamBold,
            Text = title,
            TextColor3 = Color3.fromRGB(255, 255, 255),
            TextSize = 14,
            TextXAlignment = Enum.TextXAlignment.Left
        })
        
        local NotifText = create("TextLabel", {
            Parent = NotifFrame,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 15, 0, 35),
            Size = UDim2.new(1, -30, 1, -45),
            Font = Enum.Font.Gotham,
            Text = text,
            TextColor3 = Color3.fromRGB(180, 180, 180),
            TextSize = 12,
            TextXAlignment = Enum.TextXAlignment.Left,
            TextYAlignment = Enum.TextYAlignment.Top,
            TextWrapped = true
        })
        
        TweenService:Create(NotifFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quint), {
            Position = UDim2.new(0, 0, 0, 0)
        }):Play()
        
        task.delay(duration, function()
            TweenService:Create(NotifFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quint), {
                Position = UDim2.new(1, 50, 0, 0)
            }):Play()
            
            task.wait(0.3)
            NotifFrame:Destroy()
        end)
    end
    
    function Window:ToggleVisibility()
        Window.Hidden = not Window.Hidden
        MainFrame.Visible = not Window.Hidden
    end
    
    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.L or input.KeyCode == Enum.KeyCode.Insert then
            Window:ToggleVisibility()
        elseif input.KeyCode == Enum.KeyCode.K then
            if not Window.Hidden then
                Window:ToggleMinimize()
            end
        end
    end)
    
    function Window:ToggleMinimize()
        Window.Minimized = not Window.Minimized
        
        if Window.Minimized then
            TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quint), {
                Size = UDim2.new(0, 850, 0, 50)
            }):Play()
            
            MinimizeButton.Text = "+"
        else
            TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quint), {
                Size = UDim2.new(0, 850, 0, 550)
            }):Play()
            
            MinimizeButton.Text = "-"
        end
        
        Sidebar.Visible = not Window.Minimized
        ContentArea.Visible = not Window.Minimized
        PlayerInfoFrame.Visible = not Window.Minimized
    end
    
    local dragging, dragInput, dragStart, startPos
    
    TopBar.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = MainFrame.Position
        end
    end)
    
    TopBar.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
    
    UserInputService.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            if dragging then
                local delta = input.Position - dragStart
                MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
            end
        end
    end)
    
    Window.Tabs = {}
    
    function Window:AddTab(tabName)
        local Tab = {}
        local icon = TabIcons[tabName] or "rbxassetid://10723434711"
        
        local TabButton = create("TextButton", {
            Name = tabName,
            Parent = SidebarContainer,
            BackgroundColor3 = Color3.fromRGB(25, 25, 35),
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 40),
            Font = Enum.Font.GothamSemibold,
            Text = "",
            TextColor3 = Color3.fromRGB(160, 160, 160),
            TextSize = 13,
            TextXAlignment = Enum.TextXAlignment.Left,
            AutoButtonColor = false,
            LayoutOrder = #Window.Tabs
        })
        
        create("UICorner", {
            CornerRadius = UDim.new(0, 8),
            Parent = TabButton
        })
        
        local TabIcon = create("ImageLabel", {
            Parent = TabButton,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 15, 0.5, -8),
            Size = UDim2.new(0, 16, 0, 16),
            Image = icon,
            ImageColor3 = Color3.fromRGB(160, 160, 160)
        })
        
        local TabLabel = create("TextLabel", {
            Parent = TabButton,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 40, 0, 0),
            Size = UDim2.new(1, -40, 1, 0),
            Font = Enum.Font.GothamSemibold,
            Text = tabName,
            TextColor3 = Color3.fromRGB(160, 160, 160),
            TextSize = 13,
            TextXAlignment = Enum.TextXAlignment.Left
        })
        
        local TabIndicator = create("Frame", {
            Parent = TabButton,
            BackgroundColor3 = Color3.fromRGB(139, 92, 246),
            BorderSizePixel = 0,
            Position = UDim2.new(0, 0, 0.5, -12),
            Size = UDim2.new(0, 0, 0, 24),
            ZIndex = 2
        })
        
        create("UICorner", {
            CornerRadius = UDim.new(0, 2),
            Parent = TabIndicator
        })
        
        local TabContent = create("ScrollingFrame", {
            Name = tabName .. "Content",
            Parent = ContentArea,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, -10, 1, -10),
            Position = UDim2.new(0, 5, 0, 5),
            ScrollBarThickness = 6,
            ScrollBarImageColor3 = Color3.fromRGB(139, 92, 246),
            ScrollBarImageTransparency = 0.3,
            CanvasSize = UDim2.new(0, 0, 0, 0),
            Visible = false,
            AutomaticCanvasSize = Enum.AutomaticSize.Y
        })
        
        local LeftColumn = create("Frame", {
            Name = "LeftColumn",
            Parent = TabContent,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 15, 0, 15),
            Size = UDim2.new(0, 290, 1, -30),
            AutomaticSize = Enum.AutomaticSize.Y
        })
        
        local LeftLayout = create("UIListLayout", {
            Parent = LeftColumn,
            SortOrder = Enum.SortOrder.LayoutOrder,
            Padding = UDim.new(0, 12)
        })
        
        local RightColumn = create("Frame", {
            Name = "RightColumn",
            Parent = TabContent,
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 315, 0, 15),
            Size = UDim2.new(0, 290, 1, -30),
            AutomaticSize = Enum.AutomaticSize.Y
        })
        
        local RightLayout = create("UIListLayout", {
            Parent = RightColumn,
            SortOrder = Enum.SortOrder.LayoutOrder,
            Padding = UDim.new(0, 12)
        })
        
        local function UpdateCanvasSize()
            task.wait(0.1)
            local leftHeight = LeftLayout.AbsoluteContentSize.Y
            local rightHeight = RightLayout.AbsoluteContentSize.Y
            local maxHeight = math.max(leftHeight, rightHeight) + 30
            TabContent.CanvasSize = UDim2.new(0, 0, 0, maxHeight)
        end
        
        LeftLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(UpdateCanvasSize)
        RightLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(UpdateCanvasSize)
        
        TabButton.MouseEnter:Connect(function()
            if TabContent.Visible == false then
                TweenService:Create(TabButton, TweenInfo.new(0.2), {
                    BackgroundColor3 = Color3.fromRGB(35, 35, 45),
                    TextColor3 = Color3.fromRGB(200, 200, 200)
                }):Play()
                TweenService:Create(TabIcon, TweenInfo.new(0.2), {
                    ImageColor3 = Color3.fromRGB(200, 200, 200)
                }):Play()
            end
        end)
        
        TabButton.MouseLeave:Connect(function()
            if TabContent.Visible == false then
                TweenService:Create(TabButton, TweenInfo.new(0.2), {
                    BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                    TextColor3 = Color3.fromRGB(160, 160, 160)
                }):Play()
                TweenService:Create(TabIcon, TweenInfo.new(0.2), {
                    ImageColor3 = Color3.fromRGB(160, 160, 160)
                }):Play()
            end
        end)
        
        TabButton.MouseButton1Click:Connect(function()
            for _, content in pairs(ContentArea:GetChildren()) do
                if content:IsA("ScrollingFrame") then
                    content.Visible = false
                end
            end
            
            for _, btn in pairs(SidebarContainer:GetChildren()) do
                if btn:IsA("TextButton") then
                    TweenService:Create(btn, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                        TextColor3 = Color3.fromRGB(160, 160, 160)
                    }):Play()
                    
                    local btnIcon = btn:FindFirstChild("ImageLabel")
                    if btnIcon then
                        TweenService:Create(btnIcon, TweenInfo.new(0.2), {
                            ImageColor3 = Color3.fromRGB(160, 160, 160)
                        }):Play()
                    end
                    
                    local indicator = btn:FindFirstChild("Frame")
                    if indicator then
                        TweenService:Create(indicator, TweenInfo.new(0.2), {
                            Size = UDim2.new(0, 0, 0, 24)
                        }):Play()
                    end
                end
            end
            
            TabContent.Visible = true
            UpdateCanvasSize()
            
            TweenService:Create(TabButton, TweenInfo.new(0.2), {
                BackgroundColor3 = Color3.fromRGB(139, 92, 246),
                TextColor3 = Color3.fromRGB(255, 255, 255)
            }):Play()
            
            TweenService:Create(TabIcon, TweenInfo.new(0.2), {
                ImageColor3 = Color3.fromRGB(255, 255, 255)
            }):Play()
            
            TweenService:Create(TabIndicator, TweenInfo.new(0.3, Enum.EasingStyle.Quint), {
                Size = UDim2.new(0, 3, 0, 24)
            }):Play()
        end)
        
        if #Window.Tabs == 0 then
            TabContent.Visible = true
            TabButton.BackgroundColor3 = Color3.fromRGB(139, 92, 246)
            TabButton.TextColor3 = Color3.fromRGB(255, 255, 255)
            TabIcon.ImageColor3 = Color3.fromRGB(255, 255, 255)
            TabIndicator.Size = UDim2.new(0, 3, 0, 24)
            UpdateCanvasSize()
        end
        
        function Tab:AddLeftGroupbox(groupName)
            local gb = Tab:CreateGroupbox(groupName, LeftColumn)
            UpdateCanvasSize()
            return gb
        end
        
        function Tab:AddRightGroupbox(groupName)
            local gb = Tab:CreateGroupbox(groupName, RightColumn)
            UpdateCanvasSize()
            return gb
        end
        
        function Tab:CreateGroupbox(groupName, parent)
            local Groupbox = {}
            
            local GroupFrame = create("Frame", {
                Name = groupName,
                Parent = parent,
                BackgroundColor3 = Color3.fromRGB(20, 20, 28),
                BorderSizePixel = 0,
                Size = UDim2.new(1, 0, 0, 50),
                AutomaticSize = Enum.AutomaticSize.Y
            })
            
            create("UICorner", {
                CornerRadius = UDim.new(0, 8),
                Parent = GroupFrame
            })
            
            local GroupTitle = create("TextLabel", {
                Name = "GroupTitle",
                Parent = GroupFrame,
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 12, 0, 8),
                Size = UDim2.new(1, -24, 0, 22),
                Font = Enum.Font.GothamBold,
                Text = groupName,
                TextColor3 = Color3.fromRGB(255, 255, 255),
                TextSize = 14,
                TextXAlignment = Enum.TextXAlignment.Left
            })
            
            local GroupContent = create("Frame", {
                Name = "GroupContent",
                Parent = GroupFrame,
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 0, 0, 35),
                Size = UDim2.new(1, 0, 1, -35),
                AutomaticSize = Enum.AutomaticSize.Y
            })
            
            local GroupList = create("UIListLayout", {
                Parent = GroupContent,
                SortOrder = Enum.SortOrder.LayoutOrder,
                Padding = UDim.new(0, 8)
            })
            
            create("UIPadding", {
                Parent = GroupContent,
                PaddingLeft = UDim.new(0, 12),
                PaddingRight = UDim.new(0, 12),
                PaddingBottom = UDim.new(0, 12),
                PaddingTop = UDim.new(0, 5)
            })
            
            GroupList:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
                UpdateCanvasSize()
            end)
            
            function Groupbox:AddToggle(id, options)
                options = options or {}
                local Toggle = {Value = options.Default or false}
                
                local ToggleFrame = create("Frame", {
                    Parent = GroupContent,
                    BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 35)
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = ToggleFrame
                })
                
                local ToggleLabel = create("TextLabel", {
                    Parent = ToggleFrame,
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 12, 0, 0),
                    Size = UDim2.new(1, -60, 1, 0),
                    Font = Enum.Font.Gotham,
                    Text = options.Text or id,
                    TextColor3 = Color3.fromRGB(200, 200, 200),
                    TextSize = 13,
                    TextXAlignment = Enum.TextXAlignment.Left
                })
                
                local ToggleButton = create("TextButton", {
                    Parent = ToggleFrame,
                    BackgroundColor3 = Toggle.Value and Color3.fromRGB(139, 92, 246) or Color3.fromRGB(35, 35, 45),
                    BorderSizePixel = 0,
                    Position = UDim2.new(1, -45, 0.5, -11),
                    Size = UDim2.new(0, 40, 0, 22),
                    Text = "",
                    AutoButtonColor = false
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(1, 0),
                    Parent = ToggleButton
                })
                
                local ToggleCircle = create("Frame", {
                    Parent = ToggleButton,
                    BackgroundColor3 = Color3.fromRGB(255, 255, 255),
                    BorderSizePixel = 0,
                    Position = Toggle.Value and UDim2.new(1, -20, 0.5, -10) or UDim2.new(0, 2, 0.5, -10),
                    Size = UDim2.new(0, 20, 0, 20)
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(1, 0),
                    Parent = ToggleCircle
                })
                
                function Toggle:SetValue(value)
                    Toggle.Value = value
                    
                    TweenService:Create(ToggleButton, TweenInfo.new(0.25, Enum.EasingStyle.Quint), {
                        BackgroundColor3 = value and Color3.fromRGB(139, 92, 246) or Color3.fromRGB(35, 35, 45)
                    }):Play()
                    
                    TweenService:Create(ToggleCircle, TweenInfo.new(0.25, Enum.EasingStyle.Quint), {
                        Position = value and UDim2.new(1, -20, 0.5, -10) or UDim2.new(0, 2, 0.5, -10)
                    }):Play()
                    
                    if options.Callback then
                        pcall(function()
                            options.Callback(value)
                        end)
                    end
                end
                
                ToggleButton.MouseButton1Click:Connect(function()
                    Toggle:SetValue(not Toggle.Value)
                end)
                
                ToggleFrame.MouseEnter:Connect(function()
                    TweenService:Create(ToggleFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                    }):Play()
                end)
                
                ToggleFrame.MouseLeave:Connect(function()
                    TweenService:Create(ToggleFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(25, 25, 35)
                    }):Play()
                end)
                
                UpdateCanvasSize()
                return Toggle
            end
            
            function Groupbox:AddButton(options)
                if type(options) == "string" then
                    options = {Text = options}
                end
                
                local ButtonFrame = create("TextButton", {
                    Parent = GroupContent,
                    BackgroundColor3 = Color3.fromRGB(30, 30, 40),
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 35),
                    Font = Enum.Font.GothamSemibold,
                    Text = options.Text or "Button",
                    TextColor3 = Color3.fromRGB(200, 200, 200),
                    TextSize = 13,
                    AutoButtonColor = false
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = ButtonFrame
                })
                
                ButtonFrame.MouseEnter:Connect(function()
                    TweenService:Create(ButtonFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(139, 92, 246)
                    }):Play()
                end)
                
                ButtonFrame.MouseLeave:Connect(function()
                    TweenService:Create(ButtonFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                    }):Play()
                end)
                
                ButtonFrame.MouseButton1Click:Connect(function()
                    if options.Func then
                        pcall(function()
                            options.Func()
                        end)
                    end
                end)
                
                UpdateCanvasSize()
                return ButtonFrame
            end
            
            function Groupbox:AddSlider(id, options)
                options = options or {}
                local Slider = {Value = options.Default or options.Min or 0}
                local min = options.Min or 0
                local max = options.Max or 100
                local suffix = options.Suffix or ""
                
                local SliderFrame = create("Frame", {
                    Parent = GroupContent,
                    BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 50)
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = SliderFrame
                })
                
                local SliderLabel = create("TextLabel", {
                    Parent = SliderFrame,
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 12, 0, 6),
                    Size = UDim2.new(0.65, 0, 0, 18),
                    Font = Enum.Font.Gotham,
                    Text = options.Text or id,
                    TextColor3 = Color3.fromRGB(200, 200, 200),
                    TextSize = 13,
                    TextXAlignment = Enum.TextXAlignment.Left
                })
                
                local SliderValue = create("TextLabel", {
                    Parent = SliderFrame,
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0.65, 0, 0, 6),
                    Size = UDim2.new(0.35, -12, 0, 18),
                    Font = Enum.Font.GothamBold,
                    Text = tostring(Slider.Value) .. suffix,
                    TextColor3 = Color3.fromRGB(139, 92, 246),
                    TextSize = 13,
                    TextXAlignment = Enum.TextXAlignment.Right
                })
                
                local SliderBackground = create("Frame", {
                    Parent = SliderFrame,
                    BackgroundColor3 = Color3.fromRGB(30, 30, 40),
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 12, 1, -18),
                    Size = UDim2.new(1, -24, 0, 6)
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(1, 0),
                    Parent = SliderBackground
                })
                
                local SliderFill = create("Frame", {
                    Parent = SliderBackground,
                    BackgroundColor3 = Color3.fromRGB(139, 92, 246),
                    BorderSizePixel = 0,
                    Size = UDim2.new((Slider.Value - min) / (max - min), 0, 1, 0)
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(1, 0),
                    Parent = SliderFill
                })
                
                local dragging = false
                
                function Slider:SetValue(value)
                    value = math.clamp(value, min, max)
                    if options.Rounding then
                        value = math.floor(value / options.Rounding + 0.5) * options.Rounding
                    end
                    Slider.Value = value
                    
                    local pos = (value - min) / (max - min)
                    TweenService:Create(SliderFill, TweenInfo.new(0.1), {
                        Size = UDim2.new(pos, 0, 1, 0)
                    }):Play()
                    SliderValue.Text = tostring(value) .. suffix
                    
                    if options.Callback then
                        pcall(function()
                            options.Callback(value)
                        end)
                    end
                end
                
                SliderBackground.InputBegan:Connect(function(input)
                    if input.UserInputType == Enum.UserInputType.MouseButton1 then
                        dragging = true
                        local pos = math.clamp((input.Position.X - SliderBackground.AbsolutePosition.X) / SliderBackground.AbsoluteSize.X, 0, 1)
                        local value = min + (max - min) * pos
                        if options.Rounding then
                            value = math.floor(value / options.Rounding + 0.5) * options.Rounding
                        else
                            value = math.floor(value)
                        end
                        Slider:SetValue(value)
                    end
                end)
                
                SliderBackground.InputEnded:Connect(function(input)
                    if input.UserInputType == Enum.UserInputType.MouseButton1 then
                        dragging = false
                    end
                end)
                
                UserInputService.InputEnded:Connect(function(input)
                    if input.UserInputType == Enum.UserInputType.MouseButton1 then
                        dragging = false
                    end
                end)
                
                UserInputService.InputChanged:Connect(function(input)
                    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
                        local pos = math.clamp((input.Position.X - SliderBackground.AbsolutePosition.X) / SliderBackground.AbsoluteSize.X, 0, 1)
                        local value = min + (max - min) * pos
                        if options.Rounding then
                            value = math.floor(value / options.Rounding + 0.5) * options.Rounding
                        else
                            value = math.floor(value)
                        end
                        Slider:SetValue(value)
                    end
                end)
                
                SliderFrame.MouseEnter:Connect(function()
                    TweenService:Create(SliderFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                    }):Play()
                end)
                
                SliderFrame.MouseLeave:Connect(function()
                    TweenService:Create(SliderFrame, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(25, 25, 35)
                    }):Play()
                end)
                
                UpdateCanvasSize()
                return Slider
            end
            
            function Groupbox:AddLabel(text, options)
                options = options or {}
                local Label = {}
                
                local LabelFrame = create("TextLabel", {
                    Parent = GroupContent,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 20),
                    Font = Enum.Font.Gotham,
                    Text = text,
                    TextColor3 = Color3.fromRGB(150, 150, 150),
                    TextSize = 12,
                    TextXAlignment = Enum.TextXAlignment.Left,
                    TextWrapped = true
                })
                
                function Label:SetText(newText)
                    LabelFrame.Text = newText
                end
                
                UpdateCanvasSize()
                return Label
            end
            
            function Groupbox:AddDropdown(id, options)
                options = options or {}
                local Dropdown = {
                    Value = options.Default or "",
                    Values = options.Values or {},
                    Multi = options.Multi or false
                }
                
                local DropdownFrame = create("Frame", {
                    Parent = GroupContent,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 58)
                })
                
                local DropdownLabel = create("TextLabel", {
                    Parent = DropdownFrame,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 20),
                    Font = Enum.Font.Gotham,
                    Text = options.Text or id,
                    TextColor3 = Color3.fromRGB(200, 200, 200),
                    TextSize = 13,
                    TextXAlignment = Enum.TextXAlignment.Left
                })
                
                local DropdownButton = create("TextButton", {
                    Parent = DropdownFrame,
                    BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 0, 0, 24),
                    Size = UDim2.new(1, 0, 0, 32),
                    Font = Enum.Font.Gotham,
                    Text = Dropdown.Value or "Select...",
                    TextColor3 = Color3.fromRGB(180, 180, 180),
                    TextSize = 12,
                    TextXAlignment = Enum.TextXAlignment.Left,
                    AutoButtonColor = false
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = DropdownButton
                })
                
                create("UIPadding", {
                    Parent = DropdownButton,
                    PaddingLeft = UDim.new(0, 12)
                })
                
                local DropdownArrow = create("TextLabel", {
                    Parent = DropdownButton,
                    BackgroundTransparency = 1,
                    Position = UDim2.new(1, -30, 0, 0),
                    Size = UDim2.new(0, 30, 1, 0),
                    Font = Enum.Font.GothamBold,
                    Text = "▼",
                    TextColor3 = Color3.fromRGB(139, 92, 246),
                    TextSize = 10
                })
                
                local DropdownList = create("Frame", {
                    Parent = DropdownFrame,
                    BackgroundColor3 = Color3.fromRGB(20, 20, 28),
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 0, 0, 60),
                    Size = UDim2.new(1, 0, 0, 0),
                    Visible = false,
                    ClipsDescendants = true,
                    ZIndex = 10
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = DropdownList
                })
                
                local DropdownScroll = create("ScrollingFrame", {
                    Parent = DropdownList,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 1, 0),
                    ScrollBarThickness = 4,
                    ScrollBarImageColor3 = Color3.fromRGB(139, 92, 246),
                    ScrollBarImageTransparency = 0.3,
                    CanvasSize = UDim2.new(0, 0, 0, 0),
                    AutomaticCanvasSize = Enum.AutomaticSize.Y
                })
                
                local ListLayout = create("UIListLayout", {
                    Parent = DropdownScroll,
                    SortOrder = Enum.SortOrder.LayoutOrder,
                    Padding = UDim.new(0, 3)
                })
                
                create("UIPadding", {
                    Parent = DropdownScroll,
                    PaddingTop = UDim.new(0, 6),
                    PaddingBottom = UDim.new(0, 6),
                    PaddingLeft = UDim.new(0, 6),
                    PaddingRight = UDim.new(0, 6)
                })
                
                local function UpdateDropdown()
                    for _, child in pairs(DropdownScroll:GetChildren()) do
                        if child:IsA("TextButton") then
                            child:Destroy()
                        end
                    end
                    
                    for _, value in pairs(Dropdown.Values) do
                        local Option = create("TextButton", {
                            Parent = DropdownScroll,
                            BackgroundColor3 = Color3.fromRGB(30, 30, 40),
                            BorderSizePixel = 0,
                            Size = UDim2.new(1, -12, 0, 30),
                            Font = Enum.Font.Gotham,
                            Text = value,
                            TextColor3 = Color3.fromRGB(180, 180, 180),
                            TextSize = 12,
                            AutoButtonColor = false
                        })
                        
                        create("UICorner", {
                            CornerRadius = UDim.new(0, 5),
                            Parent = Option
                        })
                        
                        Option.MouseEnter:Connect(function()
                            TweenService:Create(Option, TweenInfo.new(0.2), {
                                BackgroundColor3 = Color3.fromRGB(139, 92, 246)
                            }):Play()
                        end)
                        
                        Option.MouseLeave:Connect(function()
                            TweenService:Create(Option, TweenInfo.new(0.2), {
                                BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                            }):Play()
                        end)
                        
                        Option.MouseButton1Click:Connect(function()
                            Dropdown.Value = value
                            DropdownButton.Text = value
                            DropdownList.Visible = false
                            DropdownFrame.Size = UDim2.new(1, 0, 0, 58)
                            
                            TweenService:Create(DropdownArrow, TweenInfo.new(0.2), {
                                Rotation = 0
                            }):Play()
                            
                            UpdateCanvasSize()
                            
                            if options.Callback then
                                pcall(function()
                                    options.Callback(value)
                                end)
                            end
                        end)
                    end
                end
                
                DropdownButton.MouseButton1Click:Connect(function()
                    DropdownList.Visible = not DropdownList.Visible
                    if DropdownList.Visible then
                        UpdateDropdown()
                        task.wait(0.05)
                        local contentSize = ListLayout.AbsoluteContentSize.Y + 12
                        local maxHeight = math.min(contentSize, 160)
                        DropdownList.Size = UDim2.new(1, 0, 0, maxHeight)
                        DropdownFrame.Size = UDim2.new(1, 0, 0, 60 + maxHeight + 5)
                        
                        TweenService:Create(DropdownArrow, TweenInfo.new(0.2), {
                            Rotation = 180
                        }):Play()
                        
                        UpdateCanvasSize()
                    else
                        DropdownFrame.Size = UDim2.new(1, 0, 0, 58)
                        
                        TweenService:Create(DropdownArrow, TweenInfo.new(0.2), {
                            Rotation = 0
                        }):Play()
                        
                        UpdateCanvasSize()
                    end
                end)
                
                DropdownButton.MouseEnter:Connect(function()
                    TweenService:Create(DropdownButton, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                    }):Play()
                end)
                
                DropdownButton.MouseLeave:Connect(function()
                    TweenService:Create(DropdownButton, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(25, 25, 35)
                    }):Play()
                end)
                
                function Dropdown:SetValues(values)
                    Dropdown.Values = values
                    if DropdownList.Visible then
                        UpdateDropdown()
                    end
                end
                
                function Dropdown:SetValue(value)
                    Dropdown.Value = value
                    DropdownButton.Text = value
                    if options.Callback then
                        pcall(function()
                            options.Callback(value)
                        end)
                    end
                end
                
                UpdateCanvasSize()
                return Dropdown
            end
            
            function Groupbox:AddInput(id, options)
                options = options or {}
                local Input = {Value = options.Default or ""}
                
                local InputFrame = create("Frame", {
                    Parent = GroupContent,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 58)
                })
                
                local InputLabel = create("TextLabel", {
                    Parent = InputFrame,
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 20),
                    Font = Enum.Font.Gotham,
                    Text = options.Text or id,
                    TextColor3 = Color3.fromRGB(200, 200, 200),
                    TextSize = 13,
                    TextXAlignment = Enum.TextXAlignment.Left
                })
                
                local InputBox = create("TextBox", {
                    Parent = InputFrame,
                    BackgroundColor3 = Color3.fromRGB(25, 25, 35),
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 0, 0, 24),
                    Size = UDim2.new(1, 0, 0, 32),
                    Font = Enum.Font.Gotham,
                    PlaceholderText = options.Placeholder or "Type here...",
                    Text = Input.Value,
                    TextColor3 = Color3.fromRGB(180, 180, 180),
                    TextSize = 12,
                    TextXAlignment = Enum.TextXAlignment.Left,
                    ClearTextOnFocus = false
                })
                
                create("UICorner", {
                    CornerRadius = UDim.new(0, 6),
                    Parent = InputBox
                })
                
                create("UIPadding", {
                    Parent = InputBox,
                    PaddingLeft = UDim.new(0, 12)
                })
                
                InputBox.FocusLost:Connect(function(enter)
                    if enter and options.Callback then
                        Input.Value = InputBox.Text
                        pcall(function()
                            options.Callback(InputBox.Text)
                        end)
                    end
                end)
                
                InputBox.Focused:Connect(function()
                    TweenService:Create(InputBox, TweenInfo.new(0.2), {
                        BackgroundColor3 = Color3.fromRGB(30, 30, 40)
                    }):Play()
                end)
                
                InputBox:GetPropertyChangedSignal("Text"):Connect(function()
                    if not InputBox:IsFocused() then return end
                    if options.Numeric then
                        InputBox.Text = InputBox.Text:gsub("%D", "")
                    end
                end)
                
                function Input:SetValue(value)
                    Input.Value = value
                    InputBox.Text = value
                    if options.Callback then
                        pcall(function()
                            options.Callback(value)
                        end)
                    end
                end
                
                UpdateCanvasSize()
                return Input
            end
            
            function Groupbox:AddDivider()
                local Divider = create("Frame", {
                    Parent = GroupContent,
                    BackgroundColor3 = Color3.fromRGB(139, 92, 246),
                    BackgroundTransparency = 0.6,
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 1)
                })
                
                UpdateCanvasSize()
                return Divider
            end
            
            return Groupbox
        end
        
        table.insert(Window.Tabs, Tab)
        return Tab
    end
    
    return Window
end

return Library
