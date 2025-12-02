# 🎵 Data-Driven Songwriting: Predicting Song Popularity with Machine Learning

This project is based on my MSc Business Analytics dissertation:  
**“Data-Driven Songwriting: Using Text Mining and Audio Analysis to Forecast Music Preferences or Genres.”**   

Using a dataset of **22,000+ songs from Spotify**, I built a machine learning pipeline to predict song popularity by combining **audio features, genre, lyrical mood, and seasonal trends**.

---

## 🎯 Objectives

- Identify the **musical features** (e.g. energy, danceability, valence, tempo) that most strongly influence popularity.   
- Analyse **genre-specific** and **seasonal** patterns in song success.  
- Classify **lyrical mood** using text mining and pre-trained NLP models.   
- Build and validate a **Random Forest model** to predict popularity and provide recommendations for artists and producers.

---

## 📊 Dataset

- Source: Spotify API + lyrics from Genius API (via a HuggingFace dataset uploaded in Dec 2023).   
- Time period: Songs released between **2018-01-01 and 2023-12-01**.   
- Size: ~114,000 raw tracks → filtered to ~22,000 for modelling.
- Key features:
  - Popularity (0–100)
  - Audio features: energy, danceability, valence, tempo, loudness, acousticness, instrumentalness, speechiness, liveness, duration_ms, time_signature, key, mode   
  - Engineered features:
    - **sub_genre** (112 Spotify genres grouped into ~14 broader sub-genres)   
    - **quarter** of release (Q1–Q4)
    - **season** (Winter/Spring, Spring/Summer, Summer/Fall, Fall/Winter)   
    - **scale** = musical key + major/minor (C major, G major, etc.)   
    - **mood** from lyrics (13 emotion classes such as joy, sadness, triumph, anxiety, etc.)   
    - **tier**: popularity tier 1–3 based on Spotify score.

---

## 🧹 Preprocessing & Feature Engineering

Main steps:

- Filtered dataset to songs from **2018 onwards**.   
- Retrieved **exact release dates** and **lyrics** via APIs.  
- Cleaned lyrics:
  - Removed contributor names, translation notes, tags like `[Chorus]`, `[Verse]`, `[Intro]`, and embed codes/numbers.   
- Grouped 112 Spotify genres into broader **sub-genres** such as Pop, Rock, Latin, Hip-Hop, Electronic, R&B, Jazz, Country, Classical, Folk, World, Alternative, etc.   
- Created:
  - `quarter` and `season` based on release date.   
  - `scale` from key (0–11) + mode (major/minor) → e.g. C Major, D# Minor.   
- Attempted several **alternative popularity scores** (Recency & Popularity Index, Piecewise Linear Decay, Time Bins model) but cross-validation showed poor performance (negative R²), so the original Spotify popularity metric was retained.   

---

## 🔍 Exploratory Data Analysis (EDA)

Highlights:   

- **Descriptive statistics** for all numeric features (popularity, energy, danceability, tempo, etc.)  
- **Skewness & kurtosis analysis** to understand distribution shapes and outliers.  
- Frequency plots for:
  - sub_genre distribution (Electronic & Rock dominant, Hip-Hop & World underrepresented)
  - musical scales (C, G, D Major most common)
  - release quarter (release spike in Q4).  
- Popularity tier analysis (Tier 1 = very popular, Tier 3 = low popularity).  

---

## 🧠 Modelling

Target variable:  
- Either **continuous popularity score** or **tiered classification** (depending on version).

Models explored:

- Baseline: simple regression / basic ML model  
- Main model: **Random Forest**  
- Other models: Gradient methods / alternative baselines (not all code may be in this repo yet).

Pipeline:

1. Train–test split  
2. Feature scaling / encoding where needed  
3. Model training & hyperparameter tuning  
4. Feature importance analysis  
5. K-fold cross validation (5-fold)   

Key findings:

- **Energy, danceability, and valence** emerged as the strongest predictors of popularity.   
- Seasonal trends: energetic, danceable, positive-valence songs perform especially well in **Spring/Summer (Q2)**.   
- Genre and mood interact with season (e.g. introspective moods more common in Fall/Winter).   

---

## 🛠 Tech Stack

- Python  
- Pandas, NumPy  
- Scikit-Learn  
- Matplotlib, Seaborn  
- Jupyter Notebook  
- (NLP) HuggingFace models for emotion classification  

---

## 📬 Contact

Questions about the project or dataset?  
📧 **budhaditydasfall@gmail.com**  
🔗 [LinkedIn](https://www.linkedin.com/in/dasbudhaditya/)
