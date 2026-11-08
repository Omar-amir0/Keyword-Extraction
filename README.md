# NLP Keyword Extraction System

An NLP project that extracts the top 5 keywords from news articles using three different approaches: **TF-IDF, Word2Vec, and GloVe**. The project compares statistical and embedding-based methods to understand which approach produces the most meaningful keywords for representing a document.

## Project Overview

The system allows users to select a news article and extract its most relevant keywords using three different methods. The results are displayed side by side through an interactive Streamlit application.

The main objective is to compare how traditional statistical techniques perform against word embedding approaches in identifying important information within a document.

## Features

- Extracts the top 5 keywords from each selected article.
- Compares three keyword extraction approaches.
- Preprocesses text using NLTK.
- Detects frequently occurring word combinations (bigrams).
- Trains Word2Vec on the available news articles.
- Uses pretrained GloVe word embeddings.
- Provides an interactive Streamlit interface.
- Caches dataset preprocessing and the pretrained GloVe model to improve runtime performance.

## Dataset

BBC News Summary Dataset

Source: https://zenodo.org/records/14752618

The project uses a subset of 511 English news articles
stored as individual TXT files.

The articles are used to train Word2Vec and evaluate
keyword extraction using TF-IDF, Word2Vec, and GloVe.

## Techniques Used

### 1. TF-IDF (Term Frequency–Inverse Document Frequency)

A statistical approach that identifies important words based on their frequency within a document and their rarity across documents.

### 2. Word2Vec

A word embedding technique that learns semantic relationships between words by training on the available news articles.

The project uses:
- Vector size: 100
- Window size: 5
- Minimum word count: 1

The document representation is calculated by averaging its word vectors. Cosine similarity is then used to rank candidate keywords.

### 3. GloVe (Global Vectors for Word Representation)

Uses pretrained word embeddings to capture semantic relationships between words.

The project uses the pretrained `glove-wiki-gigaword-100` model through Gensim. Similar to Word2Vec, document vectors are calculated by averaging word embeddings and ranking candidate words using cosine similarity.

## Text Preprocessing

Before keyword extraction, the documents go through the following preprocessing steps:

1. Convert text to lowercase.
2. Remove punctuation.
3. Tokenize text into individual words.
4. Remove English stopwords.
5. Remove additional frequent but uninformative words, such as "said", "reported", and "according".
6. Detect common word combinations using bigram detection in the embedding-based approaches.

## Dataset

The project uses a collection of **511 English news articles** stored as individual `.txt` files.

- Format: Plain-text files.
- Language: English.
- Content: News articles covering different subjects.
- Usage: Training the Word2Vec model and testing keyword extraction methods.

**Dataset source:** [BBC News Summary Dataset – Zenodo](https://zenodo.org/records/14752618)

The project uses a subset of the available news articles.

## Evaluation and Results

The three approaches were evaluated using human judgment on 10 randomly selected articles.

Each method received a score out of 5 based on how effectively its extracted keywords represented the main ideas of the article.

| Method | Average Score |
|---|---:|
| TF-IDF | 4.15 / 5 |
| Word2Vec | 1.95 / 5 |
| GloVe | 1.85 / 5 |

### Key Findings

**TF-IDF**
- Best overall performance in the manual evaluation.
- Successfully identified important names, organizations, locations, and article-specific terms.
- Sometimes produced redundant or less meaningful words.

**Word2Vec**
- Captured general contextual relationships.
- Frequently produced generic words that were not sufficiently informative.
- Struggled to identify important entities within individual articles.

**GloVe**
- Captured semantic relationships between words.
- Sometimes produced contextually related but uninformative keywords.
- Did not consistently identify the main entities of an article.

### Conclusion

TF-IDF achieved the highest average evaluation score. Although Word2Vec and GloVe capture semantic relationships, they are not specifically designed to identify the most important terms within an individual document.

This comparison demonstrates that more advanced representations do not necessarily produce better results for every NLP task. The suitability of an approach depends on the problem being solved.

## Technologies Used

- Python
- Natural Language Processing (NLP)
- NLTK
- Scikit-learn
- Gensim
- NumPy
- Streamlit

## Project Structure

```text
NLP/
│
├── Dataset/
│   ├── 001.txt
│   ├── 002.txt
│   └── ...
│
├── app.py
├── Preprocessing.py
├── tfidf.py
├── word2vec.py
├── glove.py
├── test.py
│
└── README.md
```

## Installation and Usage

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd NLP
```

### 2. Install dependencies

```bash
pip install streamlit numpy nltk scikit-learn gensim
```

### 3. Run the application

```bash
streamlit run app.py
```

### 4. Use the application

1. Select a news article from the available dataset.
2. Click the analysis button.
3. View the extracted keywords from TF-IDF, Word2Vec, and GloVe.
4. Compare the results side by side.

**Note:** The first run downloads the required NLTK resources and pretrained GloVe model. An internet connection is required for these downloads.

## Limitations

- Evaluation was based on human judgment using only 10 randomly selected articles.
- Word2Vec performance depends on the size and diversity of the training corpus.
- Embedding-based approaches may produce generic words instead of document-specific keywords.
- TF-IDF is currently fitted on the selected document in the application, rather than the entire corpus, limiting its use of cross-document inverse document frequency.



---

**Project Focus:** Natural Language Processing | Keyword Extraction | Text Processing | Word Embeddings
