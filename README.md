[![Null Ui](https://uibin.orqan.xyz/api/card?id=3874a0c2-b2b6-43be-9107-2f05cd3b1547&theme=black)](https://uibin.orqan.xyz/library/3874a0c2-b2b6-43be-9107-2f05cd3b1547)
# Null UI
### Made by Yomka

A sleek, modern glassmorphism UI library for Roblox. Designed for performance, ease of use, and full customization.

## Key Features

* **Glassmorphism Design:** Translucent surfaces with blur-like effects.
* **Theme System:** 20+ built-in presets (Arctic, Sunset, Midnight, Ocean, RoseGold, Terminal, etc.) and custom theme registration.
* **Lucide Icons:** Integrated support for `Icon = "house"` - just type the icon name.
* **Custom UI Backgrounds:** Set/clear a background image via URL, Roblox ID, or `rbxassetid://...`.
* **Config System:** Built-in Save/Load with JSON, plus autoload support.
* **Adaptive Layouts:** Move tabs to Top, Bottom, Left, or Right at runtime.
* **Mobile Ready:** Responsive scaling, draggable show/hide button, touch-friendly controls.
* **Non-blocking:** the window shows instantly, assets stream in behind it.

---

## Quick start

```luau
local NullLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/ginzuss/nullui/refs/heads/main/NullUI.lua"))()

local Window = NullLib:CreateWindow({
    Title = "Null UI",
    Subtitle = "yomkamadeit",
    BadgeText = "v5.7",
    ToggleKey = Enum.KeyCode.B,
    ConfigFolder = "NullUI"
})

local Tab = Window:CreateTab({Name = "Main", Icon = "house", Description = "Some main things"})
local Section = Tab:CreateSection({Title = "Mazafaka", Icon = "sparkles", Side = "Left"})

Section:AddToggle({
    Text = "Enable ESP",
    Description = "example toggle for visual color",
    Flag = "EnableESP",
    Default = true,
    Callback = function(state)
        print("ESP:", state)
    end
})

Window:Notify({Title = "Hello", Content = "You unfolded me!", Icon = "bell", Color = NullLib.Theme.Good})
```

---

## Full example (all features)

```luau
local NullLib = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/ginzuss/nullui/refs/heads/main/NullUI.lua"))()

local Window = NullLib:CreateWindow({
    Name = "NullUI",
    Title = "Null UI",
    Subtitle = "yomkamadeit",
    BadgeText = "v5.7",
    Icon = "https://i.postimg.cc/QxPqrLGq/image-Photoroom.png", -- u can change it
    WatermarkIcon = "https://i.postimg.cc/QxPqrLGq/image-Photoroom.png", -- u can change it too lol
    ShowHideButtonIcon = "https://i.postimg.cc/8CWY0LCY/raw-68251a78f0683b2ed02ae20e25f976ea.png", -- change by string if u want
    ShowHideButtonSize = 38, -- optional
    -- Scale = 0.95, -- optional: global UI scale (library default: 1 on PC, 0.94 on phone)
    -- Loading = true, -- optional: show the animated loading screen (default true)
    -- LoadingDelay = 0.55, -- optional: how long the loader stays before the reveal
    -- IntroDuration = 0.75, -- optional: length of the reveal tween (no overlay, just the window animating in)
    -- AutoloadDelay = 0.7, -- optional: wait before the autoloaded config is applied (needs to be after themes are registered)
    ToggleKey = Enum.KeyCode.B,
    ConfigFolder = "NullUI",
    ConfigName = "ExampleConfig",
    TabPosition = "Bottom",
    ShowTabTitle = true,
    WelcomeNotification = true,
    UIWatermark = true
})


local RS = game:GetService("RunService")
local Player = game:GetService("Players").LocalPlayer

local elapsed = 0
local frames = 0
local updateInterval = 0.5

RS.RenderStepped:Connect(function(deltaTime)
    elapsed += deltaTime
    frames += 1

    if elapsed >= updateInterval then
        local fps = math.floor(frames / elapsed)

        -- You can change the text, or you can use text + a new image: Window:SetWatermark("text", "link")
        Window:SetWatermark(string.format(
            "YomkaWasHere | User: %s | FPS: %d",
            Player.Name,
            fps
        ))

        elapsed = 0
        frames = 0
    end
end)

local MainTab = Window:CreateTab({
    Name = "Main",
    Icon = "house",
    Description = "Some main things"
})

local MediaTab = Window:CreateTab({
    Name = "Media",
    Icon = "image",
    Description = "Some media things"
})

local ConfigTab = Window:CreateTab({
    Name = "Configs",
    Icon = "settings-2",
    Description = "Some config things"
})

local LeftSection = MainTab:CreateSection({
    Title = "Mazafaka",
    Description = "blah blah blah",
    Icon = "sparkles",
    Side = "Left" -- choose side here Left or Right
})

LeftSection:AddParagraph("Test text yomkayomkayomkayomka")

LeftSection:AddButton({
    Text = "Show Notification",
    Icon = "circle-check",
    Callback = function()
        Window:Notify({
            Title = "Success!",
            Content = "Yay!",
            Icon = "check",
            Duration = 4,
            Color = NullLib.Theme.Good
        })
    end
})

local WalkSpeed = LeftSection:AddSlider({
    Text = "WalkSpeed",
    Flag = "WalkSpeed",
    Min = 16,
    Max = 100,
    Default = 32,
    Callback = function(value)
        print("WalkSpeed:", value)
    end
})

local AimSmoothness = LeftSection:AddSlider({
    Text = "Aim Smoothness",
    Flag = "AimSmoothness",
    Decimals = true,
    Min = 0.10,
    Max = 1.00,
    Default = 0.35,
    Callback = function(value)
        print("Aim Smoothness:", value)
    end
})

local RightSection = MainTab:CreateSection({
    Title = "ajghwshbhbvergvefe",
    Description = "blah blah blah",
    Side = "Right"
})

local AutoFarm = RightSection:AddToggle({
    Text = "Auto Farm",
    Description = "just a toggle lol",
    Flag = "AutoFarm",
    Default = false,
    Callback = function(state)
        print("Auto Farm:", state)
    end
})

local EspEnabled = RightSection:AddToggle({
    Text = "Enable ESP",
    Description = "example toggle for visual color",
    Flag = "EnableESP",
    Default = true,
    Callback = function(state)
        print("ESP Enabled:", state)
    end
})

local EspColor = RightSection:AddColorPicker({
    Text = "ESP Color",
    Flag = "ESPColor",
    DefaultColor = Color3.fromRGB(255, 90, 90),
    DefaultAlpha = 0.85,
    Callback = function(color, alpha)
        print("ESP Color:", color, "Alpha:", alpha)
    end
})

local Mode = RightSection:AddDropdown({
    Text = "Target Mode",
    Flag = "TargetMode",
    Values = {"Closest", "Random", "Low HP", "Behind Wall"},
    Default = "Closest",
    Callback = function(value)
        print("Mode:", value)
    end
})

local MultiTargetModes = RightSection:AddDropdown({
    Text = "Target Modes",
    Flag = "TargetModes",
    Values = {"Closest", "Random", "Low HP", "Behind Wall", "Visible", "Distance"},
    Default = {"Closest", "Visible"},
    MultiSelect = true,
    Callback = function(values, summary)
        print("Target Modes:", summary, table.concat(values, ", "))
    end
})

local Nickname = RightSection:AddTextbox({
    Placeholder = "Target Nickname...",
    Flag = "TargetNick",
    Default = "Yomka",
    Callback = function(text)
        print("Textbox:", text)
    end
})

local MediaSection = MediaTab:CreateSection({
    Title = "Images & Visuals",
    Description = "sup broski",
    Side = "Left"
})

MediaSection:AddImage({
    Image = "https://i.pinimg.com/736x/53/22/cc/5322cc580a42baaa36a7d76d721339c7.jpg",
    Height = 200,
    ScaleType = Enum.ScaleType.Crop, 
    Caption = "yomkawashere"
})

local ConfigSection = ConfigTab:CreateSection({
    Title = "Configs Manager",
    Description = "Configs Stuff Here",
    Side = "Left"
})

local ThemeSection = ConfigTab:CreateSection({
    Title = "Themes",
    Description = "Pick a style preset",
    Side = "Right"
})

local BackgroundSection = ConfigTab:CreateSection({
    Title = "UI Background",
    Description = "Set custom wallpaper for the UI",
    Side = "Right"
})

local RawThemeNames = NullLib:ListThemes()
local ThemeDisplayToRaw = {}
local ThemeNames = {}
for _, rawName in ipairs(RawThemeNames) do
    local displayName = rawName == "Null" and "Null (Default)" or rawName
    ThemeDisplayToRaw[displayName] = rawName
    table.insert(ThemeNames, displayName)
end

local ThemeDropdown = ThemeSection:AddDropdown({
    Text = "Theme",
    Flag = "ThemePreset",
    Values = ThemeNames,
    Default = "Null (Default)",
    Callback = function(value)
        print("Theme selected:", tostring(value))
    end
})

ThemeSection:AddButton({
    Text = "Apply Theme",
    Icon = "palette",
    Callback = function()
        local selectedDisplay = tostring(ThemeDropdown:Get() or "Null (Default)")
        local rawName = ThemeDisplayToRaw[selectedDisplay] or "Null"
        Window:SetThemeByName(rawName)
    end
})

local BackgroundInput = BackgroundSection:AddTextbox({
    Placeholder = "URL / Roblox ID / rbxassetid://...",
    Flag = "UIBackgroundSource",
    Default = "",
})

local function trimText(value)
    return tostring(value or ""):gsub("^%s+", ""):gsub("%s+$", "")
end

local function resolveBackgroundSource()
    local typedSource = trimText(BackgroundInput:Get())
    if typedSource ~= "" then
        return typedSource
    end

    local current = Window:GetBackground()
    return trimText(current and current.Source or "")
end

local BackgroundOpacity

local function applyBackgroundLive(source, silent)
    local opacityPercent = math.clamp(tonumber(BackgroundOpacity and BackgroundOpacity:Get()) or 30, 0, 100)
    local targetSource = trimText(source)
    if targetSource == "" then
        targetSource = resolveBackgroundSource()
    end
    local ok = Window:SetBackground(targetSource, {
        Transparency = 1 - (opacityPercent / 100),
        ScaleType = Enum.ScaleType.Crop
    }, silent)
    return ok, targetSource
end

BackgroundOpacity = BackgroundSection:AddSlider({
    Text = "Opacity (%)",
    Flag = "UIBackgroundOpacity",
    Min = 5,
    Max = 100,
    Default = 30,
    Callback = function()
        applyBackgroundLive(resolveBackgroundSource(), true)
    end
})

BackgroundSection:AddButton({
    Text = "Apply Background",
    Icon = "image-plus",
    Callback = function()
        local source = resolveBackgroundSource()
        if source == "" then
            Window:Notify({
                Title = "Background",
                Content = "Type URL/ID in the textbox.",
                Icon = "alert-circle",
                Color = NullLib.Theme.Bad
            })
            return
        end

        local ok = applyBackgroundLive(source, false)
        if not ok then
            Window:Notify({
                Title = "Background",
                Content = "Failed to apply background.",
                Icon = "alert-circle",
                Color = NullLib.Theme.Bad
            })
        end
    end
})

BackgroundSection:AddButton({
    Text = "Clear Background",
    Icon = "image-off",
    Callback = function()
        Window:SetBackground("")
    end
})

local ConfigNameBox = ConfigSection:AddTextbox({
    Placeholder = "Config name...",
    Flag = "ConfigNameInput",
    Default = Window.ConfigName or "ExampleConfig",
    Callback = function(text)
        local name = tostring(text or ""):gsub("^%s+", ""):gsub("%s+$", "")
        if name ~= "" then
            Window.ConfigName = name
        end
    end
})

local function getCurrentConfigName()
    local typed = tostring(ConfigNameBox:Get() or ""):gsub("^%s+", ""):gsub("%s+$", "")
    if typed ~= "" then Window.ConfigName = typed end
    return Window.ConfigName
end

ConfigSection:AddButton({
    Text = "Save Config",
    Icon = "save",
    Callback = function()
        Window:SaveConfig(getCurrentConfigName())
    end
})

ConfigSection:AddButton({
    Text = "Load Config",
    Icon = "download",
    Callback = function()
        Window:LoadConfig(getCurrentConfigName())
    end
})

local function getConfigValues()
    local configs = Window:RefreshConfigs()
    if #configs == 0 then configs = {"None"} end
    return configs
end

local ConfigList = ConfigSection:AddDropdown({
    Text = "Config List",
    Flag = "ConfigList",
    Values = getConfigValues(),
    Default = Window.ConfigName or getConfigValues()[1],
    Callback = function(value)
        if tostring(value) == "None" then return end
        Window.ConfigName = tostring(value)
        ConfigNameBox:Set(Window.ConfigName, true)
    end
})

local function refreshConfigList(keepSelection)
    ConfigList:SetValues(getConfigValues(), keepSelection ~= false)
end

ConfigSection:AddButton({
    Text = "Refresh Configs",
    Icon = "rotate-cw",
    Callback = function()
        refreshConfigList(true)
        Window:Notify({
            Title = "Configs",
            Content = "Updated!",
            Icon = "refresh-cw",
            Color = NullLib.Theme.AccentSoft
        })
    end
})

local refreshAutoloadStatus

ConfigSection:AddButton({
    Text = "Enable Autoload",
    Icon = "power",
    Callback = function()
        Window:SetAutoloadConfig(Window.ConfigName, true)
        if refreshAutoloadStatus then refreshAutoloadStatus() end
    end
})

ConfigSection:AddButton({
    Text = "Delete Selected Config",
    Icon = "trash-2",
    Callback = function()
        local selected = tostring(ConfigList:Get() or Window.ConfigName or "")
        selected = selected:gsub("^%s+", ""):gsub("%s+$", "")
        if selected == "" or selected == "None" then
            Window:Notify({
                Title = "Configs",
                Content = "No config selected.",
                Icon = "alert-circle",
                Color = NullLib.Theme.Bad
            })
            return
        end

        local ok = Window:DeleteConfig(selected)
        if ok then
            refreshConfigList(false)
            local values = getConfigValues()
            local nextName = values[1] and values[1] ~= "None" and values[1] or selected
            Window.ConfigName = nextName
            ConfigNameBox:Set(nextName, true)
            refreshAutoloadStatus()
        end
    end
})

local AutoloadStatusLabel = ConfigSection:AddLabel("")

refreshAutoloadStatus = function()
    local state = Window:GetAutoloadState()
    local configName = state.Config or "none"
    if state.Enabled and state.Config then
        AutoloadStatusLabel.Text = "Will autoload: " .. configName
    else
        AutoloadStatusLabel.Text = "Will autoload: none"
    end
end

ConfigSection:AddButton({
    Text = "Disable Autoload",
    Icon = "power-off",
    Callback = function()
        Window:DisableAutoload()
        refreshAutoloadStatus()
    end
})

ConfigSection:AddKeybind({
    Text = "Toggle UI",
    Flag = "UIToggleKeybind",
    DefaultKey = Window.ToggleKey,
    Mode = "Toggle",
    Callback = function(_, bindKey)
        if bindKey and bindKey ~= Enum.KeyCode.Unknown then
            Window.ToggleKey = bindKey
        end
    end,
    OnKeyChanged = function(bindKey)
        if bindKey and bindKey ~= Enum.KeyCode.Unknown then
            Window.ToggleKey = bindKey
        end
    end
})

local InterfaceSection = ConfigTab:CreateSection({
    Title = "Interface Scale",
    Description = "Resize the whole UI live",
    Icon = "maximize-2",
    Side = "Right"
})

InterfaceSection:AddSlider({
    Text = "UI Scale",
    Flag = "UIScaleValue",
    Decimals = 2,
    Min = 0.70, -- the library clamps the scale to 0.70 .. 1.30
    Max = 1.30,
    Default = Window:GetScale(),
    Callback = function(value)
        Window:SetScale(value) -- Window:GetScale() / Window:ResetScale() also exist
    end
})

InterfaceSection:AddButton({
    Text = "Reset Scale",
    Icon = "rotate-ccw",
    Callback = function()
        Window:ResetScale()
        Window:Notify({
            Title = "Interface",
            Content = string.format("Scale reset to %d%%", math.floor(Window:GetScale() * 100 + 0.5)),
            Icon = "check",
            Color = NullLib.Theme.AccentSoft
        })
    end
})

local NotifySection = ConfigTab:CreateSection({
    Title = "Notifications",
    Description = "buttons and positions",
    Icon = "bell",
    Side = "Left"
})

NotifySection:AddButton({
    Text = "Ask (Yes / No)",
    Icon = "circle-question-mark",
    Callback = function()
        Window:Notify({
            Title = "Delete config?",
            Content = "This cannot be undone after.",
            Icon = "triangle-alert",
            Color = NullLib.Theme.Bad,
            Buttons = {
                -- max two buttons; the first one is the accent coloured primary
                { Text = "Delete", Callback = function() print("config deleted") end },
                { Text = "Cancel", Callback = function() print("cancelled") end }
            }
        })
    end
})


local CollapsibleExample = ConfigTab:CreateSection({
    Title = "Collapsible Section",
    Description = "click the header or the arrow",
    Icon = "chevron-down",
    Side = "Right",
    Collapsible = true, -- sections are NOT collapsible unless you ask for it
    Collapsed = true -- optional: starts folded
})

CollapsibleExample:AddParagraph("Folded by default", "Click the section header, the title or the arrow to fold and unfold it.")

CollapsibleExample:AddButton({
    Text = "Unfolded content",
    Icon = "eye",
    Callback = function()
        Window:Notify({ Title = "Hello", Content = "You unfolded me!", Color = NullLib.Theme.Good })
    end
})

refreshAutoloadStatus()
```

---

## CreateWindow options

| Option | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | `"NullUI"` | Internal name of the ScreenGui. |
| `Title` / `Subtitle` | string | `"Null UI"` / `""` | Header text. |
| `BadgeText` | string | `nil` | Small badge next to the title. |
| `Icon` | string | `nil` | Header icon (lucide name, URL, `rbxassetid://...`). |
| `WatermarkIcon` | string | `nil` | Icon used by the watermark text. |
| `ShowHideButtonIcon` / `ShowHideButtonSize` | string / number | - / 52 | Floating show/hide button (mobile). |
| `ToggleKey` | Enum.KeyCode | `RightShift` | Key that shows/hides the UI. |
| `ConfigFolder` / `ConfigName` | string | `"NullUI"` / `"Default"` | Where configs are stored. |
| `TabPosition` | string | `"Left"` | `"Left"`, `"Right"`, `"Top"`, `"Bottom"`. |
| `ShowTabTitle` | boolean | `true` | Show the tab title in the content header. |
| `WelcomeNotification` | boolean | `true` | Show the "UI launched" notification. |
| `Size` | UDim2 | `840x520` | Window size. |
| `Position` | UDim2 | centered | Window position. |
| `Loading` | boolean | `true` | `false` = no loading pause and no reveal tween. |
| `LoadingDelay` | number | `0.25` | Seconds the window stays hidden before revealing. |
| `IntroDuration` | number | `0.75` | Length of the reveal tween. |
| `AutoloadDelay` | number | `0.7` | Seconds to wait before applying an autoloaded config. |

---

## Loading / reveal

```luau
-- default behaviour
CreateWindow({Loading = true, LoadingDelay = 0.25, IntroDuration = 0.75})

-- no pause at all
CreateWindow({Loading = false})

-- or finish it yourself whenever you are ready
Window:FinishLoading()        -- animated reveal
Window:FinishLoading(true)    -- instant
```

---

## UI scale and resizing

```luau
Window:SetScale(0.8)   -- clamped to 0.70 .. 1.30
Window:GetScale()
Window:ResetScale()
```

The scale is hard-limited to **0.70 - 1.30**, and the window also keeps a minimum *on-screen* size (460x360 desktop / 236x228 phone). A small scale plus the corner grip can therefore never shrink the UI into an unreadable state. The built-in settings menu (sliders icon) has the same slider under **Interface -> UI Scale**.

To resize, drag the small arc that curls around the bottom-right corner of the window - it grows and lights up on hover.

---

## Notifications

```luau
-- position: 9 presets
NullLib:SetNotificationPosition("TopRight")
-- TopLeft / TopCenter / TopRight / MiddleLeft / MiddleCenter / MiddleRight / BottomLeft / BottomCenter / BottomRight
-- or explicit:
NullLib:SetNotificationPosition("Top", "Right")
NullLib:GetNotificationPosition()  --> e.g. "TopRight"
NullLib:GetNotificationAnchor()    --> "Top", "Right"

Window:Notify({
    Title = "Saved",
    Content = "Config written to disk.",
    Icon = "check",                  -- lucide name / URL
    Color = NullLib.Theme.Good,
    Duration = 5,
    Type = "Normal",                 -- "Normal" or "Small"

    -- action buttons (optional, max 2)
    Buttons = {
        {Text = "Delete", Callback = function() end},
        {Text = "Cancel", Callback = function() end}
    }
})
```

Button layout: two buttons split the card width exactly in half, one button spans the full width. The notification position can also be changed from the settings menu (**Notifications -> Position**).

---

## Sections

```luau
local Section = Tab:CreateSection({
    Title = "Combat",
    Description = "optional subtitle",
    Icon = "swords",       -- optional
    Side = "Left",         -- "Left" or "Right" column
    Collapsible = true     -- optional, off by default
})

Section:SetCollapsed(true)
Section:ToggleCollapsed()
Section:IsCollapsed()
Section:SetTitle("New title")
```

`Collapsible = true` turns the section header into a collapse/expand control (chevron in the header). Sections without it behave exactly as before.

---

## Themes

```luau
NullLib:ListThemes()                              -- array of names
NullLib:HasTheme("Yoxi")                          -- true if registered
NullLib:GetTheme("Yoxi")                          -- theme table
NullLib:RegisterTheme("MyTheme", {Accent = ..., Background = ..., Text = ..., ...})
Window:SetThemeByName("MyTheme")
```

Available presets: `Null`, `Arctic`, `Ember`, `Forest`, `Sunset`, `Midnight`, `Mint`, `Snow`, `Blackout`, `Yoxi`, `Yoxi Blue`, `RoseGold`, `Ocean`, `Lavender`, `Cyber`, `Cherry`, `Matcha`, `Coral`, `Sapphire`, `Terminal`.

**Autoload + custom themes:** register your themes before or after `CreateWindow` - both work now. If an autoloaded config mentions a theme that is not registered yet, Null UI queues it and applies it the moment `RegisterTheme` adds it. `AutoloadDelay` (default `0.7` s) keeps autoload from firing while your script is still building the UI.

---

## Window methods

| Method | Description |
| --- | --- |
| `Window:Toggle(bool)` | Show/hide the UI. |
| `Window:FinishLoading(instant?)` | Finish the loading state manually. |
| `Window:SetScale(n)` / `GetScale()` / `ResetScale()` | UI scale (0.70 - 1.30). |
| `Window:CreateTab(options)` / `SelectTab(...)` | Tabs. |
| `Window:SetTabPosition(mode)` | `"Left"`, `"Right"`, `"Top"`, `"Bottom"` at runtime. |
| `Window:SetThemeByName(name)` / `SetTheme(theme)` | Change theme on the fly. |
| `Window:SetBackground(source, options?)` | URL / ID / `rbxassetid://...`; `options.Transparency`, `options.ScaleType`. |
| `Window:GetBackground()` | `{Source, Transparency, ScaleType}`. |
| `Window:Notify(options)` | Push a notification. |
| `Window:SetWatermark(text, image?)` / `SetWatermarkVisible(bool)` | Watermark. |
| `Window:SetTitle(text)` / `SetSubtitle(text)` | Change header text. |
| `Window:SaveConfig(name)` / `LoadConfig(name)` | Config files. |
| `Window:ListConfigs()` / `RefreshConfigs()` | Config list. |
| `Window:DeleteConfig(name)` | Delete a config. |
| `Window:SetAutoloadConfig(name, enabled)` / `GetAutoloadState()` / `DisableAutoload()` | Autoload. |
| `Window:SetConfigVal(flag, value)` / `GetConfigVal(flag)` | Read/write flags directly. |
| `Window:Destroy()` | Remove the UI. |

### Background quick use

```lua
Window:SetBackground("image url")   -- one arg is fine
Window:SetBackground("1234567890")  -- Roblox asset id
Window:SetBackground("", true)      -- clear silently
```

---

## Section elements

| Element | Notes |
| --- | --- |
| `AddLabel(text)` / `AddParagraph(text)` | Static text. |
| `AddButton{Text, Icon, Callback}` | Clickable action. |
| `AddToggle{Text, Description, Flag, Default, Callback}` | Boolean switch. |
| `AddSlider{Text, Flag, Min, Max, Default, Decimals, Callback}` | `Decimals = true` for float values. |
| `AddTextbox{Placeholder, Flag, Default, Callback}` | String input. |
| `AddDropdown{Text, Flag, Values, Default, MultiSelect, Callback}` | `MultiSelect = true` for multi choice. |
| `AddColorPicker{Text, Flag, DefaultColor, DefaultAlpha, Callback}` | RGBA, saves as table/hex. |
| `AddImage{Image, Height, ScaleType, Caption}` | Local asset, rbxassetid or URL. |
| `AddKeybind{Text, Flag, DefaultKey, Mode, Callback, OnKeyChanged}` | Rebindable key. |

Controller methods returned by the elements:

```luau
toggle:Set(true, true)      -- value, skipCallback
toggle:Get()
slider:Set(0.5, true)
dropdown:Set("Closest", true)
dropdown:SetValues(newValues, keepSelection)
dropdown:ToggleValue(value) / Clear() / SelectAll()
textbox:Set("text", true) / GetText()
keybind:SetKey(Enum.KeyCode.F) / Trigger()
colorpicker:Set(color, alpha) / GetColor()
controller:Serialize() / Deserialize(data)
```

---

## Icon support

Use `icon-name` for any icon parameter - names come from [lucide.dev](https://lucide.dev/icons/). Example: `"shield"`, `"user"`, `"wand-sparkles"`, `"person-standing"`.

Icons and images are resolved **in the background**: the window never waits for them, and each icon appears as soon as it is available (there is a small built-in retry for slow loads).

---

## Troubleshooting

* **Icons show as text** ("house", "sparkles") - the icon table failed to download; it retries automatically, and any icon name passed as a plain string is treated as a lucide name.
* **Custom theme missing after autoload** - register your themes as early as possible and leave `AutoloadDelay` at its default so the config loads after your script registers them.
