### 🧠 Animator Component

The **Animator** is a **Unity component** added to a GameObject that plays animations from the Animator Controller.

```csharp
Animator animator = GetComponent<Animator>();
animator.SetFloat("Speed", 5f);
```
#### 🧩 Key Features:

- Connects to the Animator Controller asset
- Runs state machine logic
- Can be controlled via C# script

#### 📦 Typical Folder Setup:

```plaintext
Assets/
├── Animations/
│   ├── Idle.anim
│   ├── Walk.anim
├── Animator/
│   └── PlayerController.controller
├── Prefabs/
│   └── Player.prefab (has Animator component)
```
#### 🎥 Visual Example:

- 🔗 Unity Docs: Animator

[[Animator State Machine Behaviour]]