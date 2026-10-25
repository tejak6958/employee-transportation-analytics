# Data Model — Employee Transportation Analytics

## Purpose

This document describes the intended Power BI data model for analysing employee transportation operations using synthetic sample data.

The relationships must be validated against the actual table columns, key uniqueness, and business requirements before implementation.

## Tables

### Reference and Dimension Tables
- Clients
- Employees
- Drivers
- Vehicles
- Routes
- RateCard

### Operational and Transaction Tables
- Rosters
- EmployeeAssignments
- CompanyInvoices
- DriverPayments
- DriverComplaints
- EmployeeFeedback
- Exceptions

## Proposed Relationship Review

The following relationships are candidates for validation, not confirmed relationships:

| Potential parent table | Potential child table | Key to investigate |
|---|---|---|
| Clients | CompanyInvoices | ClientID |
| Clients | Rosters | ClientID |
| Employees | EmployeeAssignments | EmployeeID |
| Drivers | Rosters | DriverID |
| Vehicles | Rosters | VehicleID |
| Routes | Rosters | RouteID |
| Drivers | DriverPayments | DriverID |

Additional relationships involving complaints, feedback, exceptions, rate cards, and rosters must be determined from the actual columns and business rules.

## Modelling Principles

1. Validate that each proposed parent key is unique.
2. Confirm the grain of each table before creating relationships.
3. Prefer one-to-many relationships where the data supports them.
4. Avoid many-to-many relationships unless they are justified.
5. Avoid directly joining transaction tables when doing so could multiply financial amounts.
6. Use a calendar table for date-based reporting where appropriate.
7. Document which date each measure uses, such as invoice date, payment date, or roster date.

## Financial Rules

- Company revenue is calculated per chargeable roster.
- Driver payout is calculated per completed roster.
- Company invoices and driver payments must be analysed at their own documented grain.
- Financial measures must be reconciled against source records to ensure that amounts are not duplicated.

## Validation Status

The final relationships and model design remain subject to validation against the actual workbook and the business requirements document.
