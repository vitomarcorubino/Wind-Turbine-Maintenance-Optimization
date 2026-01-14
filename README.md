# ⚡ Wind Turbine Maintenance Optimization
by **[Vito Marco Rubino](https://www.linkedin.com/in/vitomarcorubino/)** \
MSc in Data Science – University of Bari Aldo Moro \
*Course Project: Decisional Models and Optimization – A.Y. 2025-2026*


## 📌 Overview

Wind turbine maintenance is a critical operational task ensuring the reliability, safety, and long-term efficiency of a wind farm.
This project formulates and solves a **Maintenance Scheduling Problem** using **Integer Linear Programming (ILP)**.


## 🗂 Repository Structure
- 📂 [data/figs/](data/figs/)              # Generated plots (Heatmap, Line chart and Gantt chart)
- 📂 [data/pdf/](data/pdf/)
  - 📄 [report](data/pdf/report.pdf)                # Final Project Report
  - 📄 [wind_turbine_maintenance_optimization.pdf](data/pdf/wind_turbine_maintenance_optimization.pdf)                # Exported notebook in PDF format
- 📄 [requirements.txt](requirements.txt)                # Dependencies for the environment
- 📄 [wind_turbine_maintenance_optimization.ipynb](wind_turbine_maintenance_optimization.ipynb)                # Main Jupyter Notebook with ILP implementation


## 📐 Problem Statement
The scenario involves a wind farm with **7 turbines** that must be maintained over a **5-day working week** (Mon-Fri). 

The problem is modeled as an **Integer Linear Programming (ILP)** problem.

**Decision Variables:**

$$
x_{i,j,k} =
\begin{cases}
1 & \text{if team } k \text{ performs maintenance on turbine } i \text{ on day } j, \\
0 & \text{otherwise}.
\end{cases}
$$

**Objective Function:**

Minimize the total weekly maintenance cost:

$$\sum_{i\in \mathcal{T}}\sum_{j\in \mathcal{D}}\sum_{k\in \mathcal{K}} c_{ij} \, x_{i,j,k} \ \equiv \ \min_{\mathbf{x}} \mathbf{c}^\top \mathbf{x} $$

**Constraints:**
1.  **Coverage Constraint** (Each turbine must be maintained exactly **once** during the week):

$$\sum_{j \in \mathcal{D}} \sum_{k \in \mathcal{K}} x_{i,j,k} = 1, \qquad \forall i \in \mathcal{T}$$ 

3.  **Team Capacity Constraint** (Each team can service at most **one turbine per day):
   
$$\sum_{i \in \mathcal{T}} x_{i,j,k} \leq 1, \qquad \forall j \in \mathcal{D}, \ \forall k \in \mathcal{K}$$ 

## 🛠 Tech Stack & Implementation
The solution is implemented in **Python** using the following libraries:

* **Modeling:** `PuLP` (Linear Programming toolkit)
* **Solver:** `CBC` (Coin-OR Branch and Cut)
* **Data Handling:** `NumPy`

### Solver Algorithm
The project utilizes the **Branch-and-Cut** algorithm (implemented in CBC). Unlike standard Branch-and-Bound, it uses cutting planes (e.g., Chvátal-Gomory cuts) to tighten the linear relaxation, significantly reducing the search tree size and solving the problem efficiently.


## 📊 Key Results

The model successfully identified the optimal schedule with a minimum total cost of **105.0**.

### 📅 Optimal Weekly Schedule
The solver generated the following assignment plan, ensuring balanced workloads and cost efficiency:

| Day | Team 1 | Team 2 |
| :--- | :--- | :--- |
| **Mon** | Turbine 1 | Turbine 2 |
| **Tue** | Turbine 5 | Turbine 7 |
| **Wed** | Turbine 6 | Turbine 3 |
| **Thu** | *No Task* | *No Task* |
| **Fri** | Turbine 4 | *No Task* |

*Note: Thursday is left empty as optimal costs were found on other days.

---

## 🌐 Author
* **Vito Marco Rubino**  
  [![GitHub](https://img.shields.io/badge/GitHub-100000?logo=github&logoColor=white)](https://github.com/vitomarcorubino) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/vitomarcorubino/)
