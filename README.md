# scheduler

Runs the scheduled work for the products of IT Services by Rajat Agarwal, from one public repository (public repositories get unlimited free Actions minutes), so that every product repository can be private.

| Workflow | Every | What it does |
|---|---|---|
| ticks.yml | 5 minutes | asks each game to do its housekeeping (reports, 24-hour deletion, 365-day cleanup) |
| uptime.yml | 15 minutes | checks that every website answers; a failure is emailed by GitHub |
| reconcile.yml | 30 minutes | files any Razorpay payment a missed webhook did not file in the one ledger |
| keepalive.yml | week | one small commit so GitHub never switches the schedules off |

Each game's key is a repository secret named CRON_KEY_<GAME>. Nothing secret is in this repository.

## Second trigger (backup): Supabase pg_cron
GitHub's schedule runs late and sometimes skips. As a second, independent trigger, the shared Supabase project has a job `game-ticks` (pg_cron, every 5 minutes) that calls `ops.tick_games()`, which POSTs `/api/lifecycle/tick` on each of the five games with that game's key. The keys are kept in Supabase Vault (secret names `game_tick_<game>`), the targets in `ops.game_tick_target`. Both triggers are safe to run together: every housekeeping step is idempotent and only does work that is due. Checked 2026-10-14: all five games answered 200.
