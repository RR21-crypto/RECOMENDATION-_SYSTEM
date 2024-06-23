# Machine Learning Project Report - Rayhan Gibrani Uhum


## Project Overview

With the rise of live streaming services like Disney Plus, Netflix, and others, viewers have more options than ever before. Sometimes, after watching a film, viewers want to watch another film with similar characteristics. Therefore, this project aims to help viewers/movie enthusiasts enjoy new series or films after finishing their favorite series.

## Business Understanding

As discussed in the previous section, this system will make it easier for users to find films or series that match their preferences. Additionally, this system benefits both users and service providers.

### Problem Statements

- How to provide film recommendations that are relevant and match user preferences and user behavior ratings.
- How to evaluate the relevance of the recommendation model to user behavior and ratings from other users.

### Goals

The goals of this project are as follows:

- To understand how to identify films relevant to users and evaluate the model.
- To provide relevant recommendations based on user preferences and other users' ratings.

### Solution Statements

After outlining the problem statement and goals, the solutions proposed in this project are as follows:

- Perform data exploration, cleaning, and feature selection for the recommendation model.
- Use two techniques: Content-Based Filtering and Collaborative Filtering. These methods are highly relevant for recommending films as users tend to look at genres and ratings.

## Data Understanding

This project uses the MovieLens dataset, which is specifically for learning purposes. It contains 100,000 ratings, 3,600 tags, and 9,000 films. The dataset can be downloaded from the following link:

