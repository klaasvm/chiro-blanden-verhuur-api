# Chiro Blanden Data API

This repository acts as a small intermediary between Google Calendar and the static website [chiroblanden.be](https://chiroblanden.be), whose source is maintained in [`klaasvm/chiroblanden`](https://github.com/klaasvm/chiroblanden).

It fetches calendar data using credentials stored as GitHub Actions secrets and publishes the result as JSON files in this repository. The website can load these files without exposing a Google API key or other Google credentials in its client-side code.

## Data files

- [`planning.json`](planning.json) — Chiro activities by date.
- [`verhuur.json`](verhuur.json) — rental status by date.

The files are generated automatically by the workflow in [`.github/workflows/main.yml`](.github/workflows/main.yml). It runs every six hours and can also be started manually from the GitHub Actions tab. When the data changes, the workflow commits the updated JSON files to this repository.

## Security

Google OAuth credentials and calendar IDs are configured as GitHub Actions repository secrets. They are used by the workflow to retrieve calendar data and are not included in the published JSON files. The website only needs to request the generated JSON data; it does not need a Google API key.

## Configuration

The workflow expects these repository secrets:

- `GOOGLE_CALENDAR_ID_PLANNING`
- `GOOGLE_CALENDAR_ID_VERHUUR`
- `GOOGLE_CLIENT_ID`
- `GOOGLE_CLIENT_SECRET`
- `GOOGLE_REFRESH_TOKEN`

The account associated with the OAuth credentials must have access to both calendars.
