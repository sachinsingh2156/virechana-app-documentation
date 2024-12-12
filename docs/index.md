# Welcome to the Virechana Karma Assessment App

## Overview

The **Virechana Karma Assessment App** is a comprehensive tool designed for the documentation and assessment of Virechana Karma procedures. This application streamlines the process of recording patient details, conducting evaluations, and documenting post-procedure observations. Integrated with Google Sheets, it ensures efficient data storage and accessibility.

---

## Purpose

The primary objective of this app is to:

- Facilitate seamless data collection during the Virechana Karma procedure.
- Standardize the evaluation process with structured forms.
- Store data securely and accessibly in Google Sheets for further analysis and record-keeping.

---

## Key Features

### **1. Sequential Navigation**

The app ensures a guided workflow by organizing the assessment process into multiple pages. Each page focuses on a specific step of the procedure:

- **Patient Details**: Collect basic information about the patient.
- **Purvakarma**: Record pre-procedure metrics.
- **Pradhana Karma**: Document key procedure details.
- **Shuddhi Assessment**: Evaluate the effectiveness of the procedure.
- **Samyak Yoga Lakshana**: Record observations for `Samyak Yoga`.
- **Ayoga**: List symptoms indicating incomplete Virechana.
- **Atiyoga**: Document excessive Virechana symptoms.
- **Post-Procedure**: Record post-procedure observations.
- **Summary**: Review all collected data and submit it to Google Sheets.

### **2. Data Integration with Google Sheets**

The app leverages the Google Sheets API for:

- Secure data storage.
- Easy access to patient records for further analysis.
- Reliable backups and efficient record management.

### **3. User-Friendly Interface**

- Clean and intuitive navigation.
- Dropdowns, checkboxes, and text fields tailored for specific inputs.
- Dynamic forms, such as Vega entries, for flexible data recording.

### **4. State Management with Riverpod**

- Efficient handling of form states and user interactions.
- Real-time updates across pages for a seamless experience.

### **5. Validation and Error Handling**

- Ensures accuracy with input validations (e.g., numeric fields, required fields).
- Prevents data loss with warnings and validation checks.

---

## How It Works

**Initialization**

- The app initializes the Google Sheets API and prepares the environment for data collection.

**Sequential Assessment**

- The user is guided through structured steps, ensuring all relevant data is captured.

**Data Submission**

- At the end of the assessment, the collected data is submitted to Google Sheets.
- Dynamic Vega entries and assessment scores are calculated and stored efficiently.

**State Reset**

- After submission, the form resets for the next assessment.

---

## Workflow Overview

**Patient Details**  
 Record the patient's name, age, diagnosis, and other basic information.

**Pre-Procedure Metrics (Purvakarma)**  
 Evaluate the patient's bowel habits, consistency, urgency, and related metrics.

**Procedure Details (Pradhana Karma)**  
 Document key observations such as temperature, pulse rate, BP, and respiratory rate.

**Shuddhi Assessment**  
 Assess the effectiveness of the procedure with classification into `Avara`, `Madhyama`, or `Pravara Shuddhi`.

**Symptom Tracking**

- **Samyak Yoga Lakshana**: Record observations for proper Virechana outcomes.
- **Ayoga Symptoms**: Note signs of incomplete Virechana.
- **Atiyoga Symptoms**: Identify excessive Virechana outcomes.

**Post-Procedure Observations**  
 Document post-procedure metrics like weight, temperature, and complications.

**Summary and Submission**  
 Review all collected data and submit it to Google Sheets.

---

## Getting Started

To start using the app:

1. Install Flutter and the required dependencies.
2. Clone the project repository.
3. Initialize the app with your Google Sheets credentials.
4. Run the app on your preferred device.

For detailed setup instructions, refer to the [Getting Started](getting_started.md) page.

---

## Additional Resources

Explore the following sections for more information:

- [Folder Structure](folder_structure.md): Understand the organization of the project files.
- [API Integration](api_integration.md): Learn about the Google Sheets API integration.

---

## Conclusion

The **Virechana Karma Assessment App** is a robust and efficient solution for standardizing the Virechana procedure documentation. By integrating cutting-edge technologies, it ensures accuracy, reliability, and ease of use.

## **Contacts**

Created by <a href="mailto:sumitk@iitj.ac.in">Dr. Sumit Kalra</a>,
<a href="mailto:m24cse033@iitj.ac.in">Sachin Singh</a>,
<a href="mailto:m24cse030@iitj.ac.in">Richard David</a>. &copy; 2024.
