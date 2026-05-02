# 🗺️ Wumpus World – Propositional Logic Agent

A simple web-based AI agent that navigates the classic **Wumpus World** problem using **Propositional Logic** and **Resolution Refutation**. Built with plain HTML, CSS, and JavaScript — no libraries, no frameworks, no installation needed.

> **Course:** AI 2002 – Artificial Intelligence (Spring 2026)
> **Assignment:** Assignment 6 – Question 6
> **Institution:** NUCES Chiniot-Faisalabad Campus

---

## 🎮 What is Wumpus World?

The Wumpus World is a classic AI problem from the textbook *Artificial Intelligence: A Modern Approach* by Russell & Norvig.

The agent explores a grid of rooms where:
- 🕳️ Some rooms have **Pits** — fall in and die
- 👾 One room has a **Wumpus** — get eaten and die
- 💰 One room has **Gold** — the goal is to find it safely
- 🤖 The **Agent** starts at the bottom-left corner

The agent **cannot see** the whole grid. It only gets clues:

| Percept | Meaning |
|---------|---------|
| 💨 Breeze | A pit is in a neighboring room |
| 🦨 Stench | The Wumpus is in a neighboring room |
| ✨ Glitter | Gold is in the current room |
| (nothing) | All neighboring rooms are safe |

---

## 🧠 How the Logic Works

The agent uses **Propositional Logic** to make decisions:

### 1. Knowledge Base (KB)
The KB is a plain array of **CNF clauses**. Each clause is an array of literals (strings).

```
KB = [
  ["-P_3_0"],          // No pit at row 3, col 0
  ["-W_3_0"],          // No wumpus at row 3, col 0
  ["P_2_0", "P_3_1"]   // Pit is at (2,0) OR (3,1)
]
```

### 2. TELL — Updating the KB
When the agent visits a cell, it observes percepts and updates the KB:
- **No Breeze** → add `-P_r_c` for every neighbor (no pits nearby)
- **Breeze** → add a clause saying at least one neighbor has a pit
- **No Stench** → add `-W_r_c` for every neighbor
- **Stench** → add a clause saying at least one neighbor has the Wumpus

### 3. ASK — Resolution Refutation
Before moving to any unvisited cell, the agent **asks the KB** if it is safe:

```
checkSafe(r, c):
  prove("-P_r_c")   // Can we prove there is NO pit here?
  prove("-W_r_c")   // Can we prove there is NO wumpus here?
```

The `prove()` function uses **Resolution Refutation**:
1. Add the **negation** of the goal to the KB copy
2. Find pairs of clauses that cancel each other
3. If an **empty clause** is produced → contradiction found → **goal is PROVED**

---

## 🚀 How to Run

### Option 1 – Open Locally (Easiest)
```
1. Download wumpus_basic.html
2. Double-click to open in any browser (Chrome, Firefox, Edge)
3. Done — no installation needed
```

### Option 2 – Deploy on Vercel
```
1. Push this file to a GitHub repository
2. Go to vercel.com → New Project → Import your repo
3. Vercel detects it as a static site automatically
4. Click Deploy → your live URL is ready
```

---

## 🕹️ How to Play

1. Set **Rows**, **Cols**, and **Pits** using the input boxes
2. Click **Start** to generate a new random world
3. Use **Step** to move the agent one step at a time
4. Use **Auto** to let the agent run automatically
5. Use **Restart** to start a new game

---

## 🎨 Grid Colors

| Color | Meaning |
|-------|---------|
| 🟡 Yellow | Agent's current position |
| 🔵 Light Blue | Visited cell |
| 🟢 Light Green | Proved safe by logic |
| ⬜ Gray | Unknown — not visited yet |
| 🔴 Red | Pit (revealed after death or game end) |
| 🟠 Orange | Wumpus (revealed after death or game end) |

---

## 📊 Metrics

| Metric | Description |
|--------|-------------|
| Steps | Number of cells the agent has moved to |
| Inferences | Total resolution operations performed |
| KB Size | Number of clauses currently in the Knowledge Base |
| Safe Cells | Number of cells proved safe by the logic engine |

---

## 📁 File Structure

```
wumpus_basic.html
  ├── <style>         Page layout and cell colors
  ├── <body>          Input form, grid, info panels, log
  └── <script>
        ├── KB[]            The Knowledge Base (array of clauses)
        ├── flip()          Negate a literal
        ├── addClause()     Add a clause to KB
        ├── prove()         Resolution Refutation engine
        ├── checkSafe()     Ask KB if a cell is safe
        ├── startGame()     Initialize the world
        ├── tellKB()        Update KB from percepts (TELL)
        ├── doStep()        One agent step (ASK + MOVE)
        ├── moveTo()        Move agent and check for death
        ├── toggleAuto()    Auto-run with timer
        └── drawGrid()      Render the HTML table grid
```

---

## 🔑 Key Concepts Used

- **Knowledge-Based Agent** — agent that maintains a KB and uses it to decide actions
- **Propositional Logic** — logic using true/false statements (literals and clauses)
- **CNF (Conjunctive Normal Form)** — KB stored as AND of clauses, each clause is OR of literals
- **Resolution Refutation** — proving a fact by adding its negation and deriving a contradiction
- **BFS (Breadth-First Search)** — used to find the shortest path back to an unvisited safe cell

---

## 📚 Reference

- Russell, S. & Norvig, P. — *Artificial Intelligence: A Modern Approach* (Chapter 7 — Logical Agents)
- Wumpus World problem — classic benchmark for Knowledge-Based Agents

---

## 👨‍💻 Built With

![HTML](https://img.shields.io/badge/HTML-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

> Plain HTML + CSS + JavaScript only. Zero dependencies. Zero frameworks.

