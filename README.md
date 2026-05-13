# part-3-nlp-sequence-modeling

## Task 1: Dataset Understanding

The dataset used in this project is a customer support text classification dataset, where each record contains a customer message and its corresponding sentiment label.

The dataset includes fields such as ticket ID, communication channel, customer message, sentiment label, word count, and urgency flag.

The total number of records in the dataset is **1500**.

The target labels/classes in the dataset are:
- Positive  
- Neutral  
- Negative  

Sample text records include customer queries and feedback such as:
"I need information about the payment process."
"My refund is still pending and this experience is frustrating."

The dataset consists of short conversational messages collected from different channels such as chat, phone, email, and social media.

The average text length is approximately **12.7 words**, indicating that most messages are short and concise.

The class distribution is as follows:
- Neutral: 524  
- Negative: 497  
- Positive: 479  

The dataset is **fairly balanced**, with all three classes having a similar number of samples.

Overall, this dataset represents a **multi-class text classification problem**, where the objective is to predict the sentiment of customer messages based on their textual content.

---

## Task 2: Text Preprocessing

In this step, the raw text data was cleaned and prepared for further processing.

The following preprocessing steps were applied:

- Converted all text to lowercase
- Removed special characters and punctuation
- Tokenized the text into individual words
- Removed common stopwords (e.g., "the", "is", "and")
- Removed additional non-informative words such as "please", "need", and "tell"

A new column `clean_text` was created, which contains the processed version of the original customer messages.

### Example:

Original:
"I need information about the payment process."

Cleaned:
"information payment process"
