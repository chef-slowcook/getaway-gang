# Getaway Gang: Game Design Document

**Version:** 1.0
**Status:** Pre-Production / Vertical Slice Planning
**Engine:** Unity (URP)
**Target Platform:** PC (Local Split-Screen Focus)

---

## 1. High Concept

### Hook
An isometric, physics-driven driving roguelike where you execute perfect getaways in a procedurally escalating heists, aiming for a "clean escape" before the FVI (Federal Vice Intelligence) ends your criminal career.

### Elevator Pitch
Getaway Gang is a co-op driving roguelike initially set in a vice-gripped 80s Miami. You act as the wheelman for high-stakes heists where every job cranks up the police heat. Drive fast, drive clean, and stash your cash. You won't escape forever—so how much can you bank before you burn?

### Unique Selling Points (USPs)
* **Roguelike Heat:** Notoriety carries over between levels. The greedier you are, the aggressive the police response becomes in the next zone.
* **The Clean Getaway:** Unlike destruction derbies, players are rewarded for precision. Smashing slows you down; drifting, weaving, and using the environment to trap cops maximizes speed and score.
* **Couch Criminals:** Built primarily for local split-screen co-op. Player 2 isn't just a passenger; they manage navigation, diverting police comms, or driving a decoy vehicle.
* **AI-Assisted Development:** Codebase designed for modularity to leverage AI code generation for rapid prototyping of vehicle handling and procedural city blocks.

---

## 2. Core Gameplay Loop

### The Run Loop
1. **Briefing:** Select a heist contract (Risk vs. Reward). Higher reward means tighter time limits and more police presence.
2. **The Job (Gameplay events):**
   * **Infiltration:** Drive to the target location without triggering alarms (Stealth driving mechanics).
   * **Pickup:** Collect the package/crew. **The Alarm Triggers.**
   * **Escape:** Navigate from Point A to Point B while evading the FVI.
3. **Extraction:** Reach the Safe Zone to bank the cash.
4. **Heat Escalation:** The Heat Meter rises based on chaos caused. This modifies the next level's difficulty.
5. **Preparation:** Spend cash on vehicle repairs, gadgets, or bribe logic to lower heat.

### The Macro Loop (Meta)
* **Offshore Banking:** After a successful run, a percentage of cash is laundered to the meta-progression account.
* **The Bust (Permadeath):** If the vehicle is disabled or the driver is arrested, the run ends. Unlaundered cash is lost. Or is it?
* **Progression:** Use Offshore accounts to unlock new starting vehicles, permanent driver perks, and aesthetic customization.

---

## 3. Driving & Physics Design

### Handling Philosophy
**Arcade-Sim Hybrid.**
The game requires the satisfying weight transfer of a simulation but the forgiving traction of an arcade racer.
* **Suspension:** Soft, bouncy suspension (80s Cadillacs and Muscle cars). Players should visually see the car body roll when cornering.
* **Drifting:** Brake-to-drift mechanic. Successfully holding a drift builds a Turbo meter.
* **Momentum:** Conservation of momentum is key. Hitting obstacles doesn't stop the car instantly but drastically affects handling and speed.

### Environmental Interaction
* **Collision Rules:** Static buildings are immovable. Street props (lamp posts, mailboxes, fences) are destructible rigidbodies.
* **Speed Penalty:** Every collision applies a drag force. A Clean Getaway requires avoiding debris that slows the rigidbodies.
* **Traffic:** NPC traffic follows boids-based logic. They panic when sirens are near, creating unpredictable obstacles.

---

## 4. Heist Getaway Systems

### The Heat System (Run Persistence)
Heat is a variable (0-100) that persists across levels in a single run.
* **Tier 1 (0-25):** Local Patrol. Standard cruisers. Try to pit maneuver the player.
* **Tier 2 (26-50):** Detectives. Unmarked cars. Faster, more aggressive AI.
* **Tier 3 (51-75):** SWAT. Armored vans act as mobile roadblocks. Road spikes deployed.
* **Tier 4 (76-100):** The FVI. Helicopters with spotlights (blinds player), fast interceptors, and complete district lockdowns.

