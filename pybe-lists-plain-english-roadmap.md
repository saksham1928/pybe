# PyBe Lists Unit Plain-English-First Roadmap (Levels 1–5)

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

## LEVEL 1 Quiz Scoreboard

**Scenario:** "You need to track the scores of 5 players in a quiz game. Right now you're using five separate variables: `score1`, `score2`, `score3`, `score4`, `score5`."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Group all the scores together into a single ordered collection, so I can work with them as one thing but still access each individually." | ✅ Correct | Concept Reveal |
| "Keep using a separate variable for each player's score, adding a new variable every time a new player joins." | ❌ Wrong (doesn't scale, and each variable needs its own name) | Reflective Prompt |
| "Combine all the scores into one single number, like adding them all together into a total." | ❌ Wrong (loses each individual score entirely) | Reflective Prompt |
| "Store all the scores in one long piece of text, separated by commas." | 🟡 Not absolutely correct (works as storage, but everything has to be manually split and converted back later) | Reflective Prompt |

**Reflective Prompt (separate variable each time):**
> "What happens when your quiz game grows to 50 players? Would you want to write and manage 50 separate variable names by hand?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Use a single structure that can hold as many scores as needed, without creating a new variable name each time." | ✅ | Concept Reveal (via reflection) |
| "I'll just keep adding new variables as needed, one per player." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (combine into one total number):**
> "If you only keep the total, can you still tell me what Player 3 individually scored?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No I need each individual score to stay accessible, not just their sum." | ✅ | Concept Reveal (via reflection) |
| "It's fine, I only ever need the total anyway." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (one long comma-separated text):**
> "You could pull individual scores back out of that text, but you'd have to manually split it and convert every piece back into a number, every single time. Is there something built specifically to hold multiple individual values, ready to use, without that extra text-processing work?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Yes something built specifically to store multiple individual values in order, that I can access directly by position." | ✅ | Concept Reveal (via reflection) |
| "No, plain text is the standard way to store multiple values in Python." | ❌ | Concept Reveal (direct) |

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'group related values into a single ordered collection' is written in Python as a **list**. Breaking it down piece by piece:
> - Square brackets `[ ]` mark the start and end of the collection.
> - Commas `,` separate each individual value inside.
> - Python numbers positions starting at **0**, not 1 so the first item is `scores[0]`.
> - You can access any item directly using its position, called its **index**, inside square brackets."

### Stage 3 Guided Code Build

**Code shown:**
```
_______________________________
print(scores[0])
```
**Token buttons:** `scores = [88, 92, 79, 95, 84]` ✅ · `scores = (88, 92, 79, 95, 84)` (wrong brackets creates a tuple, not a list) · `scores = {88, 92, 79, 95, 84}` (wrong brackets creates a set)

Wrong click → inline correction only: "Almost round brackets `()` create a tuple, and curly braces `{}` create a set. Square brackets `[ ]` are what create a list." No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. New Player Joins (Appending)

**Scenario:** "A new player joins the quiz game mid-way. Add their score, 90, to the end of the existing `scores` list."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Add the new value onto the end of the existing list, without creating a whole new list from scratch." | ✅ | Concept Reveal |
| "Create a brand-new list from scratch, retyping all the old scores plus the new one." | ❌ | Reflective Prompt |
| "Add the new score by directly assigning it to a brand-new index number placed right after the current items." | 🟡 partial (works, but risky and error-prone if you miscount the next index) | Reflective Prompt |

**Reflective Prompt (retype whole list):**
> "What if there were already 500 scores in the list would you want to retype all 500 just to add one more?"

**Attempt 2:** "No I want an approach that adds just the one new value onto the existing list, leaving everything else untouched." ✅ vs. "I'd still prefer to rebuild the whole list each time." ❌

**Reflective Prompt (manual index assignment):**
> "That means you'd have to know exactly how many items are already there, and get the next index number exactly right. What if you're off by one, or the list's length changes without you noticing?"

**Attempt 2:** "I'd rather use something that automatically adds the item to the end, without me tracking index numbers myself." ✅ vs. "I'll just carefully count the items myself each time." ❌

**Stage 2 Concept Reveal:**
> "This is Python's `.append()` method. `scores.append(90)` tacks `90` onto the very end of the `scores` list, automatically no index counting, no rebuilding."

**Stage 3 Guided Code Build:**
```
scores = [88, 92, 79, 95, 84]
_______________________________
print(scores)
```
Tokens: `scores.append(90)` ✅ · `scores.add(90)` (wrong method name that's for sets) · `append(scores, 90)` (wrong call order)

---

### B. Last Score Check (Negative Indexing)

**Scenario:** "Print the most recent score added to the list, without counting how many scores are in it."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Access the last item directly using a position counted backward from the end." | ✅ | Concept Reveal |
| "Count how many scores are in the list, then use that count as the index." | 🟡 partial (works, but is an extra roundabout step) | Reflective Prompt |
| "Guess the last index number based on how many scores you remember adding." | ❌ | Reflective Prompt |

**Reflective Prompt (count then index):**
> "That works, but it means doing an extra counting step every single time and remembering to subtract 1, since indexing starts at 0. Is there a more direct way to say 'give me the last one,' without counting first?"

**Attempt 2:** "Yes access it directly by counting backward from the end, with no separate counting step needed." ✅ vs. "No, counting first is the only reliable way." ❌

**Reflective Prompt (guess from memory):**
> "Relying on memory breaks the moment the list changes size without you noticing. What if instead you had a way to always land on 'the end,' automatically, no matter how long the list currently is?"

**Attempt 2:** "Yes something that always points at the last item, regardless of the list's current length." ✅ vs. "I'll just keep track of the size in my head." ❌

**Stage 2 Concept Reveal:**
> "Python lets you index from the *end* using negative numbers. `scores[-1]` means 'the last item,' `scores[-2]` means 'the second-to-last,' and so on no counting or length-checking needed."

**Stage 3 Guided Code Build:**
```
scores = [88, 92, 79, 95, 84]
print(_______________)
```
Tokens: `scores[-1]` ✅ · `scores[-0]` (there's no separate negative zero it's the same as `scores[0]`, the *first* item) · `scores[last]` (not valid Python syntax)

---

### C. How Many Scores? (`len()`)

**Scenario:** "Before announcing results, check how many players actually submitted a score."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Ask Python directly for the number of items currently in the list." | ✅ | Concept Reveal |
| "Manually count the scores by reading through the list yourself each time." | ❌ | Reflective Prompt |
| "Keep a separate counter variable that you increase every time you add a score." | 🟡 partial (works, but has to be kept in sync by hand forever) | Reflective Prompt |

**Reflective Prompt (manual count):**
> "What happens once the list has hundreds of scores in it would counting them by eye still be practical or reliable?"

**Attempt 2:** "No I want Python to tell me the count directly, instantly, no matter how big the list is." ✅ vs. "I'll just keep counting by eye, carefully." ❌

**Reflective Prompt (separate counter variable):**
> "That means keeping two things in sync forever the list *and* your counter and remembering to update the counter every single time the list changes. Is there a way to just ask the list itself, right when you need the number?"

**Attempt 2:** "Yes ask directly for the current count, whenever I need it, instead of tracking it separately." ✅ vs. "No a separate counter is the only way to know a list's size." ❌

**Stage 2 Concept Reveal:**
> "This is Python's built-in `len()` function. `len(scores)` returns the number of items currently in `scores` always accurate, since it checks the list itself, right now."

**Stage 3 Guided Code Build:**
```
scores = [88, 92, 79, 95, 84]
print(_______________)
```
Tokens: `len(scores)` ✅ · `scores.len()` (wrong `len()` is a function you call *on* the list by passing it in, not a method) · `count(scores)` (wrong function `.count()` counts occurrences of a *specific value*, not the list's length)

---

## LEVEL 3 Two Case Studies

### A. Top 3 Leaderboard (Slicing)

**Scenario:** "Display just the top 3 scores from a sorted list of scores, without the rest."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Take a portion of the list a *slice* spanning from the start up to (but not including) the 4th position." | ✅ | Concept Reveal |
| "Loop through the whole list and print only the first three items, using a check on the position each time." | 🟡 partial (works, but is a lot of machinery for a simple chunk) | Reflective Prompt |
| "Create three separate variables, one for each of the first three scores, copied by hand." | ❌ | Reflective Prompt |

**Reflective Prompt (loop + position check):**
> "That works, but it means writing a whole repeat structure with a counting check just to grab three items. Is there a way to grab a *chunk* of the list directly, in one step, without looping at all?"

**Attempt 2:** "Yes take a direct slice of the list covering just those positions, no loop needed." ✅ vs. "No, looping with a check is the only way to get part of a list." ❌

**Reflective Prompt (3 separate variables):**
> "What if the leaderboard needed the top 10 instead of the top 3 would copying each one into its own variable by hand still be practical?"

**Attempt 2:** "No I want one instruction that grabs a range of positions at once, however many that is." ✅ vs. "I'd still copy each one individually, just more of them." ❌

**Stage 2 Concept Reveal:**
> "This is called **slicing**: `scores[0:3]` means 'give me items starting at index 0, up to but not including index 3.' The end number is always *exclusive*, so `0:3` grabs exactly 3 items: indexes 0, 1, and 2."

**Stage 3 Guided Code Build:**
```
scores = [95, 92, 88, 84, 79]
print(scores[___])
```
Tokens: `0:3` ✅ · `1:3` (wrong start skips the very first item) · `0:4` (wrong end includes a 4th item, since the end is exclusive)

---

### B. Disqualified Player (Removing by Value)

**Scenario:** "A player is disqualified. Remove their score, 79, from the list you don't know its position, just its value."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Remove the item by its actual value directly, without needing to know its position in the list." | ✅ | Concept Reveal |
| "Find the position of the value first by manually scanning the list, then delete that exact position." | 🟡 partial (works, but adds an unnecessary search step) | Reflective Prompt |
| "Create a brand-new list that leaves out that one value, by retyping everything else." | ❌ | Reflective Prompt |

**Reflective Prompt (scan then delete by position):**
> "That means doing an extra manual search step every time, just to find a position you don't actually care about remembering. Is there a way to remove something by *what it is*, directly, skipping the position-finding step?"

**Attempt 2:** "Yes remove it directly by its value, and let Python find and delete it." ✅ vs. "No, I'd always find the position first." ❌

**Reflective Prompt (retype without it):**
> "If the list had hundreds of scores, would retyping all of them minus one still make sense?"

**Attempt 2:** "No I want to remove just that one value from the existing list, in place." ✅ vs. "I'd still prefer to rebuild it from scratch." ❌

**Stage 2 Concept Reveal:**
> "This is Python's `.remove()` method. `scores.remove(79)` searches the list for the value `79` and deletes the *first* matching item it finds no position needed."

**Stage 3 Guided Code Build:**
```
scores = [95, 92, 88, 84, 79]
_______________________________
print(scores)
```
Tokens: `scores.remove(79)` ✅ · `scores.delete(79)` (wrong method name lists have no `.delete()`) · `remove(scores, 79)` (wrong call order it's called *on* the list)

---

## LEVEL 4 Filtering Passing Scores (Combining Loop + Condition + List)

**Scenario:** "Go through all scores and build a new list containing only the passing scores (60 or above)."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Start with an empty new list, then loop through every score, and for each one that meets the passing condition, add it to the new list." | ✅ | Concept Reveal |
| "Loop through the scores and just print out the ones that pass, without saving them anywhere new." | ❌ | Reflective Prompt |
| "Build a new list manually, typing in only the scores you remember being passing ones." | 🟡 partial (works once, but isn't reusable or accurate as data changes) | Reflective Prompt |

**Reflective Prompt (just print):**
> "If you need to *reuse* the passing scores later say, to calculate their average would printing them be enough, or do you need them saved somewhere?"

**Attempt 2:** "I need them saved in a new list I can reuse later, not just displayed once." ✅ vs. "Printing is enough, I don't need to reuse them." ❌

**Reflective Prompt (manual typing):**
> "What happens if the original list has 500 scores and changes every day would manually retyping the passing ones by memory still work reliably?"

**Attempt 2:** "No I need the computer to check each score automatically and build the new list itself." ✅ vs. "I'll just keep updating it by hand whenever it changes." ❌

**Stage 2 Concept Reveal:**
> "This combines three things you already know: start with an **empty list** (`passing = []`), a **`for` loop** to go through every score, and an **`if` check** inside it. When the condition is true, `.append()` adds that score to the new list. None of these three pieces alone solves it it's their combination that builds a filtered list."

**Stage 3 Guided Code Build:**
```
scores = [45, 88, 60, 30, 92, 55]
passing = ___
for score in scores:
    if score >= 60:
        _______________________________
print(passing)
```
Tokens for blank 1: `[]` ✅ · `{}` (wrong creates an empty dictionary/set, not a list)
Tokens for blank 2: `passing.append(score)` ✅ · `scores.append(score)` (wrong list appends back onto the original instead of the new one) · `passing.append(scores)` (wrong value appends the *entire* list instead of the single current score)

---

## LEVEL 5 Teach-Back (Extended Abstract)

> "Design a new case study that teaches **sorting a list** (using `sorted()` or `.sort()`) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), the reflective prompts, the concept reveal, and the syntax token set for the guided build afterward."

This asks the learner to build *all three stages* of the engine themselves logic test, concept reveal, and guided build which is the strongest possible test of understanding: they're not just solving the scaffold, they're designing it.
