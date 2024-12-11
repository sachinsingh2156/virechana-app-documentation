# Atiyoga of Virechana Page

The **Atiyoga of Virechana Page** is a user-friendly interface designed to record symptoms of excessive cleansing (**Atiyoga**) dynamically. It allows users to select symptoms via checkboxes and stores the data for further evaluation. This page integrates seamlessly with the app’s state management system to provide real-time updates and dynamic UI.

---

## **Overview**

**Purpose**: To collect and manage symptoms of **Atiyoga of Virechana** (excessive cleansing).
**Features**:

- Dynamically generated checkboxes for symptoms.
- Integration with Riverpod for real-time state management.
- Navigation controls to move between pages.
- Responsive design for all screen sizes.

---

## **Key Features**

**Dynamic Checkbox List**

- Checkboxes for all **Atiyoga symptoms** are dynamically generated.
- The list is based on the state provided by the `atiyogaProvider`.

**Real-Time State Management**

- Uses Riverpod's `StateNotifierProvider` to manage and update checkbox states.
- Ensures all changes are reflected immediately in the UI.

**Symptom Data Collection**

- Records user inputs for each checkbox and stores the selected symptoms in the app state.

**Seamless Navigation**

- Includes **Back** and **Next** buttons for moving between pages.

**Responsive Design**

- Ensures proper layout and scrolling for all screen sizes.

---

## **Code Breakdown**

### **Class Declaration**

```
class AtiyogaOfVirechanaPage extends ConsumerWidget {
  final PageController controller;

  AtiyogaOfVirechanaPage({required this.controller});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final atiyodaState = ref.watch(atiyogaProvider);
    // Rest of the code...
  }
}
```

- **Inherits** from `ConsumerWidget` to integrate with Riverpod.
- Accepts a `PageController` for managing navigation between pages.

---

### **Dynamic Checkbox List**

The checkboxes are generated dynamically using the keys from the `atiyogaProvider` state:

```
...atiyodaState.keys.map((option) {
  return CheckboxListTile(
    title: Text(option),
    value: atiyodaState[option] ?? false,
    onChanged: (bool? value) {
      ref.read(atiyogaProvider.notifier).toggleCheckbox(option, value);
    },
  );
}).toList(),
```

- **`title`**: Displays the symptom name.
- **`value`**: Represents the current state of the checkbox.
- **`onChanged`**: Updates the state when the checkbox is toggled.

---

### **State Management**

The state is managed using Riverpod's `atiyogaProvider`:

```
final atiyodaState = ref.watch(atiyogaProvider);
```

- Watches the state of all checkboxes.
- Changes are handled by the `toggleCheckbox` method in the `AtiyogaState` class.

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
    atiyodaState.forEach((key, value) {
      ref.read(atiyogaProvider.notifier).updateField(key, value);
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

The state is initialized in the `AtiyogaState` class with the following symptoms set to `false` by default:

- **Medomamsa Udakaopmam**
- **Angamarda**
- **Jarjaribhava**
- **Klama / Balabhava**
- **Vepana**
- **Tamah Pravesha**
- **Hikka**
- **Guda Bhramsha / Nissarana**
- **Netra Pravesha**
- **Parikartika**
- **Chimchimayan**
- **Parshva Shoola**
- **Shoonyata**

---

### **State Updates**

The state is updated dynamically when a checkbox is toggled:

```
ref.read(atiyogaProvider.notifier).toggleCheckbox(option, value);
```

### **State Watching**

The state is watched using the `ref.watch` method to ensure the UI reflects the latest state:

```
final atiyodaState = ref.watch(atiyogaProvider);
```

---

## **Conclusion**

The **Atiyoga of Virechana Page** is a critical part of the Virechana Assessment App. It enables dynamic and real-time data collection for **Atiyoga symptoms**, ensuring accurate evaluation. The integration with Riverpod ensures seamless state management, providing a responsive and user-friendly experience.
