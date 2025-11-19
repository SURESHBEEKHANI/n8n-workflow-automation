# Automated Invoice Reminder System

An intelligent n8n workflow that automatically sends payment reminders to customers based on invoice status, helping businesses maintain healthy cash flow and reduce manual follow-up work.

## Overview

This workflow automates the invoice reminder process by reading invoice data from Google Sheets, filtering unpaid and overdue invoices, and sending personalized email reminders to customers based on their payment status.

![Automated Invoice Reminder System Workflow](Automated%20Invoice%20Reminder%20System.png)

## Architecture

The system follows a simple 5-step pipeline:

1. **Manual Trigger** - Initiates the workflow execution
2. **Get Invoice Data** - Retrieves invoice records from Google Sheets
3. **Filter Data** - Keeps only overdue and unpaid invoices
4. **Group by Status** - Categorizes invoices into Unpaid, Overdue, or Ambiguous
5. **Send Emails** - Dispatches appropriate reminder emails to each group

## Workflow Logic

### Step 1: Data Retrieval
- Connects to Google Sheets to fetch invoice data
- Reads from the configured spreadsheet (Invoice sheet)
- Retrieves all invoice records with customer details

### Step 2: Filtering
- Filters out invoices with "Paid" status
- Keeps only records that require follow-up (Unpaid or Overdue)

### Step 3: Categorization
The workflow intelligently routes invoices into three categories:

**Unpaid Invoices**
- Status: "Unpaid"
- Action: Sends friendly payment reminder before due date

**Overdue Invoices**
- Status: "Overdue"
- Action: Sends urgent overdue notice requesting immediate payment

**Ambiguous Cases**
- Status: Neither "Unpaid" nor "Overdue"
- Action: Sends notification to internal team for manual review

### Step 4: Email Delivery
Each category receives a tailored email template:

- **Unpaid**: Polite reminder with due date
- **Overdue**: Urgent notice with late fee warning
- **Ambiguous**: Internal team notification for investigation

## Components

### Data Source
- **Google Sheets** - Invoice database with customer information

### Email Service
- **Gmail** - Email delivery for customer and team notifications

### n8n Nodes
- Manual Trigger - Workflow initiation
- Google Sheets - Data retrieval
- Filter - Status-based filtering
- Switch - Multi-way routing by payment status
- Gmail (3 instances) - Email sending for each category

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google Sheets with invoice data
- Gmail account for sending emails
- Google Sheets API credentials
- Gmail OAuth2 credentials

### Google Sheets Structure

Your invoice spreadsheet should include these columns:
- Customer Name
- Customer Email
- Invoice Due (due date)
- Payment Status (Paid/Unpaid/Overdue)
- Due Date

### Configuration

1. **Import the workflow**
   - Import `Automated Invoice Reminder System.json` into your n8n instance

2. **Configure Google Sheets**
   - Set up Google Sheets OAuth2 API credentials
   - Update the document ID to point to your invoice spreadsheet
   - Ensure the sheet name matches your data source

3. **Configure Gmail**
   - Set up Gmail OAuth2 credentials
   - Update sender email addresses in all three Gmail nodes
   - Customize email templates as needed

4. **Customize email templates**
   - Edit the "Send Email Unpaid User" node for unpaid reminders
   - Edit the "Send Email Overdue User" node for overdue notices
   - Edit the "Send Email Team Data Ambigouse" node for internal alerts
   - Update company name and contact information in templates

## Usage

### Running the Workflow
1. Click "Execute workflow" on the manual trigger
2. The system will:
   - Fetch all invoice records from Google Sheets
   - Filter for unpaid and overdue invoices
   - Categorize them by payment status
   - Send appropriate email reminders to each customer
3. Check execution logs to verify emails were sent successfully

### Scheduling (Optional)
To automate this workflow on a schedule:
1. Replace the Manual Trigger with a Schedule Trigger node
2. Configure the schedule (e.g., daily at 9 AM, weekly on Mondays)
3. Activate the workflow

## Email Templates

### Unpaid Invoice Reminder
```
Subject: Payment Reminder – Invoice Due

Dear [Customer Name],

I hope this message finds you well. This is a friendly reminder that your invoice is due on [Invoice Due]. We kindly request you to ensure the payment is completed by the due date to avoid any late fees or service interruptions.

If you have already made the payment, please disregard this message. Otherwise, please reach out if you have any questions or need assistance.

Thank you for your prompt attention to this matter.

Best regards,
[Your Name]
[Your Company Name]
[Contact Information]
```

### Overdue Invoice Notice
```
Subject: Overdue Invoice Notice – Action Required

Dear [Customer Name],

We hope you are doing well. Our records indicate that your invoice, originally due on [Invoice Due], is now overdue. We kindly request that you make the payment at your earliest convenience to avoid any late fees or service interruptions.

If you have already completed the payment, please disregard this notice. Otherwise, feel free to reach out if you have any questions or require assistance.

Thank you for your prompt attention to this matter.

Best regards,
[Your Name]
[Your Company Name]
[Contact Information]
```

## Features

- **Automated invoice tracking** from Google Sheets
- **Smart status-based filtering** to identify action-required invoices
- **Multi-tier reminder system** (unpaid vs. overdue)
- **Personalized email templates** with customer and invoice details
- **Internal team alerts** for ambiguous cases
- **Manual or scheduled execution** for flexibility

## Workflow Tags
- AUTOMATION
- INVOICE MANAGEMENT
- EMAIL REMINDERS

## Best Practices

1. **Data Quality**: Ensure your Google Sheets has consistent status values
2. **Email Customization**: Personalize templates to match your brand voice
3. **Testing**: Test with a small dataset before running on all invoices
4. **Scheduling**: Set up appropriate reminder frequency (daily/weekly)
5. **Monitoring**: Review execution logs regularly to catch any errors

## Troubleshooting

**Emails not sending?**
- Verify Gmail OAuth2 credentials are valid
- Check that customer email addresses are properly formatted
- Ensure Gmail API quotas haven't been exceeded

**Wrong invoices being filtered?**
- Verify the "Payment Status" column values match exactly ("Paid", "Unpaid", "Overdue")
- Check filter conditions in the Filter and Switch nodes

**Missing data?**
- Confirm Google Sheets document ID is correct
- Verify sheet name matches the configuration
- Check that all required columns exist

## Documentation

For additional information, refer to:
- Workflow diagram: `Automated Invoice Reminder System.png`
- Workflow definition: `Automated Invoice Reminder System.json`

## License

This project is provided as-is for educational and development purposes.
