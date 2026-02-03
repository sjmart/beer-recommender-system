# Analytics for Unstructured Data: Crowdsourced Beer Recommender System

## 📌 Project Overview
The objective of this project was to build a crowdsourced recommender system for craft beers. By analyzing thousands of user-generated reviews from BeerAdvocate, the system identifies key product attributes and recommends the top 3 beers that best match a user's specific flavor preferences.

This project demonstrates proficiency in **Web Scraping**, **Statistical Linguistics (Zipf's Law)**, **Natural Language Processing (NLP)**, and **Unsupervised Machine Learning**.

---

## 🚀 The Workflow
### 1. Data Acquisition
* **Scraping:** Developed a custom automated scraper using **Selenium** and **BeautifulSoup** to extract ~10,000 reviews for the top 250 beers on BeerAdvocate.
* **Output:** A structured dataset containing product names, text reviews, and numerical ratings.

### 2. Exploratory Data Analysis (Zipf's Law)
* Verified the natural language distribution of the review corpus using Zipf's Law.
* **Results:** The calculated **Theta estimate (~ -1.008)** with a p-value of 0 confirmed that the word frequency follows a power-law distribution, validating the dataset's representativeness.

### 3. Attribute Discovery & Lift Analysis
* **Extraction:** Utilized **spaCy** for Part-of-Speech (POS) tagging to extract meaningful Adjective-Noun and Noun-Noun pairs (e.g., "dark chocolate," "roasted malt").
* **Validation:** Applied **Lift Analysis** to filter for attributes that were not only frequent but highly descriptive of specific beer styles.
* **Selected User Attributes:** `dark chocolate`, `tropical fruit`, and `roasted malt`.

### 4. Recommendation Modeling
Two distinct NLP strategies were compared:
* **Bag-of-Words (Baseline):** Represented reviews using **TF-IDF** and calculated **Cosine Similarity** between the user’s attributes and the review corpus.
* **Sentiment Integration:** Leveraged the **VADER** sentiment analyzer to weight similarity scores. This ensures that a beer is recommended only if the relevant attributes are mentioned in a *positive* context.
* **Custom Word Embeddings:** Trained a domain-specific **Word2Vec (Skip-gram)** model using Gensim to capture semantic relationships that pre-trained models might miss in a niche craft beer context.

---

## 📊 Key Results
### Top 3 Recommendations (Bag-of-Words Model)
Based on the attributes: *Dark Chocolate*, *Tropical Fruit*, and *Roasted Malt*.

| Rank | Beer Name | Similarity Score | Sentiment Score |
| :--- | :--- | :--- | :--- |
| 1 | **All That Is And All That Ever Will Be** | 0.096 | 0.907 |
| 2 | **Triple Shot** | 0.090 | 0.899 |
| 3 | **Double Shot** | 0.090 | 0.921 |

### Critical Analysis
* **Attribute Match vs. General Popularity:** Our analysis showed that the top 3 recommended beers (based on flavor similarity) were entirely different from the top 3 highest-rated beers in the dataset (e.g., *10 Year Barleywine*). This justifies the need for an attribute-based recommender over a simple popularity-based baseline.
* **Word Vectors:** Using custom **Word2Vec** embeddings shifted recommendations toward beers with semantic similarity (e.g., *Peche Du Fermier*), capturing latent features that literal word-matching might overlook.

---

## 🛠 Tech Stack
* **Language:** Python 3.11
* **Libraries:** Pandas, NumPy, Scikit-Learn (TF-IDF, Cosine Similarity)
* **NLP:** spaCy, NLTK, Gensim (Word2Vec), VADER Sentiment
* **Scraping:** Selenium, BeautifulSoup4
* **Visualization:** Matplotlib, Seaborn

