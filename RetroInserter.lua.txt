
--hi










succ, errr = pcall(function()
local file = loadfile("troll.txt")()
local thing = file
local creater = game:GetService("ReplicatedStorage").RemoteFunctions.CreateObject
local deez = game:GetService("ReplicatedStorage").RemoteFunctions.ChangeObjectPropertyAndReturn
local Tlimit = 5
local Tasks = 0

local list = {
    ["Locked"] = true,
    ["Anchored"] = true,
}

function dee(the, fromthe, frompart)
	for i, v in pairs(the) do
	    repeat task.wait() until Tasks <= Tlimit
		task.spawn(function()
		    Tasks = Tasks + 1
		    task.delay(1, function()
		        Tasks = Tasks - 1
		    end)
			local dogdoin, dog = pcall(function()
				local instance = creater:InvokeServer(v["TypoLol"], v["Parent"] or (frompart or workspace))
				if instance and v["Name"] ~= "MeshPart" then
					if instance:IsA("BasePart") then
						deez:InvokeServer({instance}, "FormFactor", "Custom")
					end
					for e, g in pairs(v) do
						if e ~= "TypoLol" and e ~= "Name" and e ~= "C_" then
							if tostring(instance[e]) ~= tostring(g) then
								deez:InvokeServer({instance}, e, g)
							else
								if list[e] then
									deez:InvokeServer({instance}, e, g)
								end
							end
						elseif e == "C_" then
							dee(g, v, instance)
						end
					end
				elseif instance and v["Name"] == "MeshPart" then
					deez:InvokeServer({instance}, "FormFactor", "Custom")
                    
                    local meshp = creater:InvokeServer("SpecialMesh", instance)
					deez:InvokeServer({meshp}, "MeshType", Enum.MeshType.FileMesh)
					deez:InvokeServer({meshp}, "MeshId", string.gsub(v["MeshId"], "%D", ""))
					deez:InvokeServer({meshp}, "TextureId", string.gsub(v["TextureID"], "%D", ""))
					local ktest = deez:InvokeServer({meshp}, "Scale", v["Size"]/v["MeshSize"])
                    
					for e, g in pairs(v) do
						if e ~= "TypoLol" and e ~= "Name" and e ~= "C_" and e ~= "MeshId" and e ~= "TextureID" and e ~= "TextureId" and e ~= "MeshSize" then
							if tostring(instance[e]) ~= tostring(g) then
								deez:InvokeServer({instance}, e, g)
							else
								if list[e] then
									deez:InvokeServer({instance}, e, g)
								end
							end
						elseif e == "C_" then
							dee(g, v, instance)
						end
					end
				end
			end)
		end)
		task.wait(0.1)
	
	end
end

dee(thing)
repeat task.wait() until Tasks <= 0
print("Place loading finished!")
end)
if not succ then
    warn("Error:")
    warn(errr)
end