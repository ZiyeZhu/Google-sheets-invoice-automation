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
