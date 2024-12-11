# Folder Structure

This document provides an overview of the folder structure used in the Virechana Assessment App. Each folder and file is described to help you understand its purpose within the application.

## **Project Directory**

The root directory of the project contains the following:

```

virechana-App/
├── .dart_tool/ # Flutter's internal tools and build cache
├── .idea/ # Project metadata for JetBrains IDEs (e.g., IntelliJ, Android Studio)
├── android/ # Android-specific files and configuration
├── build/ # Generated build files
├── code-documentation/ # MkDocs-based project documentation
├── ios/ # iOS-specific files and configuration
├── lib/ # Main source code of the app
├── linux/ # Linux-specific files (optional for Flutter desktop apps)
├── macos/ # macOS-specific files (optional for Flutter desktop apps)
├── test/ # Unit and widget test files
├── web/ # Web-specific files (for Flutter web apps)
├── windows/ # Windows-specific files (optional for Flutter desktop apps)
├── pubspec.yaml # Flutter project configuration file
└── README.md # Project description and usage guide

```

---

## **Source Code Structure**

The `lib/` folder contains the primary codebase for the app:

```

lib/
├── api/ # Handles API integrations
│ └── virechana_sheets_api.dart # Google Sheets API integration
├── model/ # Contains app-specific data models
│ └── user.dart # User data model
├── screens/ # Contains individual screens of the app
│ ├── page1_patient_details.dart
│ ├── page2_purvakarma.dart
│ ├── page3_pradhana_karma.dart
│ ├── page4_shuddhi_assessment.dart
│ ├── page5_samyak.dart
│ ├── page6_ayoga.dart
│ ├── page7_atiyoga.dart
│ ├── page8_post_procedure.dart
│ └── page9_summary.dart
├── state/ # Manages application state
│ ├── form_state.dart
│ ├── samyak_state.dart
│ ├── ayoga_state.dart
│ └── atiyoga_state.dart
├── widgets/ # Reusable widgets for UI components
│ └── form_widgets.dart
└── main.dart # Entry point of the application

```

---

## **Detailed Descriptions**

### **`api/`**

- **Purpose**: Contains logic for API interactions.
- **File**: `virechana_sheets_api.dart` handles the integration with Google Sheets for storing form data.

### **`model/`**

- **Purpose**: Defines data models used in the app.
- **File**: `user.dart` represents the structure of a user's data.

### **`screens/`**

- **Purpose**: Contains the UI and logic for each individual screen.
- **Key Files**:
  - `page1_patient_details.dart`: Form for patient details.
  - `page2_purvakarma.dart`: Form for Purvakarma assessment.
  - `page3_pradhana_karma.dart`: Tracks vitals during Pradhana Karma.
  - `page4_shuddhi_assessment.dart`: Shuddhi Assesments sections.
  - `page5_samyaka.dart`: Samyak Yoga Lakshana Assessment.
  - `page6_ayoga.dart`: Ayoga of Virechana Assessment.
  - `page7_atiyoga.dart`: Atiyoga of Virechana Assessment.
  - `page6_post_procedure.dart`: Post Procedure Assessment Details.
  - `page6_summary.dart`: Summary of Assessment.

### **`state/`**

- **Purpose**: Manages app-wide and screen-specific states.
- **Key Files**:
  - `form_state.dart`: Global state for form management.
  - `samyak_state.dart`: State management for the Samyak screen.
  - `Ayoga_state.dart`: State management for the Ayoga screen.
  - `Atiyoga_state.dart`: State management for the Atiyoga screen.

### **`widgets/`**

- **Purpose**: Houses reusable UI components.
- **File**: `form_widgets.dart` contains shared widgets like dropdowns, input fields, etc.

### **`main.dart`**

**Purpose**: Entry point of the app.

**Functionality**:

- Initializes the app.
- Configures routing and theme.

This folder structure ensures the app is modular, easy to maintain, and scalable for future enhancements.