### Civilian & World Reactions
* **Panic:** Pedestrians dive out of the way (ragdoll physics). Hitting pedestrians increases Heat instantly.
* **Traffic Yield:** Cars pull over for police sirens, potentially blocking the player's escape route.

---

## 5. Level & World Design

### City Layout Logic
The game takes place in Vice Bay. The map is generated via a tile-based procedural system for the roguelike elements, but individual tiles are hand-crafted for gameplay flow.
* **The Grid:** The city is a grid of 100x100m blocks.
* **The Arteries:** Wide boulevards for speed (high risk of roadblocks).
* **The Veins:** Narrow alleys and backlots for evasion (high risk of collision).

### Verticality
* **Ramps & Jumps:** Key to escaping encirclement. Jumping over a canal or highway breaks the police AI pathfinding.
* **Parking Garages:** Multi-level structures acting as vertical mazes to lose helicopters.

---

## 6. Player Tools & Abilities

### Vehicle Classes
1. **Runner:** Balanced speed/handling. (Reference: Ferrari Testarossa).
2. **Muscle:** High health, low acceleration, high top speed. Good for ramming roadblocks. (Reference: 1970 Chevelle).
3. **Weasel:** Tiny, extremely agile, low health. Can fit through gaps cop cars cannot. (Reference: Mini Cooper).

### Gadgets (Active Abilities)
* **Oil Slick:** Raycast behind the car; sets friction of trailing cars to near zero.
* **Smoke Screen:** Breaks line-of-sight for AI, forcing them to switch to Search Mode.
* **Plate Flipper:** Reduces current Heat accumulation rate for 10 seconds.

---

## 7. Enemy & AI Design

### FVI Behavior
The AI uses a **Context-Based Steering** system. They do not cheat; they must drive physics objects.
* **Chasers:** Attempt to maintain a position behind and to the side of the player (PIT maneuver logic).
* **Blockers:** Spawn ahead of the player on the navmesh. They park sideways to form roadblocks.
* **Rubber-banding:** Kept minimal. Instead of teleporting, higher Heat spawns faster units.

### Difficulty Scaling
* **Run Time:** The longer a distinct heist takes, the more units spawn.
* **Notoriety:** As the run progresses, AI reaction times decrease, and their maximum speed increases.

---

## 8. Progression & Meta Systems

### The Offshore Account
* **Cash:** Earned by escaping. Used in-run for repairs/fuel, gadgets, traps, vehicles, boosts, etc.
* **Notoriety Points:** Earned by performing dangerous maneuvers (Near Miss, Drift, Jump). Used to unlock persistent upgrades.

### Roguelike Structure
* **Session Length:** 15 - 25 minutes per run.
* **Failure:** Player sees a newspaper headline, newscast, recounting their capture and stats. "LOCAL DRIVER CAUGHT: 2 MILLION IMPOUNDED."

---

## 9. Art & Audio Direction

### Visual Style
* **Reference:** Hotline Miami meets Driver in 3D.
* **Palette:** Neon pinks, cyans, deep sunset oranges, and dark asphalt greys.
* **Readability:** The player car always has a subtle rim-light. Enemy view cones are visualized on the pavement (Metal Gear Solid style) to aid in stealth/evasion sections.
* **Camera:** Isometric (Orthographic). Smooth dampening. Camera leads the player based on velocity (looks ahead).

### Audio Design
* **Soundtrack:** Synthwave / Retrowave. "Push it to the Limit" energy.
* **Dynamic Music:**
    * *Stealth:* Low-pass filter, bass only.
    * *Chase:* Full instrumentation.
    * *Critical Heat:* Tempo increases, distortion added.
* **Cues:** Police radio chatter gives players information (e.g., "Setting up spike strips on Ocean Drive").

---

## 10. Technical Design (Unity-Focused)

