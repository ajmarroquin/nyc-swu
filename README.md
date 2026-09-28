# NYC Star Wars Unlimited Events

Live site: [ajmarroquin.github.io/nyc-swu](https://ajmarroquin.github.io/nyc-swu/)

A single-page community hub for Star Wars Unlimited weekly events and tournaments in New York City.

## How to Update Event Data

All data lives in the `data/` folder as JSON files. **You do not need to edit `index.html`** — just update the JSON and the site will reflect the changes automatically.

### `data/weeklies.json` — Recurring Weekly Events

An array of weekly events. Each entry:

```json
{
  "store": "Store Name",
  "days": [3, 5],
  "time": "7:00 PM",
  "fee": "$15 Constructed",
  "maps": "https://maps.google.com/?q=..."
}
```

| Field   | Type       | Description |
|---------|------------|-------------|
| `store` | string     | Store name as displayed on the site |
| `days`  | number[]   | Day(s) of the week — `0` = Sunday, `1` = Monday, ... `6` = Saturday |
| `time`  | string     | Start time (e.g. `"7:00 PM"`) |
| `fee`   | string     | Entry fee or format info (e.g. `"$15"`, `"Free"`, `"Rotating"`) |
| `maps`  | string     | Google Maps link to the venue |
| `every` | number     | *Optional.* Repeat every N weeks (e.g. `2` for bi-weekly). Defaults to every week |
| `start` | string     | *Optional, with `every`.* Any known "on" date, `YYYY-MM-DD`. Without it the site flags the event as "confirm on Discord" |
| `overrides` | object[] | *Optional.* One-off changes for a specific date: `{ "date": "YYYY-MM-DD", "time", "fee", "note" }`, or `{ "date": "...", "cancelled": true }` for a skipped week |

Overrides replace the regular time/fee on that date in "Happening Today". A store card with `<div class="store-overrides" data-store="Store Name">` in `index.html` also lists its upcoming overrides.

### `data/events.json` — Major Tournaments & Events

An array of one-time events (PQs, Sectors, Regionals, Galactic). Each entry:

```json
{
  "tier": "planetary",
  "label": "Planetary",
  "name": "Hex & Co — Union Square",
  "loc": "NYC, New York",
  "date": "2026-04-12",
  "fmt": "eternal"
}
```

| Field   | Type   | Description |
|---------|--------|-------------|
| `tier`  | string | One of: `showdown`, `prerelease`, `planetary`, `sector`, `regional`, `galactic` — controls the color/badge |
| `label` | string | Display label (e.g. `"Planetary"`, `"Sector"`) |
| `name`  | string | Event or store name |
| `loc`   | string | City/state location |
| `date`  | string | Date in `YYYY-MM-DD` format |
| `fmt`   | string | Format: `"premier"`, `"eternal"`, `"limited"`, or `""` if unknown |
| `end`   | string | *Optional.* Last day of a multi-day event, `YYYY-MM-DD` |
| `link`  | string | *Optional.* Ticket/registration URL |
| `note`  | string | *Optional.* Short extra line (time, cost, venue) |

## Contributing

1. Clone the repo
2. Create a new branch (`git checkout -b my-update`)
3. Edit the JSON file(s) in `data/`
4. Commit and push your branch
5. Open a pull request

The `main` branch is protected — changes require a PR.
