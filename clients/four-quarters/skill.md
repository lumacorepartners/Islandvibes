# Command Center Skill — Four Quarters

---

## 1. Generation Prompt Template

```
You are generating the weekly Business Command Center for Four Quarters,
a construction company with plumbing subsidiaries operating across 2 locations.

Read the client profile at profile.md for full context on the business,
roles, metrics, and data sources.

This week's raw data files are in the /data/ folder. Process each file
using the Data Extraction Rules below. Match files by name pattern — the
client may use slightly different file names week to week.

Produce three outputs:
1. output.html — interactive dashboard with role-switchable views
   (Rob/Owner, Bennett/CFO, Jay/COO, John/VP Sales)
2. output.pdf — one page per role, printable, with narrative + numbers
3. output.xlsx — full detail with every source number and calculation

Critical context: This company's #1 pain is cash flow timing from new
construction pay cycles. Every view should make cash position and cash
forecast prominent. Flag any job where costs are outpacing billings.
```

---

## 2. Data Extraction Rules

### Report: Job Cost Detail (Trimble)
- **Source file pattern:** `*job*cost*` or `*trimble*`
- **Format:** CSV / Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Job #              | job_id                 | Primary key — links across all reports    |
  | Job Name           | job_name               |                                          |
  | Phase / Cost Code  | cost_category          | Group into: Labor, Material, Sub, Equipment, Other |
  | Original Budget    | estimated_cost         |                                          |
  | Committed Cost     | committed_cost         | POs and subs under contract              |
  | Actual Cost to Date | actual_cost           |                                          |
  | Budget Remaining   | budget_remaining       | estimated_cost − actual_cost             |
  | Contract Amount    | contract_amount        | What the customer is paying              |
  | Billed to Date     | billed_to_date         |                                          |
  | % Complete         | pct_complete           |                                          |

### Report: Service Titan Work Orders
- **Source file pattern:** `*service*titan*` or `*work*order*` or `*ticket*`
- **Format:** CSV / Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Ticket / WO #      | ticket_id              |                                          |
  | Customer Name      | customer               |                                          |
  | Job #              | job_id                 | Link to Trimble if available             |
  | Revenue            | service_revenue        |                                          |
  | Technician         | tech_assigned          |                                          |
  | Status             | ticket_status          | Open, Complete, Invoiced                 |
  | Completion Date    | completion_date        |                                          |

### Report: Equipment Rentals
- **Source file pattern:** `*equipment*` or `*rental*`
- **Format:** Excel / PDF
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Job #              | job_id                 |                                          |
  | Equipment Type     | equipment_type         |                                          |
  | Rental Period      | rental_dates           | Start and end date                       |
  | Rate               | rental_rate            | Daily or weekly — normalize to weekly    |
  | Total Cost         | rental_total           |                                          |

### Report: Credit Card Transactions
- **Source file pattern:** `*credit*card*` or `*cc_*`
- **Format:** CSV
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Date               | txn_date               |                                          |
  | Vendor             | vendor                 |                                          |
  | Amount             | txn_amount             |                                          |
  | Card Holder        | card_holder            |                                          |
  | Job #              | job_id                 | May be blank — flag uncoded transactions |

### Report: Bank Transactions
- **Source file pattern:** `*bank*`
- **Format:** CSV
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Date               | txn_date               |                                          |
  | Description        | txn_description        |                                          |
  | Amount             | txn_amount             | Positive = deposit, negative = withdrawal |
  | Running Balance    | bank_balance           | Use latest row as cash on hand           |

### Report: Estimating Spreadsheets
- **Source file pattern:** `*estimat*` or `*bid*`
- **Format:** Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Job #              | job_id                 |                                          |
  | Bid Amount         | bid_amount             |                                          |
  | Estimated Cost     | estimated_cost         |                                          |
  | Estimated Margin % | estimated_margin       |                                          |
  | Status             | bid_status             | Pending, Won, Lost                       |

### Report: Fleet Management (Enterprise)
- **Source file pattern:** `*fleet*` or `*enterprise*`
- **Format:** CSV / Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Vehicle #          | vehicle_id             |                                          |
  | Driver             | driver                 |                                          |
  | Mileage            | mileage                |                                          |
  | Maintenance Cost   | maintenance_cost       |                                          |
  | Job Assignment     | job_id                 |                                          |

