# PyBe Dictionaries Unit Plain-English-First Roadmap (Levels 1–5)

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

## LEVEL 1 Two Lists Falling Out of Sync

**Scenario:** "You're tracking players and their scores using two separate lists: `names = ['Aditi', 'Ravi', 'Meera']` and `scores = [88, 92, 79]`. You need to look up Ravi's score."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Store each name paired directly with its own score, so looking one up doesn't depend on two lists staying in the same order." | ✅ Correct | Concept Reveal |
| "Find Ravi's position in the names list, then use that same position number to look up the score in the scores list." | ❌ Wrong (fragile the two lists can silently fall out of sync) | Reflective Prompt |
| "Just remember the pairing in your head Ravi is always second in both lists." | 🟡 Not absolutely correct (works for 3 players, breaks down at scale) | Reflective Prompt |

**Reflective Prompt (matching positions across two lists):**
> "What happens if someone sorts the scores list by highest first, but forgets to sort the names list the same way would the pairing still be correct?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No that's risky since the two lists could easily fall out of sync. I need the name and score bound together directly, not linked by matching position." | ✅ | Concept Reveal (via reflection) |
| "It's fine as long as I'm careful to keep both lists in the same order." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (remember in your head):**
> "That works for 3 players. What about 300 would you still be able to reliably remember every pairing?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No I need the computer to store the pairing directly, not rely on my memory." | ✅ | Concept Reveal (via reflection) |
| "I'd just keep memorizing more pairings as the list grows." | ❌ | Concept Reveal (direct) |

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'pair each name directly with its score' is written in Python as a **dictionary**. Breaking it down piece by piece:
> - Curly braces `{ }` mark the start and end.
> - Each entry is written as `key: value` here, a name paired with its score.
> - Commas separate multiple pairs.
> - You look up a value using its key in square brackets, not a position number: `scores['Ravi']`."

### Stage 3 Guided Code Build

