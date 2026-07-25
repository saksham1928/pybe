# PyBe Error Handling Unit Plain-English-First Roadmap (Levels 1–4)

## Design Notes

Error Handling is PyBe's fifth unit, following Loops, Conditionals, Functions, and String Manipulation. The same three-stage engine applies:

1. **Logic Test (plain English)** Attempt 1, and Attempt 2 if needed, ask the learner to choose an approach for dealing with things going wrong, described entirely in plain English never as Python syntax.
2. **Concept Reveal (syntax explained)** only here does PyBe introduce `try`, `except`, `else`, `finally`, and `raise`, explained piece by piece.
3. **Guided Code Build (syntax practice)** the learner fills in blanks using the syntax just explained, with quick inline corrections on wrong clicks.

Level 1 is the pain of a single unhandled error crashing an entire program. Level 2 isolates three separate error-handling mechanics side by side without mixing them. Level 3 combines a known mechanic with one brand-new one deliberately raising an error yourself. Level 4 requires combining several mechanics inside a single working scenario, plus an open-ended Teach-Back.

---

## LEVEL 1 Quiz Age Crash

**Scenario:** "A quiz app asks the user to type their age as a number. If someone accidentally types 'twenty' instead of '20,' the entire program crashes immediately with a red error message and everything else the quiz was about to do never happens."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Watch the risky part of the code specifically, and if something goes wrong there, catch it and let the program keep running with a friendly message instead of crashing." | ✅ | Concept Reveal |
| "Tell users very clearly, in big letters, to only type numbers, and hope they follow the instructions." | ❌ (relies entirely on the user's cooperation; doesn't actually prevent a crash) | Reflective Prompt |
| "Check character by character whether the typed input looks like a number, before trying to use it." | 🟡 partial (could work here, but has to be rewritten by hand for every different kind of risky input elsewhere in the program) | Reflective Prompt |
| "Automatically restart the whole program whenever it crashes." | ❌ | Reflective Prompt |

**Reflective Prompt (rely on instructions):**
> "Even with clear instructions, will every single user always type exactly what's expected? What happens to the program the very first time someone doesn't?"

**Attempt 2:** "It still crashes instructions alone don't stop bad input from reaching the program; something needs to catch it when it happens anyway." ✅ vs. "It's fine, most users will follow instructions." ❌

**Reflective Prompt (character-by-character check):**
> "This same crash risk could show up in dozens of different places in a program reading a file, connecting to the internet, dividing numbers. Would you rewrite a custom character-by-character check for every single one of those situations?"

**Attempt 2:** "No I need one general way to catch something going wrong, wherever it happens, instead of custom-checking every possible mistake in advance." ✅ vs. "Yes, I'd write a custom check for each situation separately." ❌

**Reflective Prompt (auto-restart):**
> "If the program restarts completely from scratch every time it crashes, what happens to any progress or data the user already had in that session?"

**Attempt 2:** "It's all lost restarting doesn't preserve anything; I need the program to recover from the specific problem and keep going, not start over entirely." ✅ vs. "That's fine, users can just start again." ❌

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'watch for a problem and catch it instead of crashing' is written in Python as a **`try`/`except`** block. Breaking it down:
> - `try:` marks the block of code that might fail.
> - Python runs everything inside `try` normally, until (and unless) something goes wrong.
> - `except:` marks what to do *instead*, only if something inside `try` actually fails.
> - If nothing goes wrong, the `except` block is simply skipped entirely."

### Stage 3 Guided Code Build

**Code shown:**
```
_____:
    age = int(input("Enter your age: "))
_______:
    print("That's not a valid number!")
```
**Token buttons:** `try` ✅ (first blank) · `except` ✅ (second blank) · `attempt` (wrong keyword inline-corrected: "Python uses `try`, not `attempt`.") · `catch` (wrong keyword inline-corrected: "Python uses `except`, not `catch` that's from other languages like JavaScript or Java.")

Wrong click → inline correction only, as shown above. No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. Calculator Guard

