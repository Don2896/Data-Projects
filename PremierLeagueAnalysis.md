# Premier League Player Performance Analysis

> An exploratory data analysis of Premier League player performance, examining goals, assists, expected metrics (xG/xA), passing behaviour, and workload distribution across positions to derive tactical and recruitment insights.

---

## Project Overview

This project analyses individual player performance across the Premier League using a combination of traditional statistics and advanced metrics. The objective is to understand how player output varies by position, identify efficiency in goal creation and passing, and highlight patterns that can inform tactical decisions and recruitment strategy.

---

## Key Insights & Visual Analysis

### 1. Goals, Assists & Passing Accuracy by Position

Visualisations showing **average goals, assists, and passing accuracy by position** largely align with tactical expectations:

- Players in **forward and attacking positions** score the most goals on average.
- **Forwards and attacking midfielders** contribute the highest number of assists, reflecting their proximity to goal and creative responsibilities.
- These players operate closest to the opposition box and are tasked with finishing and chance creation, explaining their higher attacking output.

---

### 2. Passing Accuracy Distribution (Box Plot)

A box plot illustrating **passing accuracy distribution by position** shows:

- **Defenders, defensive midfielders, and central midfielders** have the highest passing accuracy.
- Modern football emphasises building play from the back, meaning defenders and holding midfielders frequently exchange **short, low-risk passes**.
- This is reflected in the **tight distribution** for defensive midfielders, indicating consistency and ball security.

---

### 3. Goal Scoring Efficiency (xG vs Goals)

A combined bar chart and scatter plot analyses the **top 10 goal scorers** and their efficiency relative to expected goals (xG):

- Players above the diagonal parity line **outperformed their xG**.
- **7 of the top 10 scorers exceeded their xG**, while 3 underperformed.
- Players such as **Harry Kane and Mohamed Salah** marginally exceeded their xG, indicating reliable finishing.
- **Son Heung-min** stood out as the most efficient finisher, significantly outperforming his xG.

**Why this matters:**  
xG is critical in recruitment decisions. A striker who consistently scores below xG may rely on high chance volume rather than finishing quality — a risk when investing heavily in the transfer market.

A similar pattern was observed for **assists vs expected assists (xA)**:
- All top 10 assist providers outperformed their xA.
- **Harry Kane and Marcus Rashford** emerged as standout overperformers.

---

### 4. Passing Volume vs Accuracy (Top Passers)

A scatter plot comparing **passing volume and accuracy** identified the league’s top 10 passers:

- All were **defensive midfielders**, highlighting their role in possession recycling and tempo control.
- **Rodri and Pierre-Emile Højbjerg** ranked highest for both volume and accuracy.
- **Stuart Dallas and Rúben Neves** showed lower volume and accuracy relative to their peers, making them the weakest performers among the top passers.

---

### 5. Workload Distribution by Position

A bar chart showing **average minutes played per position** reveals:

- **Goalkeepers, defenders, and defensive midfielders** play the most minutes, with minimal variance.
- **Attacking midfielders and forwards** show greater variance and lower average minutes.

**Interpretation:**
- Defensive roles form the structural base of a team, leading to less rotation.
- Forwards rely on **explosive, high-intensity actions** (sprints, pressing, runs in behind), causing faster fatigue.
- Managers often substitute attackers late in matches to introduce fresh attacking energy.

---

## Tools & Technologies

- **Python** (pandas, NumPy)
- **Data Visualisation** (matplotlib, seaborn)
- **Jupyter Notebook**
- **Football Analytics Metrics** (xG, xA)
