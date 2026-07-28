# PyBe Application Workflow

The PyBe application is designed as a scenario-driven learning platform for Python. The general workflow for a user (learner) progressing through the application involves several distinct phases:

## 1. Scenario Browser & Selection
- **Discovery:** The user starts at the scenario browser.
- **Filtering:** Users can filter scenarios by difficulty, topic/concept, or use the search functionality.
- **Selection:** The user selects a specific scenario or case study to begin a learning session.

## 2. Interactive Learning Session
Once a scenario is selected, the user enters an interactive learning session managed by the `CaseStudyEngine.jsx`. This session is broken down into pedagogical stages:

### Stage 1: Logic Test (`Stage1LogicTest.jsx`)
- **Reasoning Support:** The learner is prompted to think through the problem logically.
- **Abstraction Mapping:** The learner maps out the concepts conceptually without writing actual Python code yet.

### Stage 2: Concept Reveal (`Stage2ConceptReveal.jsx`)
- **Conversational Prompts:** The system interacts with the learner using conversational prompts to bridge the gap between their logic and Python constructs.
- **Concept Mastering:** The underlying Python concepts needed to solve the scenario are revealed and explained.

### Stage 3: Code Build (`Stage3CodeBuild.jsx`)
- **Construct Generation:** The user generates the actual Python code based on the prior logic and concept mapping.
- **Execution & Testing:** The user can execute the Python code directly in the browser. This is powered locally using Pyodide (`usePyodide.js`).

## 3. Evaluation & Feedback
- **Prompt Scoring:** The user's prompts and answers are evaluated (handled locally via deterministic rules in `learningEngine.js`).
- **Reflection Capture:** The user is encouraged to reflect on the learning session.

## 4. Dashboard & Analytics Updates
After the session concludes, the data is pushed to the backend (`server/src/routes/sessions.js` and `analytics.js`).
- **Progress Tracking:** The user's dashboard is updated.
- **Metrics Updated:** Key metrics such as prompt maturity, concept mastery, and identified misconceptions are recalculated and displayed.
- **Recent Sessions:** The session is logged in the user's history.

## System Architecture Workflow
- **Frontend (React/Vite):** Manages the UI, state of the learning session, and runs Python in the browser (Pyodide). Makes API calls to the backend.
- **Backend (Express/Node.js):** Receives API calls, processes logic using `learningEngine.js`, and reads/writes to the local `db.json` storage without relying on external databases or third-party AI APIs.
