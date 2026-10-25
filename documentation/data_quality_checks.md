# Data Quality Checks

## 1. Purpose

The purpose of these checks is to assess data completeness, uniqueness, and consistency before developing the Power BI report.

## 2. Checks Performed

| Check | Result | Status |
|---|---|---|
| Primary key uniqueness | Identified key columns had no duplicates or blank values | Passed |
| Foreign key integrity | No orphan references found in the relationships tested | Passed |
| Employee assignment duplicates | No duplicate RosterID and EmployeeID pairs found | Passed |
| Client consistency | Rosters and Routes had matching ClientID values | Passed |
| Assignment consistency | EmployeeAssignments matched the client associated with each roster | Passed |
| Rate card coverage | DutyType and VehicleType combinations in Rosters were covered by RateCard | Passed; relationship design still required |

## 3. Items Requiring Business Review

| Field or scenario | Observation | Follow-up |
|---|---|---|
| ActualPickup | Some roster records have no actual pickup time | Check roster status and determine whether the blank is expected |
| PaidDate | Some company invoices have no paid date | Compare with PaymentStatus and confirm the business rule |
| DriverPayments.RosterID | Some weekly payments and emergency advances are not linked to individual rosters | Preserve these records and analyse them according to payment type |
| DriverSharePct and MonthlySalary | Some driver records have blank values | Check whether the fields depend on ContractType or another business rule |
| Exceptions references | A small number of records have blank roster or driver references | Confirm whether these exceptions are valid or require correction |

## 4. Modelling Considerations

- Avoid relationships that cause revenue or payout amounts to be counted multiple times.
- Do not assume every driver payment corresponds to one roster.
- Confirm relationship cardinality and filter direction in Power BI.
- Determine how RateCard should connect to roster transactions, because Rosters does not contain RateCardID.

## 5. Data Privacy and Publication

Before publishing data to GitHub, review names, contact details, vehicle registration identifiers, and any other potentially identifying information. Use a synthetic or appropriately anonymised dataset for the public portfolio.

## 6. Status

Initial structural checks have been documented. Business-rule validation, final relationship settings, and publication-safety checks remain to be completed.

*Note: These results apply to the sample workbook reviewed for this project. They do not establish that every business rule or record is correct.*
