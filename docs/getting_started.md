# Getting Started

Welcome to the Virechana Assessment App Documentation! This guide will help you set up and run the application on your local system.

---

## **Prerequisites**

Before getting started, ensure you have the following:

- [Flutter SDK](https://docs.flutter.dev/get-started/install): Installed and properly set up on your system.
- **Google Sheets API Credentials**: Obtain and configure credentials to enable integration with Google Sheets.

---

## **Installation**

Follow these steps to set up the project:

1. **Clone the Repository**  
   Clone the project repository from GitHub using the following command:

   ```
   git clone https://github.com/ritchi-e/virechana-App
   ```

2. **Navigate to the Project Directory**  
   Move into the project folder:

   ```
   cd virechana-App
   ```

3. **Install Dependencies**  
   Fetch and install all required dependencies using Flutter:

   ```
   flutter pub get
   ```

4. **Configure Google Sheets API**

   - Open the file `lib/api/virechana_sheets_api.dart`.
   - Replace the placeholders with your Google Sheets API credentials:
     - Spreadsheet ID
     - API Key

   For more details on setting up the Google Sheets API, refer to the [official guide](https://developers.google.com/sheets/api/guides/concepts).

---

## **Running the App**

To run the app on your local machine, follow these steps:

1. **Connect a Device or Start an Emulator**  
   Ensure a physical device or emulator is connected and ready for deployment.

2. **Run the Application**  
   Execute the following command in the terminal from the project directory:

   ```bash
   flutter run
   ```

   This will launch the app on the connected device or emulator.

---

## **Troubleshooting**

- If you encounter errors, verify your Flutter installation using:

  ```bash
  flutter doctor
  ```

- Ensure your Google Sheets API credentials are correctly configured.
- Refer to the [Flutter documentation](https://docs.flutter.dev/) for additional help.

---

You're now ready to use the Virechana Assessment App! If you have further questions, feel free to consult the [API Integration](api_integration.md) or [State Management](state_management.md) sections of this documentation.

```

```
