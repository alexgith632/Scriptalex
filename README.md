-- QUANTUM HUB MINI v1.0
local P,R,U,T,W=game:GetService("Players"),game:GetService("RunService"),game:GetService("UserInputService"),game:GetService("TweenService"),game:GetService("Workspace")
local LP=P.LocalPlayer
local C=W.CurrentCamera

-- CONFIG
local M={Speed=50,Jump=100,Fly=false,FlySpeed=50,Noclip=false,ESP=false,Fullbright=false,Aimbot=false,FOV=100,InfJump=false,AntiAFK=false}

-- FUNCTIONS
local function A()local H=LP.Character:FindFirstChild("Humanoid")if H then H.WalkSpeed=M.Speed H.JumpPower=M.Jump end end
local function F()M.Fly=not M.Fly if M.Fly then local B=Instance.new("BodyVelocity")B.Name="Fly"B.MaxForce=Vector3.new(1e4,1e4,1e4)B.P=1e4
R.Heartbeat:Connect(function()if M.Fly and LP.Character then local R=LP.Character:FindFirstChild("HumanoidRootPart")if R then local D=Vector3.new(0,0,0)
if U:IsKeyDown(Enum.KeyCode.W)then D=D+C.CFrame.LookVector end if U:IsKeyDown(Enum.KeyCode.S)then D=D-C.CFrame.LookVector end
if U:IsKeyDown(Enum.KeyCode.A)then D=D-C.CFrame.RightVector end if U:IsKeyDown(Enum.KeyCode.D)then D=D+C.CFrame.RightVector end
if U:IsKeyDown(Enum.KeyCode.Space)then D=D+Vector3.new(0,1,0)end if U:IsKeyDown(Enum.KeyCode.LeftShift)then D=D-Vector3.new(0,1,0)end
B.Velocity=D.Unit*M.FlySpeed B.Parent=R end end else if B then B:Destroy()end end end)end end
local function N()M.Noclip=not M.Noclip if M.Noclip then R.Stepped:Connect(function()if M.Noclip and LP.Character then for _,P in pairs(LP.Character:GetDescendants())do
if P:IsA("BasePart")then P.CanCollide=false end end end end)end end
local function E()M.ESP=not M.ESP if M.ESP then for _,P in pairs(P:GetPlayers())do if P~=LP and P.Character then local H=P.Character:FindFirstChild("Head")if H then
local B=Instance.new("BillboardGui")B.Size=UDim2.new(0,100,0,30)B.StudsOffset=Vector3.new(0,3,0)B.AlwaysOnTop=true B.Adornee=H
local L=Instance.new("TextLabel")L.Size=UDim2.new(1,0,1,0)L.BackgroundTransparency=1 L.Text=P.Name L.TextColor3=Color3.new(1,0,0)L.TextSize=14 L.Font=Enum.Font.Code
L.Parent=B B.Parent=game.CoreGui end end end else for _,O in pairs(game.CoreGui:GetChildren())do if O.Name=="BillboardGui"then O:Destroy()end end end end
local function FB()M.Fullbright=not M.Fullbright local L=game:GetService("Lighting")if M.Fullbright then L.Ambient=Color3.new(1,1,1)L.Brightness=2
L.GlobalShadows=false else L.Ambient=Color3.new(0.5,0.5,0.5)L.Brightness=1 L.GlobalShadows=true end end
local function IJ()M.InfJump=not M.InfJump if M.InfJump then U.JumpRequest:Connect(function()if M.InfJump then local H=LP.Character:FindFirstChild("Humanoid")if H then
H:ChangeState(Enum.HumanoidStateType.Jumping)end end end)end end
local function AAFK()M.AntiAFK=not M.AntiAFK if M.AntiAFK then local VU=game:GetService("VirtualUser")LP.Idled:Connect(function()VU:CaptureController()VU:ClickButton2(Vector2.new())end)end end
local function AM()M.Aimbot=not M.Aimbot if M.Aimbot then R.Heartbeat:Connect(function()local CP,CD=nil,M.FOV for _,P in pairs(P:GetPlayers())do if P~=LP and P.Character then
local H=P.Character:FindFirstChild("Head")if H then local SP,OS=C:WorldToViewportPoint(H.Position)if OS then local D=(Vector2.new(SP.X,SP.Y)-Vector2.new(C.ViewportSize.X/2,C.ViewportSize.Y/2)).Magnitude
if D<CD then CD=D CP=P end end end end end if CP then local H=CP.Character:FindFirstChild("Head")if H then C.CFrame=CFrame.new(C.CFrame.Position,H.Position)end end end)end end

