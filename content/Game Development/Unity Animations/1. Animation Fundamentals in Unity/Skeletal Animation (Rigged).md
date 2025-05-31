### 🧠 What is Skeletal Animation?

Skeletal Animation (also known as **rigged animation**) is a technique used in **3D character animation** where the model is divided into two key parts:

- **Mesh (Skin):** The visual surface of the character.
- **Skeleton (Rig or Armature):** A hierarchy of bones that controls the mesh.

When the bones move, the mesh deforms accordingly, allowing for realistic animation like walking, jumping, waving, etc.

### 🦴 Key Components

|Component|Description|
|---|---|
|**Bone/Joint**|A pivot point that controls parts of the mesh.|
|**Rig**|A skeleton composed of multiple bones.|
|**Skinning**|Binding the mesh to the bones, defining how it deforms with movement.|
|**Weight Painting**|Specifies how much influence each bone has over the vertices of the mesh.|
|**Animator / Animation Controller**|Unity component that manages transitions and playback of animations.|

---

### 🧩 How It Works (Simplified Steps)

1. **3D Artist creates a mesh** in tools like Blender or Maya.
3. **Bones (rig) are added** inside the mesh forming a skeleton.
4. **Mesh is skinned** (bound) to the skeleton.
5. **Animations are created** by rotating and moving bones over time.
6. **Exported as FBX** or similar format and imported into Unity.
7. **Animator Controller in Unity** manages state transitions for different animations (idle, walk, jump, etc.)

---

### 🔧 Unity Integration

```
Assets/
├── Models/
│   └── Character.fbx (includes mesh, bones, and animations)
├── Animations/
│   ├── Idle.anim
│   ├── Walk.anim
│   └── Run.anim
├── Animator/
│   └── CharacterController.controller
```

> 🔗 The FBX file contains the rigged mesh and animations baked into it.

**Workflow in Unity:**
- Import the FBX.
- Drag into the scene.
- Assign an Animator Controller.
- Use the `Animator` component to control animations via scripts or animation events.

---

### 💡 Benefits of Skeletal Animation

- **Reusable:** One rig can be used for multiple animations.
- **Lightweight:** Animations only modify bones, not the entire mesh.
- **Blendable:** Supports blending (e.g., walk + shoot).

---

### 📌 Example Use Cases

- Player Characters
- NPCs (Non-Player Characters)
- Animals
- Mech Robots with joints
---

### 🎥 Visual References

- 📹 [YouTube: Skeletal Animation - From Theory and Math to Code](https://youtu.be/ZzMnu3v_MOw)
- 💻 [Unity Docs: Working with Humanoid Avatars](https://docs.unity3d.com/6000.1/Documentation/Manual/AvatarCreationandSetup.html)
- 🛠️ [Mixamo (Free animated rigs)](https://www.mixamo.com/)
- 📚 [Rigging and Skinning Basics – Blender Manual](https://youtu.be/3RSwjZLClRc)

---

### 📘 Learn More

- [Unity Learn: Rigging and Animation](https://learn.unity.com/tutorial/working-with-animation-rigging)]
- [Mixamo Auto-Rigging Tutorial](https://helpx.adobe.com/creative-cloud/help/mixamo-rigging.html)
- [Blender-to-Unity Workflow](https://www.youtube.com/watch?v=llxG3REr3bY)

---

### 🧠 Tips for Learning

- Start with **humanoid rigs**; Unity has a built-in Humanoid system.
- Use **Mixamo** to quickly get characters and animations.
- Try **blending animations** in Unity using Animator Layers and Blend Trees.
- Practice exporting from Blender or Maya to Unity.