# PyBe Loops Unit Plain-English-First Roadmap (Levels 1–5)

## What changed and why

Previously the Attempt 1 / Attempt 2 options were written as Python syntax choices (`for i in range(100):` vs `while True:`). That silently assumes the beginner already half-knows Python which defeats the entire "discover the concept before the syntax" philosophy this project is built on.

**New three-stage engine per case study:**

1. **Logic Test (plain English)** Attempt 1, and Attempt 2 if needed, are now options written entirely in plain English describing an *approach*, never code. The learner is choosing a strategy, not recognizing syntax.
2. **Concept Reveal (syntax explained)** only here does PyBe introduce the actual Python keywords, and explains them piece by piece: what `for` means, what `in` means, what `range()` produces, what `while` checks, what `break` does. This is the first time the learner sees real code for this concept.
3. **Guided Code Build (syntax practice)** immediately after the explanation, the learner gets the same fill-in-the-blank-with-buttons mechanic as before, but now it's low-stakes practice applying the syntax they were just shown, not a test of the underlying logic (that was already tested in stage 1). Mistakes here get a quick inline correction, not a full reflective-prompt cycle the conceptual work is done; this stage is pure retrieval/consolidation, closer to Vygotsky's "guided practice with fading support" than to open problem-solving.

This also sharpens the Kolb cycle: Concrete Experience now happens twice once abstractly (choosing a strategy in words) and once concretely (running real code) with Reflective Observation sitting between them at the logic stage, and Active Experimentation happening at the code-build stage.

---

## LEVEL 1 Birthday App