**Code shown:**
```
_______________________________________________
print(scores['Ravi'])
```
**Token buttons:** `scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}` ✅ · `scores = ['Aditi': 88, 'Ravi': 92, 'Meera': 79]` (wrong brackets square brackets can't hold `key: value` pairs) · `scores = {'Aditi'=88, 'Ravi'=92, 'Meera'=79}` (wrong separator dictionaries use `:`, not `=`)

Wrong click → inline correction only: "Almost dictionaries use curly braces `{ }` with `key: value` pairs separated by colons, not equals signs, and square brackets are for lists." No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. New Player Registers (Adding a Key)

**Scenario:** "A new player, Kabir, joins with a score of 74. Add him to the existing `scores` dictionary."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Assign the new score directly to a new key, and Python will add it to the dictionary automatically." | ✅ | Concept Reveal |
| "Rebuild the whole dictionary from scratch, retyping every existing pair plus the new one." | ❌ | Reflective Prompt |
| "Add Kabir's score to the end of the dictionary, the same way you'd append to a list." | 🟡 partial (right instinct, wrong tool dictionaries have no `.append()`) | Reflective Prompt |

**Reflective Prompt (rebuild from scratch):**
> "If the dictionary already held hundreds of players, would retyping all of them just to add one more make sense?"

**Attempt 2:** "No I want to add just the one new pair, leaving everything else untouched." ✅ vs. "I'd still prefer to retype the whole thing." ❌

**Reflective Prompt (append like a list):**
> "Dictionaries don't have a position-based 'end' the way lists do pairs aren't ordered by when you added them for lookup purposes. What might actually work for adding a *new key*, specifically?"

**Attempt 2:** "I should assign a value directly to the new key using square brackets, not use a list method like append." ✅ vs. "I'll just try `.append()` on it anyway." ❌

**Stage 2 Concept Reveal:**
> "To add a new pair, assign directly: `scores['Kabir'] = 74`. If the key `'Kabir'` doesn't already exist, Python creates it. There's no `.append()` for dictionaries assignment *is* how you add."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
_______________________________
print(scores)
```
Tokens: `scores['Kabir'] = 74` ✅ · `scores.append('Kabir', 74)` (wrong dictionaries have no `.append()`) · `scores['Kabir'] == 74` (wrong operator `==` checks equality, it doesn't store anything)

---

### B. Does This Player Exist? (`in` keyword)

**Scenario:** "Before printing a score, check whether `'Zara'` is actually in the `scores` dictionary she might not have played yet."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Directly ask Python whether that key exists in the dictionary before trying to use it." | ✅ | Concept Reveal |
| "Just try to look up the score anyway, and assume it'll show something like 'None' or blank if she's missing." | ❌ | Reflective Prompt |
| "Loop through every key in the dictionary by hand, comparing each one to `'Zara'`." | 🟡 partial (works, but reinvents something Python already provides) | Reflective Prompt |

**Reflective Prompt (assume a quiet blank result):**
> "What actually happens in Python when you look up a key that isn't there does it quietly give you nothing, or does it stop your program with an error?"

**Attempt 2:** "I should check first, since looking up a missing key actually causes an error, not a quiet blank result." ✅ vs. "I'll just look it up directly and hope it's fine." ❌

**Reflective Prompt (loop through manually):**
> "Checking membership one key at a time works, but is there something built directly into Python that already asks 'is this key in here?' without you writing the loop yourself?"

**Attempt 2:** "Yes a direct built-in way to check membership, without looping myself." ✅ vs. "No, I'd always write my own loop to check." ❌

**Stage 2 Concept Reveal:**
> "Python's `in` keyword checks membership directly: `'Zara' in scores` returns `True` or `False` depending on whether that key exists no loop needed, and no risk of an error from a missing key."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
if _______________________:
    print(scores['Zara'])
else:
    print("No score yet")
```
Tokens: `'Zara' in scores` ✅ · `scores in 'Zara'` (wrong order this checks if the whole dictionary is inside the word 'Zara') · `'Zara' == scores` (wrong operator compares the whole dictionary to the name)

---

### C. Correcting a Score (Updating a Value)

**Scenario:** "Ravi's score was entered wrong. Update it from 92 to 95."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Assign the new value directly to the existing key Python will overwrite the old value automatically." | ✅ | Concept Reveal |
| "Remove Ravi's entry entirely first, then add a brand-new pair with the corrected score." | 🟡 partial (works, but is an unnecessary extra step) | Reflective Prompt |
| "Add a second entry for Ravi with the new score, keeping the old one too." | ❌ | Reflective Prompt |

**Reflective Prompt (remove then re-add):**
> "Since assigning to an existing key just replaces its value automatically, is that extra remove-then-add step actually necessary?"

**Attempt 2:** "No I can just assign directly to the existing key and the old value gets overwritten automatically." ✅ vs. "I'll still remove it first, just to be safe." ❌

**Reflective Prompt (add a second entry):**
> "A dictionary key can only point to *one* value at a time what actually happens if you assign to a key that already exists, rather than adding a new one?"

**Attempt 2:** "Assigning to an existing key overwrites its current value it doesn't create a duplicate." ✅ vs. "I believe both values would somehow be kept." ❌

**Stage 2 Concept Reveal:**
> "Updating uses the exact same syntax as adding: `scores['Ravi'] = 95`. If the key already exists, Python overwrites its value instead of creating a new one one key always maps to exactly one value."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
_______________________________
print(scores['Ravi'])
```
Tokens: `scores['Ravi'] = 95` ✅ · `scores['Ravi'] += 92` (wrong adds to the existing value instead of replacing it, giving 184, not 95) · `scores.update(95)` (wrong `.update()` needs a key:value pair or another dictionary, not a lone number)

---

## LEVEL 3 Two Case Studies

### A. Announce All Player Names (`.keys()` and looping)

**Scenario:** "Print every player's name in the `scores` dictionary, one per line you don't need their scores for this."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Loop through just the keys of the dictionary, printing each one directly." | ✅ | Concept Reveal |
| "Loop through the whole dictionary and print each item as though it were a score." | ❌ | Reflective Prompt |
| "Convert the dictionary into a list of names first, typing them out by hand from what you remember." | 🟡 partial (unreliable and doesn't scale) | Reflective Prompt |

**Reflective Prompt (loop as if it gives scores):**
> "A dictionary holds pairs, not a single flat sequence what specifically do you get if you loop over a dictionary directly, without asking for keys or values?"

**Attempt 2:** "Looping over a dictionary directly gives me the keys, not the values so I should loop over it (or `.keys()`) to get names." ✅ vs. "I'd assume looping gives me the values automatically." ❌

**Reflective Prompt (retype from memory):**
> "If the dictionary had 200 players, would retyping their names from memory be accurate or realistic?"

**Attempt 2:** "No I want Python to pull the actual names directly from the dictionary itself." ✅ vs. "I'd still try to recall and retype them." ❌

**Stage 2 Concept Reveal:**
> "Looping over a dictionary directly `for name in scores:` automatically gives you each **key**, one at a time (that's the default behavior). You can also be explicit with `.keys()`: `for name in scores.keys():` both do the same thing here."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
_______________________:
    print(name)
```
Tokens: `for name in scores` ✅ · `for name in scores.values()` (wrong this gives scores, not names) · `for name, score in scores` (wrong looping bare gives just one value per round, the key not a pair, so this errors)

---

### B. Total of All Scores (`.values()`)

**Scenario:** "Add up every score in the dictionary to find the class total names don't matter for this."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Loop through just the values of the dictionary, adding each one to a running total." | ✅ | Concept Reveal |
| "Loop through the dictionary's keys, and try adding the names themselves as if they were numbers." | ❌ | Reflective Prompt |
| "Manually type in each score from what you remember seeing, and add those together." | 🟡 partial (unreliable and doesn't scale) | Reflective Prompt |

**Reflective Prompt (add the keys/names):**
> "Names are text, not numbers what actually happens if you try to add a piece of text to a running numeric total with `+`?"

**Attempt 2:** "That would raise an error immediately, since you can't add text to a number that way I need the *values*, not the keys, to add numbers." ✅ vs. "I'll just try adding the names and see what happens." ❌

**Reflective Prompt (manual retyping):**
> "What if scores change frequently, or the dictionary grows large would manually re-adding remembered numbers stay accurate?"

**Attempt 2:** "No I want Python to pull the current values directly and add them up itself." ✅ vs. "I'd keep recalculating by hand each time." ❌

**Stage 2 Concept Reveal:**
> "`.values()` gives you just the values from a dictionary, ignoring the keys entirely: `for score in scores.values():` lets you loop through only the numbers, ready to add up."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
total = 0
_______________________:
    total = total + score
print(total)
```
Tokens: `for score in scores.values()` ✅ · `for score in scores.keys()` (wrong gives names, not numbers) · `for score in scores` (wrong here gives keys by default, same problem)

---

## LEVEL 4 Full Leaderboard (Combining Keys and Values)

**Scenario:** "Print a full leaderboard line for every player, formatted like `'Aditi: 88'` you need both the name *and* the score together, for every entry."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Loop through the dictionary in a way that gives you *both* the key and the value together, for each pair, in a single step." | ✅ | Concept Reveal |
| "Loop through just the keys, then separately loop through just the values, and hope they line up in the same order." | ❌ | Reflective Prompt |
| "Loop through the keys, and inside the loop, look up each score separately using the key each time." | 🟡 partial (works, but adds an unnecessary lookup every round) | Reflective Prompt |

**Reflective Prompt (two separate loops):**
> "Even if both loops technically go in the same order, you'd need to run two separate loops and carefully keep them in sync. Is there a way to get both pieces *together*, in one loop, one pair at a time?"

**Attempt 2:** "Yes I want one loop that gives me the key and value together for each pair, not two separate loops to keep in sync." ✅ vs. "I'll just trust two separate loops to line up correctly." ❌

**Reflective Prompt (separate lookup inside the loop):**
> "That actually works, but it means doing an extra lookup step inside every round of the loop. Is there a way the loop just *hands you* both pieces directly, without a separate lookup?"

**Attempt 2:** "Yes I want the loop to give me both the key and its value directly, together, without a separate lookup each time." ✅ vs. "I'll keep doing the separate lookup it works fine." ❌

**Stage 2 Concept Reveal:**
> "This combines two things: a `for` loop, and Python's `.items()` method, which hands you *both* the key and value together, each round: `for name, score in scores.items():`. Neither `.keys()` alone nor `.values()` alone gives you both `.items()` is what pairs them."

**Stage 3 Guided Code Build:**
```
scores = {'Aditi': 88, 'Ravi': 92, 'Meera': 79}
_______________________________________:
    print(name, ":", score)
```
Tokens: `for name, score in scores.items()` ✅ · `for name, score in scores` (wrong looping bare only gives one value per round, so unpacking two names would error) · `for name, score in scores.keys()` (wrong `.keys()` gives only names, not pairs)

---

## LEVEL 5 Teach-Back (Extended Abstract)

> "Design a new case study that teaches using `.get()` with a default value (to safely look up a key that might not exist, without an error) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), the reflective prompts, the concept reveal, and the syntax token set for the guided build afterward."

This asks the learner to build *all three stages* of the engine themselves logic test, concept reveal, and guided build which is the strongest possible test of understanding: they're not just solving the scaffold, they're designing it.
