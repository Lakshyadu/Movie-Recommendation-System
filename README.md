<div align="center">

# 🎬 End-to-End Movie Recommendation System

**Content-based movie recommendations, rich cast details and review sentiment analysis, served through a Flask web app.**

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Web%20App-000000?logo=flask&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.2.2-F7931E?logo=scikitlearn&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)
![License](https://img.shields.io/badge/License-GPL%20v3-blue)

<img src="infographic.svg" alt="Project infographic: how the recommendation system works" width="100%">

</div>

---

## 📖 Overview

This project helps users discover movies they are likely to enjoy. Enter a movie title and the app will:

1. **Recommend** the 10 most similar movies using content-based filtering.
2. **Enrich** the result with posters, genres, ratings, runtime, overview and cast biographies from [TMDB](https://www.themoviedb.org/).
3. **Analyse** user reviews scraped from IMDb and label each one as **Good** or **Bad** using a trained NLP sentiment model.

## ✨ Features

| Feature | Description |
|---|---|
| 🔎 Smart search | Auto-complete suggestions built from the movie dataset |
| 🤝 Content-based recommendations | `CountVectorizer` + cosine similarity over combined movie metadata |
| 🎭 Cast & movie details | Posters, cast profiles, birthdays, birthplaces and biographies |
| 💬 Review sentiment | IMDb reviews classified as Good / Bad by a pre-trained model |
| 🐳 Docker support | One-command deployment from DockerHub |
| 📦 Reproducible pipeline | DVC for data and artifact versioning |

## 🧠 How It Works

```
User ─► Flask (/similarity) ─► Cosine similarity on main_data.csv ─► Top 10 similar titles
     └► Flask (/recommend)  ─► TMDB details + IMDb reviews ─► Sentiment model ─► Results page
```

- **Recommendation engine** – movie metadata is combined into a single `comb` text field, vectorised with `CountVectorizer`, and compared with cosine similarity. The requested movie is excluded and the next 10 closest matches are returned.
- **Sentiment analysis** – each scraped review is transformed with a saved vectorizer (`tranform.pkl`) and classified by a saved model (`nlp_model.pkl`).

## 📁 Project Structure

```
.
├── app.py                      # Flask application
├── Artifacts/                  # main_data.csv, nlp_model.pkl, tranform.pkl
├── NoteBook_Experiments/       # Recommendation & sentiment analysis notebooks
├── static/                     # CSS / JS assets
├── templates/                  # HTML templates (home, recommend)
├── infographic.svg             # Project infographic
├── Dockerfile
├── requirements.txt
└── template.py                 # Project scaffolding script
```

## 🛠️ Tech Stack

Flask · scikit-learn · Pandas · NumPy · SciPy · NLTK · BeautifulSoup4 · lxml · tmdbv3api · Docker · DVC

## 🚀 Getting Started

### Option 1 — Run locally

```bash
# 1. Clone the repository
git clone https://github.com/KalyanMurapaka45/End-to-End-Movie-Recommendation-System.git
cd End-to-End-Movie-Recommendation-System

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
docker pull kalyan45/movierecommend-app
docker run -p 5000:5000 kalyan45/movierecommend-app
```

Then open **http://localhost:5000**.

## 🔌 API Endpoints

| Route | Method | Purpose |
|---|---|---|
| `/` , `/home` | GET | Home page with search and auto-complete |
| `/similarity` | POST | Returns the 10 most similar movies for a given title |
| `/recommend` | POST | Renders the results page with details, cast and review sentiment |

## 🗺️ Roadmap

- [ ] Cache IMDb reviews to reduce scraping latency
- [ ] Add collaborative filtering and a hybrid recommender
- [ ] Add automated tests and CI
- [ ] Move configuration (API keys, ports) to environment variables

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

## 🙏 Acknowledgements

- [TMDB](https://www.themoviedb.org/) for movie and cast metadata
- [IMDb](https://www.imdb.com/) for user reviews
- The open-source maintainers of Flask, scikit-learn, Pandas, NLTK and the rest of the stack

---

<div align="center">⭐ If you find this project useful, please give it a star!</div>
