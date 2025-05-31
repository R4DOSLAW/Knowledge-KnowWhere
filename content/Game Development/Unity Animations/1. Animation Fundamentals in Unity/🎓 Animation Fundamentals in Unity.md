In this section, I will learn and understand Unity's core animation tools and systems.
This will help me get comfortable with how animations are created, controlled, and blended inside Unity, from importing a character to making it move with logic.

---
### **1. Learning the Difference Between Skeletal and Procedural Animation**

#### 🧠 What I’m Learning:

- **[[Skeletal Animation (Rigged)]]**:  
    This is animation done using a skeleton (bones) inside a mesh. A rigged mesh is deformed by bones (transforms) that animate over time using keyframes. Most characters (humanoids, animals, creatures) use skeletal animation.
    
- **[[Procedural Animation]]**:  
    This is movement generated in real-time by code or mathematical functions. It’s often used for physics-driven effects (camera shake, recoil), secondary motion (tail sway), or non-human patterns (tentacle motion, snake slithering).
    

> [!done] Summary:
>- Skeletal = keyframe-driven, pre-made animations (e.g., from Mixamo)
>- Procedural = code-driven, often dynamic and adaptive

---

### **2. Get Familiar with Animator, Animator Controller, and Animation Clips**

#### 🧠 What I’m Learning:

Unity uses a **[[Component-Based Animation System]]**:

- **[[Animation Clip]]**: A file that stores [[Keyframes]] (e.g., a walk cycle).
    
- **[[Animator Controller]]**: A state machine that holds logic to switch between clips.
    
- **[[Animator]]**: A component attached to [[GameObjects]] that plays the controller.
    
#### 🔁 Full Animation Flow
```plaintext
GameObject
  └── Animator (Component)
        └── Animator Controller (.controller)
              ├── States (Animation Clips)
              ├── Transitions
              └── Parameters
```

#### C# Scripting Example:
```csharp
Animator animator = GetComponent<Animator>();

if (Input.GetKeyDown(KeyCode.Space))
{
    animator.SetTrigger("Jump");
}
```

---

## 💡 Tips

- Always test animation transitions in Play Mode.
    
- Use **Animator Parameters** for dynamic control.
    
- Preview `.anim` clips using the **Animation window**.
    
- Combine with **Root Motion** for realistic movement.
    
- Consider using **Animation Rigging** for procedural blend-ins.

#### 🛠 Tutorial Steps in Unity:

1. **Create a new Unity project** (3D template).
    
2. **Create a test object**:
    
    - Right-click in Hierarchy → `3D Object > Capsule`
        
3. **Open [[Animation]] window**:
    
    - `Window > Animation > Animation`
        
4. **Create a new [[Animation Clip]]**:
    
    - Select the Capsule.
        
    - In Animation window, click `Create`, name it `Idle`.
        
    - Record basic keyframes (e.g., scale up/down slightly).
        
5. **Unity auto-creates Animator + Controller**
    
    - The clip is added to the default state in the Animator Controller.
        
6. **Create another clip** (e.g., `Jump`, or `Stretch`):
    
    - Use dropdown in Animation window → `Create New Clip`
        
7. **Open Animator Controller**:
    
    - `Window > Animator`
        
    - Add transitions between Idle ↔ Jump
        

#### ✅ Goal:

Understand how to manually create animations, assign them, and build logic between them.

---

### **3. Explore [[Timeline]] and [[Cinemachine]] Basics**

#### 🧠 What I’m Learning:

- **[[Timeline]]** lets me create cinematic sequences (camera pans, animation events, audio sync).
    
- **[[Cinemachine]]** gives me powerful, smooth virtual cameras.
    

#### 🛠 Tutorial Steps:

1. **Install [[Cinemachine]]**:
    
    - `Window > Package Manager > Cinemachine > Install`
        
2. **Create a [[Timeline]] sequence**:
    
    - Add a [[GameObject]] → Right-click → `Create Empty` → Name: `Director`
        
    - Select it → `Add Component > Playable Director`
        
    - Click `Create` [[Timeline]] → Save as `MyCutscene`
        
3. **Add a character or camera** to Timeline:
    
    - Drag Main Camera or character into Timeline tracks
        
    - Right-click track → Add [[Animation]] or [[Activation track]]
        
4. **Create a [[Cinemachine]] camera**:
    
    - `GameObject > Cinemachine > Virtual Camera`
        
    - Assign `Look At` and `Follow` targets (like a character)
        
    - Switch between cameras using Timeline for cinematic effect
        

#### ✅ Goal:

Learn how to make Unity cutscenes, using virtual cameras and timeline events.

---

### **4. Import a Character from [[Mixamo]] and Test Animations**

#### 🧠 What I’m Learning:

Mixamo provides free, ready-to-use rigged humanoids and animation clips (idle, run, jump).

#### 🛠 Tutorial Steps:

1. **Go to [Mixamo](https://www.mixamo.com/)** → Sign in
    
2. **Pick a character** (e.g., Y-Bot or custom upload)
    
3. **Choose animations**:
    
    - Search for "Idle", "Walk", "Run"
        
    - Download with settings:
        
        - Format: `FBX for Unity`
            
        - Skin: `With Skin` (only once, for the base model)
            
        - Frame Rate: 30 fps
            
4. **Import into Unity**:
    
    - Drag [[FBX]] files into Unity’s Assets folder
        
    - Select model → In Inspector:
        
        - `Rig` tab → Set `Animation Type: Humanoid` → Apply
            
        - `Animations` tab → Check loop time, if needed
            
5. **Create [[Animator Controller]]**:
    
    - Right-click → `Create > Animator Controller`
        
    - Assign to the imported character's `Animator` component
        
6. **Assign animations to states** in Animator Controller
    

#### ✅ Goal:

See a Mixamo character moving inside Unity using downloaded animations.

---

### **5. Understand and Use [[Blend Trees]]**

#### 🧠 What I’m Learning:

**[[Blend Trees]]** let me transition smoothly between animations based on parameters (e.g., movement speed).

- Instead of jumping directly between "Idle", "Walk", "Run", I can blend them.
    
- Controlled via a float parameter like "Speed"
    

#### 🛠 Tutorial Steps:

1. **Create a new Blend Tree**:
    
    - Open [[Animator Controller]]
        
    - Right-click → `Create State > From New Blend Tree`
        
    - Double-click to enter Blend Tree editor
        
2. **Set Blend Type** to `1D`
    
    - Parameter: `Speed` (float)
        
    - Add `Idle`, `Walk`, `Run` animation clips
        
    - Set thresholds (e.g., 0 = Idle, 1 = Walk, 3 = Run)
        
3. **Write a basic C# script** to control the parameter:
    
``` csharp
public class CharacterAnimator : MonoBehaviour
{
    public Animator animator;
    public float speed;

    void Update()
    {
        float input = Input.GetAxis("Vertical");
        speed = Mathf.Abs(input) * 3f; // scale to run speed
        animator.SetFloat("Speed", speed);
    }
}
```

4. **Attach script** to your character and assign the Animator in the Inspector

#### ✅ Goal:

Control animation transitions based on player input using a smooth blend tree system.

---

### 🧪 Practical Project

> I will build a small test scene with a [[Mixamo]] character that can **walk**, **run**, and **idle**.  
> Input (WASD or arrow keys) will control the animation through a Blend Tree.  
> The goal is to get a smooth transition between animations based on movement speed.

---

