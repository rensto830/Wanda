--[[ 
    WANDA MOBILE FIXER - COLE NO FINAL DO SCRIPT
    Este trecho limpa o código e cria o botão de abrir no Mobile.
--]]

local function SetupMobileWanda()
    local Player = game:GetService("Players").LocalPlayer
    local pGui = Player:WaitForChild("PlayerGui")
    
    -- 1. Tenta achar a GUI que o script original criou
    local wandaGui = pGui:FindFirstChild("WandaVision_Enhanced") or pGui:FindFirstChildOfClass("ScreenGui")
    
    if not wandaGui then
        print("❌ Script original falhou em criar a GUI. Verifique o topo do código.")
        return
    end

    -- 2. Acha o Frame Principal
    local main = wandaGui:FindFirstChild("MainFrame") or wandaGui:FindFirstChildOfClass("Frame")
    
    if main then
        main.Visible = false -- Começa fechado para não travar o mobile
        
        -- 3. Cria o Botão de Abrir (Mobile Toggle)
        local MobileBtn = Instance.new("TextButton")
        local UICorner = Instance.new("UICorner")
        
        MobileBtn.Name = "WandaMobileToggle"
        MobileBtn.Parent = wandaGui
        MobileBtn.Size = UDim2.new(0, 60, 0, 60)
        MobileBtn.Position = UDim2.new(0.1, 0, 0.15, 0) -- Fica no topo esquerdo
        MobileBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
        MobileBtn.Text = "W"
        MobileBtn.TextColor3 = Color3.new(1,1,1)
        MobileBtn.TextSize = 30
        MobileBtn.Font = Enum.Font.Bangers
        MobileBtn.Active = true
        MobileBtn.Draggable = true -- Você pode arrastar o botão de abrir
        
        UICorner.CornerRadius = UDim.new(0.5, 0)
        UICorner.Parent = MobileBtn

        -- 4. Função de Abrir/Fechar
        MobileBtn.MouseButton1Click:Connect(function()
            main.Visible = not main.Visible
            if main.Visible then
                -- Centraliza o painel se ele estiver sumido
                main.Position = UDim2.new(0.5, -main.Size.X.Offset/2, 0.5, -main.Size.Y.Offset/2)
            end
        end)
        
        print("✅ Botão Mobile Criado! Clique no 'W' para abrir.")
    end
end

-- Executa após o script original carregar
task.wait(1.5)
SetupMobileWanda()
