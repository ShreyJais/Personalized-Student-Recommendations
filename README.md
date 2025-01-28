# Personalized-Student-Recommendations
Develop a Python-based solution to analyze quiz performance and provide students with personalized recommendations to improve their preparation.

## Project Overview

This Python project provides personalized study recommendations for students based on their quiz performance. It analyzes data from two sources: a current quiz submission and historical quiz data. The project identifies weak areas, improvement trends, and performance gaps, and it suggests actions to improve future performance.

## Data Overview

This project works with three datasets obtained from API endpoints,

1. Current Quiz Data
Details of a user’s latest quiz submission, including questions, topics, and responses, etc. 
* Quiz Endpoint Data :  https://jsonkeeper.com/b/LLQT
* Quiz Submission Data : https://api.jsonserve.com/rJvd7g

2. Historical Quiz Data 
Performance data from the last 5 quizzes for each user, including scores and  response map (Key:Question Id, Value: Selected option id).
* API Endpoint : https://api.jsonserve.com/XgAgFJ

## Setup Instructions

### Prerequisites

*   Python 3.6 or higher
*   `requests` library
*   `pandas` library
*   `json` library
*   `matplotlib` library

### Installation

1.  **Install the required packages:**

    ```bash
    pip install requests pandas matplotlib json plotly
    ```
3. Get the latest data by executing the program, or update the data in the api endpoints used.

### Running the Script

1.  Navigate to the project directory.
2.  Run the Python notebook

## Approach Description

The project is structured as follows:

1.  **Data Extraction:**
    *   Fetches data from the three API endpoints using the `requests` library.
    *   Handles potential errors during API requests.

2.  **Data Transformation and Cleaning:**
    *   Converts the fetched JSON data into Pandas DataFrames using `json_normalize`.
    *   Drops duplicate rows.
    *   Removes columns that are all null.
    *   Converts relevant date/time columns to the correct format.
    * Fills null values in the `detailed_solution` column with "NA".

3.  **Feature Engineering**
    * Calculates the `score_percentage` by dividing correct questions over total questions and multiply by 100
    * Extracts `quiz_duration_seconds` by calculating difference from started and ended time for `currentQuizSubmission` and parses string with format 'minutes:seconds' to seconds for  `HistoricalQuiz` DataFrame.

4. **Data Analysis:**
   *   Calculates descriptive statistics on the `currentQuizSubmission` such as mean scores, incorrect/correct answers count and time spent on the most recent quiz.
   *   Analyzes question wise performance of the current quiz by inspecting user's responses.
   *   Groups the `HistoricalQuiz` data by quiz ID, calculating average scores, average score percentages and average time taken.
   *   Analyzes the historical performance trends to check how the student is improving with their studies over multiple submissions.
   *   Identifies the best and worst performing quizes based on mean scores, and accuracy, and the fastest quiz completed based on duration.

6. **Recommendation Generation:**
   *   Recommends focusing on topics where the student had incorrect answers in the current quiz
   *   Recommends retaking the quiz with the lowest score.
   *   Suggests actions to improve pace or accuracy based on the mean time spent and accuracy.
7. **Visualizations**
   * Creates a bar chart of the questions where the student made a mistake on the recent quiz
   * Creates a line plot of Score percentages vs submitted dates for all the quizzes
   * Creates scatter plot of Time taken vs score percentage.

## Recomandations Example output:
<img width="674" alt="Screenshot 2025-01-28 at 7 34 00 PM" src="https://github.com/user-attachments/assets/69c16291-a67f-44e6-8830-5e72f759a889" />

## Notes
* The data comes from various API end points
* You may need to regenerate data or have up to date data in API end points for the program to work correctly
