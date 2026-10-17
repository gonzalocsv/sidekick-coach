# Your progress is never touched by an update

Sidekick keeps everything on your Mac: meetings, reviews, XP, achievements, path ticks, drills (SQLite), and your
files in `~/Sidekick`. An app update may add to them. It may never remove or rewrite them. This is how that is
enforced, and what every change to the code has to respect.

## The rules

1. **Migrations are additive.** New tables, new columns, new indexes, back-filled keys. Never `DROP TABLE`, never a
   `DELETE` of progress, never a rewrite of XP amounts. The schema version lives in `PRAGMA user_version`
   (`safety.SCHEMA_VERSION`).
2. **A copy before every schema change.** When the app opens a database older than its schema, it first writes
   `<data>/backups/hud-<time>-schema-v<N>.db` with the SQLite backup API (the last 10 per version are kept).
   Otherwise it writes one `-daily` copy a day (the last 14 are kept).
3. **Migrations are guarded.** They run in one transaction. Afterwards the progress counts (`safety.PROGRESS`:
   meetings, reviews, moments, scores, XP events and total, achievements, path ticks, drills and attempts, goals,
   commitments) are compared with the counts before. If any went down, the transaction is rolled back and the app
   stops with `ProgressGuardError` instead of running on damaged data.
4. **Only you remove progress, one item at a time.** Deleting a meeting, re-reviewing or re-transcribing a meeting,
   correcting a meeting's kind or goal, removing a goal, and Reset are the only places that delete progress rows.
   Each such line carries `# progress-ok: <your action>`; `tests/test_safety.py` fails on any other.
5. **Big actions back up first.** Reset (which also needs `{"confirm": "reset"}`) and Re-review all write a
   `before-…` copy first. Restoring a backup copies the current database first, so a restore can be undone.
6. **Edited routes retire steps; they never delete ticks.** A step that leaves a route is marked `retired_at`; its
   tick and XP stay, and it comes back if the step does.
7. **Your files are versioned.** Every save of `profile.md` and `objectives.md` by the app keeps the previous version
   as `.bak` and a dated copy in `~/Sidekick/.history/` (the last 30). A replayed onboarding keeps the sections Growth
   owns (Tracks, Direction, Broken patterns) and starts the Languages step from the languages you saved.
8. **Profiles are separate.** Each profile on this Mac has its own database and folder. Switching to a demo profile
   shows an empty Growth; your own profile's data is untouched and comes back when you switch back.
9. **Audio is temporary.** While a meeting runs, and while its summary is made, the app writes 16 kHz WAVs (`you.wav`,
   `them.wav`) to `<data>/tmp-audio/<meeting id>/`. They exist only for the after-meeting steps: grouping voices on
   this Mac (`[voices] enabled`) and the more accurate transcript (`[summary] retranscribe`, which sends the audio to
   your own Gemini key). The folder is deleted as soon as those steps finish, also when one of them fails, and right
   away when a meeting is discarded or too short to summarize. `record = true` (or "Record this call" in the menu-bar
   menu) is the only way to keep meeting audio; it then goes to `recordings_dir` instead. If the app quits mid-meeting, the folder can remain until
   you delete it.

## Where to look

- Growth › Settings › Backups lists every copy with its meetings, XP and achievements, and restores one.
- `tests/test_safety.py` migrates a database exactly as 1.0.0 created it (`tests/fixtures/schema_v1_0.sql`) and
  checks every row survives. When a release changes the schema, add its schema as a new fixture; never delete one.
