# **FAQ Generation and Classification Utility**

## **Overview**
This project is designed to generate **Frequently Asked Questions (FAQs)** for **fertility-related topics** using **Large Language Models (LLMs)**. The goal is to create structured, categorized FAQs that are useful to individuals seeking information on fertility treatments such as **IVF (In Vitro Fertilization), ICSI, ovulation tracking, and related procedures**.

The system utilizes **LLMs (Google Gemini)** to **generate and classify FAQs** into:
- **Medical Questions** – Must be answered by a medical professional.
- **Non-Medical Questions** – Can be answered by non-medical experts.
- **Lived Experience Questions** – Best answered by individuals who have undergone fertility treatments / lived with conditions.

## **Purpose**
This utility serves the following objectives:
- **Generate FAQs from a structured dataset** (CSV file of fertility topics and descriptions).
- **Classify each question** into appropriate categories (**Medical, Non-Medical, Lived Experience**).
- **Ensure Reusability** by allowing the system to adapt to different datasets of medical conditions.

## **Components**
### **1. FAQ Generation Pipeline**
- Reads a **CSV file** containing fertility topics.
- Uses **LLMs to generate 10-20 FAQs per topic**.
- Outputs a structured dataset in **JSON format**.

### **2. Classification System**
- **Medical**: Questions related to treatment, symptoms, or diagnosis.
- **Non-Medical**: Questions about logistics, cost, and general knowledge.
- **Lived Experience**: Questions best answered by individuals who have undergone fertility treatments.

### **3. Prompt Engineering**
The system uses a structured **LLM prompt** to generate FAQs while adhering to the problem statement guidelines. The prompt ensures:
- **Questions are common and relevant** to fertility treatments.
- **Balanced categorization** of medical, non-medical, and lived experience questions.
- **Strict adherence to the provided topic** (i.e., no off-topic questions).


### **5. Output Format**
The system generates FAQs in **JSON format** as specified in the problem statement:
```json
{
  "1": {"question_text":"What is IVF and how does it work?","category":"medical"},
  "2": {"question_text":"How much does IVF cost?","category":"non_medical"},
  "3": {"question_text":"What was your personal experience with IVF?","category":"lived_in"}
}
