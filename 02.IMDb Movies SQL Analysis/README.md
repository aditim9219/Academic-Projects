# IMDb Movies SQL Analysis

## Overview

This project is an academic SQL analysis case study based on movie industry data.

The project was designed around a business scenario in which RSVP Movies, an Indian film production company, planned to enter the global market and wanted to use historical movie data to make data-informed decisions for a new project.

The analysis uses SQL to explore movie releases, genres, ratings, production houses, directors, actors, actresses, and previous movie performance. The project progresses from basic database exploration and aggregation to multi-table joins, subqueries/CTEs, window functions, ranking, conditional classification, and analytical window calculations.

> **Project Type:** Academic / SQL Data Analysis  
> **Domain:** Movies & Entertainment  
> **Database:** MySQL  
> **Primary Tool:** SQL / MySQL Workbench

---

## Business Problem

RSVP Movies traditionally produced movies primarily for the Indian audience but planned to release a movie for a global audience.

The objective of the case study was to analyze historical movie data and derive insights that could support decisions related to:

- Movie genres
- Release patterns
- Movie ratings
- Production houses
- Directors
- Actors and actresses
- Global partnerships
- Movie duration
- Gross income
- Multilingual movies

The original assignment divided the analysis into four segments, with each segment requiring SQL queries against different combinations of database tables.

---

## Objectives

The analysis aimed to:

1. Understand the structure and size of the IMDb database.
2. Identify missing values in important tables.
3. Analyze movie release trends by year and month.
4. Explore movie genres and their distribution.
5. Analyze movie duration by genre.
6. Examine movie ratings and voting patterns.
7. Identify highly rated movies.
8. Identify production houses associated with highly rated movies.
9. Analyze directors, actors, and actresses based on movie performance.
10. Compare movie performance across countries and languages.
11. Rank actors based on weighted average ratings.
12. Identify highly rated actresses in Hindi movies released in India.
13. Classify thriller movies according to rating categories.
14. Apply advanced SQL techniques such as window functions.
15. Analyze highest-grossing movies by year and genre.
16. Identify production houses associated with multilingual hits.
17. Identify actresses with the highest number of super-hit drama movies.
18. Translate SQL analysis into business-oriented insights and recommendations.

---

## Database Structure

The project uses a relational IMDb database containing six primary analytical tables:

```text
                         ┌──────────────┐
                         │    MOVIE     │
                         │              │
                         │ id           │
                         │ title        │
                         │ year         │
                         │ date_published
                         │ duration     │
                         │ country      │
                         │ languages    │
                         │ production_company
                         └──────┬───────┘
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                 │
              ▼                 ▼                 ▼
       ┌────────────┐    ┌──────────────┐   ┌────────────┐
       │   GENRE    │    │   RATINGS    │   │  DIRECTOR  │
       │            │    │              │   │  MAPPING   │
       │ movie_id   │    │ movie_id     │   │ movie_id   │
       │ genre      │    │ avg_rating   │   │ name_id    │
       └────────────┘    │ total_votes  │   └─────┬──────┘
                         │ median_rating│         │
                         └──────────────┘         │
                                                  ▼
                                           ┌────────────┐
                                           │   NAMES    │
                                           │            │
                                           │ id         │
                                           │ name       │
                                           │ height     │
                                           │ date_of_birth
                                           │ known_for_movies
                                           └────────────┘
                                │
                                ▼
                         ┌────────────┐
                         │   ROLE     │
                         │  MAPPING   │
                         │            │
                         │ movie_id   │
                         │ name_id    │
                         │ category   │
                         └────────────┘
```

The accompanying Excel workbook contains the dataset tables and an ERD illustrating the relationships between them.

---

## Dataset

The database contains the following tables:

