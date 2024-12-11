# Ayoga of Virechna Page

The **Ayoga of Virechna Page** allows users to record symptoms of insufficient cleansing (Ayoga) dynamically through checkboxes. This page is an integral part of the Virechana Assessment App, facilitating accurate data collection about the patient's condition.

---

## **Overview**

- **Purpose**: Collect symptoms associated with **Ayoga of Virechna** (incomplete cleansing) using checkboxes.
- **Features**:

        Dynamically generates checkboxes for Ayoga symptoms.
        Real-time state management using Riverpod.
        Collects selected symptoms and stores them for further evaluation.
        Provides navigation between pages.

---

## **Key Features**

1. **Dynamic Checkbox List:** Each checkbox corresponds to an **Ayoga of Virechna** symptom. The list is dynamically generated from the **AyogaState**.

2. **Real-Time State Management:** Uses Riverpod's `StateNotifierProvider` to manage checkbox states. Updates the state dynamically when a checkbox is toggled.

3. **Symptom Collection:** Collects selected symptoms and stores them in the form state.

4. **Seamless Navigation:** Includes navigation buttons to move between pages.

5. **Responsive Design:** Ensures proper layout and scrolling for all screen sizes.

---

## **Code Breakdown**

### **Class Declaration**

```
class AyogaOfVirechnaPage extends ConsumerWidget {
  final PageController controller;

  AyogaOfVirechnaPage({required this.controller});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final ayogaState = ref.watch(ayogaProvider);
    // Rest of the code...
  }
}
```

- Inherits from `ConsumerWidget` to enable Riverpod integration.
- Accepts a `PageController` to manage navigation.

---

### **Checkbox List**

Checkboxes are dynamically generated based on the keys in the `ayogaProvider` state:

```
...ayogaState.keys.map((option) {
  return CheckboxListTile(
    title: Text(option),
    value: ayogaState[option] ?? false,
    onChanged: (bool? value) {
      ref.read(ayogaProvider.notifier).toggleCheckbox(option, value);
    },
  );
}).toList(),
```

- **`title`**: Displays the name of the symptom.
- **`value`**: Represents the current state of the checkbox.
- **`onChanged`**: Toggles the checkbox state and updates it in the `ayogaProvider`.

---

### **State Management**

The state is managed using Riverpod's `ayogaProvider`:

```
final ayogaState = ref.watch(ayogaProvider);
```

- The `ayogaProvider` holds the current state of all checkboxes.
- Changes to the checkboxes are handled by the `toggleCheckbox` method in the `AyogaState` class.

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
    ayogaState.forEach((key, value) {
      ref.read(ayogaProvider.notifier).updateField(key, value);
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

The initial state is defined in the `AyogaState` class and includes the following symptoms:

- **Pratiloma Gati Dosha Srava**
- **Glani**
- **Hridya Ashuddhi**
- **Kale Apravartan**
- **Kshtheevana**
- **Tandra**
- **Marutasya Nigraha**
- **Paridaha**
- **Bhrama**
- **Gatreshu Bhramana**

Each symptom is set to `false` by default.

---

### **State Updates**

The state is updated dynamically when a checkbox is toggled:

```
ref.read(ayogaProvider.notifier).toggleCheckbox(option, value);
```

- **`toggleCheckbox(String option, bool? value)`**: Toggles the checkbox state for the given symptom.

---

### **State Watching**

The `ref.watch` method ensures that the UI reflects the latest state:

```
final ayogaState = ref.watch(ayogaProvider);
```

---

## **Conclusion**

The **Ayoga of Virechna Page** provides a dynamic and efficient way to collect data about Ayoga symptoms. By leveraging Riverpod for state management, it ensures real-time updates and seamless navigation. This page is essential for evaluating the completeness of the cleansing process in the Virechana Assessment App.
