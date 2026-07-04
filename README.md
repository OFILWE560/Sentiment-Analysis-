<p><strong>Built with:</strong><br>
<img src="https://img.shields.io/badge/Python-14354C?style=for-the-badge&logo=python&logoColor=3776AB" alt="Python">
<img src="https://img.shields.io/badge/NLTK-1B1F3B?style=for-the-badge&logo=python&logoColor=76B5C5" alt="NLTK">
<img src="https://img.shields.io/badge/TextBlob-4B8BBE?style=for-the-badge&logo=python&logoColor=white" alt="TextBlob">
<img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
<img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge&logo=plotly&logoColor=white" alt="Matplotlib">
</p>

# Sentiment Analysis on Social Media Text

## Overview
This project performs sentiment analysis on a dataset of social media posts, classifying each piece of text as **Positive**, **Negative**, or **Neutral**. It covers text preprocessing (tokenization, stopword removal, lemmatization), polarity scoring with `TextBlob`, and visualization of sentiment distribution and word frequency.

## Objectives
- Preprocess text data (tokenization, stopword removal, lemmatization)
- Classify sentiment using `TextBlob` polarity scoring
- Visualize the sentiment distribution and word frequencies using word clouds

## Dataset
- **732 posts** scraped from social platforms (Twitter, Instagram, Facebook), with metadata including platform, country, timestamp, likes, and retweets.
- The dataset's own `Sentiment` column contains **191 fine-grained emotion labels** (Joy, Excitement, Awe, Loneliness, etc.) rather than a simple 3-class split, so it's kept only as a reference — the actual classification below is generated independently from the raw text using TextBlob.

## Preprocessing
Each post's text was cleaned before analysis:
- Lowercased, with URLs, @mentions, and #hashtags stripped
- Punctuation and numbers removed
- Tokenized with `nltk.word_tokenize`
- Stopwords removed and remaining tokens lemmatized with `WordNetLemmatizer`

Example:
| Original | Cleaned |
|---|---|
| "Enjoying a beautiful day at the park!" | `enjoying beautiful day park` |
| "Traffic was terrible this morning." | `traffic terrible morning` |

## Sentiment Classification
Each cleaned post was scored with TextBlob's polarity (range −1 to +1) and bucketed as:
- **Positive**: polarity > 0.05
- **Negative**: polarity < −0.05
- **Neutral**: everything in between

### Results
| Sentiment | Count | Share |
|---|---|---|
| Neutral | 348 | 47.5% |
| Positive | 277 | 37.8% |
| Negative | 107 | 14.6% |

Nearly half the posts landed as neutral — a common outcome with lexicon-based polarity scoring on short, casual text, where many posts don't contain strongly charged words.

## Visualizations
| File | Description |
|---|---|
| `sentiment_distribution.png` | Bar chart of Positive/Neutral/Negative counts |
| `polarity_score.png` | Histogram of raw polarity scores across all posts |
| `word_clouds.png` | Word clouds for each sentiment class |
| `word_frequency.png` | Top 20 most frequent words across all posts |

## Repository Structure
```
.
├── sentiment_analysis.ipynb      # Main notebook (preprocessing, sentiment scoring, visualizations)
├── Sentiment dataset.csv         # Raw input data
├── sentiment_distribution.png
├── polarity_score.png
├── word_clouds.png
├── word_frequency.png
└── README.md
```

## How to Run
1. Clone the repository:
   ```
   git clone https://github.com/OFILWE560/Sentiment-Analysis.git
   cd <your-repo>
   ```
2. Install dependencies:
   ```
   pip install pandas numpy matplotlib seaborn nltk textblob wordcloud jupyter
   python -m textblob.download_corpora
   ```
3. Launch Jupyter and run all cells in order:
   ```
   jupyter notebook sentiment_analysis.ipynb
   ```
   The first cell downloads the required NLTK corpora (punkt, stopwords, wordnet). Plots render inline and save automatically to the project folder.

## Notes
- Sentiment thresholds (±0.05) are a common convention for TextBlob polarity and can be tuned depending on how conservative you want the "Neutral" bucket to be.
- Emojis (e.g. 💪) are stripped out during cleaning since punctuation/non-alphanumeric removal happens before tokenization — worth flagging as a limitation, since emojis often carry real sentiment signal.