**Scenario:** "A calculator app divides two numbers the user types in. Typing '0' as the second number crashes it one way; typing a letter instead of a number crashes it a completely different way. Right now both crash identically, but the app should tell the user exactly what actually went wrong."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Catch each specific kind of problem separately, so a division-by-zero gets its own message, and a non-number entry gets a different one." | ✅ | Concept Reveal |
| "Catch absolutely anything that could possibly go wrong with one single, generic 'something went wrong' message, regardless of what actually happened." | 🟡 partial (stops the crash, but never tells the user what the real problem actually was) | Reflective Prompt |
| "Add a check specifically for division by zero, and simply ignore the possibility of someone typing a letter instead of a number." | ❌ | Reflective Prompt |

**Reflective Prompt (one generic catch-all message):**
> "A user who typed a letter and a user who tried dividing by zero made two completely different mistakes. Does one identical, generic message actually help either of them understand what they did wrong?"

**Attempt 2:** "No different kinds of problems deserve different, specific messages, so the user knows exactly what to fix." ✅ vs. "It's fine, a generic message stops the crash, that's the important part." ❌

**Reflective Prompt (only handle division by zero):**
> "If someone types a letter instead of a number, and you only prepared for division by zero, does the program still crash on that second kind of mistake?"

**Attempt 2:** "Yes every distinct kind of problem needs its own specific check, not just the one you happened to think of first." ✅ vs. "It's fine, dividing by zero is the only mistake I need to worry about." ❌

**Stage 2 Concept Reveal:**
> "Python lets you catch **specific error types** with separate `except` blocks: `except ZeroDivisionError:` catches division by zero specifically, and `except ValueError:` catches an invalid number specifically. Python checks them in order and runs whichever one actually matches what went wrong."

**Stage 3 Guided Code Build:**
```
try:
    result = int(a) / int(b)
______________________:
    print("You can't divide by zero!")
______________________:
    print("Please enter valid numbers!")
```
Tokens: `except ZeroDivisionError` ✅ (first blank) · `except ValueError` ✅ (second blank) · `except Error` (too vague inline-corrected: "`Error` isn't a real Python error type the specific names are `ZeroDivisionError` and `ValueError`.") · `except:` (a bare except with no type inline-corrected: "This catches everything the same way again, losing the specific message for each problem.")

---

### B. Login Success

**Scenario:** "Check a user's password. If it's correct with no errors at all, print 'Login successful' but only in that clean success case, kept separate from the risky checking code itself."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Add a block that runs *only* when nothing in the risky part went wrong at all a dedicated 'everything succeeded' section." | ✅ | Concept Reveal |
| "Just put the success message as the very last line inside the risky block itself." | 🟡 partial (works by coincidence here, but blurs together 'risky' code and 'only-on-success' code in the same place) | Reflective Prompt |
| "Print the success message right after the whole risky-and-catching section, regardless of whether an error happened or not." | ❌ | Reflective Prompt |

**Reflective Prompt (last line inside try):**
> "If a completely unrelated risky step were added later, right above the success message inside that same block, would the success message still only print on genuine success or could it get tangled up with unrelated risky code?"

**Attempt 2:** "It's safer to keep the 'only-on-success' message in its own separate, clearly labeled section instead of just tucking it inside the risky block." ✅ vs. "It's fine, keeping it as the last line inside the block works well enough." ❌

**Reflective Prompt (print after regardless):**
> "If the password check actually fails, should 'Login successful' still print? What does printing it unconditionally, no matter what happened, actually communicate to the user?"

**Attempt 2:** "No the success message should only appear when there genuinely was no error, not automatically every single time." ✅ vs. "It's fine, users will just ignore it if it's wrong." ❌

**Stage 2 Concept Reveal:**
> "This uses `try/except/else`. The **`else`** block runs *only* if nothing in `try` raised an error it's the dedicated place for 'this only happens on clean success,' kept separate from both the risky code and the error-handling code."

**Stage 3 Guided Code Build:**
```
try:
    check_password(entered_password)
except ValueError:
    print("Incorrect password!")
______:
    print("Login successful!")
```
Tokens: `else` ✅ · `finally` (runs regardless of success or failure inline-corrected: "`finally` always runs, even after an error. `else` is what runs only when nothing went wrong.") · `except` (would need its own error type, and runs on failure, not success inline-corrected: "Another `except` still only runs when something fails `else` is for the success case.")

---

### C. File Cleanup

