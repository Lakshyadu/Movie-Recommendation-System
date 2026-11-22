<div align="center">

# 🎬 Movie Recommendation System

**Content-based movie recommendations, rich cast details and review sentiment analysis, served through a Flask web app.**

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20App-000000?logo=flask&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-NLP%20%26%20ML-F7931E?logo=scikitlearn&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)
![License](https://img.shields.io/badge/License-GPL%20v3-blue)
![Stars](https://img.shields.io/github/stars/Lakshyadu/Movie-Recommendation-System?style=social)

<img src="infographic.svg" alt="Project infographic: how the recommendation system works" width="100%">

</div>

---

## 📖 Overview

Type in a movie you like and the app will:

1. **Recommend** the 10 most similar movies from a dataset of roughly 6,000 titles, using content-based filtering on director, lead cast and genres.
2. **Enrich** each result with posters, genres, ratings, runtime, overview and cast biographies from [TMDB](https://www.themoviedb.org/).
3. **Analyse** user reviews scraped from IMDb and label each one as **Good** or **Bad** with a trained NLP sentiment model.

## ✨ Features

| Feature | Description |
|---|---|
| 🔎 Smart search | Auto-complete suggestions built from the movie dataset |
| 🤝 Content-based recommendations | `CountVectorizer` + cosine similarity over director, top 3 actors and genres |
| 🎭 Cast & movie details | Posters, cast profiles, birthdays, birthplaces and biographies |
| 💬 Review sentiment | IMDb reviews classified as Good / Bad by a pre-trained model |
| 🐳 Docker support | Ships with a `Dockerfile` for containerised runs |
| 📦 Reproducible pipeline | DVC for data and artifact versioning |

## 🧠 How It Works

```
Browser (JS) ──► TMDB API ──► movie, cast & poster details
     │
     ├──► Flask /similarity ──► cosine similarity on main_data.csv ──► Top 10 similar titles
     │
     └──► Flask /recommend  ──► IMDb reviews (BeautifulSoup) ──► Sentiment model ──► Results page
```

- **Recommendation engine** – director, actors and genres are combined into a single `comb` text field, vectorised with `CountVectorizer` and compared using cosine similarity. The requested movie is excluded and the 10 closest matches are returned.
- **Sentiment analysis** – each scraped review is transformed with a saved vectorizer (`tranform.pkl`) and classified by a saved model (`nlp_model.pkl`).
- **Front end** – `static/autocomplete.js` powers search suggestions and `static/recommend.js` calls TMDB and posts the collected details to Flask.

## 📁 Project Structure

```
.
├── app.py                       # Flask application
├── Artifacts/                   # Dataset and trained models
│   ├── main_data.csv            #   movie metadata + combined features
│   ├── movies.csv
│   ├── reviews.txt
│   ├── nlp_model.pkl            #   sentiment classifier
│   └── tranform.pkl             #   fitted text vectorizer
├── NoteBook_Experiments/        # Experiments
│   ├── Exploratory Data Analysis.ipynb
│   ├── Movie Recommendation System.ipynb
│   └── Sentimental Analysis on Reviews.ipynb
├── static/                      # autocomplete.js, recommend.js, style.css
├── templates/                   # home.html, recommend.html
├── .dvc/                        # DVC configuration
├── infographic.svg              # Project infographic
├── Dockerfile
├── requirements.txt
└── template.py                  # Project scaffolding script
```

## 🛠️ Tech Stack

Flask · scikit-learn · Pandas · NumPy · SciPy · NLTK · BeautifulSoup4 · lxml · tmdbv3api · Docker · DVC

## 🚀 Getting Started

### Option 1 — Run locally

```bash
# 1. Clone the repository
git clone https://github.com/Lakshyadu/Movie-Recommendation-System.git
cd Movie-Recommendation-System

# 2. (Recommended) Create and activate a virtual environment
conda create -p venv python=3.8 -y
conda activate ./venv

# 3. Install dependencies
pip install -r requirements.txt

# 4. Start the app
python app.py
```

Then open **http://localhost:5000** in your browser.

### Option 2 — Run with Docker

```bash
docker build -t movie-recommender .
docker run -p 5000:5000 movie-recommender
```

Then open **http://localhost:5000**.

### 🔑 TMDB API key

Movie details are fetched from TMDB in `static/recommend.js`. Create a free key at [themoviedb.org](https://www.themoviedb.org/settings/api) and set it as `my_api_key` in that file before deploying your own copy.

## 🔌 API Endpoints

| Route | Method | Purpose |
|---|---|---|
| `/` , `/home` | GET | Home page with search and auto-complete |
| `/similarity` | POST | Returns the 10 most similar movies for a given title |
| `/recommend` | POST | Renders the results page with details, cast and review sentiment |

## 🗺️ Roadmap

- [ ] Move the TMDB API key and other settings into environment variables
- [ ] Cache IMDb reviews to reduce scraping latency
- [ ] Add collaborative filtering and a hybrid recommender
- [ ] Add automated tests and CI

## 🤝 Contributing

Contributions are welcome!

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m "Add AmazingFeature"`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

You can also open an issue with the `enhancement` tag.

## 📄 License

Distributed under the **GNU General Public License v3.0**. See [`LICENSE`](LICENSE) for details.

<div align="center">⭐ If you find this project useful, please give it a star!</div>
