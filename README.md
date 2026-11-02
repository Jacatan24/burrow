# Burrow Focus

A cozy daily planner and pomodoro timer with Pip the hamster. It runs as a normal website in Safari or Chrome, can be added to your iPhone Home Screen, and syncs between devices with a free login.

Everything here is free: GitHub Pages hosts the website, and Firebase's free Spark plan handles login and syncing. Neither needs a credit card.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app |
| `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | App name and icons for "Add to Home Screen" |
| `firestore.rules` | Database security rules (each person can only see their own data) |

The app works right away without any setup, but it only saves on the device you're using. Steps 1–4 turn on login and syncing.

## 1. Create a Firebase project

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. Click **Create a project** (or **Add project**), name it `burrow`, and finish the wizard. You can turn Google Analytics off.

## 2. Turn on login

1. In the left menu, open **Build → Authentication** and click **Get started**.
2. Under **Sign-in method**, enable **Email/Password**.
3. Also enable **Google**, choose a support email, and save.

## 3. Create the database

1. Open **Build → Firestore Database** and click **Create database**.
2. Pick a location near you (for Vancouver, a `us-west` or `northamerica-northeast` region works) and start in **production mode**.
3. Open the **Rules** tab, replace everything with the contents of `firestore.rules`, and click **Publish**.

## 4. Connect the app to Firebase

1. Click the gear icon → **Project settings**. Under **Your apps**, click the web icon `</>`.
2. Name it `burrow-web` and register it. You don't need Firebase Hosting.
3. Firebase shows a `firebaseConfig` block. Open `index.html`, search for `FIREBASE_CONFIG`, and replace the `PASTE_...` values with yours. It looks like this:

```js
const FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "burrow-12345.firebaseapp.com",
  projectId: "burrow-12345",
  storageBucket: "burrow-12345.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abc123"
};
```

These values are safe to publish. They only identify your project; the rules from step 3 are what keep each person's data private.

## 5. Put the website online (GitHub Pages)

1. Create a free account at https://github.com if you don't have one.
2. Click **New repository**, name it `burrow`, make it **Public**, and create it.
3. Click **uploading an existing file**, drag in all the files from this folder, and click **Commit changes**.
4. Go to **Settings → Pages**. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**, then **Save**.
5. After a minute or two, your site is live at `https://YOUR-GITHUB-USERNAME.github.io/burrow/`.

## 6. Allow your website to use the login

In Firebase, go to **Authentication → Settings → Authorized domains**, click **Add domain**, and add `YOUR-GITHUB-USERNAME.github.io`. Without this, Google sign-in shows an error.

## 7. Install it on your iPhone

1. Open your site in **Safari**.
2. Tap **Share → Add to Home Screen**.
3. Open Burrow from the Home Screen, tap the **Sign in** chip in the top right, and log in.
4. Sign in with the same account on your computer and everything stays in sync.

## Updating the app later

Edit `index.html` (or get an updated copy), then upload it to the same GitHub repository. Pages redeploys automatically within a minute or two.

## Notes

- If you sign in on a device that already has data, whichever copy was changed most recently wins.
- On iPhone, the timer keeps correct time in the background, but the chime can only play while Burrow is open on screen.
- Google sign-in from a Home Screen app can sometimes open a separate browser window. Email and password always works.

## AI helper (optional, free)

1. In the Firebase console, open **AI services → AI Logic** and click **Get started**.
2. Choose **Gemini Developer API** (the free option) and finish the steps.
3. That's it. The ✦ buttons in Burrow (Plan my day, Sort with AI, Brain dump, Break it down) now work.

## Notifications

On iPhone, open Burrow from your Home Screen, then go to **Settings → Notifications → Turn on notifications**. Notifications fire while Burrow is open (or in a background tab on a computer). iPhone pauses web apps that are fully closed, so reminders can't arrive then.
