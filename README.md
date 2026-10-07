# DSA 4060 Personalized Movie Recommender

## Student Details
- **Name:** Hans Onesmo
- **Student ID:** 671463
- **Assigned User ID:** 24 (last two digits 63; 63 MOD 40 = 23; 23 + 1 = 24)

## Project Objective
This project builds a simple content-based movie recommender for a streaming company. It analyses the ratings of one assigned user (User 24) to identify their genre preferences. It then recommends five movies the user has not yet rated.

## Datasets
- **`movies.csv`** – movie catalogue with 36 movies and the fields `movie_id`, `title` and `genres` (genres separated by `|`).
- **`ratings.csv`** – 440 historical ratings from 40 users with the fields `user_id`, `movie_id` and `rating`.

Neither file has missing values.

## Method / Approach
1. Filtered the ratings to User 24, who rated 13 movies, and profiled their rated movies, top three movies and genre averages.
2. Treated movies rated **4.0 or higher** as "liked" (3 movies: The Pursuit of Happyness, The Social Network, Interstellar).
3. Converted genres into binary features with **`CountVectorizer`**.
4. Built a taste profile for the user as the rating-weighted average of the liked movies' genre vectors.
5. Scored every catalogue movie by **cosine similarity** to this profile, removed movies User 24 had already rated, and kept the top five. Ties were broken by the movie's average rating across all users.
6. Generated a reason for each recommendation from its most similar liked movie and shared genres.

## How to Run the Notebook
**Requirements:** Python 3, `pandas`, `numpy`, `scikit-learn`, and Jupyter or VS Code with the Jupyter extension.

1. Keep `movies.csv`, `ratings.csv` and the notebook in the same folder.
2. Open `DSA4060_Recommender_671463.ipynb` and select a Python kernel.
3. Run all cells from top to bottom (Task 1 to Task 5).

## Recommendation Results
| Rank | Recommended Movie | Genres |
|---|---|---|
| 1 | The Shawshank Redemption | Drama |
| 2 | Arrival | Sci-Fi \| Drama |
| 3 | Remember the Titans | Sports \| Drama |
| 4 | Ford v Ferrari | Sports \| Drama |
| 5 | Moneyball | Sports \| Drama |

**Interpretation:** User 24's three liked movies are all Dramas, and Drama has a 3.75 average rating (Biography 4.17), while Action, Adventure, Animation, Musical and Superhero movies all average 1.67 or lower. The recommendations therefore centre on Drama. Arrival ranks high because it shares both Drama and Sci-Fi with the liked movie Interstellar. The three Sports|Drama films follow because they share Drama with the user's favourites.

## Limitation and Suggested Improvement
- **Limitation:** The model uses only genre labels, so movies with identical genres are indistinguishable. The three Sports|Drama movies tied at 0.564 similarity and could only be separated by community average rating. The profile is also built from just three liked movies, which makes it thin.
- **Improvement:** Make it a hybrid recommender by adding collaborative filtering on top of the genre scores. Boosting movies that similar users among the other 39 rated highly would separate genre ties and add signal that genres cannot capture.