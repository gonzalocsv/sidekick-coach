# Sidekick privacy policy

_Last updated: 2026-10-16_

**The short version:** Sidekick runs on your Mac. Your meetings, transcripts, notes and the people you track are
stored on your computer, in folders you can open. We never see them.

## What Sidekick processes, and where
- **Audio of your meetings** is captured on your Mac. With transcription **on this Mac** (whisper.cpp), it never
  leaves your computer. With transcription by **Google Gemini or OpenAI**, it is streamed to that provider using
  **your own API key**, under that provider's terms. It is never sent to us. Audio is kept on disk only until the
  after-meeting steps are finished (grouping voices on your Mac, the more accurate transcript), then deleted, also when
  a step fails, unless you choose to keep a recording.
- **Meetings you import** (a transcript file or a recording you drop on the app) are read on your Mac and stored like
  any other meeting. The text goes to your AI provider to write the debrief and the review, as after a live meeting.
- **Transcripts, summaries, cards, people notes, commitments, prep documents** are stored in `~/Sidekick/` and a
  local database in `~/Library/Application Support/MeetingHUD/`. They never leave your Mac except as part of the
  AI requests above.
- **Your calendar** is read through macOS Calendar, on your Mac, to know who is in a meeting.
- **Google Meet** page content (meeting name, participant names, captions speaker) is read by the Sidekick browser
  extension and sent only to the app on your computer. Teams and Zoom are read the same way only if you turn them on.
- **Other AI apps on your Mac** (Claude, Cursor) can read your meetings only if you turn that on in Settings; they
  connect to the app on your computer, and what they do with it is under their own terms.

## What we receive
- **Our account service** is one small server we run on Google Cloud (Cloud Run, with its data in Firestore, in the
  United States). It checks supporter keys and receives supporters' feedback. There are no online accounts: signing in
  to Sidekick is a profile on your Mac. To limit abuse it counts requests per IP
  address for one minute, in memory; addresses are not stored.
- **License checks:** only if you enter a supporter key: the key, a device name and an anonymous device identifier,
  sent to our account service and to Polar, our merchant of record, to activate it and to check it once a day.
  Nothing about your meetings is included. Without a key, the free app makes no license calls.
- **Feedback (supporters):** only when you click Send. We receive what you typed, what kind of note it is, and, if you
  leave that box ticked, the app version and macOS version shown next to it. Nothing else is attached: no logs, no
  transcripts. If you tick "You can reply", we keep the email your supporter key was bought with, so we can answer.
  Feedback is linked to a one-way hash of your key, so the app can show you its status. We keep it until it is dealt
  with; write to us to have yours deleted sooner.
- **Transcription models:** only when you choose transcription on this Mac and click Download, the app downloads the
  model file from its public host (Hugging Face). The request carries nothing about you beyond your IP address.
- **The community library:** only when you click Browse library or Install, the app downloads the library index and
  the route you chose from GitHub (raw.githubusercontent.com). The request carries nothing about you beyond what any
  web request carries (your IP address); we do not count installs.
- **Payments:** handled by Polar as merchant of record (or GitHub Sponsors, if you sponsor there); we receive your
  email and order details. To mark route authors who are supporters, our account service keeps a one-way hash of each
  supporter's email and whether the support is active; not the email itself.
- **Support:** whatever you choose to send us. Diagnostic logs contain no transcript text.

We do not run analytics or telemetry in the app.

## The website (learnwithsidekick.com)
- **Analytics:** if turned on, a cookieless counter (no cookies, no cross-site tracking) counts page views.
- **Community route submissions:** the form sends the route text, the name and the profile link you enter. They
  become a public pull request on GitHub, credited to that name and link. If you enter a supporter email or order id,
  it is used once to check our supporter list and is not stored, logged or published. The app sends a supporter's
  signed supporter token instead of an email, checked once by our account service in the same way. To limit abuse, a hash of your
  IP address is kept for up to an hour.
- **Downloads** come from GitHub Releases, under GitHub's terms.

## AI providers
Requests go directly from your Mac to Google or OpenAI with your key, or nowhere when transcription runs on your Mac
and you point cards and reviews at a server of your own. Use a key from a **billing-enabled** project:
on Google's free tier, Google may use your data to improve its models. See each provider's data policy.

## Recording and consent
You are responsible for complying with recording and consent laws where you and your meeting participants are.
Sidekick shows a reminder the first time you start listening.

## Your rights
Delete anything by deleting the files or using the app; uninstalling removes the app, your data folder stays until
you delete it. For license or payment data, contact support@learnwithsidekick.com.
