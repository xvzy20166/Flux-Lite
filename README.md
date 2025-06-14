Flux Lite
===========

A feather‑weight, beginner‑friendly Roblox framework that helps you build games faster without hiding the “how” behind a wall of abstractions.

---------------------------------
🚀  What Makes Flux Lite Different
---------------------------------

• **Tiny core, instant comprehension** – one auto‑loader, two module types (Service & Controller), zero boilerplate.  
• **BridgeNet 2 inside** – remotes create themselves; you call `:FireTo`, `:FireAll`, `:Connect`.  
• **Batteries included** – Trove for cleanup, Promise for async flows, tiny Signal implementation.  
• **Rojo optional** – pure Studio folders out‑of‑the‑box; drop into a Rojo project later with no changes.  
• **MIT licensed** – copy, fork, ship commercial projects, no strings attached.

----------------
🏁  Quick Start
----------------

1. **Import**  
   Place the entire `Flux` folder inside **ReplicatedStorage**.

2. **Bootstrap once per side**  
   ```lua
   -- ServerScriptService/Loader
   require(game.ReplicatedStorage.Flux.Loader)

   -- StarterPlayerScripts/Loader
   require(game.ReplicatedStorage.Flux.Loader)
   ```

3. **Create a Service**  
   `ReplicatedStorage/Flux/Server/Services/CoinService.lua`
   ```lua
   local Flux = require(game.ReplicatedStorage.Flux.Core)
   local Bridge = Flux.BridgeNet.CreateBridge("CoinsUpdated")

   local CoinService = { Name = "CoinService" }

   function CoinService:Init()
       self.Balance = {}
   end

   function CoinService:Start()
       game.Players.PlayerAdded:Connect(function(p)
           self.Balance[p] = 0
           Bridge:FireTo(p, 0)
       end)
   end

   return CoinService
   ```

4. **Create a Controller**  
   `ReplicatedStorage/Flux/Client/Controllers/CoinController.lua`
   ```lua
   local Flux = require(game.ReplicatedStorage.Flux.Core)
   local Bridge = Flux.BridgeNet.CreateBridge("CoinsUpdated")

   local CoinController = { Name = "CoinController" }

   function CoinController:Start()
       Bridge:Connect(function(amount)
           print("You now have", amount, "coins!")
       end)
   end

   return CoinController
   ```

Hit **Play** – you’re syncing data across the network with five lines of real work.

---------------------------------
📂  Default Folder Layout
---------------------------------

ReplicatedStorage  
└─ Flux  
   ├─ Core.lua  
   ├─ Loader.lua  
   ├─ Libs  
   │  ├─ BridgeNet2.lua  
   │  ├─ Trove.lua  
   │  └─ Promise.lua  
   ├─ Server  
   │  └─ Services  
   └─ Client  
      └─ Controllers

---------------------------------
🔧  Roadmap
---------------------------------

* `flux g service <Name>` CLI scaffolder  
* ProfileService wrapper (`Flux.Data`)  
* In‑game debug overlay (F9)  
* Sample projects: Obby, Simulator, FPS sandbox

---------------------------------
🤝  Contributing
---------------------------------

1. Fork → branch → PR.  
2. Follow Luau strict mode and Stylua formatting (`stylua .`).  
3. Add matching unit tests in `tests/` (TestEZ).

---------------------------------
📜  License
---------------------------------

Flux Lite is released under the MIT License – do whatever you like, just keep the notice intact.
