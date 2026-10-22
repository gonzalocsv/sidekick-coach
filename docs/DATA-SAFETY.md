# Your progress is never touched by an update

Sidekick keeps everything on your Mac: meetings, reviews, XP, achievements, path ticks, drills (SQLite), and your
files in `~/Sidekick`. An app update may add to them. It may never remove or rewrite them. This is how that is
protected, and what every release has to respect.

## The rules

1. **Migrations are additive.** New tables, new columns, new indexes, back-filled keys. Nothing is dropped, deleted or rewritten, and XP amounts are never recalculated.
2. **A copy before every schema change.** When the app opens a database older than its schema, it first writes
   a backup copy in Sidekick's data folder (the last 10 per version are kept). Otherwise it writes one copy a day (the
   last 14 are kept).
3. **Migrations are guarded.** They run in one transaction. Afterwards the progress counts (meetings, reviews, moments, scores, XP events and total, achievements, path ticks, drills and attempts, goals,
   commitments) are compared with the counts before. If any went down, the transaction is rolled back and the app
   stops instead of running on damaged data.
4. **Only you remove progress, one item at a time.** Deleting a meeting, re-reviewing or re-transcribing a meeting,
   correcting a meeting's kind or goal, removing a goal, and Reset are the only places that delete progress rows.
   Nothing else in the app deletes progress, and every release is tested to prove it.
5. **Big actions back up first.** Reset (which asks you to confirm) and Re-review all save a
   copy first. Restoring a backup copies the current database first, so a restore can be undone.
6. **Edited routes retire steps; they never delete ticks.** A step that leaves a route is retired, not deleted; its
   tick and XP stay, and it comes back if the step does.
7. **Your files are versioned.** Every save of your profile and objectives files by the app keeps the previous version
   and a dated copy in `~/Sidekick/.history/` (the last 30). A replayed onboarding keeps the sections Growth
   owns (Tracks, Direction, Broken patterns) and starts the Languages step from the languages you saved.
8. **Profiles are separate.** Each profile on this Mac has its own database and folder. Switching to a demo profile
   shows an empty Growth; your own profile's data is untouched and comes back when you switch back.
9. **A forgotten password changes only the password.** Resetting or removing a profile's password (after macOS confirms
   it's you, or from Terminal) changes that one profile's password and nothing else: no meetings, notes or other
   profiles are touched, and the profiles file is copied first (the last 5 copies are kept).
10. **Audio is temporary.** While a meeting runs, and while its summary is made, the app writes 16 kHz WAVs (your side and theirs) to a temporary folder in Sidekick's data folder. They exist only for the after-meeting steps: grouping voices on
   this Mac  and the more accurate transcript (which sends the audio to your own Gemini key). The folder is deleted as soon as those steps finish, also when one of them fails, and right
   away when a meeting is discarded or too short to summarize. Turning on recording (or "Record this call" in the menu-bar
   menu) is the only way to keep meeting audio; it is then saved to your recordings folder. If the app quits mid-meeting, the folder can remain until
   you delete it.

11. **People files change only where you change them.** Starring someone, a category or a group changes that one
   line in the person file's header; nothing else in the file moves. Saving a person keeps every header line the app
   doesn't know about. The Internal helper writes nothing until you click it, and never changes a category you set.
12. **Speaker names you set are never overwritten.** "Re-identify speakers" replaces only unnamed lines and "Name?"
   guesses. Names from the call, an import or you stay, and "Not <name>" is remembered for those lines. If the AI call
   fails, nothing changes.

## Where to look

- Growth › Settings › Backups lists every copy with its meetings, XP and achievements, and restores one.
- Before every release, we open a database exactly as the first release created it, update it, and check that every
  meeting, review, score and achievement is still there.
