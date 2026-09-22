# Fishing Clicker

### Unity
- Project developed in Unity.
- Use C#.
- Avoid creating unnecessary dependencies.
- Prefer composition over inheritance when appropriate.

### Architecture
- Gameplay systems reside in Assets/_Project/Scripts.
- Configurable data should preferably use ScriptableObject.
- UI should not contain gameplay logic.
- Gameplay systems should not directly depend on UI components.

### Save
- Do not alter the existing SaveData format without justification.
- All new persistent information should be added to the save system.
- Maintain compatibility with existing saves whenever possible.

### Naming
- Classes: PascalCase
- Methods: PascalCase
- Private fields: _camelCase
- Interfaces begin with I.

### Before modifying
- First analyze the related scripts.
- Do not rewrite existing systems unnecessarily.
- Preserve existing public APIs whenever possible. 

### After modifying
- Summarize the modified files.

### Unity Project Scope

- Treat this repository as a Unity project first.
- Follow Unity-first workflows for gameplay, scenes, prefabs, assets, and C# scripts.
- Prefer Unity MCP tooling for validation, inspection, and editor-safe automation when useful.
- Never userot net commands to validate. Use Unity MCP instead.
- Do not hand-author or manually edit .meta files.
- Unity-generated `.meta` files are expected and valid when Unity creates them (for example, after adding new scripts/assets).

### Input System Standard (Mandatory)
- Always use the Input System Package (New)`.
- Do not introduce or rely on the legacy Input Manager (UnityEngine. Input old system) for new work.
- If touching input-related code, align it with the New Input System patterns already used in the project.

### UI
- Use **Unity uGUI** (`com.unity.ugui`) for runtime UI.
- **Do not use UI Toolkit** unless explicitly requested.
- Use **TextMeshPro** (`com.unity.textmeshpro`) for all UI text.
- Use `TextMeshProUGUI` for text inside a `Canvas`.
- Do not use the legacy `UnityEngine.UI.Text`.
- Prefer `[SerializeField]` references over `Find`, `GetComponent`, or similar runtime searches.
- Follow the project's existing UI architecture and screen-management patterns.
- Keep UI logic separate from gameplay/domain logic.

### Self-Improvement Loop
- After ANY correction from the user: update tasks/lessons.md with the pattern
- Write rules for yourself that prevent the same mistake 
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start for relevant project

### Verification Before Done
- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness
- Use unity mcp if needed to verify changes

### Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution" Skip this for simple, obvious fixes don't over-engineer
- Challenge your own work before presenting it

### Autonomous Bug Fixing
- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests then resolve them
- Zero context switching required from the user
- Go fix failing CI tests without being told how

### Subagent Strategy
- Spawn subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents 
- For complex problems, throw more compute at it via subagents 
- One task per subagent for focused execution