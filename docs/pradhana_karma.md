# Pradhana Karma Page

The `Pradhana Karma` page collects detailed information about vital parameters, physical examinations, and Vega-related entries during the **Pradhana Karma** process. It ensures accurate data collection with proper validation and allows dynamic additions of Vega details.

---

## **Overview**

- **Purpose**: Collect key vital signs, physical examination details, and Vega entries for the Pradhana Karma process.
- **Features**:
  - Input fields for vital parameters such as temperature, pulse rate, BP, and SpO2.
  - Dynamic addition of Vega entries with time and remarks.
  - Integration with Riverpod for state management.
  - Proper input validation using input formatters.

---

## **Key Features**

1.  **Vital Parameters Collection**  
    Includes fields to collect:

         Temperature (°F)

         Pulse Rate (bpm)

         Blood Pressure (Systolic and Diastolic in mmHg)

         Respiratory Rate (breaths/min)

         Weight (kg)

         SpO2 (Oxygen saturation in %)

2.  **Dynamic Vega Entry Management**

    Provides dynamic rows for Vega details.

    Allows time selection using a time picker.

    Supports adding new Vega entry rows dynamically.

3.  **Real-Time State Updates**

    Uses Riverpod's `formProvider` to handle real-time updates to the form state.

4.  **Validation**

    Input formatters ensure only valid data is entered in numeric fields.

5.  **Navigation**

    Includes Back and Next buttons for seamless page navigation.

---

## **Code Breakdown**

### **Class Declaration**

```
class PradhanaKarmaPage extends ConsumerStatefulWidget {
  final PageController controller;

  PradhanaKarmaPage({required this.controller});

  @override
  _PradhanaKarmaPageState createState() => _PradhanaKarmaPageState();
}
```

- Inherits from `ConsumerStatefulWidget` to leverage Riverpod for state management.
- Accepts a `PageController` for navigation.

---

### **State Initialization**

```
@override
void initState() {
  super.initState();
  final formData = ref.read(formProvider);

  // Initialize controllers with the form data
  temperatureController = TextEditingController(text: formData['temperature']);
  pulseRateController = TextEditingController(text: formData['pulse_rate']);
  bpSystolicController = TextEditingController(text: formData['bp_systolic']);
  bpDiastolicController = TextEditingController(text: formData['bp_diastolic']);
  rrController = TextEditingController(text: formData['rr']);
  spo2Controller = TextEditingController(text: formData['spo2']);
  weightController = TextEditingController(text: formData['weight']);
  peController = TextEditingController(text: formData['pe']);
}
```

- Initializes text controllers with existing form data using `formProvider`.

---

### **Input Fields**

#### **Vital Parameters**

- **Temperature**:

```
LabeledTextFormField(
  label: 'Temperature (°F)',
  controller: temperatureController,
  keyboardType: TextInputType.numberWithOptions(decimal: true),
  inputFormatters: [
    FilteringTextInputFormatter.allow(RegExp(r'^\d*\.?\d*$'))
  ],
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('temperature', value);
  },
),
```

- **Pulse Rate**:

```
LabeledTextFormField(
  label: 'Pulse Rate (bpm)',
  controller: pulseRateController,
  keyboardType: TextInputType.number,
  inputFormatters: [FilteringTextInputFormatter.digitsOnly],
  onChanged: (value) {
    ref.read(formProvider.notifier).updateField('pulse_rate', value);
  },
),
```

- **Blood Pressure**:

```
Row(
  children: [
    Expanded(
      child: LabeledTextFormField(
        label: 'BP Systolic (mmHg)',
        controller: bpSystolicController,
        keyboardType: TextInputType.number,
        inputFormatters: [FilteringTextInputFormatter.digitsOnly],
        onChanged: (value) {
          ref.read(formProvider.notifier).updateField('bp_systolic', value);
        },
      ),
    ),
    SizedBox(width: 10),
    Expanded(
      child: LabeledTextFormField(
        label: 'BP Diastolic (mmHg)',
        controller: bpDiastolicController,
        keyboardType: TextInputType.number,
        inputFormatters: [FilteringTextInputFormatter.digitsOnly],
        onChanged: (value) {
          ref.read(formProvider.notifier).updateField('bp_diastolic', value);
        },
      ),
    ),
  ],
),
```

- **Respiratory Rate**, **Weight**, **SpO2**, and **Physical Examination** follow similar patterns.

---

### **Dynamic Vega Entry Management**

#### **List of Vega Entries**

```
SizedBox(
  height: 200,
  child: ListView.builder(
    itemCount: formData['vega_entries']?.length ?? 0,
    itemBuilder: (context, index) {
      final entry = formData['vega_entries'][index];
      return Row(
        children: [
          Expanded(
            child: TextFormField(
              controller: entry['timeController'],
              decoration: InputDecoration(labelText: 'Time (HH:MM)'),
              readOnly: true,
              onTap: () => _selectTime(index),
            ),
          ),
          Expanded(
            child: TextFormField(
              controller: entry['vegaController'],
              decoration: InputDecoration(labelText: 'Vega'),
            ),
          ),
          // Additional fields for Vega details...
        ],
      );
    },
  ),
),
```

- Dynamically generates rows for Vega details.
- Uses `_selectTime` to open a time picker for selecting time.

#### **Add Vega Row**

```
ElevatedButton(
  onPressed: () {
    ref.read(formProvider.notifier).addVegaEntry();
  },
  child: Text('Add Row'),
),
```

- Adds a new row dynamically for Vega details.

---

### **Navigation Buttons**

- **Back Button**:

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

- **Next Button**:

```
ElevatedButton(
  onPressed: () {
    widget.controller.nextPage(
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  },
  child: Text('Next Page'),
),
```

---

## **Conclusion**

The `Pradhana Karma` page is a crucial component of the app, allowing users to input and manage detailed information about the Pradhana Karma process. With dynamic Vega entries, proper validation, and integration with Riverpod, it ensures accurate and efficient data handling.
