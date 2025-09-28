# Popular User Identification and Word Frequency Analysis using PySpark

This project demonstrates a **MapReduce-style data analysis workflow** in PySpark, applied to a large dataset of tweets.  
The analysis identifies popular Twitter users (based on follower counts) and extracts the **Top 10 most frequent words** used in their tweets.

---

##  Dataset
The dataset used is:

- **`Amazon_Responded_Oct05.csv`**
- Contains ~400,000 tweets
- The data is available on Kaggle and can be found at: https://www.kaggle.com/datasets/sirvana/amazon-responded-tweets
- Relevant columns:
  - `user_id_str`: unique identifier of the user  
  - `user_followers_count`: number of followers  
  - `text_`: the tweet text  

---

##  Objectives
1. **Identify popular users** → Users with more than 5,000 followers.  
2. **Analyze tweet content** → Extract and rank the Top 10 most frequently used words by these users.  

---

##  Workflow Steps
1. **Load and Clean the Data**
   - Load CSV into Pandas
   - Handle missing values
   - Clean tweet text (remove URLs, mentions, punctuation, numbers, lowercase)

2. **Convert to Spark DataFrame**
   - Use PySpark for distributed data processing.

3. **Handle Duplicate Users**
   - Some users appear multiple times with different follower counts.
   - Keep only the record with the **maximum follower count** for each user.

4. **Filter for Popular Users**
   - Select users with **> 5,000 followers**.

5. **Word Frequency Analysis (MapReduce Style)**
   - Convert tweet text into an RDD
   - `map` → Split tweets into words
   - `reduceByKey` → Count word frequencies
   - Extract the **Top 10 words**.

6. **Save Output**
   - Print the Top 10 most common words.
   - Save results into `/content/output.txt`.

---

##  How to Run in Google Colab
1. Open the notebook in Google Colab.  
2. Install and configure PySpark:
   ```bash
   !apt-get install openjdk-8-jdk-headless -qq > /dev/null
   !wget https://archive.apache.org/dist/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz
   !tar xf spark-3.4.0-bin-hadoop3.tgz
   !pip install -q findspark
