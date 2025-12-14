 TechParts Inc. Optimization System

**TechParts Inc. Optimization System** is a data-driven platform developed to enhance production allocation, task assignment, and distribution planning for a mid-sized electronics component manufacturer. The system applies Operations Research techniques including Linear Programming, Assignment Problem (Hungarian Algorithm), and Transportation Problem (LP + Vogel's Approximation) to reduce costs, increase efficiency, and maximize profits.

---

## Table of Contents

- [Problem Statement](#problem-statement)  
- [Formulation of the Problems](#formulation-of-the-problems)  
- [Methodology](#methodology)  
- [Results](#results)  
  - [Linear Programming](#linear-programming-results)  
  - [Assignment Problem](#assignment-problem-results)  
  - [Transportation Problem](#transportation-problem-results)  
- [System Performance](#system-performance)  
- [Tech Stack](#tech-stack)  
- [Usage](#usage)  
- [License](#license)  

---

## Problem Statement

TechParts Inc. operates 10 production facilities and 10 regional warehouses across the U.S. The company faces three critical challenges:

1. **Inefficient Production Allocation**  
   - Resources are allocated based on intuition rather than optimization.  
   - Profits are 15–25% below potential; capacity is underutilized.

2. **Suboptimal Task Assignment**  
   - 10 specialized tasks are manually assigned to 10 workers.  
   - Total completion time is inflated by 20–30% (current ~65 hrs vs. optimal 50 hrs).

3. **High Distribution Costs**  
   - Ad-hoc shipping from factories to warehouses increases transportation expenses.  
   - Current cost: $45,500 vs. optimal: $40,080.

**Estimated Annual Loss:** $2–3 million  

The project develops a data-driven optimization system to address these challenges.

---

## Formulation of the Problems

**Data Simulation:**  
- Product margins, worker-task times, and shipping costs were realistically simulated.  
- Each problem includes ≥10 decision variables and ≥10 constraints.

### Linear Programming (LP)

- **Objective:** Maximize profit  
- **Function:**  
Z = 50x₁ + 80x₂ + 60x₃ + 70x₄ + 55x₅ + 90x₆ + 75x₇ + 85x₈ + 95x₉ + 65x₁₀

markdown
Copy code
- **Constraints:**  
- 10 resource limits (e.g., labor ≤ 4,000 hrs, raw materials ≤ 8,000 kg)  
- 10 market demand caps (e.g., Product A ≤ 300 units)  
- Non-negativity  
- **Solver:** SciPy `linprog` with HiGHS  
- **Analysis:** Shadow prices and slack analysis included

### Assignment Problem

- **Cost Matrix:** 10×10 matrix of worker-task completion times (3–9 hrs)  
- **Objective:** Minimize total assignment time  
- **Constraints:**  
- Each worker assigned exactly one task  
- Each task assigned exactly one worker  
- Binary decision variables  
- **Solver:** `scipy.optimize.linear_sum_assignment` (Hungarian Algorithm)

### Transportation Problem

- **Sources:** 10 factories (supply = 5,600 units total)  
- **Destinations:** 10 warehouses (demand = 5,600 units total)  
- **Objective:** Minimize total shipping cost  
- **Constraints:**  
- Factory supply limits  
- Warehouse demand requirements  
- Non-negativity  
- **Cost:** $5–$24/unit (based on GPS distances)  
- **Solvers:** Vogel’s Approximation (initial), LP (optimal)

---

## Results

### Linear Programming Results

- **Maximum Profit Achieved:** $93,326.00  
- **Key Findings:**  
- Only 5 out of 10 products selected (C, D, E, G, I)  
- Four products (C, E, G, I) operate at maximum market capacity  
- Product I contributes highest profit ($19,720)  
- Products with low profit-to-resource ratio (A, B, F, H, J) are not produced  

---

### Assignment Problem Results

- **Total Completion Time:** 49.0 hours (Optimal)  
- **Performance Statistics:**  
- Average time per task: 4.9 hrs  
- Fastest: 3.0 hrs (David – Visual Inspection)  
- Longest: 6.0 hrs (Carol, Henry, Jack)  
- Range: 3.0–6.0 hrs  

---

### Transportation Problem Results

- **Minimum Total Transportation Cost:** $40,080.00  
- **Key Findings:**  
- Random distribution: ~$48,000 (20% higher)  
- Greedy approach: ~$42,500 (6% higher)  
- Savings per cycle: $2,420–$7,920  

---

## System Performance

| Module                     | Solve Time | Remarks                   |
|-----------------------------|------------|---------------------------|
| Linear Programming (LP)     | 0.08 sec   | Fast & scalable           |
| Assignment Problem          | 0.02 sec   | Optimal task assignment   |
| Transportation Problem      | 0.05 sec   | Cost-efficient routing    |
| API Response                | <160 ms    | Real-time performance     |
| Scalability                 | Tested up to 50×50 matrices | Efficient performance |

---

## Tech Stack

- **Programming Languages:** Python  
- **Libraries:** SciPy, NumPy, Pandas, Matplotlib  
- **Optimization Techniques:** Linear Programming, Hungarian Algorithm, Vogel’s Approximation  
- **Data Simulation:** Python-based random generation for realistic datasets  

---

## Usage

1. Clone the repository:
```bash
git clone https://github.com/yourusername/TechPartsOptimization.git
cd TechPartsOptimization
Install dependencies:

bash
Copy code
pip install -r requirements.txt
Run optimization scripts:

bash
Copy code
py q1.py
py q2.py
py q3.py
