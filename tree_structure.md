# PyBe Application Tree Structure

```text
pybe/
├── .gitignore
├── README.md
├── WIKI.md
├── Product.md
├── package.json
├── package-lock.json
├── client/
│   ├── index.html
│   ├── package.json
│   ├── package-lock.json
│   └── src/
│       ├── main.jsx
│       ├── styles.css
│       └── learning/
│           ├── CaseStudyEngine.jsx
│           ├── LearningPage.jsx
│           ├── Stage1LogicTest.jsx
│           ├── Stage2ConceptReveal.jsx
│           ├── Stage3CodeBuild.jsx
│           ├── usePyodide.js
│           └── utils.jsx
└── server/
    ├── .env.example
    ├── package.json
    ├── package-lock.json
    └── src/
        ├── index.js
        ├── seed.js
        ├── data/
        │   └── db.json (generated after seeding)
        ├── routes/
        │   ├── analytics.js
        │   ├── roadmap.js
        │   ├── scenarios.js
        │   ├── sessions.js
        │   └── topics.js
        └── services/
            └── learningEngine.js
```
