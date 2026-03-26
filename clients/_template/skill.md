# Command Center Skill — [Client Name]

> This file tells Cowork exactly how to generate this client's command center.
> Built during the initial creative session. Never shared between clients.

---

## 1. Generation Prompt Template

```
You are generating the weekly Business Command Center for [Client Name].

Read the client profile at profile.md for context on the business, roles, and metrics.

This week's raw data files are in the /data/ folder. Process each file as described
in the "Data Extraction Rules" section below.

Produce three outputs:
1. output.html — interactive dashboard with role-based views
2. output.pdf  — one-page-per-role printable summary
3. output.xlsx — full detail spreadsheet with all source data and calculations

Follow every section below exactly.
```

---

## 2. Data Extraction Rules

<!-- For each report type, specify exactly which fields to pull and how to handle them. -->

### Report: [Report Name 1]
- **Source file pattern:** `*P&L*` or `profit-loss.*`
- **Format:** CSV / Excel / PDF
- **Fields to extract:**
  | Column / Field        | Maps To              | Notes                        |
  |-----------------------|----------------------|------------------------------|
  | <!-- e.g. "Total Income" --> | Revenue        | <!-- Use the monthly column --> |
  |                       |                      |                              |

### Report: [Report Name 2]
- **Source file pattern:**
- **Format:**
- **Fields to extract:**
  | Column / Field | Maps To | Notes |
  |----------------|---------|-------|
  |                |         |       |

<!-- Copy the block above for each report type listed in profile.md §6. -->

---

## 3. Calculations

<!-- Define every derived metric. Reference the field names from §2. -->

| Metric              | Formula                                     | Format      |
|---------------------|---------------------------------------------|-------------|
| <!-- Gross Margin % --> | <!-- (Revenue - COGS) / Revenue × 100 --> | <!-- % with 1 decimal --> |
|                     |                                             |             |
|                     |                                             |             |

---

## 4. Thresholds & Alerts

<!-- What counts as "on track" vs. "warning" vs. "critical" for each metric. -->

| Metric              | On Track (green)   | Warning (yellow)   | Critical (red)     |
|---------------------|--------------------|--------------------|---------------------|
| <!-- Gross Margin % --> | <!-- ≥ 40% -->  | <!-- 30–39% -->    | <!-- < 30% -->      |
|                     |                    |                    |                     |
|                     |                    |                    |                     |

---

## 5. Dashboard Layout (HTML)

### Global Settings
- **Color scheme:** <!-- e.g. dark navy + white + accent green/red -->
- **Font:** <!-- e.g. Inter, system-ui -->
- **Role switcher location:** <!-- e.g. top nav tabs -->

### Role: Owner — Sections in Order
1. **[Section Name]** — <!-- e.g. "Cash Position" — single big number with week-over-week delta -->
2. **[Section Name]** — <!-- e.g. "Revenue vs. Forecast" — bar chart -->
3. **[Section Name]** — <!-- e.g. "Alerts" — red/yellow items only -->
4.
5.

### Role: CFO / Finance — Sections in Order
1. **[Section Name]** —
2. **[Section Name]** —
3. **[Section Name]** —
4.
5.

### Role: Operations / Project Manager — Sections in Order
1. **[Section Name]** —
2. **[Section Name]** —
3. **[Section Name]** —
4.
5.

<!-- Add/remove role layouts to match profile.md §4. -->

---

## 6. PDF Layout

- **Page size:** Letter / A4
- **Pages:** One per role
- **Structure per page:**
  - Header: role name, client name, week ending date
  - Narrative summary (3-5 sentences in their language)
  - Key metrics table (top 5 for that role)
  - Alerts / action items
  - Footer: generated date, data sources used

---

## 7. Excel Layout

- **Tab 1: Summary** — all metrics, all roles, current week vs. prior week
- **Tab 2: Raw Data** — every extracted field from every report, with source file name
- **Tab 3: Calculations** — every formula from §3, shown with inputs and outputs
- **Tab per role (optional):** filtered view of metrics relevant to that role

---

## 8. Tone & Language

- **Voice:** <!-- e.g. "Direct and confident. No hedging. Use their terminology." -->
- **Terminology map:**
  | They say…            | We use…              |
  |----------------------|----------------------|
  | <!-- e.g. "jobs" --> | <!-- "projects" -->  |
  |                      |                      |

---

## 9. Special Instructions

<!-- Anything unique to this client: custom logic, exceptions, things to never do. -->

