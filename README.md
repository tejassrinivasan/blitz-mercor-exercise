# Blitz Data Engineer Interview Exercise

## Overview

This repository contains NBA game data across 4 CSV files. Your task is to identify and fix data quality issues.

## Files

| File | Description |
|------|-------------|
| `teams.csv` | Team information (fully correct — use as source of truth) |
| `players.csv` | Player roster (fully correct — use as source of truth) |
| `games.csv` | Game results with scores |
| `playerstatsgame.csv` | Player box score stats per game |

## Schema Relationships

```
teams.team_id ──────────┬──► games.home_team_id / away_team_id
                        └──► playerstatsgame.player_team_id

players.player_id ─────────► playerstatsgame.player_id

games.game_id ─────────────► playerstatsgame.game_id
```

## What You Know

- `teams.csv` and `players.csv` are **fully correct** — use them as sources of truth
- In `playerstatsgame.csv`, the core box score stats (`points`, `rebounds`, `assists`) are correct
- Derived columns and other tables may contain errors

## Your Task

1. Clone this repo locally
2. Identify data quality issues across the CSVs
3. Fix the issues and explain your reasoning

You may use GenAI coding tools (Cursor, Claude Code, etc.) to assist with your analysis.

Good luck!

