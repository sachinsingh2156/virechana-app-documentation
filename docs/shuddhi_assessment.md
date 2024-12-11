# Shuddhi Assessment Page

The **Shuddhi Assessment Page** evaluates the degree of detoxification achieved during the process. This page calculates a final score based on the responses to specific criteria and classifies the Shuddhi into categories such as **Avara**, **Madhyama**, or **Pravara**.

---

## **Overview**

- **Purpose**: Assess Shuddhi (purification) using three key factors: **Antiki Shuddhi**, **Vaigiki Shuddhi**, and **Laingiki Shuddhi**.
- **Features**:

        - Dropdown fields for each Shuddhi factor with predefined options.

        - Dynamic calculation of the final score.

        - Real-time classification of Shuddhi based on the score.

        - Integrated with Riverpod for state management.

---

## **Key Features**

1.  **Shuddhi Factors**  
    Collects data for:

        Antiki Shuddhi: Determines the evacuation characteristics.

        Vaigiki Shuddhi: Assesses the frequency of bowel movements.

        Laingiki Shuddhi: Evaluates other physical signs of detoxification.

2.  **Dynamic Final Score Calculation**

    The final score is calculated by summing the scores of all three Shuddhi factors.

3.  **Shuddhi Classification**

    Based on the final score, the Shuddhi is classified as:

        Avara Shuddhi (Score: 1-4)
        Madhyama Shuddhi (Score: 5-8)
        Pravara Shuddhi (Score: 9-12)

4.  **Dropdown Options with Scoring**

    Each dropdown option is associated with a specific score, ensuring consistent scoring for all factors.

5.  **Real-Time State Updates**
    Automatically updates the state using Riverpod, ensuring the UI reflects the latest data.

---

## **Code Breakdown**

### **Class Declaration**

```
class ShuddhiAssessmentPage extends ConsumerStatefulWidget {
  final PageController controller;

  ShuddhiAssessmentPage({required this.controller});

  @override
  _ShuddhiAssessmentPageState createState() => _ShuddhiAssessmentPageState();
}
```

- Accepts a `PageController` for managing navigation between pages.
- Uses `ConsumerStatefulWidget` for Riverpod integration.

---

### **State Initialization**

```
@override
void initState() {
  super.initState();
  final formData = ref.read(formProvider);
  suddhiClassController = TextEditingController(text: formData['shuddhi_classification']);
}
```

- Initializes a `TextEditingController` for managing the Shuddhi classification field.

### **Dropdown Implementation**

The page includes dropdown fields for each Shuddhi factor, dynamically created from a predefined set of options:

```
final dropdownOptions = {
  'antiki_shuddhi': [
    'Anila, Kapha, Pitta, Vita Nirgamana',
    'Kapha, Pitta, Vita Nirgamana',
    'No Kaphanta',
  ],
  'vaigiki_shuddhi': ['1-10', '11-20', '21-30 or >30'],
  'laingiki_shuddhi': ['2 or fewer criteria', '3-5 criteria', 'More than 5 criteria'],
};
```

#### **Example Dropdown**

```
DropdownButtonFormField<String>(
  decoration: InputDecoration(
    labelText: key.replaceAll('_', ' ').capitalize(),
    border: OutlineInputBorder(),
  ),
  value: formData[key],
  items: options.map((option) => DropdownMenuItem<String>(
        value: option,
        child: Text(option),
      )).toList(),
  onChanged: (value) {
    if (value != null) {
      ref.read(formProvider.notifier).updateField(key, value);
      final int score = _getScore(key, value);
      ref.read(formProvider.notifier).updateScore(key, score);
    }
  },
),
```

- **Label Text**: Dynamically generated based on the field name.
- **Options**: Generated from the predefined `dropdownOptions`.
- **State Updates**: Updates the field value and score in the `formProvider`.

---

### **Final Score Calculation**

The final score is dynamically calculated based on the scores from all three Shuddhi factors:

```
final int finalScore = (formData['antiki_shuddhi_score'] ?? 0) +
    (formData['vaigiki_shuddhi_score'] ?? 0) +
    (formData['laingiki_shuddhi_score'] ?? 0);
```

---

### **Shuddhi Classification**

The classification is determined based on the final score using the following logic:

```
String getShuddhiClassification(int totalScore) {
  if (totalScore >= 1 && totalScore <= 4) return 'Avara Shuddhi';
  if (totalScore >= 5 && totalScore <= 8) return 'Madhyama Shuddhi';
  if (totalScore >= 9 && totalScore <= 12) return 'Pravara Shuddhi';
  return 'Invalid Score';
}
```

The classification is displayed on the UI:

```
Text(
  'Shuddhi Classification: $classification',
  style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
),
```

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
  child: Text('Next'),
),
```

---

### **Utility Extensions**

#### **String Capitalization**

```
extension StringExtension on String {
  String capitalize() {
    return "${this[0].toUpperCase()}${this.substring(1)}";
  }
}
```

- Ensures proper capitalization of dropdown labels.

---

## **Conclusion**

The **Shuddhi Assessment Page** provides an intuitive interface to evaluate the detoxification level based on critical Shuddhi factors. It ensures accurate scoring, real-time classification, and seamless navigation for a user-friendly experience.
