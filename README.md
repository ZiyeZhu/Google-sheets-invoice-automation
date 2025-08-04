# Google-sheets-invoice-automation

This Google Apps Script automates invoice registration in a Google Sheet.  
It supports dynamic data entry and updates multiple sheets based on payment method.

## 📋 Features

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

## 🧠 Tech

- Google Apps Script (JavaScript-based)

- Key Knowledge Points

    String Parsing in JavaScript: Extracting numeric values based on keywords (e.g. using regex for ESP\d+)

    Date Handling: Formatting dates as dd/MM/yyyy using JavaScript's Utilities.formatDate

    Sheet Manipulation:

        getLastRow(), appendRow(), and getRange() to interact with specific cells and rows

        Updating other sheets based on input from one main form

    Logging & Debugging: Logger.log() used to trace actions and ensure script runs correctly



# addCVNote_Final()
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
