local DataStoreService = game:GetService("DataStoreService")
local DataStore = DataStoreService:GetDataStore("TimeStats")

game.Players.PlayerAdded:Connect(function(Player)
    local Leaderstats = Instance.new("Folder")
    Leaderstats.Name = "leaderstats"
    Leaderstats.Parent = Player
    local Points = Instance.new("IntValue")
    Points.Name = "Points"
    Points.Value = 0
    Points.Parent = Leaderstats
    
    local Data = DataStore:GetAsync(Player.UserId)
    if Data then
        Points.Value = Data
    end
    
    coroutine.resume(coroutine.create(function()
        while true do
            wait(60)
            Points.Value = Points.Value + 1
        end
    end))
end)

game.Players.PlayerRemoving:Connect(function(Player)
    DataStore:SetAsync(Player.UserId, Player.leaderstats.Points.Value)
end)
