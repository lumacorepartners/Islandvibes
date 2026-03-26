# Client Profile — Four Quarters

---

## 1. Business Overview

| Field              | Details                                              |
|--------------------|------------------------------------------------------|
| **Business Name**  | Four Quarters                                        |
| **Industry**       | Construction (General Contractor + Plumbing Subs)    |
| **Business Type**  | Multiple entities under one ownership group           |
| **Number of Entities / Locations** | 2 locations; plumbing subsidiaries   |
| **Approximate Size** | Mid-market — multiple crews, fleet, equipment       |
| **Years in Operation** |                                                    |

---

## 2. Primary Problems & Blind Spots

1. **Cash flow timing** — New construction pay cycles create long gaps between work performed and cash received. Draw schedules, retainage, and slow-paying GCs/owners mean cash out runs ahead of cash in.
2. **Job cost visibility** — Cannot see in real time whether a job is making or losing money until it's too late. Costs are scattered across Trimble, Service Titan, equipment rentals, fuel, subs, and payroll with no single view.
3. **Cross-division visibility** — Hard to get one picture across the main entity and plumbing subsidiaries. Each division has its own data silos and the owner has no unified dashboard.
4. **Cost leakage** — Fleet, fuel (WEX), equipment rentals, and credit card spend are tracked in separate systems. No easy way to see if costs are running over on a per-job or per-division basis.
5. **Forecasting gaps** — Estimating spreadsheets live separately from actual costs, so there's no automatic estimated-vs-actual comparison to flag margin erosion early.

---

## 3. Weekly Decisions & Information Needs

| Decision                                          | Data Needed                                              |
|---------------------------------------------------|----------------------------------------------------------|
| Which jobs to bill / submit draws on              | Job completion %, costs to date, draw schedule status     |
| Where to allocate crews next week                 | Open jobs, job priority, crew availability, backlog       |
| Whether to rent or buy equipment for upcoming jobs | Equipment rental spend trends, utilization, job timelines |
| Which invoices to chase for collections           | A/R aging, days outstanding, customer payment history     |
| Which bills to pay now vs. hold                   | A/P aging, cash on hand, expected inflows this week       |
| Go/no-go on new bids                              | Current backlog capacity, margin on pipeline estimates    |
| Flag problem jobs before they bleed               | Job cost vs. estimate, % complete vs. % billed           |
| Payroll/labor cost check                          | Hours by job, overtime, labor cost vs. budget             |
| Fleet & fuel review                               | Fleet costs by vehicle/job, fuel spend vs. prior week     |
| Marketing ROI check                               | Lead volume, cost per lead, conversion to sold jobs       |

---

## 4. Roles & Views

### Role: Owner
- **Name:** Rob
- **Cares about:** The big picture — cash position, total profitability, whether the company is growing or shrinking, and catching problems before they become emergencies
- **Top questions each week:**
  1. How much cash do I actually have, and how long will it last at the current burn rate?
  2. Are my jobs making money or am I feeding them cash?
  3. What does the pipeline look like — do I have enough work sold to keep crews busy?
  4. Are there any fires I need to deal with this week?

### Role: CFO
- **Name:** Bennett
- **Cares about:** Cash flow forecasting, A/R and A/P management, cost control, financial accuracy across all entities, banking relationships
- **Top questions each week:**
  1. What's the 4-week cash flow forecast — when do draws land vs. when are payables due?
  2. Which receivables are past due and what's the total exposure?
  3. Are job costs tracking to estimates, or are we bleeding margin?
  4. What's the P&L looking like across entities — any surprises?
  5. Are credit card, fleet, and fuel expenses in line with budget?

### Role: COO
- **Name:** Jay
- **Cares about:** Operations execution — are jobs running on time, on budget, with the right people and equipment in the right place
- **Top questions each week:**
  1. Which jobs are behind schedule and why?
  2. Where is labor being over- or under-allocated?
  3. What equipment is rented right now and what's the burn rate?
  4. Are there any warranty / callback / punch list items piling up?
  5. What's the status of permits, inspections, and compliance items?

### Role: VP of Sales
- **Name:** John
- **Cares about:** Pipeline, estimating accuracy, closing rate, revenue growth, customer relationships
- **Top questions each week:**
  1. How much is in the active pipeline and what's the expected close rate?
  2. Which bids are outstanding and when are decisions expected?
  3. How did last week's sold jobs compare to the estimate targets?
  4. What are the marketing stats — lead flow, cost per lead, conversion?
  5. Any customer issues that could affect repeat business or referrals?

---

## 5. Learning Style

- [x] **Numbers** — construction people think in dollars per job, margins, and percentages
- [ ] **Narratives** — keep it short; bullet points over paragraphs
- [x] **Visuals** — color-coded job status, cash flow charts, gauges for KPIs
- [x] **Checklists** — action items and exception lists (what needs attention NOW)

**Notes on tone/style:**
Direct and blunt. No fluff. Use construction language — "jobs" not "projects," "subs" not "subcontractors," "draws" not "progress billings." Flag problems in red, call out wins in green, and don't bury bad news.

