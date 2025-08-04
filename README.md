# Google-sheets-invoice-automation
## function addInvoiceRecordWithPaymentHandling()

This Google Apps Script automates invoice registration in a Google Sheet.  
It supports dynamic data entry and updates multiple sheets based on payment method.

### 📋 Features

- Add a new invoice row with auto-generated invoice number and today's date
- Fill in client, amount, group ID, remarks, and payment method interactively
- Automatically write to:
  - 🧾 Invoice Sheet
  - 💵 Cash Sheet (for `ESPxxx`)
  - 🎫 Travel Cheques Sheet (for `CVxxx`)
  - 💳 Cheques Sheet (for `CHQxxx`)
- Copy formatting from previous row
- Update payment receipt column with formatted note
- Logging via `Logger.log()`

### 🧠 Tech

- Google Apps Script (JavaScript-based)

🧠 Key Knowledge Points

This project leverages Google Apps Script to automate invoice and payment record handling across multiple sheets. Below are the core concepts demonstrated:
✅ 1. Date Handling in Google Apps Script

    Generate today's date dynamically:

    const today = Utilities.formatDate(new Date(), "GMT+2", "dd/MM/yyyy");

    Custom formatting ensures locale-specific display (e.g., dd/MM/yyyy for French-style dates).

✅ 2. String Parsing with Regular Expressions

    Extract numeric values from strings like ESP600 CV800:

    const matches = paymentStr.match(/ESP(\d+)/);
    const amount = matches ? parseFloat(matches[1]) : null;

    Handles multiple payment methods in a single string.

✅ 3. Conditional Logic and Branching

    Determine which payment method is included (ESP, CV, CHQ) and take appropriate action:

    if (paymentMethod.includes("ESP")) { /* update cash sheet */ }
    if (paymentMethod.includes("CV"))  { /* update travel voucher sheet */ }
    if (paymentMethod.includes("CHQ")) { /* update cheque sheet */ }

✅ 4. Inter-Sheet Data Interaction

    Append rows to different sheets based on parsed payment methods using:

    targetSheet.appendRow([today, amount, note, invoiceNo]);

    Ensures each financial movement is tracked in the appropriate ledger.

✅ 5. Auto-Incrementing Invoice Numbers

    Determine the last used invoice number and generate the next in sequence:

    const lastRow = invoiceSheet.getLastRow();
    const lastInvoice = invoiceSheet.getRange(lastRow, 2).getValue();
    const nextInvoice = generateNextInvoiceNo(lastInvoice);

✅ 6. Logging for Debugging and Monitoring

    Uses Logger.log() to trace execution steps and capture values at key stages.


## addCVNote_Final()
🔁 Function: addCVNote_Final()

This function updates the Remarks column in the Invoices sheet based on payment records from the Travel Voucher sheet. It adds a timestamped confirmation note (e.g., 600 RECU LE 04/08/2025) to invoices that have been paid via travel vouchers.
✅ Purpose

To automate the reconciliation of received payments by:

    Matching travel voucher entries to corresponding invoice numbers

    Appending a dated payment confirmation note to the invoice’s remarks

📌 How It Works

    Iterates through rows 429 to 442 in the "Travel Voucher" sheet

    For each row:

        Extracts the amount (Column B) and invoice number (Column D)

        Searches the "Invoices" sheet for a matching invoice number in Column B

        If matched:

            Checks if the confirmation fragment already exists

            If not, appends a string like 600 RECU LE 04/08/2025 to the existing remark in Column H

        Skips any entry missing an amount or invoice number

        Logs all updates and unmatched records for debugging

📅 Date Format

    The current date is dynamically generated in dd/MM/yyyy format using:

    Utilities.formatDate(new Date(), "GMT+2", "dd/MM/yyyy")

🧠 Key Concepts

    Data validation: Ensures amount and invoice number are present

    String manipulation: Prevents duplicate remark entries by checking for existing fragments

    Data writing: Updates cell values based on dynamic match

    Logging: Uses Logger.log() to help trace execution steps and skipped rows
