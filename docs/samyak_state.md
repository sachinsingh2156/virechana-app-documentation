# Samyak Yoga State Management

The **SamyakYogaState** class is responsible for managing the state of the checkboxes on the **Samyak Yoga** page. This state management solution is built using Riverpod's `StateNotifier` and ensures efficient and dynamic updates to the state.

---

## **Overview**

- **Purpose**: Track the state of multiple checkboxes related to Samyak Yoga features such as **Srotovishuddhi**, **Vatanululomana**, **Ruchi**, and more.
- **Features**:
  - Initial state setup with default values.
  - Methods to reset, update, and toggle individual checkbox states.
  - Integrated with Riverpod to allow real-time state updates in the UI.

---

## **Key Features**

1.  **Initial State Management**: Initializes the state with all checkboxes set to `false`.It also includes the following fields:

        Srotovishuddhi
        Vatanululomana
        Ruchi
        Laghuta
        Kayagni Anuvartana
        Varna Shuddhi
        Bhuddhi Shuddhi
        Samprasadana

2.  **State Manipulation Methods**

    - **`resetState()`**: Resets all checkboxes to their initial `false` state.
    - **`updateField(String key, dynamic value)`**: Updates the value of a specific checkbox field.
    - **`toggleCheckbox(String option, bool? value)`**: Toggles the state of a specific checkbox based on the provided value.

3.  **Riverpod Integration :** Uses `StateNotifierProvider` to expose the state to the UI. It also allows real-time updates and dynamic state management.

---

## **Code Breakdown**

### **Class Declaration**

```
class SamyakYogaState extends StateNotifier<Map<String, bool>> {
  SamyakYogaState()
      : super({
          'Srotovishuddhi': false,
          'vatanululomana': false,
          'ruchi': false,
          'laghuta': false,
          'kayagni anuvartana': false,
          'varna shuddhi': false,
          'bhuddhi shuddhi': false,
          'samprasadana': false,
        });
}
```

**Inherits** from `StateNotifier<Map<String, bool>>`.

Initializes the state with default values for all checkboxes.

---

### **State Reset Method**

```
void resetState() {
  state = {
    'Srotovishuddhi': false,
    'vatanululomana': false,
    'ruchi': false,
    'laghuta': false,
    'kayagni anuvartana': false,
    'varna shuddhi': false,
    'bhuddhi shuddhi': false,
    'samprasadana': false,
  };
}
```

- Resets all fields to their default state (`false`).

---

### **State Update Method**

```
void updateField(String key, dynamic value) {
  state = {...state, key: value};
}
```

- Updates the value of a specific field in the state.
- Ensures immutability by creating a new state map using the spread operator.

---

### **Checkbox Toggle Method**

```
void toggleCheckbox(String option, bool? value) {
  state = {
    ...state,
    option: value ?? false, // Toggle the current state of the checkbox
  };
}
```

- Toggles the checkbox state for a specific field.
- If the `value` is `null`, the field defaults to `false`.

---

### **Riverpod Provider**

```
final samyakYogaProvider = StateNotifierProvider<SamyakYogaState, Map<String, bool?>>(
  (ref) => SamyakYogaState(),
);
```

- Creates a provider to expose the **SamyakYogaState** to the app.
- Allows the UI to subscribe to state changes and trigger updates dynamically.

---

## **Usage**

### **Accessing the State**

```
final samyakYogaState = ref.watch(samyakYogaProvider);
```

- Use `ref.watch` to read the current state.

### **Updating the State**

```
ref.read(samyakYogaProvider.notifier).updateField('ruchi', true);
```

- Updates the value of the **Ruchi** checkbox to `true`.

### **Toggling a Checkbox**

```
ref.read(samyakYogaProvider.notifier).toggleCheckbox('vatanululomana', true);
```

- Toggles the state of the **Vatanululomana** checkbox.

### **Resetting the State**

```
ref.read(samyakYogaProvider.notifier).resetState();
```

- Resets all checkbox fields to their default values.

---

## **Conclusion**

The **SamyakYogaState** provides a robust and efficient way to manage the state of checkboxes on the **Samyak Yoga** page. By leveraging Riverpod and `StateNotifier`, this implementation ensures real-time updates, state immutability, and seamless integration with the UI.
