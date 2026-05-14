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

---

## Task 3: Text Vectorization

The cleaned text data was converted into numerical format using the TF-IDF (Term Frequency–Inverse Document Frequency) technique.

TF-IDF assigns weights to words based on their importance:
- Words that appear frequently in a document get higher importance
- Words that appear in many documents get lower importance

This helps the model focus on meaningful and distinguishing words.

The text data was transformed into a feature matrix using:
- TfidfVectorizer from scikit-learn
- Maximum features limited to 5000

### Output

The result is a sparse matrix where:
- Rows represent text samples
- Columns represent unique words (features)
- Values represent importance scores

### Why convert text into vectors?

Machine learning models cannot understand raw text. They only process numerical data.  
Vectorization converts text into numbers so that models can learn patterns and make predictions.

---

## Task 4: Baseline Model

A baseline model was built using Logistic Regression with TF-IDF features to classify customer sentiment.

### Model Details
- Algorithm: Logistic Regression
- Input: TF-IDF feature matrix
- Output: Sentiment labels (negative, neutral, positive)

### Training Process
- The dataset was split into training (80%) and testing (20%) sets
- The model was trained using the training data
- Predictions were made on the test set

### Evaluation Metrics
The model was evaluated using:
- Accuracy score
- Precision, Recall, and F1-score
- Confusion matrix

### Results

- **Accuracy:** 1.00

The classification report shows perfect precision, recall, and F1-score across all classes.

The confusion matrix indicates that all predictions were correctly classified, with no misclassifications.

### Observations

The model achieved very high performance, likely due to:
- Clean and well-structured dataset
- Distinct patterns between sentiment classes
- Effective TF-IDF representation

While this indicates strong model performance, such perfect accuracy may not generalize to more complex real-world datasets.

---

## Task 5: Sequence Model (Conceptual Architecture)

A conceptual sequence model using LSTM (Long Short-Term Memory) is proposed to process text data.

### 1. Input Sequence

The input to the model is a sequence of tokenized words from the customer messages.

Example:
"refund still pending experience frustrating"

After tokenization:
[12, 45, 78, 23, 91]

Sequences are padded or truncated to a fixed length to ensure uniform input size.


### 2. Embedding Layer

The embedding layer converts each word index into a dense vector representation.

- Input: integer sequences
- Output: dense vectors (e.g., 100-dimensional)

This helps the model capture semantic relationships between words.


### 3. Recurrent / Sequence Layer (LSTM)

An LSTM layer processes the sequence step-by-step and captures context.

- Learns dependencies between words
- Remembers important information over long sequences
- Handles issues like vanishing gradients better than simple RNNs

Example:
"refund still pending" → captures negative sentiment pattern


### 4. Output Layer

A Dense layer with Softmax activation is used for classification.

- Output size: 3 (negative, neutral, positive)
- Produces probability distribution across classes


### 5. Loss Function

Categorical Cross-Entropy is used as the loss function.

It measures the difference between predicted probabilities and actual labels.


### 6. Evaluation Metric

The model is evaluated using:

- Accuracy
- Precision
- Recall
- F1-score


To sum up, the LSTM-based model processes sequences of text and captures contextual meaning, making it suitable for sentiment classification tasks where word order and dependencies matter.
