# Changelog

## Unreleased — Spaces behave normally around Sidekick
- **Swiping between Spaces works again.** Swiping out of a full-screen app (say, a video) no longer pulls you back to
  Sidekick's Meetings window. The HUD no longer changes the app's process type on launch, which had made Sidekick the
  active app and sent macOS to its window's Space. The HUD is also kept out of Mission Control. It still floats over
  full-screen Meet and Zoom.

## Unreleased — optional accounts; the licence server moves to GCP
- **Optional accounts.** Settings › Supporter › Online account has **Create account** (name and email) and **Sign in**,
  separate like the profiles on this Mac; both finish in the browser with Google or an emailed link, and signing in
  needs an account created first. An account holds only your name, email and whether you're a supporter; buy the Supporter plan with the same email and the badge and beta
  updates follow you, no key needed. Sign out or delete the account from the same place. The app is unchanged
  without one, and meetings never leave the Mac.
- **One service on GCP** (`server/account-service`: Cloud Run, Firestore, Firebase Auth) replaces the Cloudflare
  licence worker. Supporter keys work as before. The website's Verified-author check asks it instead of Cloudflare KV.

## Unreleased — true scores: every voice captured, every name checked (PLAN-SCORING, PLAN-CAPTURE)
- **No mic, no score.** A meeting where Sidekick heard little or none of your voice, or where the review found fewer
  than two of your own moves, is reviewed but not scored, and the review says why. Before, it could only find
  "missed openings" and scored about 40.
- **Accuracy rubric 2.** Every graded move earns points (good 82, great 94, brilliant 100); misses and mistakes cost
  points instead of being the only thing counted, and short meetings swing less. An ordinary solid meeting lands
  65–75; 90 takes great moves throughout. `hud review --rescore` applies it to past reviews locally (backup first).
- **Your voice is never lost silently.** If your mic sends only silence or stops while the meeting is talking, the HUD
  says so within a minute. Being muted in Meet, Teams or Zoom now marks your lines "muted in call" instead of dropping
  them, and a mute state that stops arriving expires after 15 s. The echo guard only acts while the meeting is
  speaking, and turns itself off if it holds back too much of your own speech.
- **Capture report.** Each meeting records which mic was used, how much each side spoke, and anything dropped and why.
  The review shows a Capture line; `hud capture <meeting id>` prints the full report.
- **The right name on every voice, with almost no AI.** The live coach no longer guesses who is speaking (it guessed
  invitees who never spoke). A name now comes from the call app, an import, you, or one checked naming call after the
  meeting, which keeps a name only when a quote proves it ("I'm just Theo"); it shows as "Theo?" until you confirm it.
  After the meeting Sidekick groups the other side's lines by voice on this Mac ("Voice A"); confirm one and it's
  remembered for your next meeting. Click any name in the transcript to fix it; the review re-scores without a model
  call (`PATCH /api/sessions/{id}/speakers`). No naming call at all when every voice already has a name.
- **No review call when your mic was missed**: the meeting says why it wasn't scored, and the debrief is told.
- The debrief judges only your own lines; it no longer credits you with what others said back.

## 1.0.0 — first public release (PLAN-LAUNCH.md)
- **Review a meeting you already had.** Drop a transcript (Zoom, Google Meet or Teams captions, Otter, Fireflies,
  Granola, a pasted text) or a recording on the meetings list, say which speaker is you, and the debrief and the
  review follow, with no permission prompt. Also `hud import <file>`. Onboarding now asks how you want to start:
  review a past meeting, set up live listening, or try the HUD first; all optional.
- **Transcription on this Mac.** Choose "On this Mac" in onboarding or Settings › Transcription: whisper.cpp with a
  model you download once; your audio never leaves the Mac. Cards, debriefs and reviews can point at a local
  OpenAI-compatible server (experimental). An AI key is required: the app stays in onboarding until one is saved
  (the backend starts without one so onboarding can take it; listening and imports refuse until then).
- **Share card.** Review › Share draws a card of the meeting: accuracy, six skills, the best and the hardest moment.
  Never anyone else's words; your own only if you tick it, with names replaced. Copy, save, or copy as text.
- **Profiles, not a sign-in wall.** First run creates a profile for this Mac with no password. Settings › Profile
  adds more (a password is optional) and switches between them.
- **Simpler launch.** Teams and Zoom are experimental and off until you turn them on in Connections (nothing is read
  through Accessibility before that). Settings › Appearance can hide levels, XP and streaks; reviews keep running.
- **Supporters through Polar**, with GitHub Sponsors beside it. Supporter tokens now last 14 days and renew daily.
- **Community.** Install a route from the website (`sidekick://route/<slug>`), or share yours from Growth › Routes
  without a GitHub account. Routes are CC BY 4.0.
- **Fixes.** The Review window recovers by itself if its page process dies (it used to stay blank until a restart)
  and logs why. Settings › Integrations is shorter: one switch, an app picker, and Advanced. Temporary meeting audio
  is deleted when it is not re-transcribed.
- Open source: AGPL-3.0, contributor guide, CI, signed releases on GitHub with a Homebrew cask, and a website with
  the community pages (`site/`).

