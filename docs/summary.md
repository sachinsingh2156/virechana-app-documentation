# Summary Page

The **Summary Page** serves as the final step in the Virechana Assessment App, summarizing the patient details, assessment metrics, and post-procedure data. It provides an option to review and submit the collected data to Google Sheets for record-keeping.

---

## **Overview**

**Purpose**: To display a consolidated summary of all data collected throughout the assessment and allow submission to Google Sheets.

**Features**:

- Displays patient and assessment details.
- Provides a `Submit` button to save data to Google Sheets.
- Automatically resets all state and navigates back to the first page upon submission.

---

## **Key Features**

**Data Summary**

- Displays data collected in previous steps, including:
  - Patient details (e.g., Name, Diagnosis, etc.).
  - Assessment metrics (e.g., Frequency, Consistency, Shuddhi details).
  - Post-procedure health data (e.g., Temperature, BP, Complications).

**Integration with Google Sheets**

- Submits all data to a Google Sheet using the `VirechanaSheetApi`.

**State Reset**

- Resets all form fields and state providers after submission.

**Navigation**

- Includes a **Back** button to return to the previous page.
- Automatically navigates to the first page upon successful submission.

---

## **Code Breakdown**

### **Class Declaration**

```
class SummaryPage extends ConsumerWidget {
  final PageController controller;

  SummaryPage({required this.controller});
}
```

- Inherits from `ConsumerWidget` for integration with Riverpod.
- Accepts a `PageController` to manage navigation between pages.

---

### **Data Summary**

The page displays all collected data as text:

```
Text('Patient Name: ${formData['patient_name']}'),
Text('Diagnosis: ${formData['diagnosis']}'),
Text('Frequency per day: ${formData['frequency_per_day']}'),
Text('Consistency: ${formData['consistency']}'),
Text('Urgency: ${formData['urgency']}'),
Text('Experience: ${formData['experience']}'),
Text('Antiki Shuddhi: ${formData['antiki_shuddhi']}'),
Text('Vaigiki Shuddhi: ${formData['vaigiki_shuddhi']}'),
Text('Temperature (°F): ${formData['post_procedural_temp']}'),
```

- **Dynamic Content**: Data is fetched from Riverpod providers (`formProvider`, `samyakYogaProvider`, etc.).
- **Formatted Display**: Each metric is displayed with a descriptive label for clarity.

---

### **Submit Button**

#### **Functionality**

- Gathers all data into a `User` object.
- Submits data to Google Sheets via the `VirechanaSheetApi`.
- Resets all state and navigates to the first page.

