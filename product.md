PyBe - Product Specification & Implementation Guide
1. Project Overview & Core Philosophy
PyBe is a scenario-driven, problem-based Python learning prototype. It shifts the cognitive burden away from syntax memorization and towards structural logic. The app will be built using a modified MERN stack (React + Node/Express), but without MongoDB. All case study data and user progress will be stored locally (via JSON files and browser localStorage) to minimize complexity in this initial version.

Target UI/UX: Modernistic, clean, and distraction-free. Use Tailwind CSS for styling. Smooth transitions between logic stages are essential.

2. Core Constraints for the AI Coding Agent
CRITICAL INSTRUCTION FOR THE AGENT: You must execute this project strictly one step at a time. At the end of each numbered step in Section 6, you must STOP and ask the user to verify the implementation. Do not hallucinate or jump ahead to the next step until the user explicitly says "Proceed to Step X."

3. Data Sources & Content Logic
The application's educational content, options, plain-English text, and branching logic (what happens when a user clicks a specific option) MUST NOT be hallucinated.

For the Loops Unit: You must extract the exact scenarios, options, reflective prompts, and logic routing directly from the provided reference file: pybe-loops-plain-english-roadmap.md.

For the Pedagogical Framework: Refer to pybe-loops-case-study-framework.md to understand the SOLO taxonomy levels and the underlying educational philosophy.

4. Application Architecture
Frontend: React (Vite recommended) with Tailwind CSS.

Backend: Node.js/Express.

Database/Storage: * Case Studies: A static content.json file served by the Express backend.

User Progress: Tracked via browser localStorage linked to two hardcoded local users.

Code Execution: Pyodide (browser-based Python environment) for running user-assembled code in the final stage of each case study.

5. View Requirements
The application will consist of two primary views:

Home Page:

A brief, modern description of the PyBe philosophy (learning through scenarios).

A simple user toggler (User A / User B) for the hardcoded local users.

A "Dashboard" section displaying the current user's progress (e.g., Topics unlocked, Levels completed within "Loops").

Learning Page:

A dropdown/selector for available Topics (currently only "Loops").

Upon selecting a topic, a UI displaying available Levels (1 through 5). Levels should be visually locked if previous levels are incomplete.

Upon selecting a Level, the Case Study Engine mounts and runs the 3-stage flow (Logic Test -> Concept Reveal -> Guided Code Build).

6. Step-by-Step Implementation Guide (Agent Workflow)
Step 1: Project Scaffold & Mock Auth
Initialize the React frontend and Express backend.

Set up Tailwind CSS.

Implement a simple context or state for two hardcoded users (e.g., "Learner 1" and "Learner 2").

Implement basic localStorage syncing so when a user is selected, their (currently empty) progress object is loaded.

AGENT STOP: Ask the user to verify the basic app compiles and the user toggle works.

Step 2: Home Page & Navigation Shell
Create the main navigation bar (Home | Learning).

Build the Home Page UI with the PyBe description and a placeholder for the progress dashboard.

Build the Learning Page shell with a dummy dropdown for "Topics".

AGENT STOP: Ask the user to verify the UI routing and styling.

Step 3: Data Modeling & JSON Structuring
Translate the logic from pybe-loops-plain-english-roadmap.md into a structured JSON format (content.json).

The JSON must support: Scenarios, Attempt 1 options, Reflective Prompts, Attempt 2 options, Concept Reveal text, and Code Build tokens.

Create an Express endpoint (e.g., GET /api/topics/loops) to serve this JSON to the frontend.

AGENT STOP: Output a snippet of the JSON structure for the user to verify before building the UI that consumes it.

Step 4: The Learning Page (Selection UI)
Fetch the content.json from the backend.

Populate the Learning Page dropdown with "Loops".

When "Loops" is selected, render a Level selector (Levels 1 to 5).

Tie the Level selector to the mock Auth progress (e.g., Level 2 is unclickable until Level 1 is marked 'complete' in localStorage).

AGENT STOP: Ask the user to verify the data fetching and level-locking UI.

Step 5: Case Study Engine - Stage 1 (Logic Test)
Build the dynamic component that mounts when a level is clicked.

Render the Scenario and the Attempt 1 plain-English options.

Implement the branching logic:

Correct -> Move to Stage 2 (Concept Reveal).

Incorrect/Partial -> Render specific Reflective Prompt and Attempt 2 options.

Note: Extract all exact copy from pybe-loops-plain-english-roadmap.md.

AGENT STOP: Ask the user to verify the plain-English logic branching flow.

Step 6: Case Study Engine - Stages 2 & 3 (Reveal & Code Build)
Implement Stage 2: Render the "Concept Reveal" explanation text.

Integrate Pyodide into the React app.

Implement Stage 3: The "Guided Code Build".

Display the pre-written code with blanks.

Provide draggable or clickable "Tokens" for the user to fill the blanks.

Provide a "Run" button that passes the assembled code to Pyodide and displays the console output.

Update the user's progress in localStorage upon successful execution.

AGENT STOP: Ask the user to verify the Pyodide execution and token-filling mechanics.

7. Template: Creating New Case Studies
When adding new topics (e.g., Conditionals, Functions) beyond Loops, the content creator must format the new data using the following standard template so the engine can parse it correctly.

Pedagogical Rules for New Topics
Prestructural (Level 1): The pain scenario. Let them feel the absence of the concept.

Unistructural (Level 2): One isolated mechanic, heavily scaffolded.

Multistructural (Level 3): Parallel scenarios, different mechanics kept separate.

Relational (Level 4): A scenario that breaks unless mechanics are combined.

JSON Schema Template for the Content File
JSON
{
  "topicId": "conditionals",
  "topicName": "Conditionals (If/Else)",
  "levels": [
    {
      "levelId": 1,
      "title": "Level 1: The Basic Choice",
      "caseStudies": [
        {
          "id": "c1",
          "scenario": "[Insert Plain English Problem Description]",
          "stage1": {
            "attempt1": [
              {
                "text": "[Correct logic approach]",
                "status": "correct",
                "routesTo": "reveal"
              },
              {
                "text": "[Plausible misconception]",
                "status": "incorrect",
                "routesTo": "reflection_1"
              }
            ],
            "reflections": {
              "reflection_1": {
                "prompt": "[Nudge without giving the answer]",
                "attempt2": [
                  { "text": "[Correct logic approach]", "status": "correct" },
                  { "text": "[Still wrong]", "status": "incorrect" }
                ]
              }
            }
          },
          "stage2": {
            "conceptReveal": "[Explain the syntax (e.g., 'if', 'else') clearly here]"
          },
          "stage3": {
            "codeTemplate": "weather = 'raining'\n____:\n    print('Take umbrella')",
            "tokens": [
              { "value": "if weather == 'raining'", "correct": true },
              { "value": "when weather is 'raining'", "correct": false, "hint": "Python uses 'if' and '==' for comparison." }
            ]
          }
        }
      ]
    }
  ]
}