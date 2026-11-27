# Executive Decision Support System

Independent AI-assisted executive planning prototype linking sales demand, team capacity, supplier availability, profitability and working capital. All assumptions are synthetic; no employer or customer data is used.

## Run
Open `index.html` with `model.js` in the same directory. No dependencies or keys. For GitHub Pages, publish `main` / root. Run `node test.js` (Node.js 18+) to test the model.

## Features
- Ten scenario inputs and five preset scenarios, including growth, supplier disruption, automation and slow collections.
- Baseline comparison, operating statement, liquidity bridge, fulfillment and capacity indicators.
- Demand × unit-cost sensitivity table, risk register, dynamic executive briefing and CSV/text exports.

## Model
One 30-day planning period for a fictional distribution business. USD amounts are hypothetical. Orders are generated from a base demand assumption, not from a forecast. Shipments = minimum of orders, team throughput and available supply. Team throughput = floor(headcount × units per employee × assumed automation uplift). Revenue and COGS use shipped units. Gross profit = revenue − COGS; EBITDA proxy = gross profit − payroll − marketing − other fixed operating expenses. Operating expenses already include payroll and marketing; do not subtract them again. Break-even units = ceil(operating expenses / unit contribution), only when unit contribution is positive; capacity may make break-even unattainable.

Working capital = receivables + inventory − payables. Targets use monthly revenue × collection days / 30, COGS × 15 / 30 for inventory, and COGS × payment days / 30 for payables. Operating cash proxy = EBITDA − change in working capital. Closing cash = opening cash + operating cash proxy − capital expenditure. This is a simplified balance-target bridge, not a dated cash-flow forecast. Opening balances are fixed for all scenarios, not calibrated to the baseline sales rate.

## Suggested experiment
1. Select Growth surge and compare profitability, backlog and cash to baseline.
2. Select Automation investment; increase supply and adjust capital expenditure. Discuss why a higher productivity assumption alone cannot remove supplier bottlenecks.
3. Select Slow collections and observe the difference between EBITDA and cash.
4. Inspect the sensitivity table before choosing a plan. Review risks and export the executive brief.

## Validation
`test.js` covers 324 combinations of demand, unit cost, headcount, automation and collection days plus eight additional checks. It checks shipment constraints, accounting identities, deterministic behavior, validation, cash sensitivity and break-even edge cases.

## Limitations
No production AI integration, live accounting data, taxes, depreciation, interest, financing, multi-period budgets, labor quality or service-time simulation, seasonality, correlated demand/cost effects, dated purchases or receipts. Productivity uplift and investment cost are independent assumptions; no measured ROI is claimed. Risk thresholds are illustrative rules rather than calibrated probabilities. No authentication or persistence. The model demonstrates business reasoning, not an audited financial model or investment advice. Future work: transaction-level cash forecasting, multi-period budgets, uncertainty simulation, business-system integrations and human approval workflows.
