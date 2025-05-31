## 🧠 Procedural Animation in Unity

### 📌 What is Procedural Animation?

**Procedural Animation** is a technique where animations are **generated through code or algorithms at runtime** rather than being pre-made in animation tools like Blender or Maya.

Unlike skeletal animation (which relies on keyframes), procedural animation **dynamically calculates** motion based on rules, inputs, or physics.

---

### 🧩 Key Characteristics

|Feature|Description|
|---|---|
|**No keyframes**|Movement is generated using math or logic.|
|**Runtime-driven**|Animation adapts in real-time (e.g., based on physics or AI decisions).|
|**Flexible**|Great for non-standard or interactive movement.|
|**Customizable**|Behavior can be tweaked via scripts or parameters.|

---

### 🛠️ Common Techniques

- **Inverse Kinematics (IK)**  
    Adjusts joints so hands/feet reach specific targets (e.g., placing feet on uneven ground).

- **Perlin Noise**  
    Used for smooth, organic movements (e.g., idle breathing, tentacle motion).

- **Math-based Oscillation**  
    Sin/Cos functions used for bobbing, swinging, etc.

- **Physics-Based Movement**  
    Characters/objects animated via Unity's Rigidbody system.

---

### 🔧 Unity Examples (Code Snippets)

#### 1. Head Bobbing (First-Person Camera)

```csharp
float bobSpeed = 5f;
float bobAmount = 0.05f;
float timer = 0f;

void Update()
{
    timer += Time.deltaTime * bobSpeed;
    float bob = Mathf.Sin(timer) * bobAmount;
    cameraTransform.localPosition = new Vector3(0, baseHeight + bob, 0);
}
```

#### 2. Tentacle Movement with Perlin Noise
```csharp
float noiseSpeed = 1.0f;
float noiseStrength = 15.0f;

void Update()
{
    float angle = Mathf.PerlinNoise(Time.time * noiseSpeed, 0f) * noiseStrength;
    transform.localRotation = Quaternion.Euler(0, angle, 0);
}
```


#### 3. Inverse Kinematics (Unity's Animator IK)
```csharp
void OnAnimatorIK(int layerIndex)
{
    animator.SetIKPositionWeight(AvatarIKGoal.LeftHand, 1f);
    animator.SetIKPosition(AvatarIKGoal.LeftHand, target.position);
}
```

---

### 🎮 Use Cases

- Foot placement on uneven terrain (IK).
- Physics-driven ragdoll effects.
- Breathing or idle motions.
- Dynamic reactions (e.g., hit reactions).
- Procedural terrain deformation.

---

### 📽️ Visual References

- 📹 [Giving Personality to Procedural Animations using Math](https://www.youtube.com/watch?v=KPoeNZZ6H4s)
- 🌐 [Unity Docs: Inverse Kinematics](https://docs.unity3d.com/6000.1/Documentation/Manual/InverseKinematics.html)
- 🎮 [Game Dev Guide: Procedural Animation](https://www.youtube.com/watch?v=XoGgQ-Qg_W0)

---

### 💡 Tips

- Combine procedural + keyframe animations for hybrid systems (e.g., base idle + procedural head turn).
- Keep things **modular and parametric** — makes tweaking easier.
- **Use Gizmos and Debug.DrawLine** to visualize bone/IK chains while developing.

---

### ✅ Advantages

- Highly **interactive and dynamic**.
- Reduces need for large animation libraries.
- Great for **non-repetitive or emergent** behaviors.

---

### ❌ Challenges

- Requires more **programming/math knowledge**.
- Harder to preview/edit compared to traditional animations.
- Debugging can be tricky.