---

## 6. Weekly Reports & Data Sources

| #  | Report Name                    | Source System             | Format         | Key Fields / Columns                                        |
|----|--------------------------------|---------------------------|----------------|--------------------------------------------------------------|
| 1  | Job Cost Detail                | Trimble                   | CSV / Excel    | Job #, phase, cost code, committed, actual, budget, variance |
| 2  | Service Tickets / Work Orders  | Service Titan             | CSV / Excel    | Ticket #, customer, job, revenue, tech, status, completion   |
| 3  | Equipment Rental Log           | Equipment Rental Stores   | Excel / PDF    | Job #, equipment type, rental period, daily/weekly rate, total |
| 4  | Credit Card Transactions       | Credit Card Provider      | CSV            | Date, vendor, amount, card holder, job # (if coded)          |
| 5  | Bank Transactions              | Bank Export               | CSV            | Date, description, amount, running balance                   |
| 6  | Estimating Spreadsheets        | Internal Excel            | Excel          | Job #, bid amount, estimated cost, margin %, status          |
| 7  | Fleet Management               | Enterprise Fleet Mgmt     | CSV / Excel    | Vehicle #, driver, mileage, maintenance cost, job assignment |
| 8  | Fuel / Gas Cards               | WEX                       | CSV            | Card #, driver, gallons, cost, vehicle, date                 |
| 9  | Payroll Summary                | Payroll System            | CSV / Excel    | Employee, hours, OT hours, gross pay, burden, job allocation |
| 10 | Accounts Receivable Aging      | Accounting System         | Excel / CSV    | Customer, invoice #, amount, date, days outstanding, job #   |
| 11 | Accounts Payable Aging         | Accounting System         | Excel / CSV    | Vendor, invoice #, amount, due date, days outstanding, job # |
| 12 | Customer List / Info           | CRM / Service Titan       | CSV            | Customer, contact, type (residential/commercial), history    |
| 13 | Marketing Stats                | Marketing Platform        | CSV / PDF      | Leads, source, cost, conversions, cost per lead              |
| 14 | HR / Headcount Info            | Payroll / HR System       | Excel          | Employee, role, start date, certifications, status           |

---

## 7. Key Metrics by Role

| #  | Metric                                  | Definition / Source                                              | Roles              |
|----|-----------------------------------------|------------------------------------------------------------------|---------------------|
| 1  | **Cash on Hand**                        | Current bank balance across all accounts                         | Rob, Bennett        |
| 2  | **Cash Flow Forecast (4-week)**         | Expected inflows (draws, A/R) minus expected outflows (A/P, payroll, fixed) | Rob, Bennett        |
| 3  | **Total A/R Outstanding**               | Sum of all unpaid invoices                                       | Rob, Bennett        |
| 4  | **A/R Over 60 Days**                    | Receivables past 60 days — the danger zone                       | Bennett             |
| 5  | **Total A/P Due This Week**             | Bills due in the next 7 days                                     | Bennett             |
| 6  | **Job Gross Margin (per job)**          | (Contract amount − actual costs) / contract amount               | Rob, Bennett, Jay   |
| 7  | **Job Cost Variance (per job)**         | Actual cost − estimated cost (negative = over budget)            | Jay, Bennett        |
| 8  | **Overall Gross Margin %**              | Total revenue minus total COGS / total revenue                   | Rob, Bennett        |
| 9  | **Backlog (sold not started + in progress)** | Sum of remaining contract value on open jobs                | Rob, Jay, John      |
| 10 | **Labor Utilization %**                 | Billable hours / total hours across all crews                    | Jay                 |
| 11 | **Equipment Rental Spend (weekly)**     | Total rental costs this week                                     | Jay, Bennett        |
| 12 | **Fleet + Fuel Spend (weekly)**         | Enterprise fleet + WEX gas combined                              | Jay, Bennett        |
| 13 | **Pipeline Value**                      | Total value of active bids / proposals                           | Rob, John           |
| 14 | **Bid-to-Win Ratio**                    | Jobs won / jobs bid (trailing 90 days)                           | John                |
| 15 | **Cost Per Lead**                       | Marketing spend / leads generated                                | John                |

---

## 8. Notes & Context

- **Cash flow timing is the #1 pain.** New construction draw cycles mean they perform work for weeks before submitting a draw, then wait 30-60+ days for payment. Meanwhile, payroll, subs, materials, equipment, and fuel are all going out the door weekly. The command center must make this gap visible and forecasted.
- **Plumbing subsidiaries** operate somewhat independently but roll up to the same ownership. Need to see them both individually and consolidated.
- **Retainage** is a factor — a percentage of each draw is held back until project completion. This is cash earned but not yet collectible and needs to be tracked separately.
- **Seasonal patterns** — construction volumes may shift with weather and permitting cycles.
- **Multiple data silos** — no single ERP ties it all together today. The command center IS the unifier.
