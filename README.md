# Product Review Sentiment Analyzer

A machine learning-based **Natural Language Processing (NLP)** project that analyzes Amazon product reviews and classifies them as **Positive** or **Negative**.

The project demonstrates a complete sentiment analysis workflow, from text preprocessing and feature extraction to model comparison and real-time prediction on new reviews.

---

## Project Objective

The goal of this project is to build a reliable sentiment classification system that can automatically identify the sentiment expressed in a product review.

The project focuses on:

* Cleaning and preprocessing review text
* Converting ratings into sentiment labels
* Handling class imbalance
* Extracting text features using TF-IDF
* Training and comparing multiple machine learning models
* Selecting the best-performing model
* Predicting sentiment for new product reviews

---

## Dataset

The project uses the **Amazon Fine Food Reviews** dataset containing **568,454 reviews**.

The original dataset contains several attributes, but only the following were used:

| Attribute | Description                 |
| --------- | --------------------------- |
| `Score`   | Customer rating from 1 to 5 |
| `Text`    | Written product review      |

Due to GitHub's file size limitations, the dataset is not included directly in this repository.

The dataset can be downloaded from Kaggle:

**Dataset:** [Amazon Product reviews Sentiment analysis](https://www.kaggle.com/code/mahmoud1mohamed/amazon-product-reviews-sentiment-analysis/notebook)

After downloading the dataset, place `Reviews.csv` in the project directory:

```text
Product-Review-Sentiment-Analyzer/
│
├── Reviews Analyzer.ipynb
├── Reviews.csv
└── README.md
```

### Sentiment Conversion

The original ratings were converted into binary sentiment labels:

* ⭐ **1–2 → Negative**
* ⭐ **3 → Removed**
* ⭐ **4–5 → Positive**

Three-star reviews were removed because they may represent neutral or mixed opinions.


### Dataset Balancing

The original dataset contains significantly more positive reviews than negative reviews. To create a balanced classification problem, a random subset was selected:

* **50,000 Positive reviews**
* **50,000 Negative reviews**
* **100,000 total reviews**

---

##  Project Workflow

```text
Amazon Product Reviews
          │
          ▼
     Data Cleaning
          │
          ▼
 Remove Neutral Reviews
          │
          ▼
 Create Sentiment Labels
          │
          ▼
   Balance Dataset
          │
          ▼
    Text Preprocessing
   ┌──────┴──────┐
   │ Lowercase   │
   │ Remove      │
   │ Punctuation │
   └──────┬──────┘
          ▼
     Train/Test Split
          │
          ▼
    TF-IDF Vectorization
          │
          ▼
 ┌────────┼────────────┐
 ▼        ▼            ▼
Logistic  Naive       Linear
Regression Bayes       SVM
 └────────┼────────────┘
          ▼
    Model Comparison
          │
          ▼
      Linear SVM
          │
          ▼
 Positive / Negative
```

---

## Text Preprocessing

The project uses basic text preprocessing before model training.

### 1. Lowercase Conversion

```text
"This Product Is AMAZING!"
        ↓
"this product is amazing!"
```

### 2. Punctuation Removal

```text
"this product is amazing!"
        ↓
"this product is amazing"
```

The original review text is preserved, while the cleaned version is stored separately.

---

## TF-IDF Feature Extraction

Machine learning models require numerical input, so the cleaned reviews are converted into numerical features using **TF-IDF (Term Frequency-Inverse Document Frequency)**.

The vectorizer uses:

* **10,000 maximum features**
* **Unigrams and bigrams**
* `ngram_range=(1, 2)`

This allows the model to learn both individual words and short phrases such as:

```text
excellent
great product
poor quality
waste money
```

---

## Machine Learning Models

Three classification algorithms were trained using the same dataset and TF-IDF features:

### Logistic Regression

Used as the baseline classification model.

### Multinomial Naive Bayes

A commonly used probabilistic algorithm for text classification.

### Linear SVM

A linear Support Vector Machine suitable for high-dimensional text classification.

---

## Model Performance

The models were evaluated using **Accuracy, Precision, Recall, and F1 Score**.

| Model               |   Accuracy |  Precision |     Recall |   F1 Score |
| ------------------- | ---------: | ---------: | ---------: | ---------: |
| Logistic Regression |     92.08% |     92.51% |     91.58% |     92.04% |
| Naive Bayes         |     89.64% |     89.88% |     89.34% |     89.61% |
| **Linear SVM**   | **92.28%** | **92.79%** | **91.67%** | **92.23%** |

### Best Model

**Linear SVM** achieved the highest performance across all four metrics and was therefore selected as the final sentiment classifier.

---

## Sentiment Prediction

The final model can analyze new product reviews.

### Example 1

**Input:**

```text
This product is amazing and the quality is excellent!
```

**Output:**

```text
Positive
```

### Example 2

**Input:**

```text
Terrible product and very poor quality.
```

**Output:**

```text
Negative
```

The prediction pipeline applies the **same text preprocessing and TF-IDF transformation** used during training before passing the review to the Linear SVM model.

---

## Technologies Used

* **Python**
* **Jupyter Notebook**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Scikit-learn**
* **TF-IDF**
* **Logistic Regression**
* **Multinomial Naive Bayes**
* **Linear SVM**

---

## Project Structure

```text
Product-Review-Sentiment-Analyzer/
│
├── Reviews Analyzer.ipynb
├── Reviews.csv
└── README.md
```

### Files

**`Reviews Analyzer.ipynb`**
Contains the complete implementation, including data preprocessing, model training, evaluation, comparison, and sentiment prediction.

**`Reviews.csv`**
Amazon product review dataset used for training and evaluation.

---

## Limitations

The analyzer only checks for empty input and reviews containing fewer than two words. It does not detect irrelevant or non-product-related text, so such inputs may still be classified as Positive or Negative.

---

## Future Improvements

Possible improvements include:

* Add a **Not a Product Review** class
* Experiment with advanced NLP preprocessing
* Test transformer-based models such as BERT
* Build a web interface using Streamlit
* Save and deploy the trained model
* Add confidence/probability visualization

---

## Conclusion

This project demonstrates an end-to-end **NLP sentiment classification pipeline** using Amazon product reviews. After comparing three machine learning algorithms, **Linear SVM achieved the best performance with 92.28% accuracy and a 92.23% F1 score**, making it the selected final model.
