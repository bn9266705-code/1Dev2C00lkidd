local P,RS,LP=game:GetService("Players"),game:GetService("ReplicatedStorage"),game:GetService("Players").LocalPlayer
local C=require(RS.Assets.Killers.c00lkidd.Config)
local F=RS.Assets.Skins.Killers.c00lkidd["#1dev2C00l"]
local DC,R=require(F.Config),F.Rig
local WSU,WVOL="rbxassetid://135207193038396",1.5
local FACE,MFACE,MSG="rbxassetid://123929445495070","rbxassetid://93284714990410","rbxassetid://14230438861"
local SKIN,BLK,BM=Color3.fromRGB(255,220,120),Color3.fromRGB(17,17,17),Color3.fromRGB(254,243,187)
local FC0=CFrame.new(0,-1,0)*CFrame.Angles(math.rad(180),0,math.rad(-90))
local Ball,Gui=F.Config:FindFirstChild("Ball")or F:FindFirstChild("Ball"),F.Config:FindFirstChild("c00lgui")or F:FindFirstChild("c00lgui")
local Ingame,wsCD=false

if DC.Animations then
	C.Animations=C.Animations or{}
	for i,v in pairs(DC.Animations)do
		if typeof(v)=="table"then
			C.Animations[i]=typeof(C.Animations[i])=="table"and C.Animations[i]or{}
			for i2,v2 in pairs(v)do C.Animations[i][i2]=v2 end
		else C.Animations[i]=v end
	end
end
if DC.Sounds then
	C.Sounds=C.Sounds or{}
	for i,v in pairs(DC.Sounds)do C.Sounds[i]=v end
end
local th=DC.TerrorRadiusThemes or(DC.Sounds and DC.Sounds.TerrorRadiusThemes)
if th then C.Sounds=C.Sounds or{} C.Sounds.TerrorRadiusThemes=th C.TerrorRadiusThemes=th end
C.Voicelines={Idle=false,Kill=false,Stunned=false,CorruptNature=false,PizzaDelivery=false,WalkspeedOverride=false,WalkspeedOverrideHit=false,WalkspeedOverrideCollide=false,WalkspeedOverrideTimeout=false,LastSurvivor=false}

local function D(...)for _,v in ipairs({...})do if v then v:Destroy()end end end
local function find(r,n)if not r then return end local l=n:lower()for _,d in ipairs(r:GetDescendants())do if d.Name:lower()==l then return d end end return r:FindFirstChild(n,true)end
local function face(ch,id)local h=ch:FindFirstChild("Head")if not h then return end for _,d in ipairs(h:GetChildren())do if d:IsA("Decal")or d:IsA("Texture")then d:Destroy()end end local f=Instance.new("Decal")f.Name="face"f.Texture=id or FACE f.Face=Enum.NormalId.Front f.Parent=h end
local function prep(p)if p and p:IsA("BasePart")then p.Massless=true p.CanCollide=false p.Anchored=false p.Transparency=0 end end

local function fire(P,arm)
	local src=R:FindFirstChild("firebrand")or R:FindFirstChild("firebrand",true)if not src then return end
	D(P:FindFirstChild("Dev2Firebrand"))local cl=src:Clone()cl.Name="Dev2Firebrand"cl.Parent=P
	for _,d in ipairs(cl:GetDescendants())do prep(d)if d:IsA("BasePart")then for _,w in ipairs(d:GetChildren())do if w:IsA("Weld")or w:IsA("Motor6D")or w:IsA("WeldConstraint")then w:Destroy()end end end end
	local a=P:FindFirstChild(arm or"Left Arm")local h=cl:IsA("BasePart")and cl or cl:FindFirstChild("Handle")or cl:FindFirstChildWhichIsA("BasePart",true)
	if a and h then local w=Instance.new("Weld")w.Part0=a w.Part1=h w.C0=FC0 w.Parent=h end
end

local function gui(P)
	if not Gui then return end
	local old=P:FindFirstChild("c00lgui")or P:FindFirstChild("c00lgui",true)
	local par=old and old.Parent or P
	if old then old:Destroy()end
	local n=Gui:Clone()n.Name="c00lgui"n.Parent=par
	local h=n:IsA("BasePart")and n or n:FindFirstChildWhichIsA("BasePart",true)
	local t=P:FindFirstChild("Torso")or P:FindFirstChild("HumanoidRootPart")
	if h and t then for _,d in ipairs(n:GetDescendants())do prep(d)end prep(h)local w=Instance.new("Weld")w.Part0=t w.Part1=h w.Parent=h end
end

local function playWS(prim)
	if wsCD or not prim then return end
	wsCD=true
	local s=Instance.new("Sound")s.Name="Dev2WS"s.SoundId=WSU s.Volume=WVOL s.Parent=prim s:Play()
	s.Ended:Connect(function()s:Destroy()end)
	task.delay(8,function()if s and s.Parent then s:Destroy()end wsCD=false end)
end

local function mute(v)
	if not v:IsA("Sound")then return end
	if v.Name=="Dev2WS"then return end
	if v.Name=="VoicelineSFX"or v.Name:find("Voice")or v.Name:find("Kill")or v.Name:find("Stun")then
		v:Stop()v.Volume=0 pcall(function()v:Destroy()end)
	end
end

