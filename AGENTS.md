### Unity & C# Coding Standards
- Project developed in Unity.
- Use C#.
- **Always ensure all curly braces `{ }` are properly closed in scripts.** Never provide truncated code snippets missing their closing braces or namespace/class closures.
- Avoid creating unnecessary dependencies.
- Prefer composition over inheritance when appropriate.

### Architecture & Structure
- Follow the project's existing folder structure for gameplay systems (e.g., `Assets/Scripts` or `Assets/_Project/Scripts`).
- Always wrap new scripts in appropriate `namespace` blocks. Namespaces should generally follow the project's root namespace or mirror the folder structure.
- Configurable data should preferably use `ScriptableObject`.
- UI should not contain gameplay logic.
- Gameplay systems should not directly depend on UI components. Use events, interfaces, or mediators.

### Performance & Memory
- Strictly avoid Garbage Collection (GC) allocations in hot paths (`Update`, `FixedUpdate`, `LateUpdate`).
- Do not use `new`, string concatenations, or LINQ inside update loops.
- Use Object Pooling for any entity that is frequently created and destroyed (e.g., bullets, enemies, floating text).

### Asynchronous Operations
- Analyze the project to see if it relies on standard `IEnumerator` Coroutines, `async/await` Tasks, Unity 6 `Awaitable`, or third-party solutions like `UniTask`.
- Do not mix paradigms unless explicitly requested. Follow the established async pattern of the project.

### Prefabs, Scenes, and Assets
- **NEVER** attempt to manually edit `.prefab`, `.unity`, `.controller`, or `.asset` files as raw text/YAML using standard file-editing tools. You will corrupt the complex FileIDs and GUIDs.
- To modify these files, you must ALWAYS use specific Unity MCP tools that interface with the Unity Editor API, OR write a temporary C# Editor script (`MenuItem`) to apply the changes safely via code.

### Unity Project Scope
- Treat this repository as a Unity project first.
- Follow Unity-first workflows for gameplay, scenes, prefabs, assets, and C# scripts.
- Prefer Unity MCP tooling for validation, inspection, and editor-safe automation when useful.
- Never use `dotnet` commands to validate or build. Use Unity MCP instead.
- Do not hand-author or manually edit `.meta` files.
- Unity-generated `.meta` files are expected and valid when Unity creates them (for example, after adding new scripts/assets).

### Input System Standard
- First, determine if the project uses the **Legacy Input Manager** or the **New Input System Package**.
- Stick to the project's established standard. Do not mix both systems unless migrating by explicit request.
- If it's a new project or migration, prefer the **New Input System Package**.

### UI Standard
- Identify if the project uses **Unity uGUI** or **UI Toolkit**. Follow the established standard.
- If using **uGUI**:
  - Use **TextMeshPro** (`com.unity.textmeshpro`) for all UI text (`TextMeshProUGUI`).
  - Do not use the legacy `UnityEngine.UI.Text`.
- Prefer `[SerializeField]` references over `GameObject.Find`, `GetComponent`, or similar runtime searches.
- Keep UI logic (presentation) strictly separate from gameplay/domain logic.

### Save System
- Respect the project's existing save architecture.
- Do not alter existing save formats or structures without justification.
- All new persistent information should be added to the current save system.
- Maintain compatibility with existing saves whenever possible.

### Naming Conventions
- Classes: `PascalCase`
- Methods: `PascalCase`
- Private fields: `_camelCase`
- Interfaces: Begin with `I` (e.g., `IInteractable`).

### Before Modifying
- First analyze the related scripts and how they fit into the broader architecture.
- Do not rewrite existing systems unnecessarily.
- Preserve existing public APIs whenever possible to avoid breaking other dependencies. 

### After Modifying
- Summarize the modified files and briefly explain the reasoning behind architectural choices.

### Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` (or the project's equivalent tracking file) with the pattern.
- Write rules for yourself that prevent the same mistake.
- Ruthlessly iterate on these lessons until the mistake rate drops.
- Review lessons at the session start for the relevant project.

### Verification Before Done
- Never mark a task complete without proving it works.
- Diff behavior between the main branch and your changes when relevant.
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, and demonstrate correctness.
- Use Unity MCP if needed to verify changes.

### Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "Is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution." 
- Skip this for simple, obvious fixes—don't over-engineer.
- Challenge your own work before presenting it.

### Autonomous Bug Fixing
- When given a bug report: just fix it. Don't ask for hand-holding.
- Point at logs, errors, failing tests, and then resolve them.
- Zero context switching required from the user.
- Go fix failing CI tests without being told how.

### Subagent Strategy
- Spawn subagents liberally to keep the main context window clean.
- Offload research, exploration, and parallel analysis to subagents. 
- For complex problems, throw more compute at it via subagents. 
- One task per subagent for focused execution.
