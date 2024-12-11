# Patient Details Page

The `PatientDetailsPage` is the first page in the Virechana Assessment App, where users input essential patient information such as name, age, UHID, and diagnosis details. This page also validates the input and saves the data for later use in the application.

---

## **Overview**

This page is implemented as a `ConsumerStatefulWidget` to allow dynamic updates to the form fields using the Riverpod state management library.
It collects the following patient details:

- **Patient Name**
- **UHID Number**
- **Age**
- **Sex**
- **OPD Number**
- **Diagnosis**
- **Date of Visit**

---

## **Key Features**

1. **Form Validation :**
   Ensures all fields are filled with valid input. It also provides meaningful error messages for invalid inputs.

2. **Dynamic State Management :**
   Uses Riverpod's `formProvider` to manage and update form data dynamically.

3. **Date Picker :**
   Allows users to select the date of visit using a calendar picker.

4. **Navigation :**
   Includes a `Next` button to proceed to the next page after successful validation.

---

## **Code Breakdown**

### **Class Declaration**

```
class PatientDetailsPage extends ConsumerStatefulWidget {
  final PageController controller;

  PatientDetailsPage({required this.controller});

  @override
  _PatientDetailsPageState createState() => _PatientDetailsPageState();
}
```

Inherits from `ConsumerStatefulWidget` to enable Riverpod integration.

Accepts a `PageController` to handle navigation between pages.

---

### **State Initialization**

```
class _PatientDetailsPageState extends ConsumerState<PatientDetailsPage> {
  late TextEditingController dateController;
  late TextEditingController patientNameController;
  late TextEditingController uhidController;
  late TextEditingController ageController;
  late TextEditingController opdNoController;
  late TextEditingController diagnosisController;

  String selectedSex = "Male";
  DateTime? selectedDate;

  @override
  void initState() {
    super.initState();
    final formData = ref.read(formProvider);

    dateController = TextEditingController(text: formData['date']);
    patientNameController =
        TextEditingController(text: formData['patient_name']);
    uhidController = TextEditingController(text: formData['uhid_no']);
    ageController = TextEditingController(text: formData['age']);
    opdNoController = TextEditingController(text: formData['opd_no']);
    diagnosisController = TextEditingController(text: formData['diagnosis']);
    selectedSex = formData['sex'] ?? "Male";
  }

  @override
  void dispose() {
    dateController.dispose();
    patientNameController.dispose();
    uhidController.dispose();
    ageController.dispose();
    opdNoController.dispose();
    diagnosisController.dispose();
    super.dispose();
  }
}
```

Initializes `TextEditingController` for each form field using existing data from `formProvider`.

Disposes of controllers when the widget is removed to free memory.

---

### **Form Input Fields**

#### **Patient Name**

```
LabeledTextFormField(
  label: 'Patient Name',
  controller: patientNameController,
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('patient_name', value);
  },
),
```

Collects and updates the patient's name dynamically.

#### **UHID Number**

```
LabeledTextFormField(
  label: 'UHID No',
  controller: uhidController,
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('uhid_no', value);
  },
),
```

Accepts a numeric unique hospital ID.

#### **Age**

```
LabeledTextFormField(
  label: 'Age',
  controller: ageController,
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('age', value);
  },
),
```

Validates that age is a positive integer within a reasonable range.

#### **Sex**

```
DropdownButtonFormField<String>(
  value: selectedSex,
  items: ['Male', 'Female', 'Other'].map((String value) {
    return DropdownMenuItem<String>(
      value: value,
      child: Text(value),
    );
  }).toList(),
  onChanged: (value) {
    setState(() {
      selectedSex = value!;
      ref.read(formProvider.notifier).updateField('sex', selectedSex);
    });
  },
  decoration: InputDecoration(labelText: 'Sex'),
),
```

Provides a dropdown for selecting the patient's gender.

#### **OPD Number**

```
LabeledTextFormField(
  label: 'OPD No.',
  controller: opdNoController,
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('opd_no', value);
  },
),
```

#### **Diagnosis**

```
LabeledTextFormField(
  label: 'Diagnosis',
  controller: diagnosisController,
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('diagnosis', value);
  },
),
```

Collects the diagnosis information.

---

### **Date Picker**

```
Future<void> _selectDate(BuildContext context) async {
  final DateTime? pickedDate = await showDatePicker(
    context: context,
    initialDate: DateTime.now(),
    firstDate: DateTime(1900),
    lastDate: DateTime.now(),
  );

  if (pickedDate != null && pickedDate != selectedDate) {
    setState(() {
      selectedDate = pickedDate;
    });
    ref.read(formProvider.notifier).updateField(
        'visit_date', "${pickedDate.day}/${pickedDate.month}/${pickedDate.year}");
  }
}
```

Allows users to select a date of visit using a date picker dialog.

---

### **Form Validation and Submission**

```
ElevatedButton(
  onPressed: () {
    final String patientName = patientNameController.text.trim();
    final String uhid = uhidController.text.trim();
    final String age = ageController.text.trim();
    final String opdNo = opdNoController.text.trim();
    final String diagnosis = diagnosisController.text.trim();

    if (patientName.isEmpty || !RegExp(r"^[a-zA-Z\s]+$").hasMatch(patientName)) {
      _showError(context, 'Enter a valid Patient Name (letters only).');
    } else if (uhid.isEmpty || int.tryParse(uhid) == null) {
      _showError(context, 'Enter a valid numeric UHID No.');
    } else if (age.isEmpty || int.tryParse(age) == null ||
        int.parse(age) <= 0 || int.parse(age) > 120) {
      _showError(context, 'Enter a valid Age (between 1 and 120).');
    } else if (opdNo.isEmpty || int.tryParse(opdNo) == null) {
      _showError(context, 'Enter a valid numeric OPD No.');
    } else if (diagnosis.isEmpty || diagnosis.length > 100) {
      _showError(context, 'Enter a valid Diagnosis (max 100 characters).');
    } else if (selectedDate == null) {
      _showError(context, 'Please select a Visit Date.');
    } else {
      // Save the data and navigate to the next page
      final DateFormat dateFormat = DateFormat('dd/MM/yyyy');
      final formattedDate = dateFormat.format(selectedDate!);

      ref.read(formProvider.notifier).updateField('visit_date', formattedDate);
      ref.read(formProvider.notifier).updateField('patient_name', patientName);
      ref.read(formProvider.notifier).updateField('uhid_no', uhid);
      ref.read(formProvider.notifier).updateField('age', age);
      ref.read(formProvider.notifier).updateField('opd_no', opdNo);
      ref.read(formProvider.notifier).updateField('diagnosis', diagnosis);
      ref.read(formProvider.notifier).updateField('sex', selectedSex);

      widget.controller.nextPage(
        duration: Duration(milliseconds: 300),
        curve: Curves.easeInOut,
      );
    }
  },
  child: Text('Next'),
),
```

Validates the form inputs and displays error messages for invalid data.

Updates the form state and navigates to the next page.

---

## **Conclusion**

The `PatientDetailsPage` ensures that patient data is collected accurately and stored dynamically in the state. The page is interactive and user-friendly, with proper validations and error handling to ensure the integrity of the input data.
