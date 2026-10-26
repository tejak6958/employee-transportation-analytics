# WhatsApp Automation (Dry-Run Concept)

Four automations driven by the same tables as the Power BI model. By default every message is written to `output/dry_run_log.csv` instead of being sent. All names, numbers and amounts are fictional.

## Folder structure to add

```
automation/
├── README.md
├── .env.example            # placeholder keys only, never real secrets
├── data/
│   ├── sample_complaints.csv
│   ├── sample_drivers_emi.csv
│   ├── sample_invoices.csv
│   └── sample_contacts.csv      # fictional agency managers and fake numbers
├── templates/
│   ├── 01_driver_complaint.txt
│   ├── 02_agency_complaint.txt
│   ├── 03_driver_emi_statement.txt
│   └── 04_payment_request.txt
├── scripts/
│   └── send_messages.py         # reads data + templates, writes the log
├── output/
│   └── dry_run_log.csv          # generated
└── images/
    └── automation_preview.png
```

## Steps

1. **Prepare the data.** Put the four sample tabs in a Google Sheet (or CSV files in `data/`), copied from the model's tables. The complaints tab needs a `RaisedBy` column (Employee or Driver); add it to the sample data if your dataset does not have one. Add a contacts tab mapping each tech park to a fictional agency manager and accounts contact.
2. **Define the trigger rules** (below) in this README so a reader sees the logic before the code.
3. **Write the templates** with placeholders such as `{driver_name}` and `{amount}`.
4. **Write the script** to read each tab, apply the rule, fill the template and append a row to the log (recipient, message, rule, timestamp). Keep `DRY_RUN=true` as the default.
5. **Run it** and save a screenshot of the log or the rendered messages as `images/automation_preview.png`.
6. **Optional live mode.** Use the WhatsApp Cloud API or a Twilio sandbox with pre-approved templates, keep tokens in `.env`, and test only with your own number.

## Trigger rules

| # | Trigger | Recipient | Source |
|---|---|---|---|
| 1 | Complaint raised by an employee and not resolved | The driver | Complaints + Drivers |
| 2 | Complaint raised by a driver | Agency manager of that tech park | Complaints + Clients + Contacts |
| 3 | Month end, driver with a monthly EMI | The driver | Drivers + payments |
| 4 | Invoice Pending or Overdue and past its due date | Agency accounts contact | Invoices + Clients + Contacts |

## Message templates

**01 Driver complaint**
```
Hello {driver_name} ({driver_id}),
A complaint was logged on {complaint_date}.
Type: {complaint_type} | Severity: {severity}
Please contact the transport desk today. Ref: {complaint_id}
- TK Travels & Services
```

**02 Agency complaint**
```
Dear {manager_name} ({tech_park}),
Driver {driver_id} reported: {complaint_type} on {complaint_date}.
Kindly review and advise. Ref: {complaint_id}
- TK Travels & Services
```

**03 EMI statement**
```
Hi {driver_name}, statement for {month}:
Trip payout: Rs {payout}
Vehicle EMI deducted: Rs {emi}
Net payable: Rs {net}
```
If `net` is negative, do not send the raw statement. Route it to an operations review and show the shortfall instead. In the sample data average EMI is higher than average monthly payout, so this case will occur.

**04 Payment request**
```
Dear Accounts Team ({client_name}),
Invoices {invoice_ids} totalling Rs {amount} are {days_past_due} days past due.
Kindly release payment by {requested_date}.
- TK Travels & Services
```
Escalate wording by ageing bucket (1 to 30, 31 to 60, 60+ days).

## Rules for this folder

- Fictional names and numbers only (for example +91 99999 00001).
- Never commit tokens. `.env` stays in `.gitignore`.
- State clearly that this is a concept running in dry-run mode.