## Unreleased — the game: a path you can see, drills that build (PLAN-GAME.md)
- Evidence-backed coaching (PLAN-EVIDENCE.md, docs/EVIDENCE.md). The six skill anchors, the judge, the meeting goal
  and the live card were checked against the research on meetings, negotiation, conversation and feedback, and
  rewritten where it disagreed: pushback that acknowledges the point and gives the fact or the alternative scores
  above a flat "that's wrong"; talking more or less earns nothing on its own, and a pause counts when it let them think
  or improve their offer; calibrated uncertainty and softened phrasing in a second language are no longer hedges;
  follow-ups that pin something down beat topic switches; a concession that matches theirs is a trade. Meeting goals
  are now something you do, tied to the moment it will happen. Chair the decision rewards framing the question and
  giving your view last; Sell the room keeps answer-first for advisors. Every route lens now grades only what
  research supports and names the rest as habits. Route rules and achievement ids are unchanged, so no tick or
  achievement moves; the eleven routes are version 2.
- Write your own routes in the app: Growth › Routes › New route. Describe the situation in a sentence or two and
  Sidekick drafts the whole route (focus tracks, path, achievements, drills); edit anything, every rule is picked, not
  typed, and checked as you type by the library's own linter. Edit
  any route the same way (a bundled one becomes your copy). Share to the community replaces names Sidekick knows,
  checks the file and opens the library repo's new-file page with it filled in; GitHub turns it into a pull request.
- Routes page: search, a filter by kind of work, a filter by source, four to a page; the community library's routes
  appear in the same list once it opens (it says "coming soon" until then). The library gets a static listing
  generated with its index, for the Sidekick site.
- Six more routes, for work that is not client work: Lead the team (1:1s and feedback), Run the ops (status
  meetings and blockers), Hold the plan (scope, dates and risks), Chair the decision (leadership meetings), Hire well
  (interviews), Ship the roadmap (discovery and roadmap talks), Close the deal (sales calls), Keep the customer
  (renewals, reviews, escalations). Routes are only recommended when they fit your role or direction; with no fit,
  none is pushed.
- Growth › Path is a map: one winding trail per route with numbered steps, the current step inside its progress ring,
  a gate when the route is complete, and the route recommended next in fog. Finished routes fold above it; projects
  and skills are side trails. Nothing is locked: steps tick in any order, and every step shows its progress.
- Open any step for what counts in plain words, the meetings that counted, your closest miss, and a drill aimed at it.
  A step that ticks animates once after the review; the toast names it.
- Overview: the six skills only (your tracks are one line of chips that lead to the skill they feed), the trail in
  miniature, and Today's drills. Skill pages have Back, the skill's path, its heat, your tracks on it, and practice
  for that skill (it used to train your weakest one).
- Drills: targeted at a skill or a step, a second beat when the counterpart pushes back, a heat ladder per skill
  (cordial, pressed, hostile), Today's drills with a drill-day streak, a re-test two weeks after you redeem a miss,
  feedback with the rubric line you reached and your line next to the stronger one, route lines rewritten in your
  language once a week. Drills still never move ratings.
- No rule grammar on screen: steps and milestones are written in words; projects get a milestone builder.
- Navigation: Back on every sub-page, ⌘[ and ⌘] through Growth history, the sidebar highlights the parent page, the
  Upcoming list sits in the Growth sidebar, and "Set a goal" with no meetings ahead offers Prep a meeting and
  Connect a calendar instead of an empty page.
- Under it: path steps keyed by rule (a reordered route keeps its ticks; existing data migrates), per-route state in
  its own table, the rule evaluator in `rules.py` with evidence and closest-miss queries, `trails.py`, and Growth's
  renderer split into a router, a store and one file per page.

## Unreleased — routes, one catalogue, the community library, the free core (PLAN-COMMUNITY.md)
- Routes: role-shaped playbooks as Markdown files (focus tracks, lens, path, achievements, drills). Three ship with the
  app: Sell the room, Hold the number, Run the account. Recommended at the end of onboarding and in Growth › Routes;
  following one is optional and reversible.
- One achievement catalogue for everyone: every route's achievements are evaluated after every review whether or not
  you follow it. Growth › Achievements groups the catalogue by route, with a role filter.
- Rule grammar v2: `kind:`, `attendees>=`, `lang:` qualifiers; review-derived counts ignore unscored meetings.
- Community library: `library/` (seed of the sidekick-routes repo) with CI lint and an index pinned to a commit;
  Browse/Install/Update fetched only on click; `make release` vendors it; `make routes` keeps tools in sync.
- Export your Growth as a route (names scrubbed). Edit any route; your copy wins.
- Free: no trial, no offline countdown, nothing gated. An optional supporter key marks you as a supporter and moves
  your app to the beta update channel. Terms and privacy drafts updated.
- Licence hardening: owner unlock signed with an Ed25519 key that never ships; optional licence server
  (`server/license-worker`, Cloudflare Worker) returning signed, device-bound tokens; the licence module ships as native
  code; Electron fuses (no run-as-node, no NODE_OPTIONS / inspector, ASAR integrity, app only from ASAR).
- Onboarding: a People step (suggestions from your calendar and meetings), every connection required before Continue,
  a guided Chrome extension install (bundled with the app; Chrome Web Store when `[meet] store_url` is set), "Try it"
  hotkeys are practice only and survive hiding the HUD, a support card on Done, and where your data lives, said plainly.
- HUD: the 9 keycap is centred in the Pause pill; popover shadows fade out instead of being cut by the window edge.
- `hud route lint|list|follow|finish|index`; `hud review-eval --route <slug>` measures how far a lens moves grades.

## 1.0.0 — 2026-10-14 (local build; not yet notarized)
- First sellable build: self-contained app, licensing with a 14-day trial, signing/notarization and auto-updates
  (when credentials are configured), Chrome Web Store package, privacy/terms/consent drafts.
