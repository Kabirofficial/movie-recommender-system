# Movie Recommender System

A content-based movie recommender system that suggests movies similar to a user's selection. This project uses a dataset from TMDB 5000 and employs TF-IDF vectorization and cosine similarity to find recommendations. The application is built with Python and served using a Flask web server.

 <!-- Optional: Add a screenshot of your web app -->

## Features

-   **Content-Based Filtering:** Recommends movies based on content attributes like genre, keywords, cast, and crew.
-   **Interactive UI:** A simple web interface built with Flask and HTML to search for a movie and view recommendations.
-   **Scalable Model:** The model logic is separated from the web app, making it easy to update or retrain.

## Technology Stack

-   **Backend:** Python, Flask
-   **Machine Learning:** Pandas, NumPy, Scikit-learn
-   **Data:** [TMDB 5000 Movie Dataset from Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)

## Project Structure

```
.
├── model/
│   ├── movie_list.pkl      # Pickled dataframe of movie data
│   └── similarity.pkl      # Pickled similarity matrix
├── templates/
│   └── index.html          # Frontend HTML file
├── .gitignore              # Files to be ignored by Git
├── app.py                  # Flask web application
├── movie recommender system.ipynb # Jupyter notebook for model training
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```

## Setup and Installation

Follow these steps to set up and run the project on your local machine.

### 1. Clone the Repository

```bash
git clone https://github.com/Kabirofficial/movie-recommender-system.git
cd movie-recommender-system
```

### 2. Download the Dataset

1.  Download the **TMDB 5000 Movie Dataset** from [Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata).
2.  Extract the archive and place `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv` in the root directory of the project.

### 3. Set Up a Virtual Environment

It is recommended to create a virtual environment to manage project dependencies.

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 4. Install Dependencies

Install the required Python libraries using the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

## Usage

There are two main steps to run this project: generating the model files and running the web application.

### 1. Generate Model Files

Run the Jupyter Notebook `movie recommender system.ipynb`. This will perform the following steps:
-   Load and preprocess the raw CSV data.
-   Create a similarity matrix.
-   Save two files: `movie_list.pkl` and `similarity.pkl`.

**Important:** After running the notebook, move the generated `movie_list.pkl` and `similarity.pkl` files into the `model/` directory.

### 2. Run the Flask Web App

Once the model files are in the `model/` directory, you can start the Flask server.

```bash
python app.py
```

Open your web browser and navigate to `http://127.0.0.1:5000` to use the application.

## How It Works

The recommendation logic is based on content-based filtering:

1.  **Data Preprocessing:** The two datasets (`movies` and `credits`) are merged. Key features like `genres`, `keywords`, `cast` (top 3 actors), and `crew` (director) are extracted.
2.  **Feature Engineering:** A `tags` column is created by combining all the extracted features into a single string for each movie. This `tags` string represents the "content" of the movie.
3.  **Vectorization:** The text in the `tags` column is converted into a numerical format using **TF-IDF (Term Frequency-Inverse Document Frequency)**. Each movie is now represented as a vector in a high-dimensional space.
4.  **Similarity Calculation:** **Cosine Similarity** is used to calculate the similarity score between all pairs of movie vectors. A higher cosine similarity score means the movies are more similar in content.
5.  **Recommendation:** When a user selects a movie, the system finds its corresponding vector and returns the top 5 movies with the highest cosine similarity scores.

---# movie-recommender-system
