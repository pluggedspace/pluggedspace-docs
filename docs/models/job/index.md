
# Welcome to job-autobot Documentation

For full API reference visit [api.pluggedspace.org/job](https://docs.pluggedspace.org/models/job).

---

## Table of Contents
1. [Requesting an API Key](#requesting-an-api-key)
2. [Authentication](#authentication)
3. [Telegram Bot Usage](#telegram-bot-usage)
4. [API Endpoints](#api-endpoints)
   - [GET /api/](#get-api)
   - [POST /api/retrain/](#post-apiretrain)
   - [GET /api/dashboard/overview/](#get-apidashboardoverview)
   - [GET /api/dashboard/confidence/](#get-apidashboardconfidence)
   - [GET /api/predictions/latest/](#get-apipredictionslatest)
   - [GET /api/dashboard/compare_versions/](#get-apidashboardcompareversions)
   - [GET /dashboard/predictions/](#get-dashboardpredictions)
5. [Rate Limits](#rate-limits)
6. [Support](#support)

---

## Requesting an API Key

To use the jobautobot API:

1. **Apply Online**
   - Visit: [https://api.pluggedspace.org/apply](https://api.pluggedspace.org/apply)
   - Fill out the application form with:
     - Name / Organization
     - Intended usage (project or integration)
     - Contact email

2. **Email Request**
   - Send to: **access@pluggedspace.org**
   - Subject: `API Access Request`
   - Body: Include your details and intended usage.

Once approved, you will receive:
- **API Key** (unique to your account)
- **Usage limits**
- **API documentation link**

---

## Authentication

All API requests must include your API key:

```http
Authorization: Bearer YOUR_API_KEY
```

---

## Telegram Bot Usage

Find the bot on Telegram: [@jobautobot](https://t.me/jobautobot)

**Commands:**
- `/findjob Arsenal vs Manchester United` — Predicts the outcome of a specific match
- `/view_cv` — Shows the next scheduled match with prediction
- `/help` — Lists all available commands

---

## API Endpoints

### GET /api/
Returns available endpoints and service info.

**Example:**
```bash
curl -H "Authorization: Bearer YOUR_API_KEY" https://api.m.pluggedspace.org/api/
```

---

### POST /api/retrain/
Triggers a model retrain. Admin access only.

**Example:**
```bash
curl -X POST -H "Authorization: Bearer ADMIN_API_KEY" \
https://api.m.pluggedspace.org/api/retrain/
```

---

### GET /api/dashboard/overview/
Returns aggregated prediction stats.

**Example Response:**
```json
{
  "total_predictions": 125,
  "accuracy": 0.82,
  "average_confidence": 0.74
}
```

---

### GET /api/dashboard/confidence/
Returns prediction confidence distribution.

**Example Response:**
```json
{
  "high_confidence": 58,
  "medium_confidence": 47,
  "low_confidence": 20
}
```

---

### GET /api/predictions/latest/
Returns the most recent match predictions.

**Example:**
```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
https://api.m.pluggedspace.org/api/predictions/latest/
```

**Example Response:**
```json
[
  {
    "match_id": 987,
    "home_team": "Arsenal",
    "away_team": "Manchester United",
    "predicted_outcome": "Home Win",
    "predicted_goal_diff": 1.4,
    "confidence": 0.81
  }
]
```

---

### GET /api/dashboard/compare_versions/
Compares prediction accuracy between model versions.

**Example Response:**
```json
{
  "version_1": { "accuracy": 0.78 },
  "version_2": { "accuracy": 0.82 }
}
```

---

### GET /dashboard/predictions/
Returns prediction data for dashboard visualization.

**Example Response:**
```json
[
  {
    "match": "Liverpool vs Chelsea",
    "outcome": "Draw",
    "confidence": 0.66
  },
  {
    "match": "Barcelona vs Real Madrid",
    "outcome": "Away Win",
    "confidence": 0.72
  }
]
```

---

## Rate Limits

| Plan        | Requests/day | Notes                          |
|-------------|-------------|--------------------------------|
| Free        | 50          | Basic access                   |
| Pro         | 5,000       | Higher limits & priority       |
| Enterprise  | Custom      | Dedicated support              |

---

## Support

- **Email:** support@pluggedspace.org
- **Telegram:** [@MatchOutcomeBot](https://t.me/MatchOutcomeBot)
- **Documentation:** [https://docs.pluggedspace.org/models/match](https://docs.pluggedspace.org/models/match)