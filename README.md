# SheetSync: Real-Time Google Sheets Change Tracker

SheetSync is a lightweight and efficient Google Apps Script that tracks changes in Google Sheets and sends the updated data to a specified backend server in real-time. This script is perfect for automating workflows, maintaining data consistency, and triggering backend actions based on spreadsheet changes.

---

## Features
- 🚀 **Real-Time Tracking**: Detects cell edits instantly.
- 📡 **Data Sync**: Sends change data (new value, old value, location, and timestamp) to your backend via HTTP POST.
- 📋 **Detailed Insights**: Captures sheet name, cell location, and both new and old values.
- 💼 **Customizable**: Easily extend or integrate into your existing workflows.

---

## How It Works
1. **Edit a Cell**: The script detects changes made in Google Sheets.
2. **Data Collection**: Collects relevant information such as the sheet name, cell location, old value, and new value.
3. **Data Transmission**: Sends this data as a JSON payload to your backend server.

---

## Getting Started

### Prerequisites
- A Google Account.
- Basic understanding of Google Sheets and Apps Script.
- A backend server endpoint to receive JSON data.

### Installation
1. Open your Google Sheet.
2. Go to **Extensions > Apps Script**.
3. Copy and paste the following code:

```javascript
function onEdit(e) {
  // Get details of the edit
  const sheet = e.source.getActiveSheet();
  const range = e.range;
  const newValue = range.getValue();
  const oldValue = e.oldValue;

  // Prepare the data to send
  const payload = {
    sheetName: sheet.getName(),
    row: range.getRow(),
    column: range.getColumn(),
    newValue: newValue,
    oldValue: oldValue || null, // Old value may be undefined
    timestamp: new Date().toISOString()
  };

  // Backend server URL
  const url = '';

  // Options for the HTTP POST request
  const options = {
    method: 'post',
    contentType: 'application/json',
    payload: JSON.stringify(payload)
  };

  // Send the data to the backend
  console.log(payload)
}
```

### Example Payload 

```
{
  "sheetName": "Sheet1",
  "row": 3,
  "column": 2,
  "newValue": "Updated Value",
  "oldValue": "Old Value",
  "timestamp": "2024-11-30T12:34:56Z"
}
```

### Use Cases 
Data Synchronization: Keep your backend database in sync with Google Sheets changes. \
Workflow Automation: Trigger workflows or notifications based on edits. \
Audit Logs: Maintain an audit trail of all changes in a Google Sheet. 
