# Samyak Yoga Lakshana Page

The **Samyak Yoga Lakshana Page** is designed to collect and manage data about the **Samyak Yoga Lakshana** features. It allows users to toggle multiple checkboxes dynamically and ensures that the selections are updated in real-time using Riverpod for state management.

---

## **Overview**

**Purpose**: Evaluate the presence of various **Samyak Yoga Lakshana** attributes using checkboxes.

**Features**:

- Displays a list of checkbox options for **Samyak Yoga Lakshana** attributes.
- Updates the state dynamically when a checkbox is toggled.
- Integrates with the **SamyakYogaState** for efficient state management.
- Includes navigation to the next or previous pages.

---

## **Key Features**

1. **Dynamic Checkbox List:**
   Each **Samyak Yoga Lakshana** attribute is displayed as a checkbox. Toggling a checkbox updates its value in the state.

2. **Real-Time State Management:** Uses Riverpod's `StateNotifierProvider` to manage and update checkbox states in real-time.

3. **Seamless Navigation:** Includes Back and Next buttons for navigating between pages.

4. **Responsive UI:** Ensures the layout is scrollable for smaller screens, providing a user-friendly experience.

---

## **Code Breakdown**

### **Class Declaration**

```
class SamyakYogaLakshanaPage extends ConsumerWidget {
  final PageController controller;

  SamyakYogaLakshanaPage({required this.controller});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final samyakState = ref.watch(samyakYogaProvider);
    // Rest of the code...
  }
}
```

- Inherits from `ConsumerWidget` to enable integration with Riverpod.
- Accepts a `PageController` to manage navigation between pages.

---

### **Checkbox List**

The checkboxes are generated dynamically based on the keys in the `samyakYogaProvider` state:

```
...samyakState.keys.map((option) {
  return CheckboxListTile(
    title: Text(option),
    value: samyakState[option] ?? false,
    onChanged: (bool? value) {
      ref.read(samyakYogaProvider.notifier).toggleCheckbox(option, value);
    },
  );
}).toList(),
```

- **`title`**: Displays the name of the **Samyak Yoga Lakshana** attribute.
- **`value`**: Represents the current state of the checkbox.
- **`onChanged`**: Toggles the checkbox state and updates it in the provider.

---

### **State Management**

The state is managed using Riverpod's `samyakYogaProvider`:

```
final samyakState = ref.watch(samyakYogaProvider);
```

- The `samyakYogaProvider` holds the current state of all checkboxes.
- Changes to the checkboxes are handled by the `toggleCheckbox` method in the `SamyakYogaState` class.

---

### **Navigation Buttons**

#### **Back Button**

```
IconButton(
  icon: Icon(Icons.arrow_back),
  onPressed: () {
    controller.previousPage(
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  },
),
```

- Navigates to the previous page.

#### **Next Button**

```
ElevatedButton(
  onPressed: () {
    // Update the form with individual checkbox values
    samyakState.forEach((key, value) {
      ref.read(samyakYogaProvider.notifier).updateField(key, value);
    });

    // Navigate to the next page
    controller.nextPage(
      duration: Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  },
  child: Text('Next'),
),
```

- Updates the form state with the current checkbox values.
- Navigates to the next page.

---

## **Usage**

### **State Initialization**

The initial state is defined in the `SamyakYogaState` class and includes the following attributes:

- **Srotovishuddhi**
- **Vatanululomana**
- **Ruchi**
- **Laghuta**
- **Kayagni Anuvartana**
- **Varna Shuddhi**
- **Bhuddhi Shuddhi**
- **Samprasadana**

Each attribute is set to `false` by default.

---

### **State Updates**

The state is updated dynamically when a checkbox is toggled:

```
ref.read(samyakYogaProvider.notifier).toggleCheckbox(option, value);
```

**`toggleCheckbox(String option, bool? value)`**: Toggles the checkbox state for the given attribute.

---

### **State Watching**

The `ref.watch` method ensures that the UI reflects the latest state:

```
final samyakState = ref.watch(samyakYogaProvider);
```

---

## **Conclusion**

The **Samyak Yoga Lakshana Page** provides an interactive and dynamic way to evaluate the presence of **Samyak Yoga Lakshana** attributes. By leveraging Riverpod for state management, it ensures real-time updates and a seamless user experience. This page is an essential component of the Virechana Assessment App, facilitating accurate data collection and evaluation.
