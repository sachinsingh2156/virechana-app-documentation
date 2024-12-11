# User Data Model

The **`User`** class represents the data model for storing information across various pages of the Virechana Assessment App. This includes patient details, koshta assessment, vitals, shuddhi classifications, procedural outcomes, and more.

---

## **Overview**

The `User` class and the `UserFields` utility provide a structured way to manage and store the data for each user. These fields are mapped directly to the headers in Google Sheets.

---

## **UserFields**

The `UserFields` class defines static constants that act as field names for both the Google Sheets headers and the `User` model. Below is the categorization of fields based on their corresponding pages.

### **Page 1: Patient Details**

- **`date`**: Date of the assessment.
- **`pName`**: Patient's name.
- **`uhid`**: Unique hospital ID.
- **`age`**: Patient's age.
- **`sex`**: Patient's gender.
- **`opd`**: OPD number.
- **`diagnosis`**: Diagnosis details.

### **Page 2: Koshta Assessment**

- **`koshta_freq`**: Frequency of bowel movements.
- **`koshta_consistency`**: Stool consistency.
- **`koshta_urgency`**: Urgency level for bowel movements.
- **`koshta_experience`**: Experience after consuming specific items.
- **`koshta_samyak`**: Snigdha Lakshana achieved in.
- **`koshtaTotalScore`**: Total score for koshta assessment.

### **Page 3: Vitals and Physical Examination**

- **`temperature`**: Body temperature.
- **`pulseRate`**: Pulse rate.
- **`bp_systolic`**: Systolic blood pressure.
- **`bp_diastolic`**: Diastolic blood pressure.
- **`RespRate`**: Respiratory rate.
- **`bmi`**: Body mass index.
- **`weight`**: Body weight.
- **`physExam`**: Observations from physical examination.

### **Page 4: Shuddhi Assessment**

- **`antiki_suddhi`**: Antiki shuddhi score.
- **`vaigiki_shuddhi`**: Vaigiki shuddhi score.
- **`laingiki_shuddhi`**: Laingiki shuddhi score.
- **`shuddhi_final_score`**: Final shuddhi score.
- **`shuddhi_classification`**: Classification of shuddhi (e.g., Pravara, Madhyama, etc.).

### **Page 5: Samyak Yoga Lakshana**

- **`srotovishuddhi`**: Srotovishuddhi observation.
- **`vatanululomana`**: Vatanululomana observation.
- **`ruchi`**: Improved taste perception.
- **`laghuta`**: Sense of lightness.
- **`kayagni_anuvartana`**: Kayagni anuvartana (long-term digestion improvement).
- **`varna_shuddhi`**: Improvement in skin complexion.
- **`bhuddhi_shuddhi`**: Clarity of mind.
- **`samprasadana`**: Restoration of sense organs.

### **Page 6: Ayoga of Virechana**

- **`pratiloma_gati_dosha_srava`**: Pratiloma gati dosha srava issues.
- **`glani`**: Lassitude and fatigue.
- **`hridya_ashuddhi`**: Discomfort in the chest region.
- **`kale_apravartan`**: Delayed response to the treatment.
- **`kshtheevana`**: Nausea or excessive salivation.
- **`tandra`**: Drowsiness or stupor.
- **`marutasya_nigraha`**: Incomplete evacuation of body waste.
- **`paridaha`**: Burning sensation.
- **`bhrama`**: Dizziness.
- **`gatreshu_bhramana`**: Involuntary body movements.

### **Page 7: Atiyoga of Virechana**

- **`medomamsa_udakaopmam`**: Foul-smelling stool.
- **`angamarda`**: Body pain.
- **`jarjaribhava`**: Weakness or loss of confidence.
- **`klama`**: Fatigue without exertion.
- **`vepana`**: Tremors.
- **`tamah_pravesha`**: Feeling of darkness or dizziness.
- **`hikka`**: Persistent hiccups.
- **`guda_bhramsha`**: Rectal prolapse.
- **`netra_Pravesha`**: Sunken eyes.
- **`parikartika`**: Cutting pain in the rectal region.
- **`chimchimayan`**: Tingling sensation.
- **`parshva_shoola`**: Pain in the flanks.
- **`shoonyata`**: Emptiness or thoughtlessness.

### **Page 8: Post-Procedural Observations**

- **`post_procedural_temp`**: Post-procedural body temperature.
- **`post_procedural_pulse`**: Post-procedural pulse rate.
- **`post_procedural_bp_systolic`**: Post-procedural systolic blood pressure.
- **`post_procedural_bp_diastolic`**: Post-procedural diastolic blood pressure.
- **`post_procedural_resp`**: Post-procedural respiratory rate.
- **`post_procedural_weight`**: Post-procedural weight.
- **`post_procedural_complications`**: Observed complications post-procedure.

---

## **User Class**

The `User` class represents an individual patient's data. Each field corresponds to a `UserFields` property and is serialized into a JSON format for integration with Google Sheets.

### **Constructor**

The `User` class constructor accepts parameters for all fields, divided into categories (Page 1 to Page 8). Here's a sample instantiation:

```
const user = User(
date: '2024-01-01',
pName: 'Sachin Singh',
uhid: 'UH123456',
age: '35',
sex: 'Male',
opd: 'OPD789',
diagnosis: 'Diagnosis Example',
// Other additional parameters...
);

```

### **toJson Method**

The `toJson()` method converts the `User` object into a JSON-compatible `Map` for data insertion into Google Sheets.

```

Map<String, dynamic> toJson() => {
UserFields.date: date ?? 'Unknown',
UserFields.pName: pName ?? 'Unknown',
UserFields.uhid: uhid ?? 'Unknown',
// Other additional mappings...
};

```

---

## **Get Fields Method**

The `getFields()` method in `UserFields` returns a list of all field names for initializing Google Sheets headers.

```

List<String> getFields() => [
UserFields.date,
UserFields.pName,
UserFields.uhid,
UserFields.age,
// Other additional fields...
];

```

---

This structured data model ensures all patient information and procedural outcomes are consistently captured and stored for analysis or further processing.
