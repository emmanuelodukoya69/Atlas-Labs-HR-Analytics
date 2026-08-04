# 📊 Atlas Labs HR Analytics — Employee Attrition Analysis

**A Power BI dashboard investigating why employees leave Atlas Labs, and what HR can actually do about it.**

![Overview Dashboard](images/Overview.PNG)

---

## 📌 Business Problem

Atlas Labs wanted to understand its employee attrition — not just the headline number, but *why* people are leaving, *who* is most at risk, and *which levers* HR can realistically pull to fix it. This project builds a full HR analytics dashboard in Power BI to answer exactly that, using employee records, performance ratings, and satisfaction data.

---

## 🗂️ Dataset

| File | Description |
|---|---|
| `Employee.csv` | Core employee records — demographics, department, role, salary, tenure, attrition status |
| `PerformanceRating.csv` | Self and manager performance ratings, satisfaction scores, training history |
| `EducationLevel.csv` | Lookup table for education levels |
| `RatingLevel.csv` | Lookup table for performance rating scale |
| `SatisfiedLevel.csv` | Lookup table for satisfaction scale |
| `DimDate.txt` | DAX calendar table (fiscal year, quarter, week logic) powering all time-based visuals |
| `HR_ANALYTICS_REPORT.pbix` | The full Power BI dashboard file |

---

## 🛠️ Tools Used

- **Power BI** — data modeling, DAX measures, dashboard design
- **DAX** — custom calendar table, attrition rate calculations, rating comparisons
- **Excel** — initial data checks

---

## 🔍 Approach

The dashboard is built across four pages, each answering a different layer of the attrition question:

1. **Overview** — the headline numbers: how many employees, how many left, overall attrition rate
2. **Demographics** — who is leaving, broken down by gender, marital status, age
3. **Attrition** — the real drivers: overtime, travel, stock options, tenure
4. **Performance Tracker** — whether satisfaction and performance scores actually predict who leaves

### Data Cleaning (Power Query)
Raw employee data was cleaned and transformed in Power Query — adding calculated columns like age bins, fixing data types, and shaping tables before they hit the model.

![Power Query Interface](images/Power_Query_Interface.PNG)

### Data Model
A star schema connects the core `FactPerformanceRating` table to `DimEmployee`, `DimDate`, `DimEducationLevel`, `DimRatingLevel`, and `DimSatisfiedLevel` — keeping the model clean and every measure fast to calculate.

![Data Model](images/Modelling.PNG)

---

## 💡 Insights & Recommendations

### The Headline Numbers
1. Atlas Labs had employed over 1,470 people.
2. Atlas Labs currently employs over 1,200 people.
3. The largest department by far is Technology.
4. The attrition rate for employees leaving the organization is 16.1%
5. Majority of employees are between 20-29 years old.
6. Currently Atlas Labs employs 2.7% more women than men.

Employees who identify as:

7. Non-binary make up 8.5% of total employees.
8. White has the highest average salary.
9. "Mixed or Multiple Ethnic Groups" have one of the lowest average salaries.

### Overview Page — The Headline Numbers
![Overview Page](images/Overview.PNG)

- 1,470 total employees, of whom 1,233 are still active and 237 have left → 16.1% overall attrition rate.
- Hiring has been steady, running 106–155 new hires per year with no major slowdown, so growth pressure isn't the issue here.
- Sales - Sales Representative (39.8%) and HR - Recruiter (37.5%) have by far the worst attrition of any role, while most Technology and management roles sit in single digits to low-20s.

### Demographics Page — Who's Affected
![Demographics Page](images/Demograhics.PNG)

- Attrition is fairly even across gender (Female 15.4%, Male 17.5%, Non-Binary 15.3%), gender is not a meaningful driver.
- Marital status tells a different story: Single employees leave at 23.3%, nearly double Married (12.7%) and more than double Divorced (10.1%).
- Oldest employee is 51, youngest 18, a fairly typical working-age spread, nothing unusual to flag.

