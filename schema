# NBA Data Schema Documentation

This document describes the database schema for the NBA data validation exercise.

---

## Tables Overview

| Table | Description |
|-------|-------------|
| `teams` | NBA team information |
| `players` | NBA player information |
| `games` | Game-level data with scores |
| `playerstatsgame` | Individual player statistics per game |

---

## Table: `teams`

Team information including venue assignments.

| Column | Type | Description |
|--------|------|-------------|
| `team_id` | UUID (STRING) | **Primary Key** - Unique team identifier |
| `team_full_name` | STRING | Full team name (e.g., "Golden State Warriors") |
| `team_abbreviation` | STRING | 3-letter abbreviation (e.g., "GSW") |
| `venue_id` | UUID (STRING) | Venue/arena identifier |

---

## Table: `players`

Player information with current team assignment.

| Column | Type | Description |
|--------|------|-------------|
| `player_id` | UUID (STRING) | **Primary Key** - Unique player identifier |
| `player_full_name` | STRING | Player's full name |
| `most_recent_team_id` | UUID (STRING) | **Foreign Key → teams.team_id** |
| `most_recent_team_abbreviation` | STRING | 3-letter team abbreviation |

---

## Table: `games`

Game-level data including final and quarter-by-quarter scores.

| Column | Type | Description |
|--------|------|-------------|
| `game_id` | UUID (STRING) | **Primary Key** - Unique game identifier |
| `venue_id` | UUID (STRING) | Venue where game was played |
| `home_team_id` | UUID (STRING) | **Foreign Key → teams.team_id** |
| `home_team_abbreviation` | STRING | Home team 3-letter abbreviation |
| `away_team_id` | UUID (STRING) | **Foreign Key → teams.team_id** |
| `away_team_abbreviation` | STRING | Away team 3-letter abbreviation |
| `home_team_points` | INTEGER | Final score for home team |
| `away_team_points` | INTEGER | Final score for away team |
| `home_team_score_q1` | INTEGER | Home team 1st quarter score |
| `home_team_score_q2` | INTEGER | Home team 2nd quarter score |
| `home_team_score_q3` | INTEGER | Home team 3rd quarter score |
| `home_team_score_q4` | INTEGER | Home team 4th quarter score |
| `home_team_score_ot1` | INTEGER (nullable) | Home team overtime score (if applicable) |
| `away_team_score_q1` | INTEGER | Away team 1st quarter score |
| `away_team_score_q2` | INTEGER | Away team 2nd quarter score |
| `away_team_score_q3` | INTEGER | Away team 3rd quarter score |
| `away_team_score_q4` | INTEGER | Away team 4th quarter score |
| `away_team_score_ot1` | INTEGER (nullable) | Away team overtime score (if applicable) |
| `total_points` | INTEGER | Sum of both teams' final scores |

---

## Table: `playerstatsgame`

Individual player statistics for each game appearance.

| Column | Type | Description |
|--------|------|-------------|
| `game_id` | UUID (STRING) | **Composite PK, Foreign Key → games.game_id** |
| `player_id` | UUID (STRING) | **Composite PK, Foreign Key → players.player_id** |
| `home_or_away` | STRING | 'home' or 'away' |
| `player_team_id` | UUID (STRING) | **Foreign Key → teams.team_id** |
| `player_team_abbreviation` | STRING | Player's team 3-letter abbreviation |
| `opponent_team_id` | UUID (STRING) | **Foreign Key → teams.team_id** |
| `opponent_team_abbreviation` | STRING | Opponent team 3-letter abbreviation |
| `player_team_score` | INTEGER | Player's team final score |
| `opponent_team_score` | INTEGER | Opponent's final score |
| `player_team_won` | BOOLEAN | TRUE if player's team won |
| `player_full_name` | STRING | Player's full name |
| `starter` | BOOLEAN | TRUE if player started the game |
| `points` | INTEGER | Points scored |
| `field_goals_made` | INTEGER | Field goals made |
| `field_goals_att` | INTEGER | Field goal attempts |
| `field_goals_pct` | FLOAT (nullable) | Field goal percentage (0-100) |
| `free_throws_made` | INTEGER | Free throws made |
| `free_throws_att` | INTEGER | Free throw attempts |
| `free_throws_pct` | FLOAT (nullable) | Free throw percentage (0-100) |
| `offensive_rebounds` | INTEGER | Offensive rebounds |
| `defensive_rebounds` | INTEGER | Defensive rebounds |
| `rebounds` | INTEGER | Total rebounds |
| `assists` | INTEGER | Assists |
| `turnovers` | INTEGER | Turnovers |
| `assists_turnover_ratio` | FLOAT (nullable) | Assists / Turnovers ratio |
| `steals` | INTEGER | Steals |
| `blocks` | INTEGER | Blocks |
| `plus_minus` | INTEGER | Plus/minus rating for game |
| `double_double` | BOOLEAN | TRUE if player achieved double-double |
| `minutes` | STRING | Minutes played (format: HH:MM:SS) |

