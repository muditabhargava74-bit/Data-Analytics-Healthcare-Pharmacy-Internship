# Pharmacy Data Analytics – Task 1

## Objective
This project performs basic healthcare data quality and governance checks on a small synthetic, de-identified patient dataset.

The task covers:
1. Field classification and de-identification rationale
2. Validation of ranges, data types, missing values, and duplicate Patient IDs
3. Cleaning/standardization without inventing clinical values
4. Documentation of the work in a public/view-only repository

## Dataset
The dataset contains 10 synthetic patient records and 10 fields.

No direct identifiers such as patient name, address, phone number, email address, or medical record number are present.

## 1. Field Classification

| Field | Type | Classification | Reason |
|---|---|---|---|
| PatientID | Text | Pseudonymous identifier | Identifies a record using a synthetic code rather than a person's name |
| Age | Integer | Clinical / quasi-identifier | Clinical/demographic information that could contribute to re-identification when combined with other data |
| Gender | Categorical | Clinical/demographic | Descriptive demographic variable |
| Diagnosis | Categorical | Clinical | Describes the patient's diagnosis |
| PrimaryMedication | Categorical | Clinical | Medication associated with the record |
| DosageMg | Numeric | Clinical | Medication dosage |
| TreatmentDurationDays | Integer | Clinical | Duration of treatment in days |
| Readmitted | Categorical | Clinical/outcome | Indicates whether the patient was readmitted |
| BloodPressure | Text in systolic/diastolic format | Clinical | Blood-pressure measurement |
| CholesterolLevel | Numeric | Clinical | Cholesterol measurement |

### Why the sample is de-identified
The dataset is presented as synthetic/de-identified training data. It does not contain direct personal identifiers such as names, addresses, phone numbers, emails, or dates of birth. Patient IDs use artificial codes (PAT-201 to PAT-210). Age and clinical variables remain because they are useful for analytics, but they should still be treated as potentially sensitive healthcare information.

## 2. Data Validation

### Missing values
- Total missing cells: **0**
- No field in the supplied 10-row sample contains a blank/null value.

### Duplicate Patient IDs
- Duplicate Patient IDs: **0**
- All Patient IDs are unique.

### Data types
- PatientID, Gender, Diagnosis, PrimaryMedication, Readmitted and BloodPressure are categorical/text fields.
- Age, DosageMg, TreatmentDurationDays and CholesterolLevel are numeric fields.
- BloodPressure is stored as text because it contains two values separated by `/`.

### Range checks
| Field | Observed range | Validation result |
|---|---:|---|
| Age | 29–76 years | No obvious invalid values |
| DosageMg | 0.05–850 mg | No blank or non-numeric values |
| TreatmentDurationDays | 14–365 days | No blank or non-numeric values |
| CholesterolLevel | 175–260 | No blank or non-numeric values |
| BloodPressure | 115/72–150/95 | All records follow systolic/diastolic format |

These checks identify structural/range issues only. They do not establish whether an individual clinical value is medically appropriate.

## 3. Cleaning Rules Applied

The following non-destructive cleaning/standardization rules were used:

1. Confirmed that PatientID values are unique.
2. Checked for missing values without replacing them with invented values.
3. Confirmed numeric fields are represented as numeric values.
4. Standardized categorical text to consistent capitalization/spelling.
5. Preserved BloodPressure in its original systolic/diastolic representation rather than inventing separate values.
6. Preserved all supplied clinical values because no evidence was available to justify changing them.
7. Retained the synthetic PatientID format.

Because the supplied sample already has consistent values and no missing/duplicate records, no clinical values required correction.

## 4. Data Quality Summary

The supplied sample contains 10 records and 10 fields. The sample has no missing cells and no duplicate Patient IDs. The numeric fields are suitable for basic validation, while BloodPressure is represented as a structured text field.

No clinical values were imputed or changed solely because they might appear unusual. This follows the task requirement not to invent clinical data.

## Files
- `healthcare_patients_sample.csv` – cleaned/standardized copy of the supplied sample
- `data_dictionary.md` – field-level documentation
- `data_quality_report.md` – validation and quality checks

## Conclusion
The sample is structurally clean for the checks performed: there are no missing values, no duplicate Patient IDs, and the fields follow consistent basic formats. The dataset remains synthetic/de-identified and should be used for training/analytics purposes rather than real-patient decision making.
