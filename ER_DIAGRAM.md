# Entity Relationship Diagram

```mermaid
erDiagram
    STUDENT_DETAILS ||--|| PLATFORM_DETAILS : "matched by Student_ID"

    STUDENT_DETAILS {
        int Student_ID PK
        int Age
        string Gender
        string Academic_Level
        string Country
        decimal Sleep_Hours_Per_Night
        int Mental_Health_Score
        string Relationship_Status
        int Conflicts_Over_Social_Media
        int Addicted_Score
    }

    PLATFORM_DETAILS {
        int Student_ID PK, FK
        decimal Avg_Daily_Usage_Hours
        string Most_Used_Platform
        string Affects_Academic_Performance
    }
```

## Relationship Details

| Parent table | Child table | Join column | Cardinality | Recommended filter direction |
|---|---|---|---|---|
| `Student Details` | `Platform Details` | `Student_ID` | One-to-one (1:1) | Single direction: Student Details → Platform Details |

`Student_ID` is unique and non-null in both tables. `Platform Details[Student_ID]` acts as the foreign key that connects each student profile to their social-media platform information.

> The Power BI model also contains a DateTable layout object, but no date field exists in the supplied source data; it is therefore omitted from this ER diagram.
