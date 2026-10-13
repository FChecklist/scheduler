# scheduler

Runs the scheduled work for the products of IT Services by Rajat Agarwal, from one public repository (public repositories get unlimited free Actions minutes), so that every product repository can be private.

| Workflow | Every | What it does |
|---|---|---|
| ticks.yml | 5 minutes | asks each game to do its housekeeping (reports, 24-hour deletion, 365-day cleanup) |
| uptime.yml | 15 minutes | checks that every website answers; a failure is emailed by GitHub |
| reconcile.yml | 30 minutes | files any Razorpay payment a missed webhook did not file in the one ledger |
| keepalive.yml | week | one small commit so GitHub never switches the schedules off |

Each game's key is a repository secret named CRON_KEY_<GAME>. Nothing secret is in this repository.