**Scenario:** "Your friend's older brother wants 'Happy Birthday!' printed 100 times."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Tell the computer to repeat one action a fixed number of times like saying 'do this 100 times.'" | ✅ Correct | Concept Reveal |
| "Keep repeating the action until some condition becomes false." | ❌ Wrong (a while-style idea; mismatched the count is already known) | Reflective Prompt |
| "Store the message 100 times in a list, then display the whole list." | ❌ Wrong (misconception overcomplicated, solves a storage problem that doesn't exist here) | Reflective Prompt |
| "Keep a counter that I increase myself, one at a time, until it reaches 100." | 🟡 Not absolutely correct (this is a manual while-style approach works, but isn't the natural fit for a *known* count) | Reflective Prompt |

**Reflective Prompt (if "until a condition" chosen):**
> "You want it to run exactly 100 times, a number you already know in advance. Does 'keep going until something becomes false' really fit when you already know the exact number you want?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Use an approach built specifically for 'repeat exactly N times when N is already known.'" | ✅ | Concept Reveal (via reflection) |
| "Just write the print line 100 times." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (if "store in a list" chosen):**
> "Think about what you actually need do you need to *save* the message somewhere for later, or just show it, right now, 100 times?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Just repeat the display action itself 100 times no need to store anything." | ✅ | Concept Reveal (via reflection) |
| "Store it in a list, since lists are how Python repeats things." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (if "manual counter" chosen):**
> "That works but you have to remember to increase your counter yourself, every single time. Since you already know it's exactly 100 up front, is there an approach that handles the counting *for* you?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Yes something built for 'repeat a known number of times' that manages the counting automatically." | ✅ | Concept Reveal (via reflection) |
| "No, counting always has to be done by hand." | ❌ | Concept Reveal (direct) |

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'repeat a fixed number of times' is written in Python as a **`for` loop** with **`range()`**. Breaking it down piece by piece:
> - `for` starts a repeating block.
> - `i` is just a name Python gives to each round you could call it anything.
> - `in` means 'take each value, one at a time, from…'
> - `range(100)` produces the numbers 0 through 99 that's 100 rounds total.
> - The colon `:` and the indented line below it mark what happens *inside* the repeat."

### Stage 3 Guided Code Build

**Code shown:**
```
_____:
    print("Happy Birthday!")
```
**Token buttons:** `for i in range(100)` ✅ · `for i on range(100)` (wrong preposition) · `for i in range[100]` (wrong brackets)

Wrong click → inline correction only: "Almost Python uses `in`, not `on`, and round brackets `()`, not square ones." No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. Rocket Countdown

**Scenario:** "A rocket counts down from 10 to 1, then prints 'Liftoff!'"

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Repeat a fixed number of times, counting *downward* from 10 to 1." | ✅ | Concept Reveal |
| "Repeat a fixed number of times, counting *upward* from 1 to 10." | ❌ (wrong direction) | Reflective Prompt |
| "Just perform the print action 10 separate times, without tracking the actual number." | 🟡 partial (ignores that the *number itself* needs to be shown) | Reflective Prompt |

**Reflective Prompt (upward):**
> "Picture the output does a countdown go 1, 2, 3… or 10, 9, 8…? What does 'countdown' actually mean?"

**Attempt 2:** "Countdown means the numbers *decrease* each round, starting high and ending low." ✅ vs. "Direction doesn't matter as long as it repeats 10 times." ❌

**Reflective Prompt (10 separate prints):**
> "You already know an approach that repeats a fixed number of times *and* can use the changing number itself. Would you need that actual counting number to show 10, 9, 8… correctly?"

**Attempt 2:** "Yes I need the real repeating number itself, not just the action, since the number is what's being displayed." ✅ vs. "No, I'll just type the numbers in myself, in order." ❌

**Stage 2 Concept Reveal:**
> "`range()` can take three numbers: where to start, where to stop, and how big a step to take each round. A *negative* step means counting down. And unlike Level 1, this time the loop's own counting number is exactly what you want to print so `i` is now real data, not just plumbing."

**Stage 3 Guided Code Build:**
```
for i in range(___, ___, ___):
    print(i)
print("Liftoff!")
```
Tokens: `10`, `0`, `-1` (correct) plus `1`, `11` (light distractors, inline-corrected).

---

### B. Guest List

**Scenario:** "Greet each of 4 guests by name at the door."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Go through the list and greet each item in it directly, without needing to count how many there are." | ✅ | Concept Reveal |
| "Count how many names are in the list first, then repeat the greeting that many times using the count." | 🟡 partial (works, but requires tracking a count that could get out of sync with the list) | Reflective Prompt |
| "Greet each person individually by writing a separate line for each name." | ❌ | Reflective Prompt |

**Reflective Prompt (count first):**
> "That works for exactly 4 names but what if the guest list grows to 200 people next year? You'd need to keep the count perfectly in sync with the list. Is there a way to just say 'for every name in this list,' directly, without counting first?"

**Attempt 2:** "Yes go through the list itself, item by item, with no separate counting step needed." ✅ vs. "No, you always need the count first." ❌

**Reflective Prompt (write each individually):**
> "Imagine the guest list had 200 names would you still write a separate line for each one? What repeats an action automatically for every item in a collection?"

**Attempt 2:** "Something that walks through the list automatically, one item at a time." ✅ vs. "I'd still write each one by hand, since names aren't numbers." ❌

**Stage 2 Concept Reveal:**
> "This is written as `for name in guest_list:` `in` here means 'take each item, one at a time, directly from this list.' No counting, no index numbers the loop variable `name` simply *becomes* each guest in turn."

**Stage 3 Guided Code Build:**
```
guest_list = ["Aditi", "Ravi", "Meera", "Kabir"]
_____________:
    print("Hello,", name)
```
Tokens: `for name in guest_list` ✅ · `for name of guest_list` (wrong keyword) · `for name in guest_list()` (unnecessary parentheses)

---

### C. Vending Machine

**Scenario:** "Keep asking for coins until ₹20 total has been inserted."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Keep repeating until a condition becomes true I don't know in advance how many coins it'll take." | ✅ | Concept Reveal |
| "Repeat a fixed number of times, once per coin, assuming every coin is worth ₹1." | ❌ | Reflective Prompt |
| "Ask the user upfront how many coins they plan to insert, then repeat that many times." | 🟡 partial (shifts the real problem onto the user instead of solving it) | Reflective Prompt |

**Reflective Prompt (fixed ₹1 assumption):**
> "What happens if someone inserts a ₹10 coin? Would repeating exactly 20 times still make sense if coins aren't always ₹1?"

**Attempt 2:** "No I don't actually know the *number of coins* in advance, only the *total amount* I'm waiting for." ✅ vs. "It's fine, I'll just assume everyone uses ₹1 coins." ❌

**Reflective Prompt (ask user upfront):**
> "That relies on the user knowing and honestly reporting how many coins they'll use which defeats the point of the machine tracking it itself. Is there a way to repeat 'until a condition is met' without asking the user to predict anything?"

**Attempt 2:** "Yes keep repeating automatically, checking the running total against the target every single round." ✅ vs. "No, Python always needs a fixed repeat count decided in advance." ❌

**Stage 2 Concept Reveal:**
> "This is a `while` loop: `while total < 20:`. Unlike `for`, `while` doesn't know or care how many rounds it'll take it just re-checks the same yes/no question before every round, and stops the instant the answer becomes false."

**Stage 3 Guided Code Build:**
```
total = 0
_____________:
    coin = get_coin_inserted()
    total = total + coin
print("Thank you!")
```
Tokens: `while total < 20` ✅ · `while total > 20` (wrong direction would never run) · `until total < 20` (Python has no `until` keyword)

---

## LEVEL 3 ATM PIN Lockout

**Scenario:** "Ask for a PIN. If correct, proceed. If wrong, ask again but lock after 3 total wrong tries."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Keep asking, repeating until *either* the correct PIN is entered *or* 3 total attempts are used whichever happens first." | ✅ | Concept Reveal |
| "Always ask exactly 3 times, no matter what, even if the correct PIN was entered on the very first try." | ❌ | Reflective Prompt |
| "Keep asking forever until the PIN is correct, with no limit on attempts." | ❌ | Reflective Prompt |

**Reflective Prompt (always exactly 3):**
> "If someone gets it right on their first try, should the machine really ask two more times anyway? What are the *two separate things* that could end this loop?"

**Attempt 2:** "There are two stopping conditions a correct PIN, or reaching 3 tries and the loop should stop the instant either one happens." ✅ vs. "I'll just make the extra tries do nothing, but still ask them out loud." ❌

**Reflective Prompt (no limit):**
> "What happens if someone keeps guessing wrong forever does your approach ever stop? A real ATM needs a *second* condition alongside 'is the PIN correct.' What would that be?"

**Attempt 2:** "I need to track how many attempts have happened, and stop once that hits 3 even if the PIN is still wrong." ✅ vs. "I'll just trust the user not to keep guessing forever." ❌

**Stage 2 Concept Reveal:**
> "This combines two things you already know: a `while` loop tracking attempts, and a brand-new keyword, **`break`** which means 'leave the loop immediately, right now, even though its main condition would normally keep it going.' You reach for `break` exactly when a *second* condition (success) needs to end things early."

**Stage 3 Guided Code Build:**
```
tries = 0
_____________:
    pin = ask_for_pin()
    tries = tries + 1
    if pin == correct_pin:
        print("Access granted")
        _____
```
Tokens: `while tries < 3` ✅ (header) · `while pin != correct_pin` ❌ (ignores the try-limit) and for the second blank: `break` ✅ · `continue` (would loop again instead of exiting, even on a correct PIN inline-corrected with: "That would ask again even after getting it right you want to *leave*, not repeat.")

---

## LEVEL 4 Wedding Seating (Nested Loops)

**Scenario:** "5 tables, 4 seats each. Print who sits where."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Repeat over each table, and *inside that*, repeat over each seat at that table a repeat inside a repeat." | ✅ | Concept Reveal |
| "Use one single repeat over all 20 seats, and work out mathematically which table each seat number belongs to." | 🟡 partial (only works because every table happens to have exactly 4 seats) | Reflective Prompt |
| "Write out all 5 tables' seating individually, since there are only 5." | ❌ | Reflective Prompt |

**Reflective Prompt (single repeat + math):**
> "That works because every table happens to have exactly 4 seats. What if table 3 had 6 seats and table 4 had only 2 would your math for figuring out which table a seat belongs to still hold up?"

**Attempt 2:** "I need a separate repeat per table, and inside each one, its own repeat for that table's seats so table sizes can differ freely." ✅ vs. "I'd just add special-case handling for tables with different sizes." ❌

**Reflective Prompt (write out by hand):**
> "This worked at 5 tables. What about 50 tables at a big wedding hall at what point does writing each one out by hand stop being realistic?"

**Attempt 2:** "A repeat inside a repeat handles any number of tables and any number of seats automatically." ✅ vs. "I'd just accept that bigger events need more typing." ❌

**Stage 2 Concept Reveal:**
> "This is a **nested loop** literally one `for` loop written inside another. The outer loop moves through tables one at a time; for *each* table, the entire inner loop runs completely before moving to the next table. It's not a new mechanic it's two loops you already know, one running inside the other."

**Stage 3 Guided Code Build:**
```
tables = 5
seats_per_table = 4
_____________:
    ___________:
        print("Table", t, "Seat", s)
```
Tokens: `for t in range(1, tables + 1)` ✅ (outer) · `for s in range(1, seats_per_table + 1)` ✅ (inner) · `for all_seats in range(20)` (collapses both into one inline-corrected: "This flattens two separate repeats into one it'll break the moment table sizes differ.")

### Teach-Back (Level 4, open-ended)

> "Design a new case study for `break` vs `continue` for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), and the syntax token set for the guided build afterward."

This now explicitly asks the learner to build *all three stages* of the engine themselves logic test, concept reveal, and guided build which is the strongest possible test of Extended Abstract understanding: they're not just solving the scaffold, they're designing it.

---

## Summary What Changed Structurally

| Stage | Old model | New model |
|---|---|---|
| Attempt 1 / 2 | Python code snippets as options | Plain-English strategy descriptions |
| What's being tested | Syntax recognition + logic, entangled | Logic only syntax literacy isn't required yet |
| Syntax introduction | Buried inside the "correct" MCQ option | Isolated into its own explicit explanation step |
| Code blanks | The test itself | Practice *after* understanding, lower-stakes, inline-corrected |
| Wrong code-build clicks | Routed into a full reflective cycle | Quick inline correction, no new reflection loop |
