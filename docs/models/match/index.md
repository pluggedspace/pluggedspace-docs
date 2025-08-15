# Welcome to match-bot Documentation

For full API reference visit [m.pluggedspace.org](https://docs.pluggedspace.org/models/match).

---

## Requesting an API Key

To use the match-bot API:

1. **Apply Online**
   - Visit: [https://match-bot.com/apply](https://match-bot.com/apply)
   - Fill out the application form with:
     - Name / Organization
     - Intended usage (project or integration)
     - Contact email

2. **Email Request**
   - Send to: **access@match-bot.com**
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


---

Telegram Bot Usage

Find the bot on Telegram: @matchbot

Commands:

/predict Arsenal vs Manchester United — Predicts the outcome of a specific match.

/nextmatch — Shows the next scheduled match with prediction.

/help — Lists all available commands.



---

API Endpoints

GET api/

Returns available endpoints and service info.

Example

curl -H "Authorization: Bearer YOUR_API_KEY" https://api.match-bot.com/api/


---

POST api/retrain/ (name: retrain_predictions)

Triggers a model retrain. Admin access only.

curl -X POST -H "Authorization: Bearer ADMIN_API_KEY" \
https://api.match-bot.com/api/retrain/


---

GET api/dashboard/overview/ (name: dashboard_overview)

Returns aggregated prediction stats.

Example Response

{
  "total_predictions": 125,
  "accuracy": 0.82,
  "average_confidence": 0.74
}


---

GET api/dashboard/confidence/ (name: dashboard_confidence)

Returns prediction confidence distribution.

Example Response

{
  "high_confidence": 58,
  "medium_confidence": 47,
  "low_confidence": 20
}


---

GET api/predictions/latest/ (name: latest_predictions)

Returns the most recent match predictions.

Example

curl -H "Authorization: Bearer YOUR_API_KEY" \
https://api.match-bot.com/api/predictions/latest/

Example Response

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


---

GET api/dashboard/compare_versions/ (name: compare_versions)

Compares prediction accuracy between model versions.

Example Response

{
  "version_1": { "accuracy": 0.78 },
  "version_2": { "accuracy": 0.82 }
}


---

GET dashboard/predictions/

Returns prediction data for dashboard visualization.

Example Response

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


---

Rate Limits

Plan	Requests/day	Notes

Free	50	Basic access
Pro	5,000	Higher limits & priority
Enterprise	Custom	Dedicated support



---

Support

Email: support@pluggedspace.org

Telegram: @MatchOutcomeBot

Docs: https://api.match-bot.com/docs