---

## Entity Relationship Diagram

```
┌─────────────────┐
│     teams       │
├─────────────────┤
│ PK: team_id     │◄────────────────────────────────────────────┐
│    venue_id     │                                             │
│    ...          │                                             │
└────────┬────────┘                                             │
         │                                                      │
         │ 1:N                                                  │
         ▼                                                      │
┌─────────────────┐                                             │
│    players      │                                             │
├─────────────────┤                                             │
│ PK: player_id   │◄─────────────────────┐                      │
│ FK: most_recent_│                      │                      │
│     team_id     │                      │                      │
│    ...          │                      │                      │
└─────────────────┘                      │                      │
                                         │                      │
┌─────────────────┐                      │                      │
│     games       │                      │                      │
├─────────────────┤                      │                      │
│ PK: game_id     │◄──────────┐          │                      │
│ FK: home_team_id│───────────┼──────────┼──────────────────────┤
│ FK: away_team_id│───────────┼──────────┼──────────────────────┘
│    venue_id     │           │          │
│    ...          │           │          │
└─────────────────┘           │          │
                              │          │
                              │ 1:N      │ 1:N
                              ▼          ▼
                    ┌─────────────────────────────┐
                    │      playerstatsgame        │
                    ├─────────────────────────────┤
                    │ PK/FK: game_id              │
                    │ PK/FK: player_id            │
                    │ FK: player_team_id ─────────┼──► teams.team_id
                    │ FK: opponent_team_id ───────┼──► teams.team_id
                    │    ...                      │
                    └─────────────────────────────┘
```

---

## Relationships Summary

| Relationship | From Table | To Table | Cardinality | Foreign Key |
|--------------|------------|----------|-------------|-------------|
| Team → Players | teams | players | 1:N | players.most_recent_team_id |
| Team → Games (Home) | teams | games | 1:N | games.home_team_id |
| Team → Games (Away) | teams | games | 1:N | games.away_team_id |
| Game → Player Stats | games | playerstatsgame | 1:N | playerstatsgame.game_id |
| Player → Player Stats | players | playerstatsgame | 1:N | playerstatsgame.player_id |
| Team → Player Stats (Player Team) | teams | playerstatsgame | 1:N | playerstatsgame.player_team_id |
| Team → Player Stats (Opponent) | teams | playerstatsgame | 1:N | playerstatsgame.opponent_team_id |

---

## Key Constraints & Business Rules

1. **Primary Keys**: Each table has a unique identifier (UUID format)
2. **Composite Key**: `playerstatsgame` uses (`game_id`, `player_id`) as composite primary key
3. **Referential Integrity**: Foreign keys should reference valid primary keys in parent tables
4. **Nullable Fields**: OT scores, percentage fields, and ratio fields may be NULL
5. **Boolean Fields**: Stored as TRUE/FALSE strings
6. **Time Format**: Minutes played uses HH:MM:SS format
