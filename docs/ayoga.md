# Ayoga of Virechna Page

The **Ayoga of Virechna Page** is a dynamic and interactive screen designed to collect and manage symptoms associated with insufficient cleansing (**Ayoga**). This page allows users to toggle checkboxes corresponding to various symptoms, stores the data in the app's state, and facilitates navigation.

---

## **Overview**

**Purpose**: To collect data about the presence of **Ayoga of Virechna** symptoms using checkboxes.
**Features**:

    Dynamically generated checkboxes for each symptom.
    Integration with Riverpod for real-time state updates.
    Navigation controls to move between pages.
    Responsive design for all screen sizes.

---

## **Key Features**

1. **Dynamic Checkbox Generation:** Checkboxes are generated dynamically based on the state managed by the `ayogaProvider`.

2. **Real-Time State Management:** Uses Riverpod's `StateNotifierProvider` to manage checkbox states. Updates the state instantly when a checkbox is toggled.

3. **Symptom Data Collection:** Collects user inputs and stores the selected symptoms for further evaluation.

4. **Seamless Navigation:** Includes navigation buttons for moving to the next or previous pages.

5. **Responsive UI:** Ensures proper layout and scrolling on smaller screens.

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

- Inherits from `ConsumerWidget` to integrate with Riverpod.
- Accepts a `PageController` for handling navigation.

---

### **Dynamic Checkbox List**

The checkboxes are generated dynamically using the keys from the `ayogaState`:

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

- **`title`**: Displays the symptom name.
- **`value`**: Represents the current state of the checkbox.
- **`onChanged`**: Updates the state when the checkbox is toggled.

---

### **State Management**

The state is managed using Riverpod's `ayogaProvider`:

```
final ayogaState = ref.watch(ayogaProvider);
```

- Watches the state of all checkboxes.
- Changes are handled by the `toggleCheckbox` method in the `AyogaState` class.

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

#### **Next Button**

```
ElevatedButton(
  onPressed: () {
    ayogaState.forEach((key, value) {
      ref.read(ayogaProvider.notifier).updateField(key, value);
    });

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

The initial state is defined in the `AyogaState` class, including the following symptoms:

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

### **State Watching**

The state is watched using the `ref.watch` method to ensure the UI reflects the current state:

```
final ayogaState = ref.watch(ayogaProvider);
```

---

## **Conclusion**

The **Ayoga of Virechna Page** provides a flexible and efficient way to collect and manage data about Ayoga symptoms. By leveraging Riverpod for state management, it ensures seamless updates and a responsive user experience. This page is a crucial component of the Virechana Assessment App, aiding in the evaluation of incomplete cleansing.