```
ElevatedButton(
  onPressed: () async {
    try {
      final newUser = User(

                    // page 1

                    date: formData['visit_date'],
                    pName: formData['patient_name'],
                    uhid: formData['uhid_no'],
                    age: formData['age'],
                    sex: formData['sex'],
                    opd: formData['opd_no'],
                    diagnosis: formData['diagnosis'],

                    // Page 2

                    koshta_freq: formData['frequency_per_day'],
                    koshta_consistency: formData['consistency'],
                    koshta_urgency: formData['urgency'],
                    koshta_experience: formData['experience'],
                    koshta_samyak: formData['samyak_snigdha'],
                    koshtaTotalScore: formData['Koshta_total_score'].toString(),

                    // page 3

                    temperature: formData['temperature'],
                    pulseRate: formData['pulse_rate'],
                    bp_systolic: formData['bp_systolic'],
                    bp_diastolic: formData['bp_diastolic'],
                    RespRate: formData['rr'],
                    bmi: formData['bmi'],
                    weight: formData['weight'],
                    physExam: formData['pe'],
                    vegaEntries: [],

                    // page 4

                    antiki_suddhi: formData['antiki_shuddhi'],
                    vaigiki_shuddhi: formData['vaigiki_shuddhi'],
                    laingiki_shuddhi: formData['laingiki_shuddhi'],
                    shuddhi_final_score: formData['shuddhi_final_score'],
                    shuddhi_classification: formData['shuddhi_classification'],

                    // page 5

                    srotovishuddhi: samyakData['Srotovishuddhi'],
                    vatanululomana: samyakData['vatanululomana'],
                    ruchi: samyakData['ruchi'],
                    laghuta: samyakData['laghuta'],
                    kayagni_anuvartana: samyakData['kayagni anuvartana'],
                    varna_shuddhi: samyakData['varna shuddhi'],
                    bhuddhi_shuddhi: samyakData['bhuddhi shuddhi'],
                    samprasadana: samyakData['samprasadana'],

                    // page 6 data

                    pratiloma_gati_dosha_srava: ayogaData['Pratiloma Gati Dosha Srava'],
                    glani: ayogaData['Glani'],
                    hridya_ashuddhi: ayogaData['Hridya Ashuddhi'],
                    kale_apravartan: ayogaData['Kale Apravartan'],
                    kshtheevana: ayogaData['Kshtheevana'],
                    tandra: ayogaData['Tandra'],
                    marutasya_nigraha: ayogaData['Marutasya Nigraha'],
                    paridaha: ayogaData['Paridaha'],
                    bhrama: ayogaData['Bhrama'],
                    gatreshu_bhramana: ayogaData['Gatreshu Bhramana'],

                    // page 7

                    medomamsa_udakaopmam: atiyogaData['Medomamsa udakaopmam'],
                    angamarda: atiyogaData['Angamarda'],
                    jarjaribhava: atiyogaData['Jarjaribhava'],
                    klama: atiyogaData['Klama / Balabhava'],
                    vepana: atiyogaData['Vepana'],
                    tamah_pravesha: atiyogaData['Tamah Pravesha'],
                    hikka: atiyogaData['Hikka'],
                    guda_bhramsha: atiyogaData['Guda Bhramsha / nissarana'],
                    netra_Pravesha: atiyogaData['Netra Pravesha'],
                    parikartika: atiyogaData['Parikartika'],
                    chimchimayan: atiyogaData['Chimchimayan'],
                    parshva_shoola: atiyogaData['Parshva Shoola'],
                    shoonyata: atiyogaData['Shoonyata'],

                    // page 8

                    post_procedural_temp: formData['post_procedural_temp'],
                    post_procedural_pulse: formData['post_procedural_pulse'],
                    post_procedural_bp_systolic: formData['post_procedural_bp_systolic'],
                    post_procedural_bp_diastolic: formData['post_procedural_bp_diastolic'],
                    post_procedural_resp: formData['post_procedural_resp'],
                    post_procedural_weight: formData['post_procedural_weight'],
                    post_procedural_complications: formData['post_procedural_complications'],
                  );
      );

      await VirechanaSheetApi.insert([user.toJson()]);
      if (formData['vega_entries'] != null && formData['vega_entries'].isNotEmpty) {
        List<List<String>> vegaRows = formData['vega_entries']
            .map((entry) => [
              entry['timeController']?.text ?? '',
              entry['vegaController']?.text ?? '',
              // Other fields...
            ])
            .toList();
        await VirechanaSheetApi.insertVegaEntries(vegaRows);
      }

      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(
          content: Text('Data Submitted Successfully!'),
          duration: Duration(seconds: 3),
        ),
      );

      ref.read(formProvider.notifier).resetForm();
      ref.read(samyakYogaProvider.notifier).resetState();
      ref.read(ayogaProvider.notifier).resetState();
      ref.read(atiyogaProvider.notifier).resetState();

      controller.jumpToPage(0);
    } catch (e) {
      print("Submission Error: $e");
    }
  },
  child: Text('Submit'),
);
```

#### **Steps Performed**

**Data Consolidation**: Combines data from various state providers into a single `User` object.
**Submission to Google Sheets**:

- Patient data is inserted using `VirechanaSheetApi.insert`.
- Vega entries are inserted using `VirechanaSheetApi.insertVegaEntries`.
  **State Reset**:
- Resets `formProvider`, `samyakYogaProvider`, `ayogaProvider`, and `atiyogaProvider`.
  **Navigation**:
- Returns to the first page upon successful submission.

---

### **Navigation**

#### Back Button

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

---

## **Usage**

### **State Management**

The page uses the following providers:

- **`formProvider`**: Holds general form data.
- **`samyakYogaProvider`**: Holds Samyak Yoga data.
- **`ayogaProvider`**: Holds Ayoga symptoms data.
- **`atiyogaProvider`**: Holds Atiyoga symptoms data.

### **Data Submission**

Data is submitted to Google Sheets using:

```
await VirechanaSheetApi.insert([user.toJson()]);
```

### **State Reset**

All state is reset to default values:

```
ref.read(formProvider.notifier).resetForm();
ref.read(samyakYogaProvider.notifier).resetState();
ref.read(ayogaProvider.notifier).resetState();
ref.read(atiyogaProvider.notifier).resetState();
```

---

## **Conclusion**

The **Summary Page** is the final step in the Virechana Assessment App. It consolidates all collected data for review and submission, ensuring accurate record-keeping and resetting the app for the next assessment. This page enhances the app's usability by providing clear data visualization and seamless state management.
