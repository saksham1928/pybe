# PyBe Functions Unit Plain-English-First Roadmap (Levels 1–4)

## Design Notes

Functions is PyBe's third unit, following Loops and Conditionals. The same three-stage engine applies:

1. **Logic Test (plain English)** Attempt 1, and Attempt 2 if needed, ask the learner to choose a *strategy* for organizing repeated or reusable logic, described entirely in plain English never as Python syntax.
2. **Concept Reveal (syntax explained)** only here does PyBe introduce `def`, parameters, `return`, and related keywords, explained piece by piece.
3. **Guided Code Build (syntax practice)** the learner fills in blanks using the syntax just explained. Wrong clicks get a quick inline correction, not a new reflective cycle.

The pedagogical arc across the four levels: Level 1 is the *pain* of not having functions at all (Prestructural). Level 2 isolates three separate function mechanics side by side without mixing them. Level 3 combines a known mechanic with one brand-new one for the first time (Relational groundwork). Level 4 requires combining several mechanics inside a single working scenario, plus an open-ended Teach-Back that pushes into Extended Abstract territory.

---

## LEVEL 1 Report Card Averages

**Scenario:** "You need to calculate the average test score for 5 different students. Each time, you write out the same three lines of math add up the scores, then divide by how many there are just swapping in different numbers for each student."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Write the steps once, give the whole process a name, and reuse that name with new numbers each time instead of retyping the steps." | ✅ Correct | Concept Reveal |
| "Copy and paste the same three lines of math for each student, changing only the numbers." | ❌ Wrong (works but doesn't scale, and every future change means editing every copy) | Reflective Prompt |
| "Put every student's scores in one list, then use a loop to repeat the calculation automatically." | 🟡 Not absolutely correct (solves repeating it *here*, but the calculation still can't be reused anywhere else in the program without rewriting it) | Reflective Prompt |
| "Write the formula as a comment above the code so you remember it correctly next time." | ❌ Wrong (a comment doesn't run it's just a note, it never actually performs the calculation) | Reflective Prompt |

**Reflective Prompt (if "copy and paste" chosen):**
> "Imagine the school later decides averages should round to one decimal place. If you copy-pasted the same three lines five times, how many places would you now have to go back and fix?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Package the steps once under one name, so fixing it in one place fixes it everywhere it's used." | ✅ | Concept Reveal (via reflection) |
| "Just be extra careful to edit all five copies correctly." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (if "list + loop" chosen):**
> "That handles these 5 students in this one script. But what if a different part of your program a report card page, a parent email also needs to calculate an average? Would you write the same math a third time?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "Give the calculation its own reusable name, so any part of the program can call it, not just this one loop." | ✅ | Concept Reveal (via reflection) |
| "Yes, I'd rewrite the same three lines wherever it's needed." | ❌ | Concept Reveal (direct) |

**Reflective Prompt (if "comment" chosen):**
> "A comment is just text for humans to read does Python ever actually run it as code? If you 'forget' to retype the math correctly, would the comment stop that mistake?"

**Attempt 2:**
| Option | Status | Routes to |
|---|---|---|
| "No I need the actual steps saved as something Python can run and reuse, not just a note beside it." | ✅ | Concept Reveal (via reflection) |
| "It's fine, comments are close enough to remind me." | ❌ | Concept Reveal (direct) |

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'package the steps once, give it a name, reuse it' is written in Python as a **function**, using the **`def`** keyword. Breaking it down piece by piece:
> - `def` tells Python you're defining a reusable block.
> - `calculate_average` is the name you're giving it you choose this.
> - `(scores)` is a **parameter** a placeholder for whatever list of numbers gets handed to it later.
> - The colon `:` and the indented lines below mark what happens *inside* the function.
> - `return` sends a result back out to wherever the function was called from."

### Stage 3 Guided Code Build

**Code shown:**
```
_____________________:
    return sum(scores) / len(scores)

print(calculate_average([85, 90, 78]))
```
**Token buttons:** `def calculate_average(scores)` ✅ · `def calculate_average(scores);` (wrong punctuation Python uses a colon `:`, not a semicolon) · `function calculate_average(scores)` (wrong keyword Python uses `def`, not `function`)

Wrong click → inline correction only: "Almost Python defines functions with `def`, and the line ends with a colon `:`, not a semicolon." No new reflective cycle; they simply retry the blank.

---

## LEVEL 2 Three Case Studies

### A. Welcome Screen

**Scenario:** "Print a welcome message on screen every time someone opens the app the message itself never needs to be used anywhere else afterward, it just needs to be shown."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Package the action itself the act of displaying something without needing to hand any result back afterward." | ✅ | Concept Reveal |
| "Package it so it hands back the message as a result, in case something later needs to reuse that exact text." | 🟡 partial (adds a result that nothing in this scenario actually needs) | Reflective Prompt |
| "Just write the print line directly every time the app opens, without wrapping it in anything reusable." | ❌ | Reflective Prompt |

**Reflective Prompt (hand back a result):**
> "Nothing in this scenario ever needs to reuse the welcome text afterward it's only ever displayed once, right there. Does handing back a result actually serve a purpose here?"

**Attempt 2:** "No since nothing downstream needs the message as data, the function can just perform the action and be done." ✅ vs. "Yes, it's safer to always hand something back just in case." ❌

**Reflective Prompt (write it directly, no wrapping):**
> "What if five different screens in the app all need to show this same welcome message? Would writing the print line separately on each screen create the same maintenance problem as before?"

**Attempt 2:** "Yes wrapping it in a reusable, named block means every screen calls the same one place." ✅ vs. "No, it's just one line, it's fine to repeat." ❌

**Stage 2 Concept Reveal:**
> "This is a function with no `return` at all it performs an action (like printing) and simply finishes. Not every function needs to hand a result back; some exist purely to *do* something, like `def show_welcome(): print('Welcome to PyBe!')`."

**Stage 3 Guided Code Build:**
```
______________________:
    print("Welcome to PyBe!")

show_welcome()
```
Tokens: `def show_welcome()` ✅ · `def show_welcome() return` (adds a `return` with nothing to return inline-corrected: "This function doesn't need to hand anything back no `return` needed.") · `def show_welcome[]` (wrong brackets parentheses `()`, not square brackets)

---

### B. Tip Calculator

**Scenario:** "Calculate the tip amount for a restaurant bill the amount changes every time depending on the bill total and what percentage the customer chooses, and the result needs to be used afterward to print the final total."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Package the calculation so it accepts the bill and the percentage as inputs, and hands back the tip amount as a result to use afterward." | ✅ | Concept Reveal |
| "Package the calculation so it prints the tip directly inside itself, without handing anything back." | 🟡 partial (works for printing, but the actual number is never available afterward to add to the total) | Reflective Prompt |
| "Package the calculation with the bill and percentage typed directly inside it, fixed in place." | ❌ | Reflective Prompt |

**Reflective Prompt (print inside, nothing handed back):**
> "You also need to add the tip to the bill afterward to show a grand total. If the function only prints the tip and never hands it back, is that number available anywhere else in your program?"

**Attempt 2:** "No I need the actual number returned, so I can use it in further calculations, not just displayed." ✅ vs. "I'll just retype the tip amount by hand after reading what got printed." ❌

**Reflective Prompt (fixed values inside):**
> "Every customer's bill and desired tip percentage is different. If the numbers are fixed inside the function itself, does it still work for the next customer with a different bill?"

**Attempt 2:** "No the bill and percentage need to be inputs the function accepts, not fixed numbers baked inside it." ✅ vs. "I'd just rewrite the function each time with new fixed numbers." ❌

**Stage 2 Concept Reveal:**
> "This function takes **two parameters** `bill` and `percent` and uses `return` to hand back a calculated result: `def calculate_tip(bill, percent): return bill * (percent / 100)`. Whatever the function returns can then be stored, printed, or used in further math wherever it's called."

**Stage 3 Guided Code Build:**
```
def calculate_tip(bill, percent):
    ________________________

tip = calculate_tip(500, 15)
print(tip)
```
Tokens: `return bill * (percent / 100)` ✅ · `print bill * (percent / 100)` (prints inside the function instead of returning inline-corrected: "This shows the number but doesn't hand it back `tip` outside the function would have nothing to store.") · `return bill * percent / 100 / 100` (double-divides by 100 wrong math)

---

### C. Shipping Confirmation

**Scenario:** "Send a shipping confirmation message for every order. Almost every order ships via 'Standard' delivery, but a rare few customers pay extra for 'Express' right now you have to type the shipping method for every single order, even though it's 'Standard' almost every time."

**Stage 1 Attempt 1:**
| Option | Status | Routes to |
|---|---|---|
| "Give the shipping-method input an automatic fallback value that's used whenever nothing different is specified, so you only type something when it's actually different." | ✅ | Concept Reveal |
| "Require the shipping method to be typed in every single time, even when it's almost always the same value." | ❌ | Reflective Prompt |
| "Write two separate, nearly identical functions one for Standard orders and one for Express orders." | 🟡 partial (duplicates almost all the logic just to handle one differing detail) | Reflective Prompt |

**Reflective Prompt (require every time):**
> "If 95% of orders are 'Standard,' how much repeated, unnecessary typing does requiring it every single time create for a value that almost never actually changes?"

**Attempt 2:** "A lot there should be a way to assume 'Standard' automatically unless told otherwise." ✅ vs. "That's fine, typing it every time isn't a big deal." ❌

**Reflective Prompt (two near-identical functions):**
> "Both functions would share almost every line except the shipping method itself. If you later need to fix a typo in the confirmation message, would you have to fix it in two separate places?"

**Attempt 2:** "Yes better to have one function where only the shipping method can optionally change." ✅ vs. "That's fine, I don't mind maintaining two copies." ❌

**Stage 2 Concept Reveal:**
> "This uses a **default parameter value**: `def confirm_shipping(order_id, method="Standard")`. If nothing is passed in for `method`, Python automatically uses `"Standard"` but you can still override it by passing something else, like `"Express"`, when needed."

**Stage 3 Guided Code Build:**
```
def confirm_shipping(order_id, ______________):
    print("Order", order_id, "shipping via", method)

confirm_shipping(101)
confirm_shipping(102, "Express")
```
Tokens: `method="Standard"` ✅ · `method = Standard` (missing quotes inline-corrected: "`Standard` needs quotes around it, `\"Standard\"`, or Python reads it as a variable name that doesn't exist.") · `"Standard"=method` (reversed order inline-corrected: "The parameter name comes first, then `=`, then its default value.")

---

## LEVEL 3 Movie Ticket Pricing

**Scenario:** "Calculate a movie ticket price based on the customer's age. But if someone accidentally enters a negative age, the function shouldn't try to calculate a price at all it should immediately stop and report that the age is invalid."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Check the age first if it's invalid, immediately hand back an error and stop right there, without running any of the pricing logic below it." | ✅ | Concept Reveal |
| "Calculate the ticket price as normal first, and only check afterward whether the age made sense." | ❌ (checks too late the flawed calculation already happened) | Reflective Prompt |
| "Calculate the price using the age as given, and let a negative price simply show up as the result." | ❌ | Reflective Prompt |

**Reflective Prompt (check afterward):**
> "If the age is negative, is there ever a version of 'ticket price for a negative age' that actually makes sense? Wouldn't it be better to catch the problem *before* doing any pricing math at all?"

**Attempt 2:** "Yes the invalid check should happen first, before any pricing calculation even runs." ✅ vs. "It's fine to calculate first and just double check the result looks reasonable after." ❌

**Reflective Prompt (let a negative price show up):**
> "Would a customer ever actually see a negative price on a real receipt? What should happen instead the moment an impossible input like that is detected?"

**Attempt 2:** "The function should immediately exit with an error message the moment it detects an impossible input, rather than continuing on to calculate anything." ✅ vs. "I'll just tell the customer to ignore a negative number if they see one." ❌

### Stage 2 Concept Reveal (syntax explained)

> "The idea you landed on 'stop immediately if something's wrong, before doing the rest' uses an **early `return`**. Inside a function, `return` doesn't just hand back a result; it also immediately **exits** the function right there, skipping every line after it even if there's more code below. So placing a `return` inside an `if` at the top of a function lets you handle bad input and leave immediately, before the real logic runs."

### Stage 3 Guided Code Build

**Code shown:**
```
def ticket_price(age):
    if age < 0:
        _______________________________
    if age < 12:
        return 100
    return 250
```
**Token buttons:** `return "Invalid age"` ✅ · `print("Invalid age")` (prints the message but doesn't exit inline-corrected: "This displays the message, but the function keeps going and still calculates a price below it. `return` is what stops it.") · `break` (wrong keyword `break` exits a loop, not a function; inline-corrected: "`break` only works inside loops. Inside a function, `return` is what exits early.")

Wrong click → inline correction only, as shown above. No new reflective cycle; they simply retry the blank.

---

## LEVEL 4 Order Total Calculator (Functions Calling Functions)

**Scenario:** "Calculate the final total for an online order: the subtotal (price × quantity), the tax on that subtotal, and the two added together but the tax calculation depends entirely on the subtotal already being calculated first."

### Stage 1 Logic Test

**Attempt 1 options (plain English):**
| Option | Status | Routes to |
|---|---|---|
| "Write a separate, smaller function for each piece one for the subtotal, one for the tax and have a third function call both of them and combine their results." | ✅ | Concept Reveal |
| "Write one large function that does the subtotal math, the tax math, and the combining, all typed out together in a single block." | 🟡 partial (works for this one case, but none of the three calculations can be reused separately elsewhere) | Reflective Prompt |
| "Calculate the subtotal and tax separately by hand each time, and only write a function for adding the two together." | ❌ | Reflective Prompt |

**Reflective Prompt (one large combined function):**
> "What if a different part of the app a receipt screen needs *just* the tax amount on its own, without the subtotal or the total? If everything is bundled into one function, can that piece be reused by itself?"

**Attempt 2:** "No each calculation should be its own separate, reusable function, even if one calls another." ✅ vs. "That's fine, I'd just copy the tax math out separately wherever it's needed again." ❌

**Reflective Prompt (calculate by hand, only combine in a function):**
> "The subtotal and tax calculations are exactly the kind of repeatable logic functions are meant to handle. If they're done by hand outside any function, does the combining function actually have a subtotal and tax to work with automatically?"

**Attempt 2:** "No the subtotal and tax should each be their own functions too, so the combining function can call them directly instead of relying on numbers typed in by hand." ✅ vs. "It's fine, I'll always calculate those two by hand right before calling the combining function." ❌

### Stage 2 Concept Reveal (syntax explained)

> "This is **function composition** one function calling another. It isn't a new keyword; it's two things you already know (`def` and `return`) used together: `calculate_total()` calls `calculate_subtotal()` to get one result, calls `calculate_tax()` using that result to get a second, and returns their sum. Each function stays focused on exactly one job, and can still be reused on its own elsewhere."

### Stage 3 Guided Code Build

**Code shown:**
```
def calculate_subtotal(price, quantity):
    return price * quantity

def calculate_tax(subtotal):
    return subtotal * 0.08

def calculate_total(price, quantity):
    subtotal = ___________________________
    tax = ______________________
    return subtotal + tax
```
**Token buttons:** `calculate_subtotal(price, quantity)` ✅ (first blank) · `calculate_tax(subtotal)` ✅ (second blank) · `calculate_subtotal(price)` (missing the `quantity` argument inline-corrected: "`calculate_subtotal` needs both `price` and `quantity` to run it's missing one.") · `calculate_tax(price, quantity)` (passes the wrong values in inline-corrected: "`calculate_tax` expects the `subtotal`, not the raw `price` and `quantity`.")

### Teach-Back (Level 4, open-ended)

> "Design a new case study for **keyword arguments** (calling a function using `name=value` pairs, like `calculate_tip(bill=500, percent=15)`, instead of relying on position order) for a peer. Write the scenario, the plain-English logic options (with at least one believable wrong one), and the syntax token set for the guided build afterward."

This asks the learner to build all three stages of the engine themselves for a related-but-not-yet-taught refinement, the strongest possible test of Extended Abstract understanding: they're not just calling functions correctly, they're designing how to teach a new way of calling them.

---

## Summary Concept Coverage Map

| Level | Case Study | Core Mechanic Introduced |
|---|---|---|
| 1 | Report Card Averages | `def`, parameters, `return` defining a basic reusable function |
| 2A | Welcome Screen | Functions with no `return` action-only functions |
| 2B | Tip Calculator | Parameters + `return` passing data in, getting a result out |
| 2C | Shipping Confirmation | Default parameter values |
| 3 | Movie Ticket Pricing | Early `return` as a guard clause (exits the function immediately) |
| 4 | Order Total Calculator | Function composition functions calling other functions |
