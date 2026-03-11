# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?


- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").

The first time I ran the game, it opened in the browser and showed a number guessing interface along with a developer debug panel. One bug I noticed was that the guess history was not stored correctly, where several guesses appeared together as one string instead of separate numbers. Another issue was that the score became negative, which does not make sense for a guessing game. I also noticed that the attempt counter did not match the guesses shown in the history, which means the game was not tracking attempts properly.


## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

I used ChatGPT to help understand errors, interpret the debug output, and identify possible bugs in the game. One correct suggestion from the AI was that the guess history issue might be caused by storing guesses as a string instead of a list, and I verified this by looking at the debug output where guesses appeared grouped together. One suggestion that was not fully accurate was when the AI assumed certain problems in the code before seeing the actual app.py file. I verified this by running the game and comparing the results to the AI’s explanation to see which issues were actually happening.

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed by running the game again and checking whether the behavior changed as expected. For example, I tested the guess history by entering several guesses and observing if each guess appeared correctly in the history list. This manual testing helped confirm whether the bug was still present or had been resolved. AI also helped me think of different test cases, such as entering multiple guesses or restarting the game to check if the score and attempts updated correctly.

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

I learned that **Streamlit reruns the entire script every time the user interacts with the app, such as when entering a guess or clicking a button. Because of this, variables can reset unless they are stored in session state. Session state allows the app to remember values like the secret number, score, and guess history between interactions. Without using session state, the game would lose its progress every time the page updates.

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse in future projects is testing programs carefully by trying different inputs and observing the results. This helped me identify problems like incorrect guess history and inconsistent scoring. Next time I work with AI on a coding task, I will verify its suggestions more carefully instead of assuming they are always correct. This project helped me realize that AI can assist with debugging ideas, but developers still need to test and understand the code themselves.

## Step 3: Ask AI for Help

I used GitHub Copilot in Visual Studio Code to help explain one of the glitches I noticed in the game. I used the variables #file:app.py and #file:logic_utils.py so Copilot could analyze the project code. I asked Copilot to explain why the guess history looked incorrect and why multiple guesses sometimes appeared as one entry.

Copilot explained that the game stores guesses in a list called history, but two different types of values are added to it. When the input is valid, the guess is stored as an integer, but when the input is invalid the program appends the raw string directly to the history list. Because of this, the list becomes a mixture of integers and strings.

This causes entries like "50 80 60 90 95" to appear as a single item instead of separate guesses. Copilot pointed out that the issue likely comes from the line `history.append(raw_guess)` in the invalid input branch of the code. This helped me understand that invalid inputs should not be added to the history list or should be handled differently to prevent corrupting the guess history.