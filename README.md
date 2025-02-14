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
```

## **a) Would you do this also with pure LLM orchestration?
Yes, pure LLM orchestration (i.e., using language models like GPT, Meta LLaMA, or Google Flan-T5) could be used to classify questions based on their medical or non-medical nature. LLMs excel at understanding language in context and can be used in a zero-shot or few-shot setting to classify questions by their medical relevance.

### **Approach:
Use a pre-trained language model to classify the input question.
Provide the model with appropriate instructions to determine whether the question is medical or non-medical. For example, you can fine-tune the LLM with labeled data or use prompt engineering to get relevant answers.
For validating whether the question needs to be answered by a doctor versus a person with lived experience, the model could be trained to recognize nuances in questions related to lived experiences (e.g., chronic conditions) versus those requiring medical expertise.

## **b) What are the data science methods which don't involve using an LLM? Can some supervised learning data be used from what you generated in 1. above?
Yes, traditional machine learning methods can be used for this task, especially when leveraging features such as keywords, sentence structure, and question semantics. These approaches are typically more interpretable and may require less computational power.

### **Approaches:
Rule-based Classification:

Build a set of rules that check for specific terms or phrases commonly associated with medical questions (e.g., "treatment," "doctor," "medication," "symptom").
Non-medical questions could contai keywords like (e.g. "logistics", "availability", "fitness devices", "financial assistance", "insurance", "costs")
This is a very naive approach, but it can serve as a baseline.
Supervised Learning (e.g., SVM, Random Forest, Logistic Regression):

Use labeled datasets to train a model on features such as:
- TF-IDF / BM25 embeddings of words or bigrams that indicate whether a question is medical or not.
- Named Entity Recognition (NER) for medical terms or references to treatments and conditions.
- Text embeddings (like Word2Vec, GloVe, or BERT embeddings) to convert questions into numerical representations and use those as inputs to ML models.
After generating a dataset of medical vs. non-medical questions, you can train a classifier (logistic regression) on it.

## **c) Would you use LLMs to validate your work?

Yes, we would use "LLM as a judge" in addition to other evaluation metrics such Context Recall, Query Recall, Context Precision, Query Precision, Classification metrics (precision, recall, F1 score etc.)

- Provides an additional layer of quality control.
- Helps catch edge cases and ensures that the classifier is not making overgeneralized assumptions.
- LLMs for validation are beneficial especially for edge cases where there might be ambiguity or subtlety in the language.

When the model encounters ambiguous or mixed-context questions, it could ask for clarification questions. 

Examples of ambigous questions :
"What can I do to reduce stress at work?"
"What are some medications to improve sleep?"
"Is it necessary to take blood pressure medication if I’m feeling fine?" 

Steps for Refining the Classification:
Initial Classification: The first model (whether traditional machine learning or LLM) classifies the question as "medical" or "non-medical" based on available training and logic.

Confidence Threshold: If the model’s confidence in its classification is low, or if it detects uncertainty, we can prompt an LLM for a deeper understanding or clarification.

Clarification Prompting: The LLM can be prompted to help refine the classification by:

1. Asking for clarification, e.g., "Is this question about medical treatments for stress, or about general advice?"
2. Analyzing the question with a more sophisticated understanding of context, asking follow-up questions, or making a better determination of the question's intent.
3. Reclassification: After the clarification, the system can reclassify the question as either medical or non-medical, or even flag it for expert review if necessary. This refinement ensures more accurate handling of borderline cases.