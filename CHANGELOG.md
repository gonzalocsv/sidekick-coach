# Changelog

## 1.0.3 — 2026-10-23

### Google Meet extension from the Chrome Web Store
- "Sidekick for Google Meet" is on the Chrome Web Store. Settings › Connections and onboarding now say "Add to
  Chrome" and open the listing: no developer mode, no folder to load, and Chrome keeps it up to date.
- The first time the installed app opens, it asks Chrome to offer the extension. The next time Chrome starts it
  shows "Enable extension": one click and the Google Meet row turns green. Sidekick asks only once; if you remove
  the extension, Chrome won't add it back. Turn this off with `[meet] auto_offer = false`.

## 1.0.2 — 2026-10-22

### Your words, not the meeting's
- Without headphones your mic also hears the meeting from your speakers, and those words were stored as yours.
  In two real meetings about half of "your" lines repeated what someone else had just said, so the review graded
  their words as yours and speaker naming got harder. After each new meeting Sidekick now takes the meeting's words
  out of your lines: a sentence of yours that mostly repeats what the others said in the seconds around it goes,
  and your own sentences stay whole. The live echo filter missed these because the high-accuracy transcript
  re-reads your whole mic track afterwards, and because the speaker-echo guard switched itself off when the echo
  was loud.
- Meetings already stored don't change. The words taken out stay in the meeting, so they can be put back.

### Voices that tell people apart
- Grouping the other side's lines by voice now uses a small speaker-recognition model that runs on your Mac
  (WeSpeaker ResNet34-LM). The old method heard one voice in every real call. In tests on real recorded meetings the
  new one never put two people in one voice; the old one did in half or more of them. A line that isn't clearly
  anyone's voice now gets no voice, rather than someone else's.
- Still nothing leaves your Mac and no audio is kept: the model reads the temporary meeting audio and stores only
  numbers. Voices remembered by the old method aren't reused; they're learned again the next time you confirm a name.
  A remembered voice is still shown as "Name?" until you confirm it.
- The app is about 64 MB bigger, and grouping voices after a long meeting takes about half a minute longer.

## 1.0.1 — 2026-10-22

### Who said what
- The transcript no longer puts one name on everybody. Grouping by voice wasn't telling people apart in real calls,
  so one "Theo, what do you think?" named every line of the other side Theo. The voice grouping is now used only
  when it actually finds different voices.
