
# Letterboxd Film Dataset

This dataset contains a comprehensive collection of 847,209 films from the Letterboxd platform, including movie information, user reviews, and ratings.

## Dataset Summary

- **Total Films**: 847,209
- **File Size**: ~1.12 GB (1,120,572,122 bytes)
- **Format**: JSONL (JSON Lines)
- **Language**: Primarily English, with some multilingual content

## Data Structure

Each line contains a JSON object with the following fields:

```json
{
  "url": "https://letterboxd.com/film/come-and-see/",
  "title": "Come and See",
  "year": "1985",
  "directors": ["Elem Klimov"],
  "genres": ["War", "Drama"],
  "cast": ["Aleksei Kravchenko", "Olga Mironova", ...],
  "synopsis": "The invasion of a village in Byelorussia by German forces...",
  "rating": "4.62 out of 5",
  "poster_url": "https://a.ltrbxd.com/resized/film-poster/...",
  "reviews": [
    {
      "username": "cameron fetter",
      "review_text": "as soon as this film ended i went online...",
      "likes": "11662"
    }
  ]
}
```

### Data Fields

| Field | Type | Description |
|-------|------|-------------|
| `url` | string | Letterboxd film page URL |
| `title` | string | Movie title |
| `year` | string | Release year |
| `directors` | array | Director names |
| `genres` | array | Movie genres |
| `cast` | array | Actor names |
| `synopsis` | string | Movie plot summary |
| `rating` | string | Average user rating (out of 5) |
| `poster_url` | string | Movie poster image URL |
| `reviews` | array | Popular user reviews (max 10) |

### Reviews Object

Each review contains:
- `username`: Reviewer's username
- `review_text`: Review content
- `likes`: Number of likes received

## Usage

### Loading Data with Python

```python
import json

# Loading JSONL file
films = []
with open('full_dump.jsonl', 'r', encoding='utf-8') as f:
    for line in f:
        films.append(json.loads(line))

print(f"Loaded {len(films)} films")
print(f"First film: {films[0]['title']} ({films[0]['year']})")
```

### Analysis with Pandas

```python
import pandas as pd
import json

# Converting to DataFrame
data = []
with open('full_dump.jsonl', 'r', encoding='utf-8') as f:
    for line in f:
        data.append(json.loads(line))

df = pd.json_normalize(data)
print(df.head())

# Basic statistics
print(f"Most popular genres: {df['genres'].explode().value_counts().head()}")
print(f"Most productive years: {df['year'].value_counts().head()}")
```

### Using Hugging Face Datasets

```python
from datasets import load_dataset

# Loading dataset
dataset = load_dataset("pkchwy/letterboxd-all-movie-data")

# Exploring first example
print(dataset['train'][0])

# Filtering example - only films after 2020
recent_films = dataset['train'].filter(lambda x: int(x['year']) > 2020)
```

## Use Cases

This dataset can be used for:

### 🎬 Movie Recommendation Systems
- Collaborative filtering based on reviews and ratings
- Content-based recommendation (genre, director, actor similarity)

### 📝 Natural Language Processing
- Sentiment analysis on film reviews
- Text classification (genre prediction from synopsis)
- Review quality assessment

### 📊 Data Analysis & Visualization
- Film industry trend analysis
- Director and actor popularity analysis
- Genre distribution and temporal changes
- 
## Data Quality

- **Missing Data**: Some films may lack synopsis, cast, or review information
- **Language**: Reviews are mostly in English, with some multilingual content
- **Time Range**: Films from 1890s to present day
- **Scope**: Popular films on Letterboxd platform (rating-based ranking)

## Ethical Use and Limitations

- This dataset consists of publicly available Letterboxd data
- Contains no personal information (only usernames)
- Check Letterboxd terms of service before commercial use
- Possible sampling bias (popular films weighted)

## Citation

If you use this dataset in your research or projects, please cite it as:

```bibtex
@dataset{letterboxd_film_dataset_2025,
  title={Letterboxd Film Dataset},
  author={Salih Mert Canseven},
  year={2025},
  publisher={Hugging Face},
  url={https://huggingface.co/datasets/pkchwy/letterboxd-all-movie-data}
}
```

Or in text format:
```
Salih Mert Canseven. (2025). Letterboxd Film Dataset. Hugging Face. https://huggingface.co/datasets/pkchwy/letterboxd-all-movie-data
```

## License

MIT License - Free for educational and research purposes. **Citation required for any use.**

## 📥 Download Dataset

The dataset is hosted on Hugging Face for easy access and ML integration:

**🔗 [Download from Hugging Face](https://huggingface.co/datasets/pkchwy/letterboxd-all-movie-data)**

- Direct download available
- Use with `datasets` library
- Built-in data viewer
- Ready for ML workflows

## Contact

For questions about the dataset, please use GitHub Issues.

---

**Source**: Letterboxd.com 
