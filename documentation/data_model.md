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


## Relationship Validation Results

Initial checks were performed against the sample workbook. The relationships below passed the initial key and reference checks; confirm the final Power BI relationship settings before treating the model as complete.

| Parent table | Child table | Relationship key |
|---|---|---|
| Clients | Employees | ClientID |
| Clients | Routes | ClientID |
| Clients | Rosters | ClientID |
| Clients | CompanyInvoices | ClientID |
| Clients | Exceptions | ClientID |
| Employees | EmployeeAssignments | EmployeeID |
| Drivers | Rosters | DriverID |
| Drivers | DriverPayments | DriverID |
| Drivers | DriverComplaints | DriverID |
| Drivers | EmployeeFeedback | DriverID |
| Drivers | Exceptions | DriverID |
| Vehicles | Rosters | VehicleID |
| Routes | Rosters | RouteID |
| Rosters | EmployeeAssignments | RosterID |
| Rosters | DriverPayments | RosterID |
| Rosters | DriverComplaints | RosterID |
| Rosters | EmployeeFeedback | RosterID |
| Rosters | Exceptions | RosterID |

### Additional Validation Notes

- All identified primary key candidates were unique and nonblank.
- No orphan foreign key references were found in the relationships tested.
- The EmployeeAssignments combination of RosterID and EmployeeID had no duplicate pairs in the sample.
- Rosters and Routes had consistent ClientID values.
- EmployeeAssignments had consistent employee and roster client assignments.
- DriverPayments contains blank RosterID values for weekly payments and emergency advances. These records should not be discarded automatically.
- Missing ActualPickup and PaidDate values require appropriate business interpretation.
- RateCard combinations matched the DutyType and VehicleType combinations found in Rosters. A suitable relationship design still needs to be determined because Rosters does not contain RateCardID.
- Avoid directly joining transaction tables in ways that could duplicate financial amounts.

These results are preliminary data-quality checks, not a substitute for validating relationship cardinality and filter direction in Power BI.

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
