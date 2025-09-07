# CITS4407 - Assignment 2: Board Games Analysis


---

# Project Overview

This project focuses on analyzing board games from BoardGameGeek dataset: https://www.kaggle.com/datasets/andrewmvd/board-games. The original data is semicolon-separated and includes inconsistencies such as missing values, non-ASCII characters, and formatting issues.

Three shell scripts are provided:
- `empty_cells`: Checks and reports the number of empty cells per column.
- `preprocess`: Cleans the dataset and standard output.
- `analysis`: Analyzes cleaned file and answers four research questions.

---

# Scripts Description

## 1. empty_cells

Purpose:  
Detect and report the number of empty (missing) values in each column of a dataset.

Usage:  
```bash
./empty_cells <file> <separator>
```

Features:
- Accepts any separator (e.g.',' ';' )
- Uses awk to count missing fields per column
- Outputs the column name and its corresponding empty cell count

Example Output:
/ID: 0
Name: 0
Year Published: 0
Min Players: 0
Max Players: 0
Play Time: 0
Min Age: 0
Users Rated: 0
Rating Average: 0
BGG Rank: 0
Complexity Average: 0
Owned Users: 0
Mechanics: 0
Domains: 0

---

## 2. preprocess

Purpose:  
Clean and standardize the raw .txt dataset and convert it into a .tsv (tab-separated) format ready for analysis.

Usage:  
```bash
./preprocess <input_file>
```
If you want to transform to .tsv format: 
```bash
./preprocess <input_file> > <cleaned_tsv_file.tsv>
```

Features:
- Converts semicolons (;) to tab characters (\t)
- Converts Windows line endings (\r\n) to Unix (\n)
- Removes non-ASCII characters
- Converts numeric values using commas (,) to standard decimal dots (.)
- Replaces empty or invalid IDs with new unique integers

Example Output: 
```
/ID     Name    Year Published  Min Players     Max Players     Play Time       Min Age Users Rated     Rating Average  BGG Rank  Complexity Average       Owned Users     Mechanics       Domains
174430  Gloomhaven      2017    1       4       120     14      42055   8.79    1       3.86    68323   Action Queue, Action Retrieval, Campaign / Battle Card Driven, Card Play Conflict Resolution, Communication Limits, Cooperative Game, Deck Construction, Deck Bag and Pool Building, Grid Movement, Hand Management, Hexagon Grid, Legacy Game, Modular Board, Once-Per-Game Abilities, Scenario / Mission / Campaign Game, Simultaneous Action Selection, Solo / Solitaire Game, Storytelling, Variable Player Powers   Strategy Games, Thematic Games
...

```
---

## 3. analysis

Purpose:  
Analyze a cleaned .tsv file to extract insights about board games.

Usage:  
```bash
./analysis <input_file>
```

Features:
- Identifies the most frequent game mechanic and game domain
- Calculates the Pearson correlation between:
  1. Year Published and Average Rating
  2. Game Complexity and Average Rating
- Handles missing and malformed data gracefully
- Reports when insufficient data prevents correlation analysis

Example Output:
```
The most popular game mechanics is Hand Management found in 48 games  
The most popular game domain is Strategy Games found in 77 games  
The correlation between the year of publication and the average rating is 0.226  
The correlation between the complexity of a game and its average rating is 0.426
```

If data is insufficient:
```
The data should contain at least 2 samples, otherwise cannot compute correlation. 
```

If the correlation is meaningless: 
```
Not enough variation to compute correlation.
```
---

# Requirements

- A Unix/Linux environment (course Docker image recommended)

---

# Notes and Assumptions

- Column order in the dataset is fixed and consistent
- Scripts produce only final output, no intermediate temp files
- Scripts include basic input validation
- The assignment requirements are ambigious, so I make assumptions below: 
  - 1. since the `preprocess` script will give a stdout, I directly use `preprocess` in `analysis` if the file is uncleaned with `.txt` format. So it can accept both .txt and .tsv file.
  - 2. plus, the `analysis` script outputs 4 research answers.

---

# License

For academic assessment in CITS4407 at UWA.

---
