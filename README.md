local function ForcePart(v)
	if v:IsA("BasePart") and not IsPlayerPart(v) and v.Name ~= "Handle" then
		
		-- ⭐ NOVO: permitir mexer em peças ancoradas
		if v.Anchored then
			v.Anchored = false
		end
		
		for _, x in ipairs(v:GetChildren()) do
			if x:IsA("BodyMover") or x:IsA("RocketPropulsion") then
				x:Destroy()
			end
		end
		
		if v:FindFirstChild("Attachment") then v:FindFirstChild("Attachment"):Destroy() end
		if v:FindFirstChild("AlignPosition") then v:FindFirstChild("AlignPosition"):Destroy() end
		if v:FindFirstChild("Torque") then v:FindFirstChild("Torque"):Destroy() end

		v.CanCollide = false  

		local Torque = Instance.new("Torque", v)  
		Torque.Torque = Vector3.new(100000, 100000, 100000)  

		local AlignPosition = Instance.new("AlignPosition", v)  
		local Attachment2 = Instance.new("Attachment", v)  

		Torque.Attachment0 = Attachment2  
		AlignPosition.MaxForce = math.huge  
		AlignPosition.MaxVelocity = math.huge  
		AlignPosition.Responsiveness = 200  
		AlignPosition.Attachment0 = Attachment2  
		AlignPosition.Attachment1 = Attachment1  
	end
end
