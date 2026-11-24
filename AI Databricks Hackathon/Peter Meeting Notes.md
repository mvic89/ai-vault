### Problem Statement and Use Case

- Peter’s idea: help customers gain awareness of recurring payments, subscriptions, and potential fraud
- Core insight: even financially savvy people are surprised by how much they spend on subscriptions
    - Peter listed his own recurring payments in 30 seconds and still missed some
    - Customers at best check bank statements once a year, leaving room for months of unnoticed charges
- Philosophical layer on top: help people align spending with what actually brings them happiness
    - Optional stretch goal; awareness alone is sufficient for the hackathon
- Regulatory tailwind: PSD3/PSR coming, transaction data will expand significantly in the next year
    - Current limit: ~25 characters of text per transaction; much richer data incoming

### Five Key Features (from Peter’s notes)

- Detect recurring payments and subscriptions, including price changes
    - Example: Netflix quietly upgrading resolution tier = higher charge
- Flag subscriptions the customer may not be using
    - Duplicate services, gym memberships that “lapsed,” streaming services never opened
- Flag transactions that look fraudulent
    - Not ID theft: focus on subscriptions customers unknowingly signed up for
    - Often cryptically named to avoid recognition
- Rank findings by money at stake
- Present a customer-facing summary with clear cancel/keep options

### Data, Scope, and Tech Notes

- No real customer data available from Sparbankensyd; team must source their own
    - Suggested approach: team members export their own bank transactions, anonymize, and combine
    - Most Swedish banks allow Excel/PDF export of last 3 months
    - PSD2 API also available to pull data across multiple banks programmatically
- Transaction types in scope: card payments, autogiro, e-faktura, SWIFT, account transfers
    - Loan/mortgage repayments: lower priority (hard to act on)
    - Swish: trickiest category, increasingly used for subscriptions; recurring Swish launched recently
    - Digital wallets: underlying card captures the transaction, so data is available
- Sparbankensyd IT stack: Teradata + Power BI, on-prem (shared with 25 smaller banks), cloud migration planned in ~2 years
- Demo date: 1st December; Peter not attending in person but may join digitally
    - Suleman to follow up with Per and Peter about remote attendance
    - Option to show Peter results the week after and explore a Databricks conversation if the demo lands well

### Next Steps

- **Collect and anonymize transaction data for the dataset**Team members export their own bank transactions (last 3 months), anonymize, and pool; manually tag Swish transactions as a priority.
- **Align team on feature scope before building**Price-change detection and unused-subscription flagging are the strongest candidates; fraud detection is lower priority per Peter.
- **Post any remaining questions to Peter in Discord**Peter offered to answer questions there or set up an extra call to discuss ideas or hypotheses.