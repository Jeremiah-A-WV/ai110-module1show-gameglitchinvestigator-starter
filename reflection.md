# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?
The game loaded visually, but mechanically it was entirely unplayable. The most obvious bug was that the hints were backwards; it told me to go lower when I used the minimum value of 1. Second, the hints acted erratically on even/odd attempts because the secret number was being converted to a string, which caused python to incorrectly evaluate lexicographical order (e.g. "9" > "50").

---

## 2. How did you use AI as a teammate?
I used AI to help me quickly verify Streamlit state management behaviors and recall how `st.session_state` preserves data across UI interaction reruns. A correct AI suggestion was to ensure that all my variables, such as `status` and `history`, get reset natively within the `if new_game:` block to fully restore game functionality.

---

## 3. Debugging and testing your fixes
I decided the code was fixed when I could successfully play a whole round with logical clues, win the game, and accurately restart it using the "New Game" button. I utilized `pytest` by updating `test_game_logic.py` to unpack the tuple that `check_guess()` returned; running the test showed me that my underlying comparison logic in `logic_utils.py` worked perfectly independently from the Streamlit UI.

---

## 4. What did you learn about Streamlit and state?
The secret number appeared to "change" because the AI's code converted the integer into a string every other attempt, completely ruining numeric comparisons and causing the hints to bounce around erratically. I would explain Streamlit to a friend as a script that reads and runs top-to-bottom every time you click a button; `st.session_state` is simply a special backpack the script wears so it doesn't forget its belongings (variables) on its next run down. Removing the string conversion and storing the secret properly fixed the erratic behavior.

---

## 5. Looking ahead: your developer habits
A habit I definitely want to reuse is separating my core logic into a separate utility file (`logic_utils.py`) to keep the frontend clean and heavily unit-testable. Next time I work with AI, I will immediately write tests for the logic it generates before attaching it to a UI. This project highlighted that AI-generated code might *look* robust and contain error handling blocks, but can house subtle, game-breaking logic flaws that only a human developer can architect properly.