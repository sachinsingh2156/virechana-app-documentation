# Atiyoga State Management

The **AtiyogaState** class manages the state of the checkboxes for the **Atiyoga of Virechana** page. It uses Riverpod's `StateNotifier` for state management, allowing efficient and dynamic updates to the checkbox states in the application.

---

## **Overview**

- **Purpose**: To manage the state of checkboxes for the symptoms related to **Atiyoga of Virechana**.
- **Features**:

        Initializes checkbox states with default values.
        Provides methods to reset, update, and toggle individual checkbox states.
        Integrated with Riverpod for seamless state management.

---

## **Key Features**

**Initial State Management:** Initializes all symptoms related to **Atiyoga** with a default value of `false`.

List of symptoms managed:

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

**Reset State:** Resets all symptoms' states to their default (`false`).

**Update Individual Fields:** Updates the state of a specific checkbox dynamically.

**Toggle Checkbox State:** Toggles the state of a specific checkbox.

**Integration with Riverpod:** Exposes the state using a `StateNotifierProvider` for easy integration with the UI.

---

## **Code Breakdown**

### **Class Declaration**

```

class AtiyogaState extends StateNotifier<Map<String, bool>> {
AtiyogaState()
: super({
'Medomamsa udakaopmam': false,
'Angamarda': false,
'Jarjaribhava': false,
'Klama / Balabhava': false,
'Vepana': false,
'Tamah Pravesha': false,
'Hikka': false,
'Guda Bhramsha / nissarana': false,
'Netra Pravesha': false,
'Parikartika': false,
'Chimchimayan': false,
'Parshva Shoola': false,
'Shoonyata': false,
});
}

```

- **Inherits** from `StateNotifier<Map<String, bool>>`.
- Initializes the state with the default values for all symptoms.

---

### **Reset State Method**

```

void resetState() {
state = {
'Medomamsa udakaopmam': false,
'Angamarda': false,
'Jarjaribhava': false,
'Klama / Balabhava': false,
'Vepana': false,
'Tamah Pravesha': false,
'Hikka': false,
'Guda Bhramsha / nissarana': false,
'Netra Pravesha': false,
'Parikartika': false,
'Chimchimayan': false,
'Parshva Shoola': false,
'Shoonyata': false,
};
}

```

- Resets all symptoms' states to `false`.

---

### **Update Individual Fields**

```

void updateField(String key, dynamic value) {
state = {...state, key: value};
}

```

- Updates the state of a specific checkbox field.
- Ensures immutability by creating a new state map using the spread operator.

---

### **Toggle Checkbox State**

```

void toggleCheckbox(String option, bool? value) {
state = {
...state,
option: value ?? false, // Toggle the current state of the checkbox
};
}

```

- Toggles the state of the checkbox for the given symptom.
- If the value is `null`, it defaults to `false`.

---

### **Provider for State Management**

```

final atiyogaProvider = StateNotifierProvider<AtiyogaState, Map<String, bool?>>(
(ref) => AtiyogaState(),
);

```

- Creates a provider to expose the **AtiyogaState** to the app.
- Allows the UI to subscribe to state changes and trigger updates dynamically.

---

## **Usage**

### **Accessing the State**

```

final atiyogaState = ref.watch(atiyogaProvider);

```

- Use `ref.watch` to read the current state of the checkboxes.

### **Updating the State**

```

ref.read(atiyogaProvider.notifier).updateField('Angamarda', true);

```

- Updates the state of the **Angamarda** checkbox to `true`.

### **Toggling a Checkbox**

```

ref.read(atiyogaProvider.notifier).toggleCheckbox('Vepana', true);

```

- Toggles the checkbox for **Vepana** to `true`.

### **Resetting the State**

```

ref.read(atiyogaProvider.notifier).resetState();

```

- Resets all checkbox fields to their default values.

---

## **Conclusion**

The **AtiyogaState** class provides a robust and efficient way to manage the checkbox states for the **Atiyoga of Virechana** page. By leveraging Riverpod's `StateNotifier`, it ensures real-time updates, state immutability, and seamless integration with the UI. This implementation is a vital component of the Virechana Assessment App, helping to accurately track and evaluate Atiyoga symptoms.

```

```
