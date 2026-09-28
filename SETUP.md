# Notes board — setup

The Notes board at the bottom of `contact.html` (and the standalone `family-chat.html`)
is a shared, password-protected message board. Both pages read and write the same
conversation, so it doesn't matter which one anyone uses.

Until the config below is filled in, the board shows **"Not configured yet."** and the
sign-in does nothing. That is the expected state of a fresh checkout.

## Why it needs Firebase

These pages are static files — there is no server of ours to check a password or store
messages. A password compared in JavaScript would sit in plain sight in the page source,
and anything saved in the browser stays in that one browser, so nobody else would ever
see it. Firebase gives us a password check and a message store that run on Google's
servers instead, which is what makes the board both private and actually shared.

## One-time setup (about 5 minutes)

1. **console.firebase.google.com** → Create project. The free Spark plan is enough.
2. **Build → Realtime Database → Create Database → locked mode.**
3. **Build → Authentication → Sign-in method → enable Email/Password.**
4. **Authentication → Users → Add user.** Create exactly one account:
   - Email: `notes@anayasuits.example` — must match `FC_ACCOUNT` in both HTML files.
     It never receives mail, so it doesn't have to be a real address, but it does
     have to be spelled identically in both places.
   - Password: **your 4 digits followed by `-anaya-notes`.** For code `1234` you
     type `1234-anaya-notes` here. Family only ever types the 4 digits.

   Firebase rejects passwords shorter than 6 characters, which is the only reason
   the suffix exists. The page appends it to whatever is typed. It is not secret
   and adds no security — the 4 digits are the whole secret.
5. **Project settings → General → Your apps →** web icon → register app → copy the
   `firebaseConfig` values.
6. Paste those five values over the `REPLACE_ME` placeholders in **both** files:
   - `contact.html` → `fcFirebaseConfig`
   - `family-chat.html` → `firebaseConfig`
7. **Realtime Database → Rules →** publish:
   ```json
   { "rules": { "family-chat": { ".read": "auth != null", ".write": "auth != null" } } }
   ```

## How signing in works

One field, four digits. There is no email and no name. Typing the fourth digit submits
automatically — no button press needed, though the button still works. The page appends
`FC_SUFFIX` and signs in as the single `FC_ACCOUNT` above, so the code is checked by
Google and never appears in the page source.

Messages carry **no sender name**. Each one shows only a timestamp, with your own on the
right and everyone else's on the left. That side-of-the-thread split comes from a random
id stored in each browser, not from the account, so it is a display convenience and
nothing more — clearing site data makes your old messages appear on the left.

**To change the code**, edit that one user's password in the Firebase console, keeping
the `-anaya-notes` suffix. No file changes, and it takes effect for everyone immediately.

## Photos

The paperclip in the compose bar attaches a photo. Images only — PDFs and documents
aren't supported.

Nothing full-resolution ever leaves the browser. Each photo is redrawn at a smaller size
before it's sent: a 1200px version that opens when the photo is tapped, and a 420px
thumbnail that sits in the thread. A 5 MB phone photo lands at roughly 250-450 KB once
stored. Both live in the database you already set up, under `family-chat/images` and in
the message itself, so the existing rules cover them and there is nothing extra to
configure.

The thread only ever loads thumbnails. The full picture is fetched when someone taps it,
which is what keeps the monthly transfer allowance from draining.

**Deleting.** Hover a message you sent and a small x appears; it removes the message and
its photo. The button only shows on messages from your own browser, but that is a display
choice, not a rule — everyone shares one account, so anyone signed in could delete
anything if they went looking. Treat the board as a shared notebook, not as private
per-person storage.

**Watching usage.** Firebase console -> Realtime Database -> **Usage** tab shows storage
and downloads against the no-cost limits (1 GB stored, 10 GB/month transferred). At a few
photos a week you will not come close, but that tab is where to look if you ever wonder.
Old photos can be deleted from the thread, or wholesale under Data -> `family-chat/images`.

## What to expect

- **Stays signed in.** Firebase keeps the session in the browser, so returning visitors
  go straight to the board without retyping the password. "Sign out" ends it.
- **Live updates.** New messages appear without a reload, for anyone with the page open.
- **History.** The last 200 messages load on sign-in. Older ones stay in the database and
  can be read in the console under Realtime Database → Data → `family-chat/messages`.
- **No notifications.** Someone has to have the page open to see a message arrive. Push
  would need Firebase Cloud Messaging or an email/webhook trigger, which isn't built.

## Security, honestly

- The Firebase config in the page source is **meant** to be public. It identifies the
  project, it doesn't grant access. The database rules plus the password are what
  protect the data.
- **Four digits is only 10,000 combinations.** That is weak against anyone determined
  enough to script guesses. Firebase throttles repeated failures from the same source
  and the board reports "Too many tries" when it does, which blunts a casual attack, but
  it is not real protection against a patient one. Fine for keeping a family thread away
  from passing eyes; not fine for anything you'd be harmed by losing. A longer code is a
  one-line change to that user's password if you want it.
- One shared code means no way to revoke one person without changing it for everyone,
  and messages are anonymous, so there is no way to tell who wrote what beyond which
  browser it came from.
- Anyone who learns the password can read the entire history, not just messages from
  after they joined.
