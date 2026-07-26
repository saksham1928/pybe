# PyBe File Handling Unit Plain-English-First Roadmap (Levels 1–5)

## About this roadmap

This document follows the same three-stage engine used across every PyBe topic, and maps its five levels onto the SOLO taxonomy from `pybe-loops-case-study-framework.md` / `product.md`:

1. **Logic Test (plain English)** Attempt 1, and Attempt 2 if needed, are strategy descriptions in plain English never Python code. The learner chooses an approach, not a syntax pattern.
2. **Concept Reveal (syntax explained)** only here does PyBe introduce the actual Python keywords/methods, broken down piece by piece.
3. **Guided Code Build (syntax practice)** low-stakes fill-in-the-blank practice with token buttons. Wrong clicks get a quick inline correction, not a new reflective cycle.

| Level | SOLO stage | What it does |
|---|---|---|
| 1 | Prestructural | The pain scenario let the learner feel the absence of the concept |
| 2 | Unistructural | Isolated mechanics, heavily scaffolded (multiple parallel case studies, one mechanic each) |
| 3 | Multistructural | Parallel scenarios, different mechanics kept separate |
| 4 | Relational | A scenario that breaks unless mechanics are combined |
| 5 | Extended Abstract | Open-ended Teach-Back the learner designs a new case study themselves |

---

## LEVEL 1 The Scores That Vanish

