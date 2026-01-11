# Getaway Gang

> **Status:** Pre-Production / Vertical Slice  
> **Engine:** Unity 6.3 LTS  
> **Pipeline:** Universal Render Pipeline (URP)  
> **Platform:** PC (Local Co-op Focus)

**Getaway Gang** is an isometric, co-op driving roguelike that blends driving mechanics with chaotic communication, and big LOOT payouts.

**Couch Co-op** experience where two players operate a single vehicle. 

**Player 1 drives the escape Vehicle**, choose route, escape the cops, reach the extraction.

**Player 2 is the Passenger**, GPS navigation and hacking together countermeasures.

The game starts when the alarm blasts!

🚗💨 **! 🚨 🚓 🚓 🚁 🚨 !**

---

## 🎨 Art Direction & Vibe

**"Miami Vice meets Low-Poly"**

The game utilizes the **Unity Universal Render Pipeline (URP)** to blend retro aesthetics with modern lighting.

* **The Palette:** Deep bruised purples, sunset oranges, and blinding cyan neon. The world is permanently set to "Magic Hour" or "Midnight Rain."
* **The Materiality:**
    * **The World:** Low-poly geometry with high-fidelity PBR materials. Wet asphalt reflects neon signs (Screen Space Reflections).
    * **The Car:** The "Hero" object. It features exaggerated suspension animations (squash and stretch) to communicate weight transfer. It should look like a toy come to life.
* **The UI (Diegetic):**
    * **Player 1:** They read the road. Physical envrioment, smoke trails, and physical vehicle damage are their status indicators.
    * **Player 2:** Sees a paper map projected over the camera UI, mimicking 80s low-tech with modern GPS. Also can trigger nearby traps.

---

## 🎮 High Concept

### The "One Car" Co-op Dynamic
The game relies on asymmetric cooperation within a shared screen.

* **Player 1 (The Wheelman):**
    * **Role:** Eyes on the road.
    * **Responsibility:** Precision driving, drifting, dodging traffic, and maintaining momentum.
* **Player 2 (The Operator):**
    * **Role:** Eyes on the city.
    * **Responsibility:** GPS Navigation, shooting, deploying countermeasures, and communication.

### The Roguelite Loop
1.  **The Job:** Spawn instantly with **Heat** depending on the **Hit** chosen.
2.  **The Escape:** Survive a chaotic physics-based chase. Crashing into buildings is a bad idea; hitting debris slows you down, hitting cops makes you lose cash.
3.  **The Stash:** Reach the **Extraction Site** to successfully escape to the **Safehouse**.
4.  **The Meta:** Spend cash in the **Safehouse** to repair/upgrade the vehicle and bank funds into an **Offshore Account** (Permanent Progression).
5.  **Escalation:** **Notoriety** persists. If you make a mess in District 1, the SWAT team is readied up in District 2.

---

## 🕹️ Controls & Input

The game supports **Mixed Input** (Gamepad + Keyboard/Mouse) to accommodate any local setup.

**Ideal Setup:** Player 1 on Gamepad, Player 2 on Mouse & Keyboard.

| Action | Player 1 (The Wheelman) | Player 2 (The Operator) |
| :--- | :--- | :--- |
| **Input Device** | **Gamepad** / **Keyboard (WASD)** | **Mouse & Keyboard** / **Gamepad** |
| **Steering** | Left Stick / A & D | *N/A* |
| **Throttle/Brake** | Triggers / W & S | *N/A* |
| **Navigation** | *N/A (Blind)* | **Mouse Cursor** (Pan Map & Ping Route) |
| **Drift / Handbrake** | South Button (A) / Space | *N/A* |
| **Boost (Nitro)** | East Button (B) / Shift | *N/A* |
| **Deploy Oil Slick** | *N/A* | **Left Click** / South Button (A) |
| **Deploy Spikes** | *N/A* | **Right Click** / East Button (B) |
| **Hack Lights** | *N/A* | **E Key** / North Button (Y) |
| **Jam Comms** | *N/A* | **Q Key** / West Button (X) |

---

## ⚙️ Technical Architecture

This project is built for **Unity 6** with a focus on modularity.

### 1. Physics Engine (Custom Raycast)

* **Philosophy:** We avoid `WheelColliders` due to their unpredictability.
* **Suspension:** A simple Raycast system using `Hooke's Law` ($F = -kx - bv$). This gives us complete control over body roll and "bounciness" without physics jitter.
* **Traction:** We use simplified vector math to calculate tire grip, allowing us to "cheat" friction for snappy, arcade-style drifting.

### 2. Input System (`com.unity.inputsystem`)
* **Structure:** A single `.inputactions` asset with two Action Maps: `Driver` and `Operator`.
* **Hot-Swapping:** Uses `PlayerInputManager` to detect devices. The first device pressed joins as Driver; the second joins as Operator.

### 3. Rendering (URP)
* **Camera:** Cinemachine 3 with an Orthographic Lens, rotated 45° X / 45° Y (Isometric).
* **Decals:** Extensive use of **URP Decal Projectors** for:
    * Skid marks (Persistent).
    * Cop vision indicators (Headlight cone zones).
    * Player 2's navigation arrows (projected onto the street surface).

---

## 🗺️ World Design: "The Neon Strip"

* **No Procedural Generation:** The map is a hand-crafted, high-fidelity high-character fun-driving district.
* **Randomized Routing:** While the streets are static, the Start and End points are randomized every run.
* **Dynamic Barriers:** Construction zones and police barricades spawn procedurally to block familiar shortcuts, forcing P2 to constantly update the route.

---

## 🚧 Development Roadmap

### Phase 1: The Chassis (Current Focus)
- [ ] Implement Raycast Suspension (The "Bouncy" feel).
- [ ] Implement Vector-based Drift (The "Snappy" feel).
- [ ] Greybox City Block 01.
- [ ] Setup Cinemachine Isometric Camera.

### Phase 2: The Co-op
- [ ] Input System configuration for Split Control schemes.
- [ ] Player 2 Mouse/Cursor implementation.
- [ ] Basic "Follow" AI for Police.

### Phase 3: The Loop
- [ ] Game Manager (Win/Loss States).
- [ ] Heat System logic.
- [ ] "Safehouse" UI.

---

## 📦 Setup & Installation

1.  Clone the repository.
2.  Open in **Unity 6.3 LTS** (or higher).
3.  Open `Scenes/Prototype/Main_Greybox`.
4.  Connect controllers (or use Keyboard).
5.  Press Play.

---

*Design Document Version: 2.1 (Refined for Clarity & Scope)*
