### 🎛 Animator Controller

An **Animator Controller** is a **state machine** that manages which animation clips play, and how they transition based on parameters.

> Think of it as the "brain" managing the logic of animations.

#### Components:

- **States**: Idle, Walk, Jump
- **Transitions**: Rules that move from one state to another
- **Parameters**: Triggers, floats, bools, and ints

#### 🎮 Example Setup:
```plaintext
Animator Controller:
  States: Idle, Walk, Run
  Transitions:
    Idle → Walk (if Speed > 0.1)
    Walk → Run (if Speed > 3.0)
```
#### 🎥 Visual Example:

- 🎬 Unity Animator Controller Overview