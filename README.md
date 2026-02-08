# Twitter Sentiment Analysis

A data analysis project that performs sentiment analysis on Twitter data using Natural Language Processing (NLP) techniques, with interactive visualizations and word cloud generation.

## Overview

This project analyzes sentiment in tweets from a labeled dataset containing over 32,000 tweets. It performs text preprocessing, feature extraction, and generates insightful visualizations including word clouds and hashtag frequency analysis to understand sentiment patterns in social media conversations.

## Features

- **Text Preprocessing**: Remove mentions, special characters, and filter short words
- **Sentiment Visualization**: Generate word clouds for overall, positive, and negative tweets
- **Hashtag Analysis**: Extract and analyze trending hashtags for both positive and negative sentiments
- **Interactive Charts**: Create interactive bar charts showing top hashtags
- **Data Exploration**: Comprehensive statistical analysis of the dataset

## Dataset

The project uses `twitter_sentiment_analysis.csv` with the following structure:
- **id**: Unique identifier for each tweet
- **label**: Sentiment label (0 = Positive, 1 = Negative)
- **tweet**: Raw tweet text

Dataset size: 32,457 tweets

## Technologies Used

- **Python 3.x**
- **Libraries**:
  - `pandas` - Data manipulation and analysis
  - `numpy` - Numerical computing
  - `matplotlib` - Static visualizations
  - `seaborn` - Statistical data visualization
  - `plotly` - Interactive visualizations
  - `nltk` - Natural Language Processing and frequency distribution
  - `wordcloud` - Word cloud generation
  - `re` - Regular expressions for text preprocessing

## Installation

1. Clone the repository:
```bash
git clone https://github.com/ashutoshranaa/twitter-sentiment-analysis.git
cd twitter-sentiment-analysis
```

2. Create a virtual environment (optional but recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install required packages:
```bash
pip install -r requirements.txt
```

## Requirements

Create a `requirements.txt` file with the following dependencies:

```
numpy
pandas
seaborn
matplotlib
plotly
wordcloud
nltk
```

Install all dependencies:
```bash
pip install -r requirements.txt
```

## Usage

1. Place your `twitter_sentiment_analysis.csv` file in the project directory

2. Run the analysis script:
```bash
python TwitterSentimentAnalysis.py
```

3. The script will:
   - Load and explore the dataset
   - Preprocess tweet text
   - Generate word clouds for all tweets, positive tweets, and negative tweets
   - Extract and visualize top hashtags for both sentiments

## Project Workflow

### 1. Data Loading and Exploration
```python
data = pd.read_csv('twitter_sentiment_analysis.csv')
data.head()
data.info()
data.describe()
```

### 2. Text Preprocessing

The preprocessing pipeline includes:

- **Remove mentions**: Strip @username patterns
```python
data['new_tweet'] = np.vectorize(pattern_remove)(data['tweet'], "@[\w]*")
```

- **Remove special characters**: Keep only letters and hashtags
```python
data['new_tweet'] = data['new_tweet'].str.replace("[^a-zA-Z#]", " ")
```

- **Filter short words**: Remove words with 3 or fewer characters
```python
data['new_tweet'] = data['new_tweet'].apply(lambda b : " ".join([c for c in b.split() if len(c) > 3]))
```

### 3. Word Cloud Generation

Generate word clouds to visualize most frequent words:

- **All tweets**
- **Positive tweets** (label = 0)
- **Negative tweets** (label = 1)

```python
freq_words = " ".join([words for words in data['new_tweet']])
cloud_word = WordCloud(width=850, height=550, random_state=50, max_font_size=90).generate(freq_words)
```

### 4. Hashtag Analysis

Extract and analyze hashtags:

```python
def get_hashtag(tweets):
    hash_tag = []
    for tweet in tweets:
        d = re.findall(r"#(\w+)", tweet)
        hash_tag.append(d)
    return hash_tag

hashtag_positive = get_hashtag(data['new_tweet'][data['label'] == 0])
hashtag_negative = get_hashtag(data['new_tweet'][data['label'] == 1])
```

### 5. Interactive Visualizations

Create interactive bar charts showing top 10 hashtags:

```python
tweet_count = nltk.FreqDist(hashtag_positive)
e = pd.DataFrame({'name_hashtag': list(tweet_count.keys()), 
                  'total_count': list(tweet_count.values())})
e = e.nlargest(columns="total_count", n=10)
fig = px.bar(e, x="name_hashtag", y="total_count", color="name_hashtag")
fig.show()
```

## File Structure

```
twitter-sentiment-analysis/
│
├── TwitterSentimentAnalysis.py    # Main analysis script
├── twitter_sentiment_analysis.csv # Dataset (rename from Sentiment_Analysis.csv)
├── requirements.txt               # Python dependencies
├── README.md                      # Project documentation
└── .gitignore                     # Git ignore file
```

## Output Visualizations

The script generates the following visualizations:

1. **Overall Word Cloud**: Most frequent words across all tweets
2. **Positive Word Cloud**: Common words in positive tweets
3. **Negative Word Cloud**: Common words in negative tweets
4. **Top Positive Hashtags**: Interactive bar chart of top 10 positive hashtags
5. **Top Negative Hashtags**: Interactive bar chart of top 10 negative hashtags

## Key Insights

The analysis reveals:
- Distribution of positive vs. negative tweets
- Most commonly used words in different sentiment categories
- Trending hashtags associated with each sentiment
- Text patterns and characteristics of positive vs. negative content

## Data Preprocessing Details

| Step | Description | Purpose |
|------|-------------|---------|
| 1 | Remove @mentions | Clean user references |
| 2 | Remove special characters | Keep only alphabets and hashtags |
| 3 | Filter words ≤ 3 characters | Remove noise and common short words |
| 4 | Normalize spacing | Ensure consistent formatting |

## Customization

You can customize various parameters:

- **Word Cloud dimensions**: Modify `width` and `height` parameters
- **Top N hashtags**: Change `n` value in `nlargest()` function
- **Word length filter**: Adjust the threshold in word filtering
- **Color schemes**: Modify WordCloud and Plotly color parameters

## Future Enhancements

- [ ] Implement machine learning models for sentiment classification
- [ ] Add neutral sentiment category
- [ ] Include emoji analysis and visualization
- [ ] Perform time-series analysis of sentiment trends
- [ ] Add sentiment prediction for new tweets
- [ ] Create a web dashboard for interactive exploration
- [ ] Multi-language sentiment analysis support

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Dataset source: Twitter Sentiment Analysis Dataset
- WordCloud library for beautiful text visualizations
- NLTK for natural language processing tools
- Plotly for interactive visualizations

## Contact

For questions or feedback, please open an issue or contact:
- GitHub: [@ashutoshranaa](https://github.com/ashutoshranaa)
- Repository: [twitter-sentiment-analysis](https://github.com/ashutoshranaa/twitter-sentiment-analysis)

---

⭐ If you found this project helpful, please consider giving it a star!
