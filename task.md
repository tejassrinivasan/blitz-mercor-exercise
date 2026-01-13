# Data Engineer Exercise

## The Data

4 CSV files with NBA game data. They have foreign key relationships.

| File | Rows |
|------|------|
| `teams.csv` | 4 |
| `players.csv` | 47 |
| `games.csv` | 3 |
| `playerstatsgame.csv` | 67 |

---

## Task 1: Find & Fix Errors

Some of these files contain data quality issues. Find and fix them.

---

## Task 2: Add New Game

Scrape this box score and add it to the relevant CSVs:

https://www.espn.com/nba/boxscore/_/gameId/401810104

Only add players who already exist in `players.csv`.
