# PyBe String Manipulation Unit Plain-English-First Roadmap (Levels 1–4)

## Design Notes

String Manipulation is PyBe's fourth unit, following Loops, Conditionals, and Functions. The same three-stage engine applies:

1. **Logic Test (plain English)** Attempt 1, and Attempt 2 if needed, ask the learner to choose an approach for extracting, cleaning, or checking text, described entirely in plain English never as Python syntax.
2. **Concept Reveal (syntax explained)** only here does PyBe introduce indexing, slicing, string methods, and operators, explained piece by piece.
3. **Guided Code Build (syntax practice)** the learner fills in blanks using the syntax just explained, with quick inline corrections on wrong clicks.

Level 1 is the pain of manually handling text character-by-character. Level 2 isolates three separate string mechanics side by side without mixing them. Level 3 combines a known mechanic with one brand-new one. Level 4 requires combining several mechanics inside a single working scenario, plus an open-ended Teach-Back.

---

## LEVEL 1 Conference Badge Initials

**Scenario:** "Print just the first letter of each attendee's name on their conference badge for hundreds of attendees, you're currently looking at each name and manually typing just its first letter yourself."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Grab the character sitting at a specific position in the text the very first one directly, instead of retyping it by hand." | ✅ | Concept Reveal |
| "Read the whole name and manually copy just the first letter for each person." | ❌ | Reflective Prompt |
| "Keep a separate list of everyone's initials, prepared in advance, and print from that instead." | 🟡 partial (doesn't scale every new attendee still needs the same manual work done somewhere) | Reflective Prompt |
| "Delete every letter except the first one, using a text editor, for each name." | ❌ | Reflective Prompt |

**Reflective Prompt (manual copy):**
> "With hundreds of attendees registering right up until the event, would manually reading and retyping each name's first letter still be realistic on the day?"

**Attempt 2:** "No I need the computer to grab that one position automatically, for any name, without me reading it myself." ✅ vs. "It's fine, I'll just work faster." ❌

**Reflective Prompt (separate prepared list):**
> "That list has to be built by doing this same manual work in advance, for every single name. Does preparing the list ahead of time actually avoid the original problem, or just move it earlier?"

**Attempt 2:** "It just moves the same manual work earlier I still need a way to grab the first character automatically, for any name, at any time." ✅ vs. "It's fine, doing it in advance is good enough." ❌

**Reflective Prompt (text editor deletion):**
> "That still requires opening and editing every single name by hand, one at a time. How is that different in effort from typing each initial yourself?"

**Attempt 2:** "It isn't really different I need the position of the first character grabbed automatically, not edited by hand." ✅ vs. "It's a bit faster, so it's fine." ❌

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'grab the character at a specific position' is written in Python using **indexing** with square brackets. Breaking it down:
> - Every character in a string has a **position**, called an index, starting from `0` not `1`.
> - `name[0]` means 'give me the character at position 0' the very first one.
> - Square brackets `[ ]` are how Python accesses a position in a string."

### Stage 3 Guided Code Build

**Code shown:**
```
name = "Aditi"
initial = _____
print(initial)
```
**Token buttons:** `name[0]` ✅ · `name[1]` (off-by-one gives the second letter, not the first) · `name(0)` (wrong brackets Python uses square brackets `[ ]` for indexing, not parentheses)

Wrong click → inline correction only, as shown above. No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. Area Code Extractor

**Scenario:** "Extract the area code the first 3 digits from a phone number like '9876543210' for every customer record, instead of manually counting and copying the first three digits each time."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Grab a whole range of characters at once from the start up to (but not including) a certain position directly." | ✅ | Concept Reveal |
| "Grab each of the first three characters one at a time, individually, and join them back together." | 🟡 partial (works, but is three separate steps for something that could be one) | Reflective Prompt |
| "Manually count and copy the first three digits from each phone number by eye." | ❌ | Reflective Prompt |

**Reflective Prompt (one at a time, then join):**
> "You already know how to grab a single character by its position. If you need three characters that sit right next to each other, is there a way to ask for that whole *range* in one step, instead of three separate ones?"

**Attempt 2:** "Yes ask for a whole range of positions at once, instead of grabbing each character separately." ✅ vs. "No, I'll always grab them one at a time and join them." ❌

**Reflective Prompt (manual copy):**
> "With thousands of customer records, would counting and copying the first three digits by eye, every single time, actually be practical?"

**Attempt 2:** "No I need the computer to grab that range of positions automatically, for any phone number." ✅ vs. "It's fine, I'll just be careful counting each time." ❌

**Stage 2 Concept Reveal:**
> "This is **slicing**: `phone[0:3]` means 'give me everything from position 0 up to, but not including, position 3' that's exactly three characters. The first number is where to start, the second is where to stop (without including that position)."

**Stage 3 Guided Code Build:**
```
phone = "9876543210"
area_code = __________
print(area_code)
```
Tokens: `phone[0:3]` ✅ · `phone[0:4]` (off-by-one includes an extra digit) · `phone[0,3]` (wrong punctuation slicing uses a colon `:`, not a comma)

---

### B. Messy Signup Form

**Scenario:** "Users type their names in all sorts of styles 'JOHN', 'john', '  John  ' with extra spaces and every name needs to look neat and consistently capitalized (like 'John') before it's saved, instead of manually retyping each one to fix it."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Use built-in text-cleanup actions to strip extra spaces and fix the capitalization automatically, for any name typed in." | ✅ | Concept Reveal |
| "Ask users to retype their name correctly if it looks wrong." | ❌ (relies on the user, doesn't actually fix anything) | Reflective Prompt |
| "Manually open each saved record afterward and fix the spacing and capitalization by hand." | 🟡 partial (fixes it after the fact, doesn't prevent the same problem on every new signup) | Reflective Prompt |

**Reflective Prompt (ask user to retype):**
> "If a user doesn't notice their name looks wrong, or doesn't bother fixing it, does asking politely actually guarantee clean data gets saved?"

**Attempt 2:** "No the cleanup should happen automatically, without depending on the user noticing or cooperating." ✅ vs. "It's fine, most users will fix it if asked." ❌

**Reflective Prompt (fix records afterward by hand):**
> "New signups keep happening every day. Does fixing old records by hand do anything to stop *new* messy names from being saved tomorrow?"

**Attempt 2:** "No the cleanup needs to happen automatically to every name, right when it's entered, not applied by hand afterward." ✅ vs. "It's fine, I'll just keep fixing records manually as they come in." ❌

**Stage 2 Concept Reveal:**
> "Python has built-in **string methods** for exactly this: `.strip()` removes extra spaces from the start and end, and `.title()` capitalizes the first letter of each word. Chaining them together `name.strip().title()` cleans the whole thing in one step."

**Stage 3 Guided Code Build:**
```
name = "  john  "
clean_name = name.____________.____________
print(clean_name)
```
Tokens: `strip()` ✅ (first blank) · `title()` ✅ (second blank) · `Strip()` (wrong capitalization Python method names are case-sensitive and lowercase) · `strip` (missing parentheses inline-corrected: "Methods need parentheses `()` to actually run, even with nothing inside them.")

---

### C. Comment Filter

**Scenario:** "Automatically flag any comment that contains the word 'spam' anywhere inside it, instead of reading every single comment yourself to check."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Ask directly whether that word appears anywhere inside the comment's text." | ✅ | Concept Reveal |
| "Check only whether the comment's text exactly equals the word 'spam,' with nothing else in it." | ❌ (too strict misses comments where 'spam' is just part of a longer sentence) | Reflective Prompt |
| "Read through the comment character by character yourself, comparing chunks of it to the word 'spam.'" | 🟡 partial (would technically work, but reinvents something the language already provides directly) | Reflective Prompt |

**Reflective Prompt (exact match only):**
> "A real comment might be 'this looks like spam to me' the whole comment isn't just the word 'spam,' but it does contain it. Would checking for an exact match catch that comment?"

**Attempt 2:** "No I need to check whether the word appears *anywhere inside* the comment, not whether the comment is only that word." ✅ vs. "That's fine, I'll assume spam comments are always just the one word." ❌

**Reflective Prompt (character-by-character comparison):**
> "There's already a direct, one-step way to ask 'does this smaller piece of text appear inside this larger piece of text?' Would writing your own character-by-character comparison actually do anything that direct check doesn't already do?"

**Attempt 2:** "No I should just use the direct built-in way of checking if one piece of text appears inside another." ✅ vs. "I'll still write my own comparison, just to be thorough." ❌

**Stage 2 Concept Reveal:**
> "This is the **`in`** operator used with text: `"spam" in comment` asks 'does this exact piece of text appear anywhere inside `comment`?' and gives back `True` or `False` no counting, no character-by-character comparison needed."

**Stage 3 Guided Code Build:**
```
comment = "this looks like spam to me"
is_flagged = ________________
print(is_flagged)
```
Tokens: `"spam" in comment` ✅ · `"spam" == comment` (checks for an exact match instead of "appears inside" inline-corrected: "`==` only matches if the *entire* comment is exactly `\"spam\"`. `in` checks whether it appears anywhere inside.") · `comment in "spam"` (reversed inline-corrected: "This checks whether the whole comment appears inside the single word 'spam,' which is backwards.")

---

## LEVEL 3 Masked Card Number

**Scenario:** "Show a credit card number on a receipt, but hide every digit except the last four for example, '1234567890123456' should display as '************3456'."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Grab the last four characters using position-based extraction like before, and join that with a run of asterisks placed in front of it." | ✅ | Concept Reveal |
| "Manually replace every digit except the last four, one at a time, for each card number." | ❌ | Reflective Prompt |
| "Turn the entire number into asterisks first, then count from the front to place the real last four digits back in." | 🟡 partial (fragile depends on knowing exactly how long the total number is, and breaks if card lengths vary) | Reflective Prompt |

**Reflective Prompt (manual replace, one at a time):**
> "Card numbers can be 15 or 16 digits depending on the card type. Would manually replacing digits one at a time still work cleanly if you didn't know the length in advance?"

**Attempt 2:** "No I need an approach that works regardless of exactly how many digits there are." ✅ vs. "It's fine, most cards are the same length anyway." ❌

**Reflective Prompt (turn all to asterisks, count from front):**
> "This depends on knowing the *exact total length* to count back in the real digits correctly. What happens if one customer's card number is a different length than you assumed?"

**Attempt 2:** "It could place the real digits in the wrong spot. I should extract the last four directly, by position from the *end*, rather than counting from the front based on an assumed total length." ✅ vs. "I'll just assume every card number is exactly the same length." ❌

### Stage 2 Concept Reveal (syntax explained)

> "You already know slicing from position 0. Slicing also works from the **end** using negative positions: `card[-4:]` means 'give me everything from the 4th-to-last character onward' the last four digits, regardless of total length. To build the masked version, Python can also **multiply** a string `"*" * 12` repeats the asterisk 12 times and **join** two strings together end-to-end using `+`."

### Stage 3 Guided Code Build

**Code shown:**
```
card = "1234567890123456"
last_four = card[-4:]
masked = _______________________________
print(masked)
```
**Token buttons:** `"*" * 12 + last_four` ✅ · `"*" + 12 + last_four` (adds a string and a number directly inline-corrected: "Python can't `+` a string and a number together directly string repetition needs `*`, like `\"*\" * 12`.") · `"*" * 12 - last_four` (wrong operator inline-corrected: "Subtraction doesn't apply to strings joining two strings together uses `+`.")

Wrong click → inline correction only, as shown above. No new reflective cycle; they simply retry the blank.

---

## LEVEL 4 Business Card Formatter (Combining String Mechanics)

**Scenario:** "Turn messy input a name typed as '  john smith  ' and a title typed as 'software engineer' into a properly formatted business card line: 'John Smith, Software Engineer' cleanly capitalized, with no extra spaces, correctly joined together."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "First remove the extra spaces and fix the capitalization on both pieces separately, then join them together with the right punctuation in between." | ✅ | Concept Reveal |
| "Join the name and title together first, exactly as typed, then try to fix the spacing and capitalization of the combined result afterward." | 🟡 partial (harder to fix correctly once everything is merged into one messy piece of text) | Reflective Prompt |
| "Just join the two pieces together with a comma, and leave the spacing and capitalization exactly as the user typed them." | ❌ | Reflective Prompt |

**Reflective Prompt (join first, fix after):**
> "Once 'john smith' and 'software engineer' are merged into one long piece of text with a comma, is it still just as easy to fix each part's capitalization individually? Or does cleaning each piece separately, *before* joining, make this simpler?"

**Attempt 2:** "It's simpler to clean each piece separately first clean each one, and only combine them at the very end." ✅ vs. "It's fine either way, I'll fix the combined text afterward." ❌

**Reflective Prompt (leave as typed):**
> "Would '  john smith  , software engineer' actually look like a properly formatted business card line to a customer?"

**Attempt 2:** "No both pieces need their spacing and capitalization cleaned up before being joined, not left exactly as typed." ✅ vs. "It's close enough, customers won't mind." ❌

### Stage 2 Concept Reveal (syntax explained)

> "This combines everything you already know: `.strip()` and `.title()` clean each piece individually `name.strip().title()` and `title.strip().title()` and then an **f-string** joins them into one final formatted line: `f"{name}, {title}"` inserts each cleaned value directly into the text, in the right place, without manually adding `+` between every piece."

### Stage 3 Guided Code Build

**Code shown:**
```
name = "  john smith  "
title = "software engineer"

clean_name = name.strip().title()
clean_title = title.strip().title()

business_card = ______________________________
print(business_card)
```
**Token buttons:** `f"{clean_name}, {clean_title}"` ✅ · `"clean_name, clean_title"` (treats the variable names as literal text instead of inserting their values inline-corrected: "Without the `f` and curly braces `{}`, Python prints the literal words `clean_name` and `clean_title`, not what's stored inside them.") · `f"{name}, {title}"` (uses the original messy values instead of the cleaned ones inline-corrected: "This inserts the original, un-cleaned `name` and `title` use `clean_name` and `clean_title` instead.")

### Teach-Back (Level 4, open-ended)

> "Design a new case study for **f-strings versus plain `+` concatenation** (when inserting numbers or multiple values makes an f-string clearer than chaining `+` signs together) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), and the syntax token set for the guided build afterward."

This asks the learner to build all three stages of the engine themselves for a related-but-not-yet-taught refinement, the strongest possible test of Extended Abstract understanding: they're not just formatting text correctly, they're designing how to teach a cleaner way of doing it.

---

## Summary Concept Coverage Map

| Level | Case Study | Core Mechanic Introduced |
|---|---|---|
| 1 | Conference Badge Initials | Indexing `text[0]`, positions starting at 0 |
| 2A | Area Code Extractor | Slicing a range `text[0:3]` |
| 2B | Messy Signup Form | String methods `.strip()`, `.title()` |
| 2C | Comment Filter | The `in` operator checking if text appears inside text |
| 3 | Masked Card Number | Negative-index slicing, string multiplication (`*`), and concatenation (`+`) |
| 4 | Business Card Formatter | Combining methods + slicing + f-strings in one working scenario |