| Table | Rows | Description |
|---|---:|---|
| `movie` | 7,997 | Movie-level information including title, year, duration, country, language and production company |
| `genre` | 14,662 | Genre associated with each movie |
| `director_mapping` | 3,867 | Mapping between movies and directors |
| `role_mapping` | 15,615 | Mapping between movies and actors/actresses |
| `names` | 25,735 | Information about directors, actors and actresses |
| `ratings` | 7,997 | Movie ratings, vote counts and median ratings |

The row counts above were obtained during the database analysis and are also documented in the SQL solution script.

---

## Analysis Workflow

The project follows four analytical segments:

```text
Database Exploration
        │
        ▼
Movie & Genre Analysis
        │
        ▼
Ratings & Production Analysis
        │
        ▼
People / Cast / Director Analysis
        │
        ▼
Advanced SQL Analysis
        │
        ▼
Business Insights & Recommendations
```

### Segment 1 — Movie & Genre Analysis

The first segment focuses on understanding the structure and basic characteristics of the database.

Topics include:

- Row counts for each table
- Null-value analysis
- Movies released by year
- Monthly release trends
- Movies produced in USA and India
- Unique genres
- Genre popularity
- Movies belonging to a single genre
- Average movie duration by genre
- Genre ranking

Some key observations from the analysis include:

- The highest number of movies in the dataset were released in 2017.
- March had the highest number of movie releases.
- 1,059 movies were produced in USA or India in 2019.
- The dataset contains 13 distinct genres.
- Drama had the highest number of movies overall.
- 3,289 movies belonged to only one genre.
- Action had the highest average movie duration among the genres analyzed.
- Thriller ranked among the top genres by number of movies.

---

## Segment 2 — Ratings & Movie Performance

The second segment focuses on movie ratings and production performance.

The analysis includes:

- Minimum and maximum rating values
- Top 10 movies by average rating
- Movie counts by median rating
- Production houses with the highest number of highly rated movies
- Genre analysis for specific release periods
- Movies beginning with `"The"`
- Median-rating analysis over a specified date range
- Comparison of German and Italian movies based on votes

The analysis found that:

- The highest-rated movies had average ratings above 9.
- Movies with a median rating of 7 were the largest group in the dataset.
- Dream Warrior Pictures and National Theatre Live had the highest number of movies with average ratings above 8.
- Thriller was among the top genres by movie count.
- German and Italian movies showed different results depending on whether language or country was used for the comparison.

---

## Segment 3 — People, Cast & Production Houses

The third segment analyzes the people and organizations associated with the movies.

The analysis includes:

- Null-value analysis in the `names` table
- Top directors in highly rated genres
- Top actors based on movies with median ratings of at least 8
- Production houses ranked by total votes
- Actors in Indian movies
- Actresses in Hindi movies released in India
- Rating-based classification of thriller movies

### Selected Findings

The analysis identified:

- **James Mangold, Soubin Shahir and Joe Russo** among the top directors within the selected high-performing genres.
- **Mammootty and Mohanlal** as the top two actors based on the specified median-rating criterion.
- **Marvel Studios, Twentieth Century Fox and Warner Bros.** as the top production houses based on total votes received by their movies.
- **Vijay Sethupathi** as the top-ranked actor under the specified weighted-average-rating criteria for Indian movies.
- **Taapsee Pannu** as the highest-ranked actress under the specified criteria for Hindi movies released in India.

The actor and actress rankings use a **weighted average rating based on total votes**, as required by the assignment.

---

## Segment 4 — Advanced SQL Analysis

The final segment applies more advanced SQL techniques to derive broader insights.

### Techniques Used

- Common Table Expressions (CTEs)
- Window functions
- `RANK()`
- `DENSE_RANK()`
- Running totals
- Moving averages
- Conditional expressions using `CASE`
- Multi-table joins
- Aggregations
- Subqueries
- Filtering and grouping
- Weighted averages

### Analyses Performed

The segment includes:

- Genre-wise running total of average movie duration
- Genre-wise moving average of average movie duration
- Five highest-grossing movies for each year within the top three genres
- Production houses with the highest number of multilingual hits
- Top actresses based on the number of super-hit drama movies