### Report: Fuel / WEX Gas Cards
- **Source file pattern:** `*wex*` or `*fuel*` or `*gas*`
- **Format:** CSV
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Card #             | card_id                |                                          |
  | Driver             | driver                 |                                          |
  | Gallons            | gallons                |                                          |
  | Total Cost         | fuel_cost              |                                          |
  | Vehicle            | vehicle_id             |                                          |
  | Date               | txn_date               |                                          |

### Report: Payroll Summary
- **Source file pattern:** `*payroll*`
- **Format:** CSV / Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Employee           | employee_name          |                                          |
  | Regular Hours      | reg_hours              |                                          |
  | OT Hours           | ot_hours               |                                          |
  | Gross Pay          | gross_pay              |                                          |
  | Burden / Taxes     | burden_cost            | Employer-side payroll taxes + benefits   |
  | Job Allocation     | job_id                 | May be split across multiple jobs        |

### Report: A/R Aging
- **Source file pattern:** `*receivable*` or `*ar_*` or `*a_r*`
- **Format:** Excel / CSV
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Customer           | customer               |                                          |
  | Invoice #          | invoice_id             |                                          |
  | Amount             | ar_amount              |                                          |
  | Invoice Date       | invoice_date           |                                          |
  | Days Outstanding   | days_outstanding       |                                          |
  | Job #              | job_id                 |                                          |

### Report: A/P Aging
- **Source file pattern:** `*payable*` or `*ap_*` or `*a_p*`
- **Format:** Excel / CSV
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Vendor             | vendor                 |                                          |
  | Invoice #          | invoice_id             |                                          |
  | Amount             | ap_amount              |                                          |
  | Due Date           | due_date               |                                          |
  | Days Outstanding   | days_outstanding       |                                          |
  | Job #              | job_id                 |                                          |

### Report: Marketing Stats
- **Source file pattern:** `*market*`
- **Format:** CSV / PDF
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Leads              | lead_count             |                                          |
  | Source / Channel   | lead_source            |                                          |
  | Spend              | marketing_spend        |                                          |
  | Conversions        | conversions            |                                          |

### Report: HR / Headcount
- **Source file pattern:** `*hr*` or `*headcount*` or `*roster*`
- **Format:** Excel
- **Fields to extract:**

  | Column / Field     | Maps To                | Notes                                    |
  |--------------------|------------------------|------------------------------------------|
  | Employee           | employee_name          |                                          |
  | Role / Title       | role                   |                                          |
  | Start Date         | start_date             |                                          |
  | Certifications     | certs                  |                                          |
  | Status             | employment_status      | Active, On Leave, Terminated             |

---

## 3. Calculations

| Metric                          | Formula                                                              | Format          |
|---------------------------------|----------------------------------------------------------------------|-----------------|
| Cash on Hand                    | Latest bank_balance (sum across all bank accounts)                   | $ whole dollars |
| Cash Flow Forecast (Week +1 to +4) | Expected A/R collections (by aging bucket) − scheduled A/P − weekly payroll − avg weekly fleet/fuel/rentals | $ whole dollars |
| Job Gross Margin %              | (contract_amount − actual_cost) / contract_amount × 100              | % with 1 decimal |
| Job Cost Variance               | actual_cost − estimated_cost (negative = over budget)                | $ whole dollars |
| Overall Gross Margin %          | Sum(contract_amount − actual_cost) / Sum(contract_amount) × 100     | % with 1 decimal |
| Cost to Complete (per job)      | estimated_cost − actual_cost (if positive; else 0 — job is over)    | $ whole dollars |
| Overbilling / Underbilling      | billed_to_date − (pct_complete × contract_amount). Positive = overbilled, negative = underbilled | $ flagged red/green |
| Backlog                         | Sum of (contract_amount − billed_to_date) on all open jobs          | $ whole dollars |
| Labor Utilization %             | Sum(job-allocated hours) / Sum(total hours) × 100                   | % with 1 decimal |
| Equipment Rental Burn (weekly)  | Sum(rental_total) for current week                                   | $ whole dollars |
| Fleet + Fuel (weekly)           | Sum(maintenance_cost) + Sum(fuel_cost) for current week              | $ whole dollars |
| Total Overhead Burn (weekly)    | Payroll burden + fleet + fuel + rentals + uncoded CC transactions    | $ whole dollars |
| Pipeline Value                  | Sum(bid_amount) where bid_status = Pending                           | $ whole dollars |
| Bid-to-Win Ratio                | Count(Won) / Count(Won + Lost) trailing 90 days × 100               | % with 0 decimal |
| Cost Per Lead                   | marketing_spend / lead_count                                         | $ with 2 decimals |
| Retainage Held                  | Sum of retainage amounts across all active jobs                      | $ whole dollars |

