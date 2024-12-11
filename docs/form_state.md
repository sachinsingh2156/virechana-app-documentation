# **Form State Management**

This documentation explains the implementation of the `FormState` class and its role in managing the state of form data throughout the Virechana Assessment App. The state is managed using Riverpod, enabling reactive updates and centralized control of data.

---

## **Overview**

The `FormState` class:

- Manages all form data in a centralized state.
- Supports updates, resets, and management of dynamic fields such as Vega entries.
- Integrates seamlessly with the app using Riverpod's `StateNotifierProvider`.

---

## **Key Features**

**Centralized State Management**

- Holds data for all pages, including patient details, assessment metrics, and post-procedure data.
- Provides a consistent interface for accessing and updating form fields.

**Dynamic Data Handling**

- Manages dynamically generated fields like Vega entries for hourly charting.

**Real-Time State Updates**

- Allows updates to individual fields or calculated scores.
- Changes are reflected immediately across the app.

**Reset Functionality**

- Provides a method to reset all form data to default values.

**Integration with Riverpod**

- Uses `StateNotifierProvider` for state management.

---

## **Code Breakdown**

### **Class Declaration**

```
class FormState extends StateNotifier<Map<String, dynamic>> {
  FormState()
      : super({
          // Default values for form fields
          'patient_name': '',
          'uhid_no': '',
          'age': '',
          // Other fields...
          'vega_entries': [],
        });
}
```

- Inherits from `StateNotifier` to enable reactive state management.
- Initializes the state with default values.

---

### **State Management Methods**

#### **Reset Form**

Resets all form fields to their default values:

```
void resetForm() {
  state = {
    'patient_name': '',
    'uhid_no': '',
    'age': '',
    // Other fields...
    'vega_entries': [],
  };
}
```

#### **Update Field**

Updates a specific field in the form state:

```
void updateField(String key, dynamic value) {
  state = {...state, key: value};
}
```

#### **Update Score**

Updates calculated scores for specific fields:

```
void updateScore(String key, int score) {
  state = {...state, '${key}_score': score};
}
```

#### **Toggle Symptom**

Toggles the state of a checkbox or boolean field:

```
void toggleSymptom(String symptom) {
  state = {
    ...state,
    symptom: !(state[symptom] ?? false),
  };
}
```

#### **Dynamic Vega Entry Management**

**Add New Vega Entry**
Adds a new row for Vega charting:

```
void addVegaEntry() {
  state = {
    ...state,
    'vega_entries': [
      ...state['vega_entries'],
      {
        'timeController': TextEditingController(),
        'vegaController': TextEditingController(),
        'upavegaController': TextEditingController(),
        'bpSystolicController': TextEditingController(),
        'bpDiastolicController': TextEditingController(),
        'pulseController': TextEditingController(),
        'spo2Controller': TextEditingController(),
        'remarksController': TextEditingController(),
      },
    ],
  };
}
```

**Update Vega Entry Time**

Updates the time field of a specific Vega entry:

```
void updateVegaEntryTime(int index, String time) {
  final updatedVegaEntries = List.from(state['vega_entries']);
  updatedVegaEntries[index]['timeController'].text = time;

  state = {
    ...state,
    'vega_entries': updatedVegaEntries,
  };
}
```

---

### **Integration with Riverpod**

#### Form State Provider

The `formProvider` is a `StateNotifierProvider` that provides access to the `FormState` class:

```
final formProvider =
    StateNotifierProvider<FormState, Map<String, dynamic>>((ref) {
  return FormState();
});
```

#### User State Provider

Manages the `User` object:

```
final userProvider = StateProvider<User?>((ref) => null);
```

---

### **Disposal of Resources**

Ensures all `TextEditingController` instances are disposed of properly:

```
@override
void dispose() {
  state.values.whereType<TextEditingController>().forEach((controller) {
    controller.dispose();
  });
  super.dispose();
}
```

---

## **Usage**

### Accessing Form Data

To access form data:

```
final formData = ref.watch(formProvider);
```

### Updating Form Data

To update a field:

```
ref.read(formProvider.notifier).updateField('patient_name', 'John Doe');
```

### Resetting Form Data

To reset the form:

```
ref.read(formProvider.notifier).resetForm();
```

### Adding a Vega Entry

To add a new Vega entry:

```
ref.read(formProvider.notifier).addVegaEntry();
```

---

## **Conclusion**

The `FormState` class provides a robust and flexible way to manage form data in the Virechana Assessment App. Its integration with Riverpod ensures real-time updates, while its methods support dynamic data handling and efficient state management.
