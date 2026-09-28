# Start a job from GitHub

You keep a small file in your own GitHub repo. When that file runs, GitHub sends a short note to [graphingest.io](https://www.graphingest.io): “please start.” Then GitHub’s computer turns off. The long work happens on GraphIngest. When the work finishes, the mark on that save turns green or red.

## When this fits

Use it when the work starts because someone saved code, and the work takes longer than GitHub will wait.

Everyday cases:

- A test suite that builds a report after each save.
- A data import that should start when a file lands in the repo.
- A nightly job you want to start from GitHub’s clock, while the hours of work happen on [graphingest.io](https://www.graphingest.io).

## What you do once

1. Create an account at [graphingest.io/signup](https://www.graphingest.io/signup).
2. In [Settings](https://www.graphingest.io/settings), create an API key. You will see it once. In the same Settings page, connect GitHub and choose the repo.
3. Open [your flows](https://www.graphingest.io/flows) and copy the flow id.
4. In the GitHub repo, add two secrets: `GRAPHINGEST_API_KEY` and `GRAPHINGEST_FLOW_ID`.

## The file

Save this as `.github/workflows/graphingest.yml` in your repo.

```yaml
name: Start a GraphIngest job
on:
  workflow_dispatch:
jobs:
  start:
    runs-on: ubuntu-latest
    steps:
      - uses: graphingest/run@v1
        with:
          api-key: ${{ secrets.GRAPHINGEST_API_KEY }}
          flow-id: ${{ secrets.GRAPHINGEST_FLOW_ID }}
```

Run it by hand from the Actions tab. GitHub’s step ends in a few seconds. The mark on the save stays in progress, then turns green or red when the job on [graphingest.io](https://www.graphingest.io) finishes. Open the mark to see the run.

Change `workflow_dispatch` when you want a different start. `push` starts it on every save. A `schedule` starts it on a clock. The rest of the file stays the same.