---

## 4. Thresholds & Alerts

| Metric                    | On Track (green)     | Warning (yellow)      | Critical (red)          |
|---------------------------|----------------------|-----------------------|--------------------------|
| Cash on Hand              | > 4 weeks of burn    | 2–4 weeks of burn     | < 2 weeks of burn        |
| Job Gross Margin %        | ≥ 20%                | 10–19%                | < 10%                    |
| Job Cost Variance         | Within 5% of budget  | 5–15% over budget     | > 15% over budget        |
| A/R Over 60 Days          | < 10% of total A/R   | 10–25% of total A/R   | > 25% of total A/R       |
| Overbilling/Underbilling  | Overbilled (positive)| Slightly underbilled   | Underbilled > 10% of contract |
| Labor Utilization %       | ≥ 80%                | 65–79%                | < 65%                    |
| Bid-to-Win Ratio          | ≥ 30%                | 20–29%                | < 20%                    |
| Cash Flow Forecast (any week) | Positive         | Positive but tight    | Negative (shortfall)     |

---

## 5. Dashboard Layout (HTML)

### Global Settings
- **Color scheme:** Dark navy (#1a1f36) background, white text, accent green (#22c55e) for on-track, amber (#f59e0b) for warning, red (#ef4444) for critical. Subtle gray cards (#2a2f45).
- **Font:** Inter, system-ui, sans-serif
- **Role switcher:** Top navigation tabs — Rob (Owner) | Bennett (CFO) | Jay (COO) | John (Sales). Active tab highlighted in white.
- **Header:** "FOUR QUARTERS — COMMAND CENTER" + week ending date
- **Entity toggle:** Consolidated | Location 1 | Location 2 | Plumbing Sub — filter that applies to all data on the page

### Role: Rob (Owner) — Sections in Order
1. **Cash Position** — Big number: cash on hand. Sparkline showing last 8 weeks. Weeks-of-runway indicator with color coding.
2. **Cash Flow Forecast** — 4-week bar chart. Green bars for positive weeks, red for negative. Show major inflows (draws) and outflows (payroll, AP).
3. **Job Scorecard** — Table of all active jobs: job name, % complete, gross margin %, cost variance, overbilled/underbilled. Sort by worst margin first. Row color = threshold color.
4. **Alerts & Action Items** — Bulleted list of everything in yellow or red across all metrics. Plain English: "Job #1042 is 18% over budget — review with Jay." Max 10 items.
5. **Pipeline & Backlog** — Two big numbers: total backlog ($) and pipeline value ($). Trend arrows vs. prior week.

### Role: Bennett (CFO) — Sections in Order
1. **Cash Dashboard** — Cash on hand, 4-week forecast chart, retainage held (not yet collectible), net position.
2. **A/R Aging Breakdown** — Stacked bar: Current, 31-60, 61-90, 90+. Total per bucket. Highlight the 60+ in red. List top 5 overdue invoices.
3. **A/P Schedule** — What's due this week, next week, next 2 weeks. Total obligations. Flag anything past due.
4. **Job Profitability Detail** — Every job: contract, estimated cost, actual cost, margin %, variance, billed vs. earned. Sortable. Over-budget jobs in red rows.
5. **Overhead & Spend Control** — Weekly totals: payroll, fleet, fuel, equipment rentals, credit card. Week-over-week comparison. Flag uncoded credit card transactions.
6. **P&L Snapshot** — If P&L report provided: revenue, COGS, gross profit, overhead, net income. Current month + YTD.

### Role: Jay (COO) — Sections in Order
1. **Job Status Board** — All active jobs: name, % complete, on schedule (Y/N), crew assigned, next milestone. Color by status.
2. **Labor Dashboard** — Utilization %, total hours this week, OT hours, OT as % of total. Top 5 employees by OT.
3. **Equipment & Fleet** — Active rentals: what, where (job), how long, cost this week. Fleet: vehicles out, mileage, maintenance due.
4. **Cost Alerts by Job** — Jobs where actual cost is trending over estimate. Show burn rate and projected overrun.
5. **Crew & Resource Gaps** — Headcount by role, anyone on leave, certifications expiring. Open positions if any.

### Role: John (VP Sales) — Sections in Order
1. **Pipeline Overview** — Total pipeline value, # of active bids, expected close rate. Funnel visual or bar chart by stage.
2. **Bid Tracker** — Table: bid name, amount, estimated margin, date submitted, expected decision date, status. Sort by decision date.
3. **Won/Lost This Week** — What closed, at what margin. Running bid-to-win ratio (90-day trailing).
4. **Marketing Performance** — Leads this week, cost per lead, conversion rate, by source/channel. Trend vs. prior 4 weeks.
5. **Customer Health** — Any customer complaints, callbacks, or service issues flagged in Service Titan. Repeat customer rate.

---

## 6. PDF Layout

- **Page size:** Letter (8.5 × 11)
- **Pages:** 4 (one per role)
- **Structure per page:**
  - **Header:** FOUR QUARTERS — [Role Name] VIEW — Week Ending [Date]
  - **Narrative summary:** 3-5 sentences, blunt and direct, using their language. Lead with the most important thing. Example: "Cash is tight — you have 2.8 weeks of runway. Two draws totaling $340K are pending but won't land until Week 14. Three jobs are over budget. Pipeline is strong at $2.1M."
  - **Key metrics table:** Top 5-7 metrics for that role, this week vs. prior week, with directional arrows and color dots
  - **Alerts / action items:** Bulleted, max 5, specific and actionable
  - **Footer:** Generated [date] from [list source files used] | Four Quarters Command Center

---

## 7. Excel Layout

- **Tab 1: Executive Summary** — All 15 key metrics, current week value, prior week value, change, status (green/yellow/red). One row per metric.
- **Tab 2: Cash Flow Forecast** — Week-by-week for 4 weeks. Rows for: starting cash, expected A/R collections, expected draw receipts, payroll, A/P due, fleet/fuel, rentals, other, ending cash.
- **Tab 3: Job Detail** — One row per job. All fields from Trimble: job #, name, contract, estimated cost, actual cost, committed, budget remaining, % complete, billed to date, margin %, variance, overbilled/underbilled.
- **Tab 4: A/R Aging** — Full A/R detail, sorted by days outstanding descending.
- **Tab 5: A/P Aging** — Full A/P detail, sorted by due date ascending.
- **Tab 6: Payroll** — Full payroll detail with job allocations. Summary row at top.
- **Tab 7: Fleet + Fuel** — Combined Enterprise fleet + WEX data. Cost per vehicle, cost per job.
- **Tab 8: Equipment Rentals** — All active rentals with job assignment and cost.
- **Tab 9: Credit Card Detail** — All transactions. Flagged column for uncoded (no job #).
- **Tab 10: Pipeline & Bids** — Estimating spreadsheet data + win/loss history.
- **Tab 11: Marketing** — Lead and spend data by source.
- **Tab 12: Raw Data** — Every field extracted from every source file, with source file name column.

---

## 8. Tone & Language

- **Voice:** Direct, confident, no hedging. Write like a foreman talks — short sentences, clear calls to action. "This job is bleeding" not "This job may be experiencing cost overruns."

- **Terminology map:**

  | They Say…         | We Use…            |
  |--------------------|--------------------|
  | Jobs               | Jobs (never "projects") |
  | Draws              | Draws (never "progress billings" or "applications for payment") |
  | Subs               | Subs (never "subcontractors") |
  | Change orders / COs | COs               |
  | Retainage          | Retainage          |
  | Crew               | Crew (never "team" or "workforce") |
  | Burn rate          | Burn rate          |
  | Bleeding / over budget | Bleeding        |
  | Pipeline           | Pipeline           |
  | Backlog            | Backlog            |

---

## 9. Special Instructions

- **Always show cash first.** Every role's view should have cash position visible within the first screen. This is their #1 pain.
- **Flag underbilled jobs prominently.** Underbilling on new construction is how cash flow problems start. If billed_to_date < (pct_complete × contract_amount), flag it in red with a note: "This job has earned more than it has billed — submit a draw."
- **Separate the plumbing sub.** Always show consolidated numbers AND entity-level breakdowns. The entity toggle should be persistent.
- **Uncoded credit card transactions** get their own alert. Every transaction without a job # is a cost that can't be tracked to a job. Surface the total uncoded amount and list the top 5 by dollar value.
- **Retainage is not cash.** When showing A/R, separate retainage from collectible receivables. Retainage won't come in until job completion — don't count it in the short-term cash forecast.
- **Never average margins across jobs.** Show weighted margin (total profit / total revenue), not the average of individual job margins. A 50% margin on a $10K job and a 5% margin on a $1M job is not 27.5%.
- **Week-over-week deltas on everything.** Every number should show the change from last week with a directional arrow. If this is the first week, show "—" for prior week.
