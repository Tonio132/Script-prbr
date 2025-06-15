--[[ Script Hub em Português - Blox Fruits ]]--

local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Trocar de time automaticamente
if getgenv().TimeEscolhido == "Piratas" then
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam", "Pirates")
elseif getgenv().TimeEscolhido == "Marinha" then
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam", "Marines")
end

-- Função para teleportar para uma ilha
local function TeleportarPara(IlhaNome)
    local locais = {
        ["Inicio"] = CFrame.new(2067, 38, 902),
        ["Jungle"] = CFrame.new(-1615, 36, 152),
        ["Deserto"] = CFrame.new(977, 7, 4400)
    }
    
    if locais[IlhaNome] then
        player.Character.HumanoidRootPart.CFrame = locais[IlhaNome]
    end
end

-- Teleporte automático
if getgenv().AutoTeleport then
    wait(2)
    TeleportarPara("Jungle")
end

-- Farm automático de NPCs
if getgenv().AutoFarm then
    while true do
        wait(0.5)
        for _, v in pairs(game.Workspace.Enemies:GetChildren()) do
            if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                pcall(function()
                    v.HumanoidRootPart.CanCollide = false
                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                    player.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,3)
                    game:GetService("VirtualInputManager"):SendKeyEvent(true, "Z", false, game)
                end)
            end
        end
    end
end
