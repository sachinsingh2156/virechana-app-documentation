# Post Procedure Page

The **Post Procedure Page** is a key component of the Virechana Assessment App, designed to collect data about the patient's condition post-procedure. It provides input fields for various metrics such as temperature, pulse rate, blood pressure, respiratory rate, weight, and complications.

---

## **Overview**

**Purpose**: To record and manage post-procedure metrics for patients.

**Features**:

- Input fields for key health parameters.
- Real-time state updates using Riverpod.
- Validations for numeric input formats.
- Easy navigation between pages.

---

## **Key Features**

**Input Fields:** Provides input fields for:

- **Temperature (°F)**
- **Pulse Rate (bpm)**
- **Blood Pressure (Systolic/Diastolic in mmHg)**
- **Respiratory Rate (breaths/min)**
- **Weight (kg)**
- **Complications (if any)**

**Real-Time State Updates**

- Uses Riverpod's `StateNotifier` to update the app's state as the user inputs data.

**Validation**

- Ensures inputs are in valid formats using `TextInputFormatter`:
- Allows only numeric or decimal inputs where applicable.
- Restricts inputs to valid characters for each field.

**Seamless Navigation**

- Includes a **Back** button to navigate to the previous page.
- Includes a **Next** button to navigate to the next page.

**Responsive Design**

- Layout adjusts to different screen sizes and provides a scrollable interface for smaller devices.

---

## **Code Breakdown**

### **Class Declaration**

```
class PostProcedurePage extends ConsumerStatefulWidget {
  final PageController controller;

  PostProcedurePage({required this.controller});

  @override
  _PostProcedurePageState createState() => _PostProcedurePageState();
}
```

- The page is implemented as a `ConsumerStatefulWidget` to manage UI state dynamically.
- Accepts a `PageController` for managing navigation between pages.

---

### **State Initialization**

The `initState` method initializes the text controllers with data from the form state:

```
@override
void initState() {
  super.initState();
  final formData = ref.read(formProvider);

  temperatureController = TextEditingController(text: formData['post_procedural_temp']);
  pulseRateController = TextEditingController(text: formData['post_procedural_pulse']);
  bpSystolicController = TextEditingController(text: formData['post_procedural_bp_systolic']);
  bpDiastolicController = TextEditingController(text: formData['post_procedural_bp_diastolic']);
  respRateController = TextEditingController(text: formData['post_procedural_resp']);
  weightController = TextEditingController(text: formData['post_procedural_weight']);
  complicationsController = TextEditingController(text: formData['post_procedural_complications']);
}
```

- Initializes the text controllers with the existing data from the `formProvider`.

---

### **Input Fields**

Each input field is created using the `LabeledTextFormField` widget for consistency and ease of use.

#### Example: Temperature Field

```
LabeledTextFormField(
  label: 'Temperature (°F)',
  controller: temperatureController,
  keyboardType: TextInputType.numberWithOptions(decimal: true),
  inputFormatters: [
    FilteringTextInputFormatter.allow(RegExp(r'^\d*\.?\d*$'))
  ],
  onChanged: (value) => ref
      .read(formProvider.notifier)
      .updateField('post_procedural_temp', value),
),
```

- **`label`**: Describes the field.
- **`controller`**: Binds the text field to the state.
- **`keyboardType`**: Specifies the input type (numeric or decimal).
- **`inputFormatters`**: Ensures valid input (e.g., numeric only).
- **`onChanged`**: Updates the app state whenever the field value changes.

---

### **Navigation Buttons**

#### Back Button

```
IconButton(
  icon: Icon(Icons.arrow_back),
  onPressed: () {
    widget.controller.previousPage(
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  },
),
```

- Navigates to the previous page.

#### Next Button

```
ElevatedButton(
  onPressed: () {
    widget.controller.nextPage(
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  },
  child: Text('Next'),
),
```

- Navigates to the next page.

---

## **Usage**

### **State Updates**

The app state is updated in real-time whenever a field value changes:

```
ref
  .read(formProvider.notifier)
  .updateField('post_procedural_temp', value);
```

### **Input Validations**

Validations ensure only valid data is entered into the input fields:

- **Temperature** and **Weight**: Allow numeric inputs, including decimals.
- **Pulse Rate**, **Blood Pressure**, and **Respiratory Rate**: Allow only integer values.

---

## **Conclusion**

The **Post Procedure Page** provides an intuitive interface for recording post-procedure metrics. With its real-time state management, input validations, and seamless navigation, it plays a crucial role in ensuring accurate and reliable data collection within the Virechana Assessment App.
