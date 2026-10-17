# Security

Sidekick hears meetings. A bug that leaks audio, transcripts, notes or keys is the most serious kind we can have, and
we treat reports about it before anything else.

## Reporting

Email **security@learnwithsidekick.com** with what you found, how to reproduce it and what it exposes. Please do not open
a public issue. You will get an answer within two working days, and credit in the release notes if you want it.

## In scope

- Anything that sends audio, transcripts, summaries, people notes or keys off the Mac, other than to the AI provider
  the user chose with their own key.
- The local API (`127.0.0.1:8765`): requests from web pages, other users on the Mac, or anything that bypasses its
  origin checks or the token other AI apps use to connect.
- The browser extension: anything a web page can make it do.
- The account service (sign-in and supporter checks): forging or replaying supporter or account tokens, taking over
  a sign-in, or reading someone else's account.
- Updates and the downloaded whisper models: anything that makes the app run code or load a model it should not.

## Out of scope

- Someone with full access to your macOS account reading `~/Sidekick` or the database: that is by design, it is your
  data in plain files.
- The supporter badge being unlocked by patching the app: it unlocks a badge (`docs/SECURITY-LICENSING.md`).