### Physics Architecture
* **Controller:** Custom Raycast Vehicle Controller. Avoid Unity's default `WheelCollider` due to instability at high speeds. Raycasts handle suspension; friction curves are calculated manually for arcade drift feel.
* **Input:** New Input System. Essential for handling split-screen gamepad assignments easily.

### AI Implementation Strategy (Solo Dev)
* **NavMesh:** Use Unity's NavMeshComponents for runtime baking (if procedural) or baked surfaces.
* **AI Code Gen:** Use LLMs to generate individual "Steering Behaviors" (Seek, Flee, Arrive, Obstacle Avoidance) as separate scripts, then combine them in a Weighted Sum manager.

### Optimization
* **Occlusion Culling:** Aggressive culling for the isometric view.
* **Object Pooling:** Essential for projectiles, debris, and police cars. No `Instantiate` during gameplay.

---

## 11. Monetization & Scope Control

### Indie Scope
* **Cut First:** Online Multiplayer. (Stick to local only for V1).
* **Cut Second:** Procedural City Generation. (Fall back to 3 hand-crafted maps if proc-gen becomes a rabbit hole).
* **Cut Third:** Story mode. (Pure arcade roguelike loop is sufficient).

### Monetization
* Premium PC title (Steam). No microtransactions.

---

## 12. Risks & Challenges

| Risk | Impact | Mitigation Strategy |
| :--- | :--- | :--- |
| **Physics Bugs** | High (Cars flying off map) | Use Raycast controller instead of Rigidbodies for wheels. Clamp maximum velocity. |
| **Split-Screen Perf** | Medium | Use Universal Render Pipeline (URP). Limit dynamic lights. Share UI canvas where possible. |
| **AI Complexity** | High | Keep AI simple: They don't need to be smart, just aggressive. Use swarm numbers rather than complex tactics. |
| **Solo Dev Burnout** | Critical | Strict adherence to the prototype scope. Focus code on gameplay feel and fun.

---

# Summary One-Pager

**Title:** Getaway Gang
**Genre:** Isometric Roguelike Driving Action
**Vibe:** 80s Miami, Synthwave, High-Octane Anxiety.

**The Game:**
Players drive a getaway car in a high-stakes heist run. The game is played in runs (roguelike); you complete a heist, escape the police, upgrade your car, and go for the next target. The police response (Heat) escalates until you are inevitably caught. The goal is to bank as much cash "offshore" as possible before the FVI shuts you down.

**Core Mechanic:**
The Clean Getaway. While the world is physics-based and destructible, the player survives by driving cleanly. Drifting, juking cops, and using alleyways are superior to ramming.

**Development Focus:**
Local Split-screen. High-quality vehicle physics. One polished city district.

---

# Prototype Milestone Plan (First 3 Months)

**Goal:** A "Vertical Slice" demo featuring one car, one enemy type, and one city block loop with split-screen enabled.

### Month 1: The Feel (Physics & Camera)
* **Week 1:** Implement custom Raycast Vehicle Controller. Focus on suspension and turning radius.
* **Week 2:** Implement Drift logic and friction curves.
* **Week 3:** Camera system (Isometric, follow-dampening, screen shake on impact).
* **Week 4:** Greybox city block. Test handling in a confined space.

### Month 2: The Opposition (AI & Systems)
* **Week 1:** Basic AI Pathfinding (NavMesh). AI can follow player.
* **Week 2:** AI Behaviors (Ramming, blocking).
* **Week 3:** Implementation of the Heat system logic (UI tracking).
* **Week 4:** Local Split-screen implementation (Input handling and camera viewport splitting).

### Month 3: The Loop (Game Flow & Polish)
* **Week 1:** Game Manager (Start State -> Gameplay -> Win/Loss State).
* **Week 2:** UI Implementation (Speedometer, Heat Meter, Cash).
* **Week 3:** Visual Polish (VFX: Smoke, tire tracks, sparks).
* **Week 4:** Audio integration (Engine sounds, basic synth loop). **Milestone Review. Possible deployment strategy execution**
