# ✍️ Pseudo CNC Bot (Test1.ino)

This Arduino-based pseudo-CNC bot is designed to draw numbers and alphabets on a sheet of paper using stepper motors and a servo motor. The bot interprets specific function calls as drawing instructions and translates them into coordinated motor movements to replicate characters in a 2D space.

---

## 🔧 Hardware Used

- 2 × NEMA 17 Stepper Motors (for X and Y axis movement)
- 1 × Servo Motor (for pen up/down mechanism)
- L298N Motor Driver or similar (to drive stepper motors)
- Arduino-compatible microcontroller (tested on Arduino Uno)
- Breadboard, Jumper Wires, Power Supply

---

## 📜 Code Overview (Test1.ino)

### 📁 Structure

- **Character Drawing Functions:** `num0()` to `num9()` and `alpA()` to `alpZ()` implement the drawing of each character by invoking movement functions in specific sequences.
- **Movement Functions:** `xmovef()`, `xmoveb()`, `ymovef()`, `ymoveb()` move the bot in the four cardinal directions.
- **Diagonal Movements:** `northeast()`, `northwest()`, `southeast()`, `southwest()` create diagonal strokes using simultaneous X and Y movements.
- **Pen Control:**
  - `zd()` lowers the pen to start drawing.
  - `zu()` lifts the pen to move without drawing.
- **Serial Input:** Listens to characters over `Serial1` and performs basic servo or motor actions (for future command parsing).

---

## ✏️ How Characters are Drawn

Each alphabet and number is represented as a function (e.g., `alpA()` for 'A') containing a sequence of directional motor calls. These simulate pen strokes in a 2D space. The servo controls the pen state (up/down), mimicking how CNC or plotter machines operate.

### Example: Drawing the Number `0`
```
void num0() {
  zd();           // Pen down
  ymoveb(4);
  xmovef(4);
  ymovef(4);
  xmoveb(4);
  southeast(4*r2);
  zu();           // Pen up
  ymovef(4);
}

```

# 🚀 How to Use

1. Upload `Test1.ino` to your Arduino board.  
2. Connect your stepper and servo motors as per the pin mappings in the code.  
3. Power on the setup and open Serial Monitor (or use `Serial1` from another microcontroller).  
4. Send characters over serial (`a`, `b`, `1`, `2`, etc.) to test responses.  
5. Call drawing functions in the code manually or via custom input parsing.

---

# 🛠️ Pin Mapping

| Function        | Pins Used       |
|----------------|-----------------|
| X-Axis Motor   | 3, 4, 5, 6      |
| Y-Axis Motor   | 7, 8, 9, 10     |
| Servo          | Connected to `my` object pin (assign in `setup()`) |

---

# 🧠 Concepts Used

- Stepper motor control using digital pin sequencing.  
- Basic kinematics in 2D space.  
- Character stroke decomposition into motor instructions.  
- Diagonal movement using a ratio constant (`r2 = 0.9`) to preserve proportional speed.  
- Modular design for extensibility.

---

# 📦 Future Improvements

- Add complete support for all alphabets and symbols.  
- Implement input string parsing and automatic letter rendering.  
- Add line/curve interpolation for smoother strokes.  
- Optimize diagonal movement speeds.

---

---

# 🙌 Acknowledgements

This project was inspired by the desire to bridge embedded systems with creative applications like handwriting simulation and CNC principles.
