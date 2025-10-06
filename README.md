# HexSoftwares_Project_MEMORY-PUZZLE-GAME
Sure 😊 Here’s a **formatted explanation** for your **Memory Puzzle Game** — just like the rent calculation example you showed.

---

## 🧠 Memory Puzzle Game

### **Program Code**

```python
import tkinter as tk
from tkinter import messagebox
import random

class MemoryGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Memory Puzzle Game 🧩")
        self.root.geometry("400x450")
        self.root.resizable(False, False)

        self.buttons = []
        self.first_card = None
        self.second_card = None
        self.flipped = []
        self.time_left = 60  # seconds

        self.symbols = ['🍎', '🍌', '🍇', '🍓', '🍉', '🍒', '🍍', '🥭']
        self.symbols *= 2  # make pairs
        random.shuffle(self.symbols)

        self.create_widgets()
        self.update_timer()

    def create_widgets(self):
        self.timer_label = tk.Label(self.root, text=f"Time left: {self.time_left}s", font=("Arial", 14, "bold"))
        self.timer_label.pack(pady=10)

        frame = tk.Frame(self.root)
        frame.pack()

        for i in range(4):
            row = []
            for j in range(4):
                btn = tk.Button(frame, text="❓", width=6, height=3,
                                font=("Arial", 16, "bold"),
                                command=lambda r=i, c=j: self.on_click(r, c))
                btn.grid(row=i, column=j, padx=5, pady=5)
                row.append(btn)
            self.buttons.append(row)

    def on_click(self, r, c):
        if (r, c) in self.flipped:
            return  # already matched

        current_btn = self.buttons[r][c]
        current_symbol = self.symbols[r * 4 + c]

        if not self.first_card:
            self.first_card = (r, c)
            current_btn.config(text=current_symbol, state="disabled")
        elif not self.second_card and (r, c) != self.first_card:
            self.second_card = (r, c)
            current_btn.config(text=current_symbol, state="disabled")
            self.root.after(600, self.check_match)

    def check_match(self):
        r1, c1 = self.first_card
        r2, c2 = self.second_card
        s1 = self.symbols[r1 * 4 + c1]
        s2 = self.symbols[r2 * 4 + c2]

        if s1 == s2:
            self.flipped.append(self.first_card)
            self.flipped.append(self.second_card)
        else:
            self.buttons[r1][c1].config(text="❓", state="normal")
            self.buttons[r2][c2].config(text="❓", state="normal")

        self.first_card = None
        self.second_card = None

        if len(self.flipped) == len(self.symbols):
            messagebox.showinfo("Congratulations!", "🎉 You matched all pairs!")
            self.root.destroy()

    def update_timer(self):
        if self.time_left > 0:
            self.time_left -= 1
            self.timer_label.config(text=f"Time left: {self.time_left}s")
            self.root.after(1000, self.update_timer)
        else:
            messagebox.showinfo("Time's Up!", "⏰ You ran out of time!")
            self.root.destroy()


if __name__ == "__main__":
    root = tk.Tk()
    game = MemoryGame(root)
    root.mainloop()
```

---

### **Explanation**

This program creates a **Memory Puzzle Game** using Python’s `tkinter` GUI library.
The goal is to match all pairs of cards before the **timer runs out**.

#### **Main Components**

1. **tkinter GUI** – used to create the window and buttons (cards).
2. **Random symbols** – a set of emojis are duplicated and shuffled to create random pairs.
3. **Button clicks** – when a player clicks a card, it flips to reveal its symbol.
4. **Match checking** – if two opened cards have the same symbol, they remain visible; otherwise, they flip back.
5. **Timer** – the player has 60 seconds to complete the game.

---

### **Key Variables**

| Variable                              | Description                                 |
| ------------------------------------- | ------------------------------------------- |
| `self.symbols`                        | List of symbols (emojis) used for the cards |
| `self.buttons`                        | 4×4 grid of buttons representing cards      |
| `self.first_card`, `self.second_card` | Store coordinates of selected cards         |
| `self.flipped`                        | Keeps track of matched cards                |
| `self.time_left`                      | Countdown timer (60 seconds)                |

---

### **Input and Output**

**Input:**

* The player interacts with the GUI by clicking on cards.
* No keyboard input is required.

**Output:**

* Displays messages:

  * “🎉 You matched all pairs!” (on win)
  * “⏰ You ran out of time!” (on timeout)

---

### **Game Flow**

1. The cards are hidden initially.
2. Player clicks two cards to flip them.
3. If they match → stay open.
4. If not → flip back after 0.6 seconds.
5. Continue until all pairs are found or the timer ends.

---

### **Test Cases**

| Player Action                               | Expected Output           | Explanation                  |
| ------------------------------------------- | ------------------------- | ---------------------------- |
| Player matches all pairs before timer ends  | 🎉 You matched all pairs! | Win condition                |
| Player fails to match all before 60 seconds | ⏰ You ran out of time!    | Lose condition               |
| Player clicks same card twice               | Ignored                   | Prevents duplicate selection |

---

### **Conclusion**

This code is a simple yet interactive **memory puzzle game** built using Python’s `tkinter`.
It helps improve memory and focus while demonstrating key programming concepts like:

* Event handling
* Loops
* Condition checking
* GUI creation

It’s beginner-friendly, visually engaging, and a great introduction to Python GUI programming.

---