**Scenario:** "Your quiz game keeps player scores in a list while it runs, but every time you close and reopen the program, all the scores are gone."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Save the scores somewhere outside the program's memory, on the computer's storage, so they're still there next time the program runs." | ✅ Correct | Concept Reveal |
| "Just keep the program running forever, so the list in memory never has a chance to disappear." | ❌ Wrong (not realistic every program eventually closes or crashes) | Reflective Prompt |
| "Print the scores to the screen before closing, so you can remember them and retype them next time." | 🟡 Not absolutely correct (works once, but doesn't scale or stay accurate) | Reflective Prompt |

**Reflective Prompt (keep it running forever):**
> "Is it realistic or even possible to guarantee a program never gets closed, restarted, or crashes?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No that's not realistic. I need the data to survive even if the program closes." | ✅ | Concept Reveal (via reflection) |
| "I'll just try to never close it." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (print and retype):**
> "If there were 500 scores, would reading them off the screen and retyping them next time be practical, or error-free?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No I want the data saved automatically somewhere that persists, not something I retype myself." | ✅ | Concept Reveal (via reflection) |
| "I'd still copy them down and retype them." | ❌ | Concept Reveal (direct) |

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'save data outside the program's memory so it survives' is written in Python using **file handling**. `open('scores.txt', 'w')` opens (or creates) a file named `scores.txt` in **write mode** (`'w'`), ready for you to save data into it data that stays on disk even after the program closes."

### Stage 3 Guided Code Build

**Code shown:**
```
file = ___________________________
file.write("88\n")
file.close()
```
**Token buttons:** `open('scores.txt', 'w')` ✅ · `open('scores.txt', 'r')` (wrong mode `'r'` is for *reading*; writing to a read-mode file causes an error) · `open('scores.txt')` (missing mode leaving it out defaults to read-only, so writing would still fail)

Wrong click → inline correction only: "Almost writing to a file needs write mode: `'w'`. Leaving the mode out (or using `'r'`) only allows reading, not writing." No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. Loading Saved Scores (Read Mode & `.read()`)

**Scenario:** "Next time the program starts, load the previously saved scores from `scores.txt` and print them."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Open the file in a mode meant for reading, then read its contents back into the program." | ✅ | Concept Reveal |
| "Open the file in write mode again, since that's how you opened it last time, and try to read from it." | ❌ | Reflective Prompt |
| "Open the file by double-clicking it outside the program, and copy the numbers in manually." | 🟡 partial (defeats the purpose of the program reading its own data) | Reflective Prompt |

**Reflective Prompt (reuse write mode):**
> "Write mode (`'w'`) is for saving new data and it actually clears the file's existing content first. What would happen to your saved scores if you reopened the file in write mode again?"

**Attempt 2:** "Write mode would erase what's already there I need read mode specifically to safely get data back out." ✅ vs. "I'll just use write mode again, it should be fine." ❌

**Reflective Prompt (open manually and retype):**
> "That defeats the purpose of saving it in the file at all, if the program can't read it back itself. Is there a way for the *program* to read the saved file directly, on its own?"

**Attempt 2:** "Yes I want the program itself to open and read the file directly, not rely on me copying data by hand." ✅ vs. "I'll keep opening it manually myself." ❌

**Stage 2 Concept Reveal:**
> "Reading uses **read mode**: `open('scores.txt', 'r')`. Once open, `.read()` pulls the entire contents of the file back as one piece of text: `contents = file.read()`."

**Stage 3 Guided Code Build:**
```
file = open('scores.txt', ___)
contents = file.______()
print(contents)
```
Tokens for blank 1: `'r'` ✅ · `'w'` (wrong this would erase the file's existing content)
Tokens for blank 2: `read` ✅ · `write` (wrong this saves new data instead of retrieving existing data)

---

### B. Adding Without Erasing (Append Mode)

**Scenario:** "A new score comes in mid-game. Add it to the end of `scores.txt` without erasing the scores already saved there."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Open the file in a mode that adds new content onto the end, keeping everything already saved intact." | ✅ | Concept Reveal |
| "Open the file in the same write mode used the very first time, and write the new score." | ❌ | Reflective Prompt |
| "Read the whole file first, add the new score to that text inside the program, then decide what to do next." | 🟡 partial (adds an unnecessary extra step) | Reflective Prompt |

**Reflective Prompt (reuse write mode):**
> "You already learned write mode clears a file's existing content first. If you open `scores.txt` in write mode again, what happens to the scores already saved there?"

**Attempt 2:** "They'd be erased I need a mode that adds on without clearing what's already there." ✅ vs. "I'll use write mode again, it should just add to what's there." ❌

**Reflective Prompt (read first, then decide):**
> "That's a reasonable start, but it still leaves the question once you have the old content plus the new score, which *mode* would you then use to save all of it, without losing anything?"

**Attempt 2:** "I'd still need a mode that safely adds new content instead of overwriting so I should just use that mode directly instead of an extra read step." ✅ vs. "I'd still just resave everything using write mode." ❌

**Stage 2 Concept Reveal:**
> "This is **append mode**: `open('scores.txt', 'a')`. Unlike `'w'`, which clears the file first, `'a'` adds new content onto the *end*, leaving everything already saved untouched."

**Stage 3 Guided Code Build:**
```
file = open('scores.txt', ___)
file.write("74\n")
file.close()
```
Tokens: `'a'` ✅ · `'w'` (wrong erases existing content before writing) · `'r'` (wrong read mode doesn't allow writing at all)

---

### C. Reading Line by Line (Looping Over a File)

**Scenario:** "Print each saved score on its own separate line not as one big block of text."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Loop through the open file directly, treating each line as a separate item to work with one at a time." | ✅ | Concept Reveal |
| "Use `.read()` to get the whole file as one block of text, then print that single block." | ❌ | Reflective Prompt |
| "Read the file, then manually search through the text for line breaks yourself." | 🟡 partial (reinvents something Python already does) | Reflective Prompt |

**Reflective Prompt (`.read()` as one block):**
> "`.read()` gives you everything as one single piece of text. If you print that directly, does it come out as neatly separated lines, or as one dense block?"

**Attempt 2:** "It prints as one block I need something that gives me each line separately, not the whole thing at once." ✅ vs. "I'll just print the whole block, it's close enough." ❌

**Reflective Prompt (manually search for line breaks):**
> "Python already knows how to recognize where each line ends. Is manually searching through the text for line breaks yourself really necessary?"

**Attempt 2:** "No I want to loop through the file directly and let Python hand me each line automatically." ✅ vs. "I'll keep searching for line breaks myself." ❌

**Stage 2 Concept Reveal:**
> "An open file can be looped over directly, just like a list: `for line in file:` hands you each line, one at a time, already split at the line breaks no manual searching needed."

**Stage 3 Guided Code Build:**
```
file = open('scores.txt', 'r')
_______________________:
    print(line)
file.close()
```
Tokens: `for line in file` ✅ · `for line in file.read()` (wrong `.read()` collapses everything into one block of text first, so this loops character by character, not line by line) · `for line of file` (wrong keyword Python uses `in`, not `of`)

---

## LEVEL 3 Two Case Studies

### A. Forgetting to Close (the `with` statement)

**Scenario:** "You keep forgetting to call `file.close()` after opening files, which can leave data unsaved or the file locked."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Use an approach that automatically closes the file for you when you're done with it, so you don't have to remember." | ✅ | Concept Reveal |
| "Just try to remember to always call `.close()` at the very end of every block of file code." | ❌ | Reflective Prompt |
| "Open and close the file twice, just to be extra sure it's really closed." | 🟡 partial (doesn't fix forgetting the first close, and adds confusion) | Reflective Prompt |

**Reflective Prompt (remember to close manually):**
> "You've already noticed you keep forgetting. Is 'trying harder to remember' actually a reliable fix, or does the real problem need a structural solution?"

**Attempt 2:** "I need something that closes the file automatically, so forgetting isn't even possible." ✅ vs. "I'll just try to be more careful about remembering." ❌

**Reflective Prompt (open/close twice):**
> "Opening and closing twice doesn't address forgetting the *first* close, and adds confusion. Is there something built to guarantee closing happens, without you managing it directly at all?"

**Attempt 2:** "Yes something that handles closing automatically and reliably, without needing my manual close call at all." ✅ vs. "I'll just add extra close calls, just in case." ❌

**Stage 2 Concept Reveal:**
> "This is the `with` statement: `with open('scores.txt', 'r') as file:`. Everything indented underneath runs with the file open, and Python **automatically closes it** the moment that block ends even if something goes wrong inside it. No `.close()` call needed."

**Stage 3 Guided Code Build:**
```
___________________________________________:
    contents = file.read()
print(contents)
```
Tokens: `with open('scores.txt', 'r') as file` ✅ · `with open('scores.txt', 'r')` (missing `as file` there'd be no name to refer to the open file by) · `open('scores.txt', 'r') as file` (missing `with` not valid on its own)

---

### B. Stray Blank Lines (`.strip()`)

**Scenario:** "When printing each saved score, there are odd extra blank lines appearing between them that shouldn't be there."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Recognize that each line already carries an invisible line-break character at the end, and remove it before using the line's content." | ✅ | Concept Reveal |
| "Assume the file itself was saved incorrectly, and manually go edit the raw text file to fix it." | ❌ | Reflective Prompt |
| "Add extra blank print statements to try to visually balance out the spacing." | 🟡 partial (treats the symptom, not the cause) | Reflective Prompt |

**Reflective Prompt (assume the file was saved wrong):**
> "Every line read from a file naturally keeps its trailing line-break character that's how Python marks where lines end, not a mistake in the file. Given that, what needs to happen to *each line's text*, not the file itself?"

**Attempt 2:** "The line-break character needs to be removed from each line's text after reading it, not fixed in the file." ✅ vs. "I still think the file itself needs to be edited." ❌

**Reflective Prompt (add blank prints to compensate):**
> "That treats the *symptom* by adding more spacing rather than removing the actual extra character causing it. Is there a way to clean the line's text directly, instead of compensating around it?"

**Attempt 2:** "Yes I want to directly remove the extra character from each line's text, not just add more spacing around it." ✅ vs. "I'll just keep adjusting spacing to compensate." ❌

**Stage 2 Concept Reveal:**
> "Each line read from a file keeps its trailing `\n` (newline) character. `.strip()` removes leading and trailing whitespace including that `\n` from a piece of text: `line.strip()` gives you the clean value, with the invisible line-break gone."

**Stage 3 Guided Code Build:**
```
with open('scores.txt', 'r') as file:
    for line in file:
        print(line.________())
```
Tokens: `strip` ✅ · `close` (wrong this closes the file, unrelated to cleaning text) · `read` (wrong `.read()` is for whole-file content, not cleaning a single line's whitespace)

---

## LEVEL 4 Calculating the Average (Combining Read + Convert + Loop)

**Scenario:** "`scores.txt` has one score per line, saved as text. Read the file and calculate the average score but the numbers were saved as text, and text can't be added together like numbers."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Read the file line by line, convert each line's text into an actual number, and only then add them together to calculate the average." | ✅ | Concept Reveal |
| "Read the file and try adding the lines together directly, since they look like numbers on the page." | ❌ | Reflective Prompt |
| "Read the file, and just hard-code the average based on the values you remember seeing." | 🟡 partial (won't stay accurate if the file changes) | Reflective Prompt |

**Reflective Prompt (add the lines directly as text):**
> "Text that *looks* like a number isn't automatically treated as one what actually happens when you try to add a piece of text to a running numeric total in Python?"

**Attempt 2:** "Adding text to a number that way raises an error it doesn't add their numeric values. I need to convert each line to a real number first." ✅ vs. "I'll just try adding them directly and see what happens." ❌

**Reflective Prompt (hard-code the remembered average):**
> "If the file's contents change new scores added, old ones removed would a hard-coded average still be accurate?"

**Attempt 2:** "No I need the average calculated freshly from whatever is actually in the file, every time." ✅ vs. "I'll just keep updating the hard-coded number myself." ❌

**Stage 2 Concept Reveal:**
> "This combines opening and looping through a file, `.strip()` to clean each line, plus one new piece: `int()`, which **converts text into a whole number**. `int(line.strip())` takes cleaned text like `'88'` and turns it into the actual number `88`, ready for arithmetic. Skip `int()` entirely, and Python still treats the line as text `total + score` would then try to add a number to text, which raises an error rather than calculating a sum."

**Stage 3 Guided Code Build:**
```
total = 0
count = 0
with open('scores.txt', 'r') as file:
    for line in file:
        score = _______________________
        total = total + score
        count = count + 1
print(total / count)
```
Tokens: `int(line.strip())` ✅ · `line.strip()` (wrong still text; adding this to `total` raises an error) · `line.strip().int()` (wrong `int()` is a function you wrap *around* a value, not a method strings have no `.int()`)

---

## LEVEL 5 Teach-Back (Extended Abstract)

> "Design a new case study that teaches checking whether a file exists before opening it (so the program doesn't crash trying to read a file that isn't there) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), the reflective prompts, the concept reveal, and the syntax token set for the guided build afterward."

This asks the learner to build *all three stages* of the engine themselves logic test, concept reveal, and guided build which is the strongest possible test of understanding: they're not just solving the scaffold, they're designing it.