local function morph(P)
	if not P or P.Name~="c00lkidd"then return end
	local u=P:GetAttribute("Username")if u and u~=LP.Name then return end
	pcall(function()D(P:FindFirstChild("cool"),P:FindFirstChild("Cool"))end)
	for _,n in ipairs({"Torso","Right Leg","Left Leg","Right Arm","Left Arm","Head"})do
		local L=P:FindFirstChild(n)if L and L:IsA("BasePart")then L.Transparency=0 L.Color=SKIN end
	end
	for _,v in ipairs(P:GetChildren())do if v:IsA("Shirt")or v:IsA("Pants")or v:IsA("ShirtGraphic")then v:Destroy()end end
	local sh,pa=find(R,"Shirt"),find(R,"Pants")
	if sh then sh:Clone().Parent=P end if pa then pa:Clone().Parent=P end
	face(P,FACE)
	local hd,fd=P:FindFirstChild("Head"),find(R,"Fedora")
	if fd and hd then D(P:FindFirstChild("Dev2Fedora"))local cl=fd:Clone()cl.Name="Dev2Fedora"cl.Parent=P
		local h=cl:IsA("BasePart")and cl or cl:FindFirstChild("Handle")or cl:FindFirstChildWhichIsA("BasePart",true)
		if h then prep(h)local w=Instance.new("Weld")w.Part0=hd w.Part1=h w.C0=CFrame.new(0,.65,0)w.Parent=h end
	end
	fire(P,"Left Arm")
	task.defer(gui,P)
	local prim=P.PrimaryPart or P:FindFirstChild("HumanoidRootPart")
	if prim then
		prim.ChildAdded:Connect(mute)
		for _,c in ipairs(prim:GetChildren())do mute(c)end
	end
	local hum=P:FindFirstChildOfClass("Humanoid")
	if hum then
		hum.AnimationPlayed:Connect(function(tr)
			local id=tr.Animation and tr.Animation.AnimationId or""
			if id:find("137488556769630")then playWS(prim)end
		end)
	end
end

local function minion(r)
	if not r or r:GetAttribute("D2M")then return end r:SetAttribute("D2M",true)
	for _,n in ipairs({"Minion","Model","robloxvisor","cool","Cool","pizzaBox","PizzaBox"})do
		local o=r:FindFirstChild(n)or r:FindFirstChild(n,true)if o and o.Name:lower()~="pziznbox"then pcall(function()o:Destroy()end)end
	end
	for _,v in ipairs(r:GetChildren())do if v:IsA("Shirt")or v:IsA("Pants")or v:IsA("ShirtGraphic")then v:Destroy()end end
	local h=r:FindFirstChild("Head")if h then h.Color=BM h.Transparency=0 end
	for _,n in ipairs({"Torso","Left Arm","Right Arm","Left Leg","Right Leg"})do local p=r:FindFirstChild(n)if p then p.Color=BLK p.Transparency=0 end end
	local sg=Instance.new("ShirtGraphic")sg.Graphic=MSG sg.Parent=r
	face(r,MFACE)fire(r,"Left Arm")
end

local function ball(p)
	if not p or p:GetAttribute("D2B")or not Ball then return end p:SetAttribute("D2B",true)
	for _,d in ipairs(p:GetDescendants())do if d:IsA("BasePart")then d.Transparency=1 elseif d:IsA("ParticleEmitter")or d:IsA("Trail")or d:IsA("Beam")then pcall(function()d:Destroy()end)end end
	if p:IsA("BasePart")then p.Transparency=1 end
	local b=Ball:Clone()b.Parent=p
	local h=b:IsA("BasePart")and b or b:FindFirstChildWhichIsA("BasePart",true)
	local host=p:IsA("BasePart")and p or p:FindFirstChildWhichIsA("BasePart",true)
	if h and host then prep(h)local w=Instance.new("Weld")w.Part0=host w.Part1=h w.Parent=h end
end

local function isMin(o)
	if not o then return false end
	local n=o.Name:lower()
	if n:find("pizza")or n:find("minion")or o:FindFirstChild("pziznbox")then return true end
	return o:FindFirstChildWhichIsA("Humanoid")and o:FindFirstChild("HumanoidRootPart")and not P:GetPlayerFromCharacter(o)
end

if LP.Character then task.delay(.5,morph,LP.Character)end
LP.CharacterAdded:Connect(function(r)task.wait(.5)morph(r)end)
task.spawn(function()
	local k=workspace:FindFirstChild("Players")and workspace.Players:FindFirstChild("Killers")
	if not k then local pf=workspace:WaitForChild("Players",20)if pf then k=pf:WaitForChild("Killers",20)end end
	if not k then return end
	for _,c in ipairs(k:GetChildren())do task.delay(.8,morph,c)end
	k.ChildAdded:Connect(function(c)task.wait(.8)morph(c)end)
end)
task.spawn(function()
	local m=workspace:FindFirstChild("Map")or workspace:WaitForChild("Map",20)if not m then return end
	Ingame=m:FindFirstChild("Ingame")or m:WaitForChild("Ingame",20)if not Ingame then return end
	local function on(v)task.delay(.25,function()
		if not v or not v.Parent then return end
		if v.Name=="HumanoidRootProjectile"then ball(v)end
		if isMin(v)then minion(v)end
	end)end
	for _,c in ipairs(Ingame:GetChildren())do on(c)end
	Ingame.ChildAdded:Connect(on)
end)
print("1dev2!")
