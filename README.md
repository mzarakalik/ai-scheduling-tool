# AI Scheduling Tool (Prototype)

An **AI-powered scheduling assistant** that ranks employee–task assignments using:
- **Skill matching** (overlap, proficiency gaps, mandatory coverage),
- **Workload optimization** (capacity, buffers, burnout risk),
- **Task urgency** (priority, complexity, size),

to predict **success probability**, **expected performance**, **on-time probability**, and a unified **overall assignment score (0–100)** for recommendation ranking.

> Built as a realistic, privacy-safe prototype using **synthetic data** generated in the notebook. End-to-end pipeline with feature engineering, ML scoring, and interpretable outputs.

---

## What it does

- **Data generation**: realistic employees, skills, tasks, requirements, performance, and history tables.
- **Master join**: builds a 20,000+ row employee↔task candidate set.
- **Feature engineering**:
  - *Skills*: overlap %, proficiency gaps, mandatory-met %, weighted skill-match score.
  - *Workload*: capacity, schedule fit, buffer hours, workload zone & burnout risk.
  - *Urgency*: normalized priority/complexity and size category.
- **Predictions & scoring**:
  - success probability (skills-first weighting),
  - predicted performance (3–10),
  - on-time probability,
  - **overall assignment score** for ranking.
- **Outputs**: top-N recommendations with drivers (skills vs workload vs schedule).

---

## Dataset

This prototype uses a **synthetically generated dataset** created inside the notebook (no external data required).

### Data components (CSV files in `/data`)
- **Employees** → [`data/Employees_Table.csv`](data/Employees_Table.csv)  
- **Employee Skills** → [`data/Employee_Skills_Table.csv`](data/Employee_Skills_Table.csv)  
- **Tasks** → [`data/Tasks_Table.csv`](data/Tasks_Table.csv)  
- **Task Requirements** → [`data/Task_Requirements_Table.csv`](data/Task_Requirements_Table.csv)  
- **Assignment History** → [`data/Assignment_History_Table.csv`](data/Assignment_History_Table.csv)  
- **Employee Performance** → [`data/Employee_Performance_Table.csv`](data/Employee_Performance_Table.csv)  
- **Weekly Hours Tracking** → [`data/Weekly_Hours_Tracking_Table.csv`](data/Weekly_Hours_Tracking_Table.csv)  
- **Collaboration History** → [`data/Collaboration_History_Table.csv`](data/Collaboration_History_Table.csv)  
- **Projects** → [`data/Projects.csv`](data/Projects.csv)

The generator combines these tables into a **20,000+ row** master dataset of employee–task pairs, then derives:
- Skill-match features,
- Workload/capacity features,
- Task urgency features.

> The data is synthetic to ensure **privacy**, while preserving realistic distributions for evaluation and model behavior.

---

## Tech stack

- **Python 3.9+**
- pandas, numpy
- scikit-learn (Gradient Boosting for tabular predictions)
- matplotlib, seaborn (plots)

---

## How to run

1. **Clone**
   ```bash
   git clone https://github.com/mzarakalik/ai-scheduling-tool.git
   cd ai-scheduling-tool
   ```

2. **Install**
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the notebook**
   - Launch Jupyter / VS Code and open:
     `notebooks/AI_Scheduling_Tool.ipynb`

4. **Run all cells**
   - Generates synthetic data (if needed),
   - Loads `/data/*.csv`,
   - Builds features (skills/workload/urgency),
   - Produces predictions and an **overall assignment score**,
   - Prints **top recommendations** and summary stats,
   - (Optional) Saves plots to `/results/`.

---

## Example outputs

- **Top recommendations** (employee → task with score & drivers)  
- **Distribution of scores** (bands: poor / good / excellent)  
- **Skill-match vs overall score** correlation check  
- **Capacity diagnostics** (workload zone, buffer hours)

---

## Repository structure

```
ai-scheduling-tool/
├─ data/
│  ├─ Employees_Table.csv
│  ├─ Employee_Skills_Table.csv
│  ├─ Tasks_Table.csv
│  ├─ Task_Requirements_Table.csv
│  ├─ Assignment_History_Table.csv
│  ├─ Employee_Performance_Table.csv
│  ├─ Weekly_Hours_Tracking_Table.csv
│  ├─ Collaboration_History_Table.csv
│  └─ Projects.csv
├─ notebooks/
│  └─ AI_Scheduling_Tool.ipynb
├─ requirements.txt
├─ .gitignore
└─ README.md
```

---

## Roadmap

- Export top-N recommendations as CSV for downstream systems  
- Add calendar (Outlook/Google) integration adapters  
- Streamlit UI for interactive “what-if” scheduling  
- OR-Tools / ILP constraints for hard time windows & exclusivity  
- REST API + DB backend for productionization

---

## License

MIT — see `LICENSE`.
