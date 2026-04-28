# oursofia_data

Public remote-data host for the OurSofia app.

## Purpose
This repo is responsible for:

- running the scheduled GitHub Actions sync job
- publishing app-facing data via GitHub Pages
- persisting server-side JSON state between workflow runs

## Public artifacts
GitHub Pages should serve:

- `https://nonsense.github.io/oursofia_data/manifest.json`
- `https://nonsense.github.io/oursofia_data/signals_latest.json.gz`

## Internal state
The workflow persists canonical JSON state on the `remote-data-state` branch.

Expected files there:

- `canonical_signals.json`
- optional `state_manifest.json`

## Workflow
Main workflow:

- `.github/workflows/publish-remote-data.yml`

That workflow checks out this repo and `nonsense/oursofia`, runs the publish pipeline from the app repo, deploys GitHub Pages artifacts, and updates the persisted JSON state.

## Notes
- The actual fetch/merge scripts currently live in `nonsense/oursofia`.
- This split keeps hosting/deployment separate from the iOS app source tree.
