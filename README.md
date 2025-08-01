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