- After a meeting, the model that writes your debrief works out who said each line, with the same notes it uses
  for profile updates. A name is kept only with evidence: the person introduces themself, is spoken to by name right
  before, is the only invited person whose role fits, or carries on right after. Mentioning someone ("I was just
  telling Ana…") is not evidence. Names stay "Name?" until you confirm them, and hovering shows why each one was
  given.
- A commitment in the debrief ("I'll send it Friday") names the line it came from, and flags a "Name?" that
  disagrees.
- **Re-identify speakers** on any meeting runs this again, also on old meetings whose audio is gone. Names from the
  call, an import or you are never changed.
- Click a name and choose **Not <name>** to clear a wrong guess; it won't be suggested for those lines again. The
  name picker lists your starred people first.

### People
- Star your favourite people: one click on the list or their page. Starred people come first in the list and in
  the pickers.
- Groups: add free tags to anyone ("Northwind", "Design team") and filter the list by them.
- Internal / Client: an option in Settings › Appearance (People) for anyone who works with clients. When it's on, people get an
  Internal or Client tag, the list gets filters, and a one-time helper offers to mark everyone at your organisation's
  email domain as Internal.

### Commitments
- The Commitments tab shows a small bubble with how many open commitments are yours. It turns red when one is
  overdue and disappears at zero.

## 1.0.0 — 2026-10-22

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
- If your mic goes silent or stops while the meeting is talking, Sidekick tells you within a minute.
- If the mic or meeting-audio helper stops sending sound, Sidekick restarts it within seconds, and keeps trying if
  a restart doesn't take (for example while Bluetooth headphones connect). If your mic sends nothing at all, the HUD
  says so within 10 seconds, even if nobody else is talking yet.
- A mic that won't start no longer stops the meeting from starting: Sidekick listens to the meeting and keeps
  trying the mic.
- Mic and audio errors clear themselves when the problem is fixed or the meeting ends, instead of staying red in
  the HUD.
- A short reconnect to the transcription service no longer flashes an error in the HUD. Only a reconnect that
  fails is shown.
- Grouping the other side's lines by voice works in the installed app again.
- If macOS takes away microphone or calendar access (a reinstall can do that), Sidekick says so in the HUD and the
  Review window with an "Allow again" button, and the notice goes away once access is back. It never asks macOS on its
  own, and it won't start recording a mic that macOS blocks.
- Lines you say while muted in the call app are kept and marked "muted in call"; the coach doesn't react to them,
  since the other side never heard them.
- Swiping between Spaces works normally: Sidekick no longer pulls you back to its window, and the HUD stays out of
  Mission Control while still floating over full-screen Meet and Zoom.
- Allowing a permission (microphone, calendar, meeting audio, Chrome or Safari) no longer leaves Sidekick hidden
  behind another app when the macOS prompt closes: its window comes back to the front.
- Sidekick no longer takes ⌘⇧R, so hard reload works again in your browser and other apps. "Record this call" is
  still in the menu-bar menu.

### Capture and names
- Transcribe in the cloud with your key, or on this Mac with a model you download once; on this Mac the audio never
  leaves it ([details](docs/LOCAL-STT.md)).
- Each meeting keeps a capture report: which mic was used, how much each side spoke, and anything that was missed and
  why. The review shows it as its Capture line.
- The live coach never guesses who is speaking. A name comes from the call app, an import, or you, or from one check
  after the meeting that keeps a name only when a quote proves it ("I'm Theo"). It shows as "Theo?" until you confirm.
- After the meeting, Sidekick groups the other side's lines by voice on this Mac ("Voice A"). Confirm a name once and
  that voice is recognised in your next meeting. Click any name in the transcript to fix it, and the review updates
  instantly.

### Scoring
- A chess-style review of every meeting: graded moves (brilliant to blunder), six skills, the goal you set, and one
  lesson. The six skill anchors, the judge and the live card were checked against research on meetings,
  negotiation, conversation and feedback ([the evidence](docs/EVIDENCE.md)).
- Every graded move earns points (good 82, great 94, brilliant 100); misses and mistakes cost points, and short
  meetings swing less. An ordinary solid meeting lands 65 to 75.
- No mic, no score: if Sidekick heard little or none of your voice, or found fewer than two of your own moves, the
  meeting is reviewed but not scored, and the review says why.
- Meetings under 5 minutes are reviewed but not scored on their own. "Score it anyway" in the review scores one
  when you want it to count, even with only a few graded moves, and tells you the accuracy it got.
- The debrief judges only your own lines and never credits you with what others said back.
- Skills you can top out: each skill now has five described rungs, and a 5 means you made the move each time it was
  due in that meeting, not a flawless meeting. A steady 4 now carries a skill to the edge of Expert (it used to stall
  at about 72), and levels keep moving after many meetings. Existing levels are recalculated once from your scores.
- Hat-trick is now 3 Great or Brilliant moments in one round, and Expert needs a band of ±10 (was ±8, which the new
  rating floor never reached). Route steps that asked for a 5 or for several Brilliant moments ask for what a meeting can
  show, and the route checker flags rules like that.

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
- Drills aimed at a skill or a step, scored on what one answer can show. Each drill says what a 5 needs before you
  answer, and a 5 is reachable in one line. When the other side pushes back, your last line decides the exchange, so
  a 4 that holds up becomes a 5. Five levels per skill (Warm, Real, Pressed, Hard, Boardroom) change what the scenario
  asks of you: a missing detail, a vague number, a trap, then conflicting constraints and two push-backs. Your rating
  sets where a skill starts; two 4s climb a level and three 2s in a row drop one. Harder levels earn more XP. A
  re-test comes two weeks after you redeem a miss. Drills never move ratings.
- Say it out loud: the mic button in a drill transcribes your answer (on this Mac or with your key, whichever you
  chose) into the box to edit before sending, and shows how long you spoke and your filler words. The audio is never
  saved, and the mic is off while Sidekick is listening to a meeting.
- A drill keeps your place while you record, transcribe and send: it no longer jumps back to the top, so the mic and
  Send stay where you left them.
- A share card of a meeting: accuracy, six skills, the best and the hardest moment. Never anyone else's words; your
  own only if you tick it, with names replaced.
- Projects: a meeting joins a project only when you add it. The review suggests the project it seems to belong to
  ("Add to … ?"), and a topic that comes up in two meetings is proposed as a new project.
- Settings › Appearance can hide levels, XP and streaks; reviews keep running.

### Profiles
- Profiles, not a sign-in wall: first run creates a profile for this Mac with no password. Add more in Settings ›
  Profile (a password is optional) and switch between them; each has its own data. That's the only sign-in: there is
  no online account, no browser sign-in page and no sign-in emails.
- Forgot a profile's password? "Forgot password?" on the sign-in screen asks macOS to confirm it's you (Touch ID or
  your Mac password), then you choose a new password or open the profile without one. Its meetings and notes stay as
  they are. Settings › Profile › Password changes, adds or removes a password.

### Supporters
- Everything works for free: no trial, nothing gated. Supporting is optional: paste your supporter key in Settings ›
  Supporter. It marks you as a supporter and moves your app to the beta update channel
  ([how licensing works](docs/SECURITY-LICENSING.md)). One key works on up to 3 Macs; remove it from one to free the
  seat.
- Supporters can send feedback straight to the developer: Send feedback in Settings › Supporter, the menu-bar menu or
  Help. Pick idea, something broke or other, write a note, and choose whether to include the app and macOS versions
  (shown before you send) and whether a reply may go to the email you bought the key with. Nothing else is attached. Earlier notes
  show whether they were read, planned or done. Everyone else's Send feedback opens the public issues page.
- Sharing a route from the app as a supporter adds the verified mark on its own: no email to type.
- A small heart in the sidebar shows you're a supporter.
- After paying, a thank-you page says where the key is and has an Open Sidekick button that goes straight to the key
  screen (the `sidekick://supporter-key` link).
- A new key no longer fails with "already used on its maximum number of devices" when the key has no device limit.
- Become a supporter opens Polar's checkout, with three tiers: Sidekick, Partner and Hero. Every tier gets the same in
  the app. Manage opens Polar's customer portal for billing, a lost key or a change of tier.

### Look
- A new flat app icon: the Sidekick mark in white with the mint signal dot on a near-black tile. On macOS 26 it is a
  native icon, so it isn't framed in a gray tile and follows the light, dark, clear and tinted icon styles.
- The Google Meet extension uses the same icon, sized for the Chrome toolbar and the Web Store.

### Privacy guarantees
- Meetings, reviews and progress stay on your Mac. An app update may add to them and never removes or rewrites them;
  Sidekick backs up first and checks nothing was lost ([Your progress is never touched](docs/DATA-SAFETY.md)).
- Meeting audio is temporary: kept only until the after-meeting steps finish (grouping voices, the more accurate
  transcript), then deleted, also when a step fails. Turning on recording is the only way to keep it.
- Supporter key checks send a hash of your Mac's hardware ID, never the ID itself.

### Known limits
- Teams and Zoom are experimental and off until you turn them on in Connections. Sidekick reads nothing from them
  before that.
- Reviews, debriefs and live cards need an AI key (Gemini or OpenAI). A local OpenAI-compatible server is
  experimental.
