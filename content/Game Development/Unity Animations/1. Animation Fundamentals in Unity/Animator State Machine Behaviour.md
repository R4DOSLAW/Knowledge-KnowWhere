### 📌 What is an Animator State Machine Behaviour?

An **Animator State Machine Behaviour** (SMB) is a **C# script attached to an animation state** in the Animator Controller. It allows you to run custom logic **when an animation state starts, updates, or exits** — without putting all animation logic inside your main `MonoBehaviour` scripts.

> 🎯 Think of SMBs as per-state mini-scripts that run only when needed.

---

### 📦 Where It Lives

- Inside the **Animator Controller**
- Attached directly to an **animation state**

> ✅ NOT a component on a GameObject — it lives in the Animator asset.

---

### 🧩 Core Methods in SMB

```csharp
public class MyStateBehavior : StateMachineBehaviour
{
    public override void OnStateEnter(Animator animator, AnimatorStateInfo stateInfo, int layerIndex) { }
    public override void OnStateUpdate(Animator animator, AnimatorStateInfo stateInfo, int layerIndex) { }
    public override void OnStateExit(Animator animator, AnimatorStateInfo stateInfo, int layerIndex) { }
}

```

|Method|Description|
|---|---|
|`OnStateEnter`|Called when state starts. Use for setup.|
|`OnStateUpdate`|Called every frame while the state is active.|
|`OnStateExit`|Called when state finishes. Use for cleanup.|
|`OnStateMove`|Called for root motion processing. (optional)|
|`OnStateIK`|Called for IK processing. (optional)|

---

### 🛠️ Example Use Case: Trigger Sound When Running Starts

#### Step 1: Create the script

```csharp
using UnityEngine;

public class RunSoundBehavior : StateMachineBehaviour
{
    public AudioClip runSound;
    private AudioSource audioSource;

    public override void OnStateEnter(Animator animator, AnimatorStateInfo stateInfo, int layerIndex)
    {
        if (audioSource == null)
            audioSource = animator.GetComponent<AudioSource>();

        if (runSound != null && audioSource != null)
            audioSource.PlayOneShot(runSound);
    }
}
```
#### Step 2: Attach it to a state

- Open your **Animator Controller**
    
- Click on the **Run** animation state
    
- In the **Inspector**, click "Add Behaviour"
    
- Select your custom script (e.g. `RunSoundBehavior`)

---

### 🎮 Example Use Case: Play Particle FX on Landing

```csharp
public class LandingEffectBehaviour : StateMachineBehaviour
{
    public GameObject landingEffect;

    public override void OnStateEnter(Animator animator, AnimatorStateInfo stateInfo, int layerIndex)
    {
        Transform feet = animator.transform.Find("Feet");
        if (landingEffect && feet)
        {
            GameObject.Instantiate(landingEffect, feet.position, Quaternion.identity);
        }
    }
}
```
---

### 🧠 When to Use SMBs

|Use SMB If...|Avoid SMB If...|
|---|---|
|You want logic tied directly to a state.|You need full gameplay control.|
|You want separation of concerns.|You need a lot of shared state access.|
|You want to react to state enter/exit.|You need performance optimization.|

---

### 🎥 Visual References

- [📺 Unity Official: StateMachineBehaviour Explained](https://www.youtube.com/watch?v=ZxFJ_MkY3EQ)
    
- 📘 Unity Docs: StateMachineBehaviour
    

---

### 🧰 Folder Example

```plaintext
Assets/
├── Animations/
│   ├── Jump.anim
├── Animator/
│   ├── Player.controller
│   └── RunSoundBehavior.cs
```
---

### 💡 Tips

- Use `animator.GetComponent<T>()` carefully — cache references when possible.
    
- Good for:
    - Playing sounds
    - Triggering particles
    - Resetting values
    - IK logic
        
- Don’t overuse for complex logic — prefer using your main `MonoBehaviour` scripts for full gameplay logic.

---

### 🔁 Related Concepts

- [[Animator Controller]]
- [[Animator]]
- [[Animation Events]] — an alternative to SMBs for clip-specific callbacks.