[MovieLens Dataset](https://grouplens.org/datasets/movielens/)

The project includes several files, such as movies, ratings, links, and tags. Each file represents something specific:

- **movies.csv**: contains a list of movies and their genres.
- **ratings.csv**: contains user ratings and values according to the movieId feature.
- **tags.csv**: contains tags and timestamps where users stopped or clicked.
- **links.csv**: contains links to the movies.

Below are the explanations for each feature in the dataset:

- movies.csv

  | Feature | Description |
  | --- | --- |
  | movieId | ID for each movie |
  | title | Movie title |
  | genre | Movie genre |

- ratings.csv

  | Feature | Description |
  | --- | --- |
  | userId | ID for each user |
  | movieId | Movie ID |
  | rating | User rating on a scale from 1 to 5 |
  | timestamp | Timestamp |

- tags.csv

  | Feature | Description |
  | --- | --- |
  | userId | User ID |
  | movieId | Movie ID |
  | tag | Movie tag |
  | timestamp | Timestamp |

- links.csv

  | Feature | Description |
  | --- | --- |
  | movieId | Movie ID |
  | imdbId | IMDb ID |
  | tmbId | TMDB ID |

**Additional Criteria (Optional)**:
- Perform several steps to understand the data, such as data visualization techniques and exploratory data analysis.

## Data Preparation

Several steps were taken to complete this project, including data cleaning, handling missing values, and data reduction. The first step was merging **movies.csv** and **ratings.csv**. The choice of these two files relates closely to the recommendation methods used in this project, i.e., user-based filtering and collaborative filtering.

### Data Cleaning on the Title Feature

After merging **movies.csv** and **ratings.csv** into a variable named **films**, the first noticeable issue in the dataset was the presence of release years in the title feature. Therefore, the title feature was simplified by removing the release years and moving them to a new feature named **release_year**. This makes the model easier to understand and avoids redundancy caused by having both numbers and letters in the same feature.

### Data Cleaning on the Ratings Feature

After data cleaning, attention was given to the rating values. It was found that the rating scale did not use whole numbers. Hence, the ratings were converted to whole numbers to make it easier for users to understand the quality of a film.

### Data Cleaning on the Timestamps Feature

The timestamp values in the rating feature were difficult to understand. Therefore, they were converted into a more readable format (year, date, and month).

### Handling Missing Values

After cleaning the data in the **films** variable, the next step was to check for completeness and the presence of null values. The dataset had some missing values, as shown below:

| Feature | Missing Values |
| --- | --- |
| release_year | 17 |
| userId | 18 |
| rating | 18 |
| timestamp | 18 |

Given the small number of missing values compared to the total data (100,000 ratings, 3,600 tags, and 9,000 films), the most efficient way to handle them was by removing the rows with missing values.

**Additional Criteria (Optional)**:
- Explain the data preparation process.
- Justify the necessity of the data preparation steps.

## Modeling

To solve the previously mentioned issues, this project offers two solutions: Content-Based Filtering and Collaborative Filtering. Both solutions have their advantages and disadvantages. The following sections explain how these methods address the problems.

### Content-Based Filtering

This method learns a user's interest profile based on data from items the user has rated. It works by recommending items similar to those the user liked in the past or is currently viewing. While more data improves this method, it has its strengths and weaknesses:

**Advantages of Content-Based Filtering**:
- Personalization: Provides highly personalized recommendations based on known user preferences.
- No Need for Other Users' Data: Does not require data from other users, beneficial when user data is limited or unavailable.
- Transparency: More transparent than collaborative methods; recommendations can be explained by referring to item features the user likes.
- Handles New Items Well: Works well with new items, even without collaborative data, since recommendations are based on item characteristics.

**Disadvantages of Content-Based Filtering**:
- Limited Recommendations: Restricts recommendations to items similar to those already consumed, reducing the likelihood of discovering diverse content.
- Limited Understanding of Complex Preferences: May struggle to capture complex or varied preferences, making it harder to recommend different items.
- Data Dependency: Highly dependent on the quality and completeness of item attribute data, which can affect recommendation quality.
- Over-Specialization: Risks being overly specific, leading to similar recommendations.
- Lack of Diversity: Tends to offer less varied recommendations due to focusing on similar items.

### Preparing Variables

The first step is to create a variable from the preprocessed data using the `tolist` command to create a variable named `data`. This variable is then renamed to `saringan` for easier model processing.

### TF-IDF Vectorizer

Next, we use the TF-IDF Vectorizer from the sklearn library. The `TfidfVectorizer()` function converts the variable into a matrix showing the correlation between films and their genres.

| Title | Horror | Thriller | Western | Drama | Adventure |
| --- | --- | --- | --- | --- | --- |
| Woyzeck | 0.0 | 0.0 | 0.0 | 1.0000 | 0.0 |
| Play the Game | 0.0 | 0.0 | 0.0 | 1.0000 | 0.0 |
| Character | 0.0 | 0.0 | 0.0 | 1.0000 | 0.0 |
| Wild Oats | 0.0 | 0.0 | 0.0 | 0.0000 | 0.0 |
| Too Late for Tears | 0.0 | 0.264118 | 0.0 | 0.180515 | 0.0 |

This step discusses the recommendation system model created to solve the problem. The top-N recommendations are presented as output.

### Cosine Similarity

Next, we use Cosine Similarity to calculate the degree of similarity between film titles and their genres. This calculation is crucial in content-based filtering as it applies the principle of item similarity to provide recommendations. The cosine similarity output is converted to a dataframe, as shown below.

![cosine similarity](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/2617a4d9-291a-417d-824a-cecdeebb01fe)

From the image above, the resulting matrix is 9708 x 9708, showing similarities between films. For example, the films _George Carlin: Jammin' in New York_ and _Oh, God! Book II_ have a similarity value of 1.0, indicating a high level of similarity based on their genres. Hence, the model can recommend these films interchangeably.

### Creating a Custom Function

This step involves creating a custom function to display the recommendation system results based on the previous model. The function uses the preprocessed data within a defined similarity range. The function outputs the recommendations by removing the user-requested film from the list and displaying recommendations based on a value **K**, which is 8 in this project.

![custom function](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/45a3533e-9990-4f8a-acae-ee1158cc0ba0)

### Recommendations

In the final step, the recommendations are obtained. First, check if the user-requested film title exists in the list, as shown below.

| No | Title | Genre | ID |
| --- | --- | --- | --- |
| 1 | Oh, God! Book II | Comedy | 5213 |

Then, the user can view the film recommendations using the function:

| No | Title | Genre |
| --- | --- | --- |
| 1 | Andrew Dice Clay: Dice Rules | Comedy |
| 2 | Made | Comedy |
| 3 | Carry On Don't Lose Your Head | Comedy |
| 4 | Jack and Jill | Comedy |
| 5 | Dr. Goldfoot and the Bikini Machine | Comedy |
| 6 | Broadway Danny Rose | Comedy |
| 7 | Zelig | Comedy |
| 8 | Big Business | Comedy |

The model recommends 8 film titles, all with the same genre, comedy.

## Model Development with Collaborative Filtering

This project involves several steps to achieve the desired results. Collaborative Filtering has its strengths and weaknesses:

**Advantages**:
- Serendipitous Recommendations: Provides highly relevant recommendations based on similar preferences with other users.
- No Need for Detailed Item Information: Useful when there is insufficient descriptive information about items.
- Handles Data Changes Well: Can adapt to new items or changing user preferences.
- Effective for Retail Items: Suitable for recommending retail items like e-commerce products, films, or music based on user behavior.

**Disadvantages**:
- Cold Start Problem: Less effective when there is little or no user or item behavior data.
- Scalability Issues: Similarity calculations can be computationally expensive for large platforms.
- Over-Specialization Risk: Can become overly specific, especially with limited training data.
- Privacy Concerns: Must consider privacy issues, especially in user-based collaborative filtering.

The following steps explain the process to obtain recommendations:

### Data Preparation

Use the `ratings.csv` file and store it in the variable **dd**. Format the ratings and timestamp values appropriately.

### Split Data for Training and Validation

Split the data into training and validation sets with an 80/20 ratio. This split ensures that the data used to develop the model and evaluate its performance is balanced.

### Training Process

The model calculates user and item embeddings with dot product between titles and genres on a [0, 1] scale and sigmoid activation. The model is compiled using BinaryCrossentropy for the loss function, Adam optimizer, and RMSE for evaluation metrics. The training process runs for 100 epochs with a callback to stop if RMSE is below 0.1, saving time due to extensive training.

### Metric Visualization

This step visualizes the training model results, showing RMSE differences between train and test sets. The graph and numbers will be discussed in the evaluation metrics section.

### Obtaining Recommendations

After completing the training and preparation steps, obtain the recommendation results using the custom function. The recommendations are displayed as shown below.

![recommendations](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/77304be7-a756-44f1-bb2a-264046423ba2)

## Evaluation

The next step is to evaluate the model performance. This project uses two methods, which are evaluated individually.

### Evaluation of Content-Based Filtering

This method uses precision metrics with cosine similarity. The cosine similarity can be calculated manually using the formula below:

![cosine similarity formula](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/1d685c64-3840-4bd0-b419-5cf2dce37948)

The similarity metric is illustrated as follows:

![similarity illustration](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/86599dca-8e81-4da1-8db8-70ccc0cac446)

Next, calculate precision using the formula below:

![precision formula](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/fa79d7ae-94d7-47bb-a4fe-0f41e90c03b8)

The user requests recommendations for the film _Oh, God! Book II_ with the comedy genre.

| No | Title | Genre | ID |
| --- | --- | --- | --- |
| 1 | Oh, God! Book II | Comedy | 5213 |

The recommendations provided by the model are:

| No | Title | Genre |
| --- | --- | --- |
| 1 | Andrew Dice Clay: Dice Rules | Comedy |
| 2 | Made | Comedy |
| 3 | Carry On Don't Lose Your Head | Comedy |
| 4 | Jack and Jill | Comedy |
| 5 | Dr. Goldfoot and the Bikini Machine | Comedy |
| 6 | Broadway Danny Rose | Comedy |
| 7 | Zelig | Comedy |
| 8 | Big Business | Comedy |

To evaluate the model, use the precision metric:

Precision = # of relevant recommendations / # of recommendations made.

For the above recommendations:
Precision = 8 / 8 = 100%

The precision of 8/8 is derived from the genre the user wanted. The comedy genre in _Oh, God! Book II_ matches all recommended films, resulting in a 100% precision.

### Collaborative Filtering

The performance of Collaborative Filtering is usually evaluated using RMSE (Root Mean Squared Error). RMSE is a standard method for measuring the average error of a model in predictions. Calculate RMSE by subtracting the predicted values from the observed values, squaring the result, summing all squared results, dividing by the number of data points (n), and taking the square root of the result, as shown below.

![RMSE formula](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/074c1ab5-c17c-4f7c-ae85-1b007979858b)

After understanding RMSE, this project visualizes the RMSE reduction as shown below. The trend shows a decrease in RMSE, with the final values being 0.27 for test and 0.17 for train.

![RMSE graph](https://github.com/RR21-crypto/RECOMENDATION-_SYSTEM/assets/81364035/14ade81f-72b2-4370-81f3-1c8419f14b1f)