**What this means:** life-stage matters more than identity. Single employees — often earlier-career, fewer local ties — are the flight-risk group, which lines up with the tenure pattern below.

### Attrition Page — The Real Drivers
![Attrition Page](images/Attrition.PNG)

This page is where the actionable story is:

| Factor | Attrition rate | Read |
|---|---|---|
| Frequent Travellers | 24.9% vs 8.0% (No Travel) | Travel burden is a real cost |
| Works Overtime | 30.5% vs 10.4% (No Overtime) | The single strongest driver in the whole dataset |
| No stock options | 24.4% vs 7.6–9.4% (Level 1-2) | Equity/vesting clearly retains people |
| Tenure Year 0-1 | 31–35% | Early-tenure flight risk, tapering to <1% by year 10 |

The standout: Overtime is the biggest single factor you've measured — employees working overtime leave at roughly 3x the rate of those who don't. Combined with frequent travel, these two "workload/burnout" factors dwarf every demographic factor on the Demographics page.

### Performance Tracker Page — An Unexpected Finding
![Performance Tracker Page](images/Performance_Tracker.PNG)

I checked whether satisfaction scores actually explain who leaves, and they mostly don't:
- Environment/Job/WorkLife/Relationship satisfaction scores are nearly identical between employees who stayed and those who left (all within ~0.1–0.2 points on a 5-point scale).
- There's a consistent self-rating vs. manager-rating gap (avg self-rating 3.98 vs. manager 3.47) — employees rate themselves higher than managers rate them, a common calibration gap worth a conversation with people managers, but not itself an attrition driver.

**What this means:** self-reported happiness surveys aren't catching the real problem. People aren't leaving because they say they're unhappy — they're leaving because of workload (overtime, travel) and lack of financial upside (no stock options), especially early in tenure.

---

## ✅ Recommendations

1. **Cap or compensate overtime for Sales Reps and Recruiters first.** This is your highest-leverage lever, it's the single strongest predictor of attrition, and it's concentrated in exactly the two roles already flagged as highest-risk.
2. **Extend stock option eligibility earlier, even at a small starting grant.** Level 0 vs Level 1 stock options nearly triples the retention rate (24.4% → 9.4%), this is a cheap, high-impact lever compared to broad salary increases.
3. **Build a structured 18-month onboarding/retention check-in**, since ~1 in 3 new hires leave in their first two years. A small investment in early mentorship or career-pathing could meaningfully cut this.
4. **Don't rely on satisfaction surveys as an early-warning system**, they don't distinguish stayers from leavers here. Use overtime hours, travel frequency, and tenure as your real predictive dashboard instead.
5. **Address the self vs. manager rating gap in manager training/coaching conversations**, not an attrition fix, but a performance-calibration issue worth flagging to HR leadership separately.

---

## 📁 Repository Structure

```
Atlas-Labs-HR-Analytics/
├── README.md
├── HR_ANALYTICS_REPORT.pbix     # Power BI dashboard file
├── Employee.csv                  # Core employee data
├── PerformanceRating.csv         # Ratings & satisfaction data
├── EducationLevel.csv            # Lookup table
├── RatingLevel.csv               # Lookup table
├── SatisfiedLevel.csv            # Lookup table
├── DimDate.txt                   # DAX calendar table logic
└── images/
    ├── Overview.PNG
    ├── Demograhics.PNG
    ├── Attrition.PNG
    ├── Performance_Tracker.PNG
    ├── Modelling.PNG
    └── Power_Query_Interface.PNG
```

---

## ▶️ How to Explore This Project

1. Download `HR_ANALYTICS_REPORT.pbix` and open it in Power BI Desktop (free from Microsoft) to interact with the dashboard directly
2. The CSV files are the raw source tables used to build the data model
3. `DimDate.txt` contains the DAX code for the custom calendar table powering all time-based visuals

---

## 👤 Author

**Odukoya Emmanuel** — Data Analyst | SQL · Excel · Power BI
📧 emmanuelodukoya69@gmail.com · 🔗 www.linkedin.com/in/odukoya-emmanuel-1a3578288
