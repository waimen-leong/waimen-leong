# Hi, I'm Wai Men 👋

**Engine & game programmer** · Year 2 Computer Science (Real-Time Interactive Simulation) @ DigiPen Institute of Technology Singapore

I build the systems underneath a game (ECS, scripting, collision, editor tools) in C++, then use them to ship games people play.

🎯 **Looking for a 1-year game client / engine programming internship starting April 2027.**

[🌐 Portfolio](https://waimen-leong.github.io/) · [📄 Resume](https://waimen-leong.github.io/assets/resume.pdf) · [💼 LinkedIn](https://www.linkedin.com/in/leong-wai-men/) · [✉️ Email](mailto:wai.men.leong@gmail.com)

---

## Start here: three projects

| | Project | What it shows |
|---|---|---|
| <img src="https://waimen-leong.github.io/assets/uma_engine/sc1.png" width="220"> | **[Umapyoi Engine](#-umapyoi-engine--flagship)**<br>🏁 Flagship | A custom C++ engine I led as tech lead (team of 7). Our game *Senki* shipped on it. |
| <img src="https://waimen-leong.github.io/assets/anytimereno/sc1.png" width="220"> | **[AnytimeReno](#-anytimereno--constrained-not-a-game)**<br>🔒 Constrained · not a game | Web app backend on a 2-core VM. Load-tested, then made 4x cheaper per request. **[Try it live](https://team35.dp-ext8.com/)** |
| <img src="https://img.youtube.com/vi/Nwifpq_tkoA/hqdefault.jpg" width="220"> | **[Droom](#-droom--skill-a-pathfinding)**<br>🎯 Skill: A* pathfinding | Doom-style 2.5D raycast shooter in plain C++, with enemies that chase you through the map using A*. |

---

### 🏁 Umapyoi Engine (flagship)
`C++` `OpenGL` `Lua / Sol2` `ImGui` `FMOD` `PlayFab` · Tech lead & engine champion, team of 7, 6 months

- **Problem:** Designers needed to build *Senki*'s levels from nested prefabs (enemy → room full of enemies → scene), with small tweaks per instance.
- **Constraint:** It was my first ECS and my first prefab system, written from scratch while the team built the game on top of it.
- **What failed:** One layer of prefabs worked. Past one layer of nesting, the layers overwrote each other's data, and it was hard to trace which one was doing it.
- **What I changed:** I split loading into two passes. First every entity is created, then overrides are applied in a fixed order from the innermost prefab out to the scene. Each instance stores only the values that differ from its prefab, so every value has one clear owner.
- **Result:** *Senki* shipped on the engine, and the whole team built levels with nested prefabs, not just the programmers.

Also built: ECS core, Lua scripting with hot reload, swept-AABB collision with spatial hashing, undo/redo, tilemap editor.
**[Source](https://github.com/waimen-leong/GAM200-250_UmapyoiEngine)** · [Engine release](https://drive.google.com/file/d/1D6a6KMbOL1d4_uWAjAhwrerCR3GEBXKS/view?usp=sharing) · [Play Senki](https://drive.google.com/file/d/11YZPx1PwK7LOcOR-0EFIoA0tadWIr67W/view?usp=sharing)

### 🔒 AnytimeReno (constrained, not a game)
`Unity WebGL` `C#` `Node.js` `MariaDB` `Docker` `Nginx` `GitHub Actions` · Tech lead, team of 7 (ongoing)

An interior planning web app for homeowners: a 2D floor plan editor with 3D models streamed in at runtime.

- **Problem:** We didn't know how many users the server could take, or what would break first.
- **Constraint:** One school VM with 2 CPU cores, 3.7 GB RAM and a single Node.js process. Argon2 password hashing is CPU-heavy on purpose, so it competes with every other request.
- **What I tested:** k6 load tests from 100 to 800 virtual users on the live server, watching CPU and memory per container.
- **What failed:** At 400 users, p95 latency hit 5.7 s with timeouts. A flood of logins let Argon2 take both cores and slowed every other endpoint.
- **What I changed:** Cached the public model catalogue in memory, turned on nginx-to-Node keepalive, limited Argon2 to one hash at a time behind a 100-slot queue, and gave each container a memory limit.
- **Result:** CPU per request dropped from 5.5 ms to 1.3 ms. The server now handles ~724 req/s at 800 users with 0% errors, and p95 at 400 users fell from 5.7 s to 39 ms.

**[Live site](https://team35.dp-ext8.com/)**

### 🎯 Droom (skill: A* pathfinding)
`C++` · Pathfinding & frontend, 3 months

- **Problem:** In a 2.5D raycast world, enemies have to chase the player through corridors instead of walking into walls.
- **Constraint:** Plain C++ with no engine. Pathfinding runs on the same 2D grid the raycaster draws from, for every enemy in a wave.
- **What failed:** Recomputing every path every frame was wasteful, and enemies on identical paths bunched into one tile.
- **What I changed:** Paths are only recalculated when the player moves to a new grid cell, and enemies spawn from different points so they come from different directions.
- **Result:** Enemies reliably find the player in every wave, even as waves grow.

**[Source](https://github.com/waimen-leong/GAM100_DROOM)** · [Gameplay video](https://www.youtube.com/watch?v=Nwifpq_tkoA) · [Play](https://drive.google.com/file/d/1NZi_sDUouOG3Rsj3D1OXAVRvwAyOr0JO/view?usp=sharing)

---

## Skills

**Languages:** C++, C#, C, Lua, GLSL, SQL
**Engine:** ECS architecture, scripting bindings, serialization, editor tooling, collision & physics
**Graphics:** OpenGL, shaders, culling, instancing, BVH / spatial hashing
**Tools:** ImGui, Sol2, FMOD, PlayFab, GLFW, Git, Docker, Nginx

## Background

- 🎓 BSc Computer Science in Real-Time Interactive Simulation, DigiPen Singapore (2024–2028)
- 💼 Game Developer, Metascape City (2022)
- 🎓 Diploma in Game Development and Technology, Nanyang Polytechnic (2019–2022)

More projects, including a multi-pass rendering pipeline and GLSL experiments, are on my **[portfolio](https://waimen-leong.github.io/)**.
