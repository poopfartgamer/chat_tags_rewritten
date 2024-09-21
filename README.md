# Roblox Chat Tags

This repository contains chat tags for Roblox games, stored in JSON format. The tags can be used to enhance the player chat experience by assigning custom labels or prefixes to usernames in chat messages.

## Features

- **Customizable chat tags**: Easily assign unique tags or titles to players.
- **JSON format**: Simple and structured data storage for easy integration.
- **Roblox-compatible**: Directly import these tags into your Roblox games and apply them in your chat system.

## How to Use

1. Clone or download the repository from GitHub.
2. Upload the `chat_tags.json` file into your Roblox project using the `InsertService` or by manually adding it to your game files.
3. Integrate the chat tags into your existing chat system. You can use the Roblox `ChatService` to customize chat messages and apply the tags dynamically based on your game's logic.

### Sample Code (Roblox Lua)

Here is an example of how you might load the chat tags from the JSON file and apply them in Roblox:

```lua
local HttpService = game:GetService("HttpService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Load the chat tags
local chatTagsData = HttpService:JSONDecode(ReplicatedStorage:WaitForChild("ChatTags").Value)

-- Apply the tags to a player
local function applyChatTag(player)
    local chatTag = chatTagsData[player.UserId]
    if chatTag then
        -- Customize the player's chat tag
        player.Chatted:Connect(function(message)
            game.Chat:Chat(player.Character.Head, "[" .. chatTag .. "] " .. message, Enum.ChatColor.Red)
        end)
    end
end

game.Players.PlayerAdded:Connect(applyChatTag)