**Scenario:** "Whenever a program opens a settings file, it needs to close that file when it's done whether the file was read successfully or an error happened partway through. Right now, if an error happens partway through reading, the closing step gets skipped entirely."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Add a block that always runs no matter what whether the risky part succeeded or failed specifically for cleanup steps like this." | ✅ | Concept Reveal |
| "Put the closing step as the very last line inside the risky block, right after the reading happens." | ❌ (if an error happens before reaching that line, it never runs) | Reflective Prompt |
| "Repeat the closing step in both the success case and every single error case separately, one copy in each place." | 🟡 partial (works, but means writing and maintaining the same cleanup step multiple times) | Reflective Prompt |

**Reflective Prompt (last line inside try):**
> "If the error happens *while* reading the file before reaching the closing line right after it does that closing line ever actually get a chance to run?"

**Attempt 2:** "No if the error interrupts the block before that line, the closing step never happens. I need something that runs regardless of where or whether an error occurred." ✅ vs. "It's fine, most of the time it'll still get there." ❌

**Reflective Prompt (repeat closing step everywhere):**
> "If there are five different kinds of errors that could happen, each with its own `except` block, would you paste the same closing step into all five?"

**Attempt 2:** "That's a lot of repetition for the exact same step. There should be one place for cleanup that always runs, regardless of which path was taken." ✅ vs. "It's fine, I don't mind repeating it in each one." ❌

**Stage 2 Concept Reveal:**
> "This uses `try/except/finally`. The **`finally`** block always runs whether `try` succeeded, whether an `except` caught something, or even if the error was never caught at all. It's the dedicated place for cleanup that must happen no matter what."

