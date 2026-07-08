# F1 Database — CS 411 Project

A full-stack web app for querying Formula 1 race data, built for the Database Systems course (CS 411) at UIUC.

## What it does

- Browse and query F1 race results, drivers, constructors, and tracks across all seasons
- CRUD operations on race data via a REST API
- Advanced SQL: correctly handles the scoring rule change between eras (10-point system pre-2010, 25-point system post-2010) using a UNION query
- React frontend with dropdowns and forms for filtered queries

## Stack

**Frontend:** React, Axios, react-dropdown
**Backend:** Node.js, Express, MySQL (hosted on Google Cloud SQL)

## Architecture

```
React (frontend) ──► Express API (port 3001) ──► MySQL (GCP Cloud SQL)
```

## Key query

Constructor standings that properly accounts for the 2010 points rule change:

```sql
(SELECT TeamName, SUM(Points) FROM constructors JOIN races
 WHERE Year < 2010 AND Points = 10 GROUP BY TeamName)
UNION
(SELECT TeamName, SUM(Points) FROM constructors JOIN races
 WHERE Year >= 2010 AND Points = 25 GROUP BY TeamName)
```

## Running locally

```bash
# Backend
cd backend && npm install && node index.js

# Frontend
cd frontend && npm install && npm start
```