The project uses window functions to perform calculations across ordered groups while retaining row-level results.

---

## Key Business Insights

The analysis generated several insights relevant to the case-study business scenario.

### Genre

Drama was the largest genre in the dataset, while Thriller also ranked among the most frequently produced genres.

### Ratings

The majority of movies were concentrated around the middle-to-high portion of the rating scale. Highly rated movies were used as a basis for identifying successful production houses, directors and performers.

### Production Houses

Production companies were evaluated using both the number of highly rated movies and the total votes received by their movies.

### Directors

Director performance was evaluated by considering the number of highly rated movies within the top-performing genres.

### Actors & Actresses

Actor and actress rankings were based on movie performance and, where specified, weighted average ratings using total votes.

### Global / Multilingual Opportunities

The analysis also considered multilingual movies and production houses with successful multilingual releases as potential indicators for international collaboration.

---

## SQL Concepts Demonstrated

This project demonstrates SQL skills across multiple levels.

### Basic SQL

- `SELECT`
- `WHERE`
- `GROUP BY`
- `ORDER BY`
- `DISTINCT`
- `COUNT`
- `SUM`
- `AVG`
- `MIN`
- `MAX`

### Intermediate SQL

- `INNER JOIN`
- Multiple-table joins
- `CASE`
- String filtering using `LIKE`
- Date functions
- Conditional aggregation
- Subqueries
- Common Table Expressions

### Advanced SQL

- Window functions
- `RANK()`
- `DENSE_RANK()`
- Running totals
- Moving averages
- Weighted averages
- Multi-stage CTE-based analysis
- Ranking within business-defined segments

---

## Project Files

### `IMDB+question - Final.sql`

The main SQL solution file containing the assignment questions, SQL queries, comments, intermediate findings, and final analytical queries.

### `IMDB+dataset+import.sql`

SQL script used to create the `imdb` database, create the required tables, and populate the database with the movie dataset.

### `IMDb+movies+Data+and+ERD+final.xlsx`

Excel workbook containing the dataset tables and ERD used to understand the database structure and table relationships.

### `Project 2.pdf`

Original academic project/problem statement describing the business scenario, analytical requirements, database setup, and submission requirements.

### `Executive Summary and Recommendations.pdf`

Executive summary documenting the major insights and recommendations derived from the SQL analysis.

---

## How to Run the Project

### Prerequisites

- MySQL Server
- MySQL Workbench or another MySQL-compatible SQL client

### Step 1 — Create the Database

Run:

```sql
IMDB+dataset+import.sql
```

This script:

1. Creates the `imdb` database.
2. Creates the required tables.
3. Inserts the dataset into the tables.

### Step 2 — Select the Database

```sql
USE imdb;
```

### Step 3 — Run the Analysis

Open:

```text
IMDB+question - Final.sql
```

The file contains the questions followed by the SQL solutions used for the analysis.

---

## Limitations

This project is an **academic SQL analysis case study** rather than a production movie-recommendation or forecasting system.

The conclusions are based on the provided historical dataset and the specific analytical questions defined by the assignment.

The analysis does not build a machine-learning model or attempt to predict future movie performance.

Some recommendations in the original executive summary are business recommendations derived from the assignment's analytical framework and should be interpreted within that academic context.

---

## Learning Outcomes

This project provided practical experience with:

- Relational database analysis
- MySQL
- SQL query development
- Database and ERD interpretation
- Multi-table joins
- Aggregation and grouping
- Data-quality checks
- Date and string functions
- CTEs
- Window functions
- Ranking
- Running totals
- Moving averages
- Weighted averages
- Conditional classification
- Business-oriented SQL analysis
- Translating query results into recommendations

---

## Project Context

This project was completed as an academic SQL case study focused on applying SQL to a business problem in the movie and entertainment industry.

The project demonstrates progression from basic database exploration and aggregation to advanced SQL analysis involving multiple related tables, window functions, rankings, and business-oriented insights.
