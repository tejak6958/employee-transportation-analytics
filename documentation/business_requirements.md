# Business Requirements — Employee Transportation Analytics

## 1. Business Context

Employee transportation operations involve coordinating employees, drivers, vehicles, routes, and daily transportation rosters.

Management needs visibility into financial performance, operational execution, driver payments, service exceptions, and employee feedback to identify issues and improve decision-making.

This project uses synthetic sample data covering April–September 2026 to demonstrate how Power BI can support these requirements.

## 2. Business Objectives

- Monitor company invoicing, collections, and outstanding amounts.
- Evaluate roster and transportation operations.
- Analyse driver payouts against completed rosters.
- Identify operational exceptions and service issues.
- Review driver complaints and employee feedback.
- Develop a data model that supports consistent reporting.

## 3. Financial Assumptions

The project follows these working assumptions:

- Company revenue is earned per chargeable roster.
- Driver payout is earned per completed roster.
- Financial calculations must follow the definitions and conditions specified in the dataset documentation.

Revenue and driver payouts must be analysed at their appropriate levels of detail to prevent duplicated amounts when tables are related.

## 4. Data Scope

The dataset contains 13 tables covering clients, employees, drivers, vehicles, routes, rate cards, rosters, employee assignments, company invoices, driver payments, driver complaints, employee feedback, and operational exceptions.

## 5. Planned Analytical Areas

### Financial Performance
- Total invoiced amount
- Amount collected
- Outstanding amount
- Invoice payment status

### Transportation Operations
- Roster activity
- Chargeable and completed roster performance
- Operational exceptions

### Driver Payments
- Driver payout analysis
- Payment status and trends
- Comparison of payouts with completed roster activity

### Service Quality
- Driver complaints
- Employee feedback
- Patterns in service-related exceptions

## 6. Data Quality and Governance

- Use synthetic sample data for public portfolio publication.
- Validate key uniqueness and relationship cardinality.
- Check missing values, duplicate records, and inconsistent categories.
- Confirm that financial calculations respect the grain of each table.
- Avoid exposing personal information, credentials, confidential records, or local machine paths.

## 7. Deliverables

- Documented Power BI data model
- Business measures aligned with defined requirements
- Interactive report pages and visualisations
- Dataset documentation
- Reproducible project documentation in GitHub

## 8. Project Status

The initial financial measures have been created in Power BI. Data-model review, additional analytical measures, and report-page development will follow.

## 9. Disclaimer

This is a portfolio demonstration using synthetic sample data. Findings from the sample dataset do not represent verified results from an actual transportation business.
