# API Integration

This page provides an overview of the API integration used in the Virechana Assessment App, specifically the integration with **Google Sheets** for data storage.

## **Overview**

The `VirechanaSheetApi` class handles the integration with Google Sheets. It allows the app to:

- Initialize sheets for storing user and vega entry data.
- Insert new data into the respective sheets.

The integration uses the `gsheets` package for seamless interaction with Google Sheets.

## **Setup**

1. **Google Sheets API Credentials**

   - The `credentials` JSON file from Google Cloud Platform is stored in `_credentials`.
   - Replace the placeholder credentials with your actual JSON credentials for the Google Sheets API.

2. **Spreadsheet ID**

   - Set the `spreadsheetID` to the ID of the Google Sheet you want to interact with.

   ```
   static final _spreadsheetID = 'your_spreadsheet_id';
   ```

3. **Dependencies**
   Add the following dependencies to your `pubspec.yaml` file:

   ```
   dependencies:
     gsheets: ^0.5.1
   ```

4. **Initialization**
   The `init()` function initializes the Google Sheets API and prepares the sheets with the required headers.

## **Key Functions**

### **1. Initialization**

Initializes the Google Sheets API and prepares the worksheets.

```
static Future init() async {
  try {
    final spreadsheet = await _gsheets.spreadsheet(_spreadsheetID);

    // Initialize the Users sheet
    _userSheet = await _getWorkSheet(spreadsheet, title: 'Users');
    final userHeaders = UserFields.getFields();
    await _userSheet!.values.insertRow(1, userHeaders);

    // Initialize the Vega Entries sheet
    _vegaSheet = await _getWorkSheet(spreadsheet, title: 'VegaEntries');
    final vegaHeaders = [
      'Date', 'Patient_name', 'Time', 'Vega', 'Upavega',
      'BP Systolic (mmHg)', 'BP Diastolic (mmHg)',
      'Pulse', 'SpO2', 'Remarks'
    ];
    final existingVegaHeader = await _vegaSheet!.values.row(1);
    if (existingVegaHeader.isEmpty) {
      await _vegaSheet!.values.insertRow(1, vegaHeaders);
    }
  } catch (e) {
    print('Init Error: $e');
  }
}
```

---

### **2. Insert Vega Entries**

Inserts multiple rows of Vega entry data into the `VegaEntries` sheet.

```
static Future insertVegaEntries(List<List<String>> rows) async {
  try {
    if (_vegaSheet == null) {
      print('VegaEntries sheet not initialized');
      return;
    }
    await _vegaSheet!.values.appendRows(rows);
    print('Data inserted successfully into VegaEntries');
  } catch (e) {
    print('Error inserting Vega Entries: $e');
  }
}
```

### **3. Insert User Data**

Adds user information into the `Users` sheet.

```
static Future insert(List<Map<String, dynamic>> rowList) async {
  if (_userSheet == null) return;
  _userSheet!.values.map.appendRows(rowList);
}
```

---

## **Helper Functions**

### **Create or Get Worksheet**

The `_getWorkSheet` function ensures a worksheet is created or fetched if it already exists.

```
static Future<Worksheet> _getWorkSheet(
  Spreadsheet spreadsheet, {
  required String title,
}) async {
  try {
    return await spreadsheet.addWorksheet(title);
  } catch (e) {
    return spreadsheet.worksheetByTitle(title)!;
  }
}
```

## **Data Format**

### **User Data**

The `Users` worksheet is initialized with the following headers:

- **Name**
- **Age**
- **Gender**
- **Contact Details**
- (Additional fields as defined in `UserFields.getFields()`)

### **Vega Entries**

The `VegaEntries` worksheet uses the following headers:

- **Date**
- **Patient Name**
- **Time**
- **Vega**
- **Upavega**
- **BP Systolic (mmHg)**
- **BP Diastolic (mmHg)**
- **Pulse**
- **SpO2**
- **Remarks**

## **Error Handling**

- **Initialization Errors**: If the spreadsheet or sheets are not correctly set up, appropriate messages are printed to the console.
- **Data Insertion Errors**: Checks are in place to ensure sheets are initialized before inserting data.

## **References**

- [GSheets Package Documentation](https://pub.dev/packages/gsheets)
- [Google Sheets API Setup Guide](https://developers.google.com/sheets/api/quickstart)
