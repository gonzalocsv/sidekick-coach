# Changelog

## 1.0.0 — not yet released

The first public release. Sidekick is free, runs on your Mac, and uses your own AI key.

### Review a meeting you already had
- Drop a transcript (Zoom, Google Meet or Teams captions, Otter, Fireflies, Granola, pasted text) or a recording on
  the meetings list, say which speaker is you, and the debrief and the review follow, with no permission prompt.
- Onboarding asks how you want to start: review a past meeting, set up live listening, or try the HUD first. Every
  path is optional.
- An imported meeting is always reviewed. If you barely spoke in it, the review says so ("you said very little")
  instead of blaming the mic, and it isn't scored.

### Live in a call
- A small HUD floats over Google Meet (and, when you turn them on, Teams and Zoom) and suggests one move at a time:
  what to ask, push back on, or close. Skip a card and the next one takes a different angle.
- A mic that sends only silence, or stops while the meeting is talking, is reported within a minute.
- Sidekick notices when macOS takes microphone or calendar access away (a reinstall can do that) and says so in the
  HUD and the Review window, with an "Allow again" button; the notice goes as soon as access is back. It checks at
  startup, every 10 minutes while idle and before you start listening, and never asks macOS on its own. Start refuses
  a mic that macOS blocks instead of recording silence.
- Lines you say while muted in the call app are kept and marked "muted in call"; the coach doesn't react to them,
  since the other side never heard them.
- Swiping between Spaces works normally: Sidekick no longer pulls you back to its window, and the HUD stays out of
  Mission Control while still floating over full-screen Meet and Zoom.
- Sidekick no longer takes ⌘⇧R, so hard reload works again in your browser and other apps. "Record this call" is
  still in the menu-bar menu.

### Capture and names
- Transcription in the cloud with your key, or on this Mac (whisper.cpp with a model you download once; the audio
  never leaves the Mac).
- Each meeting keeps a capture report: which mic was used, how much each side spoke, and anything dropped and why.
  The review shows it as its Capture line.
- The live coach never guesses who is speaking. A name comes from the call app, an import, you, or one checked naming
  call after the meeting that keeps a name only when a quote proves it ("I'm Theo"); it shows as "Theo?" until you
  confirm it.
- After the meeting, Sidekick groups the other side's lines by voice on this Mac ("Voice A"). Confirm a name once and
  that voice is recognised in your next meeting. Click any name in the transcript to fix it; the review re-scores
  without a model call.

### Scoring
- A chess-style review of every meeting: graded moves (brilliant to blunder), six skills, the goal you set, and one
  lesson. The six skill anchors, the judge and the live card were checked against research on meetings,
  negotiation, conversation and feedback (see [EVIDENCE.md](docs/EVIDENCE.md)).
- Every graded move earns points (good 82, great 94, brilliant 100); misses and mistakes cost points, and short
  meetings swing less. An ordinary solid meeting lands 65 to 75.
- No mic, no score: a meeting where Sidekick heard little or none of your voice, or where the review found fewer than
  two of your own moves, is reviewed but not scored, and the review says why. The judge isn't called at all when the
  capture report shows your mic was missed.
- The debrief judges only your own lines and never credits you with what others said back.

### Routes and community
- Routes are role-shaped playbooks (focus tracks, a path, achievements, drills). Eleven ship with the app, from Sell
  the room to Hire well; one is recommended only when it fits your role.
- One achievement catalogue for everyone: every route's achievements count whether or not you follow it.
- Write your own route in Growth › Routes › New route, or edit any route (a bundled one becomes your copy). Install a
  route from the website with one click, or share yours from the app without a GitHub account. Routes are CC BY 4.0.

### Growth
- Growth › Path is a map: one trail per route, the current step in its progress ring, and the route recommended next.
  Nothing is locked; steps tick in any order, and each shows what counts, the meetings that counted and your closest
  miss.
- Drills aimed at a skill or a step, with a second beat when the other side pushes back, a heat ladder per skill, and
  a re-test two weeks after you redeem a miss. Drills never move ratings.
- A share card of a meeting: accuracy, six skills, the best and the hardest moment. Never anyone else's words; your
  own only if you tick it, with names replaced.
- Projects: a meeting joins a project only when you add it. The review suggests the project it seems to belong to
  ("Add to … ?"), and a topic that comes up in two meetings is proposed as a new project.
- Settings › Appearance can hide levels, XP and streaks; reviews keep running.

### Profiles and the optional account
- Profiles, not a sign-in wall: first run creates a profile for this Mac with no password. Add more in Settings ›
  Profile (a password is optional) and switch between them; each has its own data.
- Optional online account: Settings › Supporter › Online account has Create account and Sign in, both finished in the
  browser with Google or an emailed link. After the browser, the app asks "Signed in as <email>. Is that you?" and
  keeps the session only if you say yes. An account holds your name, email and supporter status, nothing about your
  meetings. Sign out or delete it from the same place; deleting it also deletes its supporter record.

### Supporters
- Everything works for free: no trial, nothing gated. Supporting is optional, with a supporter key or the account
  that bought it, and marks you as a supporter and moves your app to the beta update channel.

### Privacy guarantees
- Meetings, reviews and progress stay on your Mac. An app update may add to them and never removes or rewrites them;
  migrations are checked and backed up first ([DATA-SAFETY.md](docs/DATA-SAFETY.md)).
- Meeting audio is temporary: kept only until the after-meeting steps finish (grouping voices, the more accurate
  transcript), then deleted, also when a step fails. Turning on recording is the only way to keep it.
- Supporter and account checks send a hash of your Mac's hardware ID, never the ID itself.

### Known limits
- Teams and Zoom are experimental and off until you turn them on in Connections; nothing is read through
  Accessibility before that.
- Reviews, debriefs and live cards need an AI key (Gemini or OpenAI). A local OpenAI-compatible server is
  experimental.
