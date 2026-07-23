---
name: active-network-activity-search
description: Search ACTIVE Network's public catalog of activities and events by keyword, location, category, and date range.
api: ACTIVE Network Activity Search API v2
operations:
  - searchActivities
---

# Search ACTIVE Network Activities

Use the ACTIVE Network Activity Search API v2 to find public activities and
events (races, camps, classes, tournaments) from ACTIVE.com and ACTIVEkids.com.

## Prerequisites

- An ACTIVE Network API key (register at https://developer.active.com/member/register).
- The key is passed as the `api_key` query parameter on every request.

## Steps

1. Call `searchActivities` — `GET http://api.amp.active.com/v2/search`.
2. Provide `api_key` (required) plus any filters: `query` (keyword), `near` or
   `lat_lon` + `radius` (location), `category`, `topic`, and `start_date`
   (format `yyyy-mm-dd..yyyy-mm-dd`).
3. Page through results with `current_page` (default 1) and `per_page`
   (default 10); read `total_results`, `items_per_page`, and `start_index`.
4. Parse `results[]` for each asset (`assetName`, `activityStartDate`, `place`,
   `assetPrices`).

## Conventions and limits

- Stay within 2 calls per second and 500,000 calls per day; exceeding either
  returns HTTP 403 (see errors/active-network-problem-types.yml).
- Read-only GET; no idempotency key needed (conventions/active-network-conventions.yml).

## Example

```
GET http://api.amp.active.com/v2/search?query=running&category=event&near=San%20Diego,CA,US&radius=50&api_key=YOUR_KEY
```