-- UI
local SG=Instance.new("ScreenGui")SG.Name="QuantumMini"SG.ResetOnSpawn=false
local MF=Instance.new("Frame")MF.Size=UDim2.new(0,300,0,400)MF.Position=UDim2.new(0.5,-150,0.5,-200)MF.BackgroundColor3=Color3.new(0.1,0.1,0.2)
local TB=Instance.new("Frame")TB.Size=UDim2.new(1,0,0,30)TB.BackgroundColor3=Color3.new(0,0.2,0.4)
local TL=Instance.new("TextLabel")TL.Size=UDim2.new(1,0,1,0)TL.BackgroundTransparency=1 TL.Text="QUANTUM HUB"TL.TextColor3=Color3.new(0,1,1)TL.Font=Enum.Font.Code
local SF=Instance.new("ScrollingFrame")SF.Size=UDim2.new(1,-20,1,-50)SF.Position=UDim2.new(0,10,0,40)SF.BackgroundTransparency=1 SF.ScrollBarThickness=5

local Btns={
{"Speed: "..M.Speed,function()M.Speed=M.Speed==200 and 16 or M.Speed+10 A()end,Color3.new(0,0.4,0.8)},
{"Jump: "..M.Jump,function()M.Jump=M.Jump==500 and 50 or M.Jump+50 A()end,Color3.new(0.4,0,0.8)},
{"Fly: "..(M.Fly and "ON"or"OFF"),F,M.Fly and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"Noclip: "..(M.Noclip and"ON"or"OFF"),N,M.Noclip and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"ESP: "..(M.ESP and"ON"or"OFF"),E,M.ESP and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"FullBright: "..(M.Fullbright and"ON"or"OFF"),FB,M.Fullbright and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"Aimbot: "..(M.Aimbot and"ON"or"OFF"),AM,M.Aimbot and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"Inf Jump: "..(M.InfJump and"ON"or"OFF"),IJ,M.InfJump and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)},
{"Anti AFK: "..(M.AntiAFK and"ON"or"OFF"),AAFK,M.AntiAFK and Color3.new(0,0.8,0)or Color3.new(0.8,0,0)}
}

for i,btn in ipairs(Btns)do local B=Instance.new("TextButton")B.Size=UDim2.new(1,-20,0,30)B.Position=UDim2.new(0,10,0,(i-1)*35)
B.BackgroundColor3=btn[3]B.Text=btn[1]B.Font=Enum.Font.Code B.TextColor3=Color3.new(1,1,1)B.TextSize=12
B.MouseButton1Click=function()btn[2]()B.Text=btn[1]B.BackgroundColor3=btn[3]end B.Parent=SF end

TL.Parent=TB TB.Parent=MF SF.Parent=MF MF.Parent=SG SG.Parent=LP:WaitForChild("PlayerGui")

-- DRAGGABLE
local D,DS,SP=false
TB.InputBegan:Connect(function(i)if i.UserInputType==Enum.UserInputType.MouseButton1 then D=true DS=i.Position SP=MF.Position end end)
U.InputChanged:Connect(function(i)if D and i.UserInputType==Enum.UserInputType.MouseMovement then local d=i.Position-DS
MF.Position=UDim2.new(SP.X.Scale,SP.X.Offset+d.X,SP.Y.Scale,SP.Y.Offset+d.Y)end end)
U.InputEnded:Connect(function(i)if i.UserInputType==Enum.UserInputType.MouseButton1 then D=false end end)

-- TOGGLE KEY
U.InputBegan:Connect(function(i)if i.KeyCode==Enum.KeyCode.RightShift then MF.Visible=not MF.Visible end end)

-- AUTO UPDATE
R.Heartbeat:Connect(A)
print("[QUANTUM HUB] Loaded! (RightShift to toggle)")
