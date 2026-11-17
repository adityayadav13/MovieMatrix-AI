MovieMatrix AI — Content-Based Movie Recommendation System
MovieMatrix AI is a content-based movie recommendation application that suggests films similar to a movie selected by the user. It combines movie metadata processing, text vectorization, cosine-similarity-based retrieval, and a Streamlit interface with movie posters.

Live Demo
Try MovieMatrix AI: https://moviematrixai-gidrmtyojwsyhzue2eytyp.streamlit.app/

Repository
GitHub — adityayadav13/MovieMatrix-AI

Project Overview
The recommender represents each movie through a combined text description (tags) created from movie metadata. It converts these tags into numerical feature vectors using Scikit-learn's CountVectorizer and compares movies using cosine similarity. For a selected title, the application retrieves a ranked set of similar movies and displays the top six recommendations.

The project notebook works with the TMDB 5000 Movies and Credits datasets and demonstrates the content-processing and similarity workflow on approximately 4,800 movie records.

How It Works
Data preparation: Movie and credits data are loaded and combined for feature preparation.
Tag construction: Relevant descriptive information, such as overview, genres, keywords, cast, and crew, is combined into a text representation for each movie.
Text vectorization: CountVectorizer converts the movie tags into a sparse bag-of-words feature representation, configured with up to 5,000 features and English stop-word removal.
Similarity calculation: Cosine similarity is used to measure similarity between movie vectors.
Recommendation retrieval: The system selects the most similar movie entries for the chosen title.
Poster retrieval and display: The Streamlit application uses TMDB movie IDs to retrieve poster images and displays six recommended titles.
Technology Stack
Python — core implementation
Pandas / NumPy — data processing
Scikit-learn — CountVectorizer and cosine similarity
Streamlit — interactive web application
TMDB API — movie poster metadata and images
Pickle — persistence of processed movie data and recommendation artefacts
Requests — HTTP requests with retry handling for poster retrieval
Application Features
Select a movie from the available catalogue.
Retrieve six content-similar movie recommendations.
View recommendations with poster images.
Use a browser-based Streamlit interface without needing to run the notebook.
Repository Structure
MovieMatrix-AI/
├── app.py
├── requirements.txt
├── Movie Recommendation.ipynb
├── movie_list (1).pkl
├── similarity (1).pkl
└── movie_recomendation/
    ├── app.py
    ├── requirements.txt
    ├── Movie Recommendation.ipynb
    ├── movie_list (1).pkl
    └── similarity (1).pkl
The repository currently contains duplicate copies of the application, notebook, and model artefacts in the root directory and the movie_recomendation/ subdirectory. The app code loads the serialized artefacts by relative path, so run it from the directory containing the corresponding files.

Run Locally
1. Clone the repository
git clone https://github.com/adityayadav13/MovieMatrix-AI.git
cd MovieMatrix-AI
2. Create a virtual environment
python -m venv venv
Activate it:

Windows

venv\Scripts\activate
macOS / Linux

source venv/bin/activate
3. Install dependencies
pip install -r requirements.txt
4. Configure the TMDB API key
The application retrieves poster information using TMDB. Store your TMDB API key in an environment variable rather than hard-coding it in the source code.

For example, on macOS / Linux:

export TMDB_API_KEY="your_api_key"
On Windows PowerShell:

$env:TMDB_API_KEY="your_api_key"
Update the application to read this value using os.getenv("TMDB_API_KEY") before running locally. The currently committed code contains an API key literal; rotate that key in the TMDB account and remove it from the repository history if it is active.

5. Start the application
From the directory containing app.py and the .pkl files:

streamlit run app.py
Streamlit will print a local URL, typically http://localhost:8501.

Recommendation Method
MovieMatrix AI uses a content-based filtering approach. It recommends movies based on similarity between their descriptive metadata rather than user ratings or collaborative interaction histories.

Cosine similarity between two feature vectors 
A
A and 
B
B is:

cosine
⁡
(
A
,
B
)
=
A
⋅
B
∥
A
∥
∥
B
∥
cosine(A,B)= 
∥A∥∥B∥
A⋅B
​
 
A higher cosine similarity indicates that the two movie tag vectors point in a more similar direction in the feature space.

Current Scope and Limitations
The system is content-based; it does not learn user preferences from viewing histories or ratings.
Recommendations depend on the metadata and vocabulary represented in the prepared movie tags.
The current interface returns six recommendations and does not expose similarity scores or explanations for each recommendation.
The repository does not currently report offline recommendation-quality metrics such as Precision@K, Recall@K, MAP@K, or NDCG@K. No recommendation-accuracy claim is made here.
The current app loads precomputed pickle artefacts; the notebook documents the feature-generation workflow.
Possible Future Improvements
Evaluate recommendation quality using a suitable relevance definition and metrics such as Precision@K, Recall@K, MAP@K, and NDCG@K.
Add explanations showing which genres, keywords, cast members, or themes contributed to a recommendation.
Add filters for genre, release year, language, or rating.
Compare bag-of-words features with TF-IDF and embedding-based representations.
Add a hybrid recommendation approach that combines content similarity with user ratings or interaction history.
Cache poster lookups and recommendation results to reduce repeated API requests.
Move API credentials to environment variables or Streamlit secrets and add input validation and automated tests.
Author
Aditya Yadav

GitHub: https://github.com/adityayadav13