**Stage 3 Guided Code Build:**
```
try:
    settings_file = open("settings.txt")
    data = settings_file.read()
except FileNotFoundError:
    print("Settings file is missing!")
_______:
    settings_file.close()
```
Tokens: `finally` ✅ · `else` (only runs on success, skipped if an error occurred inline-corrected: "`else` only runs when nothing goes wrong. `finally` runs no matter what, which is what cleanup needs.") · `except` (needs its own error type, and still wouldn't run in the success case inline-corrected: "Another `except` wouldn't run at all if the file opened successfully `finally` runs either way.")

---

## LEVEL 3 ATM Withdrawal Guard

**Scenario:** "Withdraw money from an ATM. If the requested amount is more than the account balance, the transaction should stop immediately and show 'Insufficient funds' even though, technically, nothing was going to fail automatically on its own here; this particular problem has to be noticed and flagged deliberately."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Manually flag this specific situation as an error yourself, the moment it's detected, so it gets caught and handled the same way any other error would be." | ✅ | Concept Reveal |
| "Just print a warning message about insufficient funds, and let the withdrawal go through anyway." | ❌ | Reflective Prompt |
| "Use a simple condition check to catch this case and print an error message directly, kept completely separate from how any other errors in this same code get handled." | 🟡 partial (stops this one case, but doesn't get handled consistently alongside other errors the same withdrawal code might raise) | Reflective Prompt |

**Reflective Prompt (warn but allow anyway):**
> "If the withdrawal happens regardless of the warning, does the account balance end up correct afterward? What does printing a warning actually *prevent*?"

**Attempt 2:** "Nothing the withdrawal still needs to actually be stopped, not just warned about while still going through." ✅ vs. "It's fine, the warning is enough to inform the user." ❌

**Reflective Prompt (separate condition check, not integrated):**
> "What if this withdrawal function also needs to handle a separate problem, like the account being frozen, which *does* trigger a real, automatic error elsewhere in the same code? Would this insufficient-funds check be handled the same consistent way as that other error?"

**Attempt 2:** "Not automatically it would help to make insufficient funds behave like any other error too, so all the problems in this function get handled the same consistent way." ✅ vs. "It's fine, I'll just keep the two handled completely differently." ❌

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'flag this myself, so it's caught like any other error' uses the **`raise`** keyword. `raise ValueError("Insufficient funds")` deliberately creates an error, even though Python itself didn't detect one on its own. Once raised, it travels to the nearest matching `except` block and gets handled exactly the same way as a built-in error would."

### Stage 3 Guided Code Build

**Code shown:**
```
try:
    if amount > balance:
        _______________________________________
    balance = balance - amount
except ValueError as e:
    print(e)
```
**Token buttons:** `raise ValueError("Insufficient funds")` ✅ · `print(ValueError("Insufficient funds"))` (prints a description of an error object but never actually raises one inline-corrected: "This only prints text about an error it doesn't stop the withdrawal or get caught by `except`. `raise` is what actually triggers it.") · `return ValueError("Insufficient funds")` (returns the error object instead of raising it inline-corrected: "`return` hands a value back, it doesn't trigger an error to be caught. `raise` is what actually throws it.")

Wrong click → inline correction only, as shown above. No new reflective cycle; they simply retry the blank.

---

## LEVEL 4 Complete ATM Transaction (Combining Error-Handling Mechanics)

**Scenario:** "Build the complete ATM withdrawal flow: attempt the withdrawal, catch invalid-amount errors and insufficient-funds errors *differently* from each other, show a success message only when nothing went wrong at all, and always print the updated balance at the end no matter what happened."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Catch each kind of problem with its own specific handler, add a success-only section for the clean case, and add a final section that always runs to show the balance regardless of outcome." | ✅ | Concept Reveal |
| "Catch every possible problem with one shared, generic error handler, and print the balance right after that shared handler." | 🟡 partial (loses the specific messages for each distinct problem, and skips showing the balance in the success case) | Reflective Prompt |
| "Only handle the two error cases, and skip having any dedicated success message or guaranteed final balance display." | ❌ | Reflective Prompt |

**Reflective Prompt (one shared generic handler):**
> "If an invalid amount and insufficient funds both get the exact same generic message, does the customer know which specific problem actually happened? And does the balance still get shown if there was no error at all?"

**Attempt 2:** "No to both each problem needs its own specific message, and the balance needs to show in every case, including success, not just after an error." ✅ vs. "It's fine, one generic message covers it well enough." ❌

**Reflective Prompt (skip success message and guaranteed balance display):**
> "If the withdrawal actually succeeds with no problems at all, does the customer see any confirmation? And is there anything guaranteeing the balance is shown, whether it succeeded or failed?"

**Attempt 2:** "No there should be a dedicated success message for the clean case, and a guaranteed final section that always shows the balance no matter what happened." ✅ vs. "It's fine, the customer can just check their balance separately." ❌

### Stage 2 Concept Reveal (syntax explained)

> "This combines everything from this unit into one working flow: multiple `except` blocks catch different specific errors (`ValueError` for insufficient funds, `TypeError` for an invalid amount), `else` runs only on clean success, and `finally` always runs at the very end, regardless of which path was taken, to display the balance."

### Stage 3 Guided Code Build

**Code shown:**
```
try:
    if not isinstance(amount, (int, float)):
        raise TypeError("Invalid amount")
    if amount > balance:
        raise ValueError("Insufficient funds")
    balance = balance - amount
except TypeError:
    print("Please enter a valid amount.")
except ValueError:
    print("Insufficient funds.")
______:
    print("Withdrawal successful!")
______:
    print("Current balance:", balance)
```
**Token buttons:** `else` ✅ (first blank) · `finally` ✅ (second blank) · `except` (in the first blank would need its own new error type and never represents pure success inline-corrected: "This only runs on failure, not success. `else` is for the clean, error-free case.") · `else` (in the second blank wouldn't run after the errors above it inline-corrected: "`else` only runs if no error happened at all. `finally` is what guarantees this always runs.")

### Teach-Back (Level 4, open-ended)

> "Design a new case study for **custom exception classes** (writing your own error type by inheriting from Python's built-in `Exception`, instead of relying only on `ValueError` or `TypeError`) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), and the syntax token set for the guided build afterward."

This asks the learner to build all three stages of the engine themselves for a related-but-not-yet-taught refinement, the strongest possible test of Extended Abstract understanding: they're not just handling errors correctly, they're designing how to teach a program-specific way of defining them.

---

## Summary Concept Coverage Map

| Level | Case Study | Core Mechanic Introduced |
|---|---|---|
| 1 | Quiz Age Crash | `try`/`except` catching a failure instead of crashing |
| 2A | Calculator Guard | Catching specific error types multiple `except` blocks |
| 2B | Login Success | `else` code that runs only on clean success |
| 2C | File Cleanup | `finally` code that always runs, regardless of outcome |
| 3 | ATM Withdrawal Guard | `raise` deliberately creating your own error |
| 4 | Complete ATM Transaction | Combining multiple `except` blocks, `else`, and `finally` in one scenario |
