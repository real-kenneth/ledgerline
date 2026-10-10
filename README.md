# Ledgerline

A budget analyzer for property owners associations. It forecasts each budget line with its own method, checks the figures against the source records, turns the accounting forecast into year-end cash scenarios, drafts next year's budget, and models reserve funding over 30 years.

**Live demo:** _add your GitHub Pages link here_

> All data in this repository is fictional. "Pecan Hollow POA" and every figure in the demo are invented. Ledgerline was built from an independent analysis I did for a real association, whose records are kept private.

## Why it exists

I built an Excel budget model for a residential property owners association and found an expense line that had already exceeded its full-year budget by mid-year. The spreadsheet answered one question once. Ledgerline turns that analysis into a reusable tool and handles problems the spreadsheet glossed over:

- Dues collected in January, an insurance premium not yet billed, and a monthly electric bill should not be projected the same way.
- An accounting surplus is not cash: receivables may not be collected, and bad debt is not a payment.
- The records were incomplete (no receivable aging, no reserve component inventory), so those items are treated as visible assumptions rather than facts.

## What it does

| Section | What it shows |
| --- | --- |
| Budget, actual, and forecast | Each line forecast by run rate, full-year amount recognized, scheduled payment, or estimate with a written basis. Flags over-budget, unbudgeted, and projected-underspend lines above a materiality threshold. |
| Agreement with source records | Line-by-line check of every budget and actual against an unchangeable copy of the source, plus forecast agreement with the source's estimates. |
| Operating-cash scenarios | Year-end cash at 0%, 50%, and 100% of receivables collected, with every assumption shown beside the result. |
| Preliminary next-year budget | Editable proposed amounts with notes, totals, surplus before and after interest, and largest changes. |
| Reserve funding model | 30-year pooled cash flow on illustrative data. Reports the minimum year-1 contribution that meets year-end balances and a stricter replacement-first low point, plus percent funded. |
| Calculation tests | 17 automated tests run on synthetic data each time the page loads. |

## Methods and assumptions

- **Share of year elapsed** is computed from the actuals cutoff date, not month-end.
- **Status thresholds** (5% watch, 15% over, plus a dollar materiality threshold) are configurable management screens, not industry standards.
- **Assessment discounts** are contra-revenue: they reduce revenue and never receive a favorable flag. Only discounts not yet recorded reduce future cash collections.
- **Cash scenarios** remove only the remaining portion of bad-debt expense from payments and never treat a forecast below the recorded amount as a cash refund.
- **Reserve costs** are inflated from the cost-estimate year; component age comes from a separate valuation year. Interest is earned on the opening balance each year (an approximation, disclosed on the page).
- **Minimum contributions** are threshold-funding results, not full funding. Percent-funded bands (under 30% weak, 30% to under 70% fair, 70% and above strong) follow common practitioner guidelines, not a CAI-mandated grade.
- **Invalid inputs** (a fractional year, a useful life under 1) block the reserve calculation with a visible warning instead of silently dropping a replacement.

## How it was built

I built Ledgerline with Claude, an AI assistant: I set the goals, supplied the data and finance requirements, and Claude wrote the code. I then had a second AI system, ChatGPT, review the methodology and later inspect and run the code, and I directed Claude to fix what each review found. Those reviews caught ten modeling errors, including blanket annualization of front-loaded dues, treating an accounting surplus as cash, and a reserve check that only looked at year-end balances.

## What is and isn't established

- **Checked:** the private version reproduces the source workbook's totals, and the calculations pass the built-in tests.
- **Not established:** board adoption of any recommendation, realized savings, the accuracy of the forecasts, receivable collectibility, or the real association's reserve needs.

## Run it

Open `index.html` in a browser. It is a single self-contained file with no build step; edits are saved in your browser only.
