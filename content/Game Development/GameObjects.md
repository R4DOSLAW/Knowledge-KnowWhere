### 🎮 GameObject

A **GameObject** is the fundamental object in Unity scenes. It represents characters, cameras, lights, etc.

> Animations in Unity are **always applied to GameObjects** (and their components).

#### Example:

- `Player` GameObject has:
    - Animator Component
    - Rigidbody
    - Collider

```plaintext
Player (GameObject)
├── Animator (Component)
├── Script: PlayerController.cs
├── Collider
```
You can animate:

- The GameObject's **transform**
- Child bones or objects  
- Attached components (e.g., material color, custom scripts) 

#### 🎥 Visual Reference:

- 📘 Unity Learn: GameObjects and Components