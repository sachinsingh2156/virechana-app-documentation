# Purvakarma Assessment Page

The `PurvakarmaPage` collects and assesses data about the **Purvakarma** process, specifically focusing on the evaluation of **Koshta** through a series of dropdown fields with scores. It calculates a total score dynamically and classifies the Koshta based on predefined thresholds.

## **Overview**

**Purpose**: To assess Koshta (digestive strength and bowel habits) based on various criteria such as frequency, consistency, urgency, experience, and Snigdha Lakshana.

**Features**:

Dropdowns for each assessment criterion with predefined scores.

Dynamic total score calculation based on selected options.

Koshta classification based on the total score.

Navigation buttons to move between pages.

## Key Features

1. **Dynamic Dropdown Fields**  
   Each dropdown represents an assessment criterion, allowing users to select an option with an associated score.  
   Updates the state dynamically when an option is selected.

2. **Total Score Calculation**  
   Automatically calculates the total score based on selected dropdown options.

3. **Koshta Classification**  
   Classifies Koshta into **Krura**, **Madhyama**, or **Mridu** based on the total score.

4. **Responsive Design**  
   Adapts to different screen sizes using `MediaQuery` for consistent UI.

5. **Navigation**  
   Back and Next buttons for seamless navigation between pages.

## **Code Breakdown**

### **Class Declaration**

```
class PurvakarmaPage extends ConsumerStatefulWidget {
  final PageController controller;

  PurvakarmaPage({required this.controller});

  @override
  _PurvakarmaPageState createState() => _PurvakarmaPageState();
}
```

Inherits from `ConsumerStatefulWidget` to enable integration with Riverpod for state management.
Accepts a `PageController` to handle navigation between pages.

---

### **Dropdown Options**

Dropdown options are predefined for each assessment criterion, with associated labels and scores:

```
final dropdownOptions = {
  'frequency_per_day': [
    {'label': 'Less than one', 'score': 1},
    {'label': 'Once/twice', 'score': 2},
    {'label': 'More than 2', 'score': 3},
  ],
  'consistency': [
    {'label': 'Hard stool', 'score': 1},
    {'label': 'Soft well-formed', 'score': 2},
    {'label': 'Loose/watery', 'score': 3},
  ],
  'urgency': [
    {'label': 'No urgency', 'score': 1},
    {'label': 'Moderate', 'score': 2},
    {'label': 'Marked urgency', 'score': 3},
  ],
  'experience': [
    {'label': 'No change in bowel', 'score': 1},
    {'label': 'Normal stool', 'score': 2},
    {'label': 'Watery stool', 'score': 3},
  ],
  'samyak_snigdha': [
    {'label': 'More than 6 days', 'score': 3},
    {'label': '4-5 days', 'score': 2},
    {'label': 'Less than 3 days', 'score': 1},
  ],
};
```

These options are used to generate dropdown fields dynamically.

---

### **Dropdown Implementation**

```
...dropdownOptions.entries.map((entry) {
  final key = entry.key;
  final options = entry.value;

  return Padding(
    padding: EdgeInsets.symmetric(vertical: screenHeight * 0.01),
    child: DropdownButtonFormField<Map<String, dynamic>>(
      decoration: InputDecoration(
        labelText: key.replaceAll('_', ' ').capitalize(),
        border: OutlineInputBorder(),
      ),
      value: options.firstWhereOrNull(
        (option) => option['label'] == formData[key],
      ),
      items: options
          .map((option) => DropdownMenuItem<Map<String, dynamic>>(
                value: option,
                child: Text(
                    '${option['label']} (Score: ${option['score']})'),
              ))
          .toList(),
      onChanged: (value) {
        if (value != null) {
          ref.read(formProvider.notifier).updateField(key, value['label']);
          ref.read(formProvider.notifier).updateScore(key, value['score']);
          _updateTotalScore();
        }
      },
    ),
  );
}).toList(),
```

Dynamically creates dropdown fields for all criteria.

Updates the selected value and score in the `formProvider` state.

---

### **Total Score Calculation**

```
void _updateTotalScore() {
  final formData = ref.read(formProvider);
  final totalScore = formData['frequency_per_day_score'] +
      formData['consistency_score'] +
      formData['urgency_score'] +
      formData['experience_score'] +
      formData['samyak_snigdha_score'];

  ref.read(formProvider.notifier).updateField('Koshta_total_score', totalScore);
}
```

Calculates the sum of all selected scores and updates the total score in the form state.

---

### **Koshta Classification**

```
Text(
  'Koshtha Classification:',
  style: TextStyle(
    fontSize: screenWidth * 0.045,
    fontWeight: FontWeight.bold,
  ),
),
Text(
  '(1-5) Krura koshta\n'
  '(6-10) Madhyama koshta\n'
  '(11-15) Mridu koshta',
  style: TextStyle(fontSize: screenWidth * 0.04),
),
```

Displays the classification criteria for Koshta based on the total score.

---

### **Navigation Buttons**

#### **Back Button**

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

#### **Next Button**

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

Allows navigation between pages with smooth animations.

---

### **Extensions**

#### **String Capitalization**

```
extension StringExtension on String {
  String capitalize() {
    return "${this[0].toUpperCase()}${this.substring(1)}";
  }
}
```

#### **Find First Element or Null**

```
extension ListFirstWhereOrNull<E> on List<E> {
  E? firstWhereOrNull(bool Function(E element) test) {
    for (var element in this) {
      if (test(element)) return element;
    }
    return null;
  }
}
```

Adds utility methods for string manipulation and safe list searches.

---

## **Conclusion**

The `PurvakarmaPage` provides an intuitive and dynamic way to collect and assess Koshta data. It ensures accurate scoring, real-time updates to the state, and proper classification. This page is crucial for the Purvakarma assessment process in the app.
