# Students Social Media Addiction — Power BI Dashboard

An interactive Power BI report that explores how social-media usage relates to student addiction scores, sleep, mental health, conflicts, and perceived academic impact.

## Project Files

| File | Description |
|---|---|
| `Students_Addiction_PowerBi.pbix` | Power BI dashboard and semantic model. |
| `Students Social Media Addiction.xlsx` | Source dataset containing student and platform details. |

## Project Structure

```text
Students-Social-Media-Addiction-PowerBI/
│
├── .gitignore
├── ER_DIAGRAM.md
├── README.md
├── Students Social Media Addiction.xlsx
└── Students_Addiction_PowerBi.pbix
```

| Item | Purpose |
|---|---|
| `.gitignore` | Defines files excluded from version control. |
| `ER_DIAGRAM.md` | GitHub-rendered entity-relationship diagram and model relationship notes. |
| `README.md` | Project documentation, dashboard overview, insights, and usage guidance. |
| `Students Social Media Addiction.xlsx` | Raw source data used by the report. |
| `Students_Addiction_PowerBi.pbix` | Interactive Power BI dashboard. |

## Dashboard Pages

- **Executive Overview** — headline metrics and a high-level view of addiction, usage, gender, age, and academic level.
- **Mental Health & Lifestyle** — relationships among addiction score, mental-health score, sleep, country, and gender.
- **Academic Impact** — social-media usage and reported academic impact by academic level and platform.
- **Relationships and Conflicts** — relationship status, social-media conflicts, and addiction score.
- **Interactive Story View** — bookmark-driven comparisons by gender and academic level.
- **Student Profile** — drill-through view for student-level detail.

## Dataset

The source workbook includes two tables joined using `Student_ID`:

| Table | Grain | Key fields |
|---|---|---|
| `Student Details` | One record per student | age, gender, academic level, country, sleep, mental health, relationship status, conflicts, addiction score |
| `Platform Details` | One record per student | average daily usage, most-used platform, reported academic impact |

The dataset contains **705 students** with complete records across both tables.

## Key Insights

- **64.3%** of students report that social-media use affects their academic performance.
- Average daily usage is **4.92 hours** and the average addiction score is **6.44 out of 9**.
- **28.2%** of students have a high addiction score (8–9); all students in this segment report academic impact in this dataset.
- Students reporting academic impact average **5.54 daily usage hours**, versus **3.80 hours** for students not reporting impact.
- High-school students show the highest average addiction score (**8.04**) and the lowest average sleep (**5.46 hours**); interpret carefully because this group has only 27 records.
- WhatsApp users have the highest average usage (**6.48 hours**). WhatsApp, Snapchat, and TikTok show the highest addiction-score averages among the larger platform groups.

> These are observed associations in a cross-sectional dataset and should not be interpreted as evidence that social-media use causes academic or health outcomes.

## How to Use

1. Download or clone this repository.
2. Open `Students_Addiction_PowerBi.pbix` in **Power BI Desktop**.
3. If Power BI requests a data source, point it to `Students Social Media Addiction.xlsx` in the project folder.
4. Select **Refresh** to load the latest workbook data.
5. Use slicers, bookmarks, and drill-through interactions to explore segments.

## Recommended Model Improvements

- Use `Student_ID` as the unique key and enforce a validated one-to-one relationship between the two source tables.
- Prefer explicit DAX measures over implicit aggregations. For example:

```DAX
Students = DISTINCTCOUNT('Student Details'[Student_ID])

Average Daily Usage =
AVERAGE('Platform Details'[Avg_Daily_Usage_Hours])

Average Addiction Score =
AVERAGE('Student Details'[Addicted_Score])

Academic Impact % =
DIVIDE(
    CALCULATE(
        [Students],
        'Platform Details'[Affects_Academic_Performance] = "Yes"
    ),
    [Students]
)
```

- Use averages and rates, rather than sums, when comparing academic levels or platforms with unequal student counts.
- Display sample size with country and small-group comparisons.
- Remove unused model objects, such as a Date table, unless dated survey data is added.
- Verify that the Student Profile drill-through page does not retain a hardcoded student filter.



## Tools Used

- Microsoft Power BI Desktop
- Microsoft Excel

## License

This project is intended for educational and portfolio use. Confirm that you have permission to redistribute the source data before publishing it publicly.

---

## 📬 Contact

**Lokesh Singh**

- LinkedIn: https://www.linkedin.com/in/lokesh-singh-da/
- GitHub: https://github.com/LokeshSingh-DA
