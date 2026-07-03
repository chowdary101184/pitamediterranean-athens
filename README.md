# Pita Mediterranean Athens Store Hours

Static employee schedule manager for store working hours.

## Features

- Weekly employee schedule calendar
- Google sign-in admin mode for editing
- Add, edit, archive, and delete employees
- Add, edit, delete, and color-code shifts
- Employee-specific weekly schedule view
- Calendar filtering, daily totals, and employee weekly totals
- Shift checks for overlaps, inactive employees, and store-hour issues
- Firebase shared database mode
- Print, export, and import support

## GitHub Pages

This repo is ready to deploy from the repository root. In GitHub, open **Settings > Pages**, set the source to the `main` branch and root folder, then save.

## Remote data with Firebase

The app uses Firebase Firestore as the source of truth. Employee and shift edits are stored remotely so everyone sees the same schedule. Browser local storage is not used for schedule data.

### Create the Firebase project

1. Go to [Firebase Console](https://console.firebase.google.com/).
2. Sign in with a Google account, or create one if you do not already have one.
3. Click **Create a project** or **Add project**.
4. Enter a project name, for example `pitamediterranean-athens`.
5. Google Analytics is optional for this app. You can disable it to keep setup simpler.
6. Finish project creation and open the new Firebase project.

### Register this web app

1. From the Firebase project overview, click the web icon, usually shown as `</>`.
2. Enter an app nickname, for example `store-hours-admin`.
3. Firebase Hosting is optional because this app can be hosted with GitHub Pages.
4. Click **Register app**.
5. Copy the Firebase config object shown by Firebase.
6. Paste those values into `firebase-config.js`.

The config should look like this shape:

```js
window.STORE_HOURS_FIREBASE_CONFIG = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT_ID.firebasestorage.app",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID",
  measurementId: "YOUR_MEASUREMENT_ID"
};
```

### Create the Firestore database

1. In Firebase, open **Firestore Database**.
2. Click **Create database**.
3. Choose **Firestore Native** mode if asked.
4. Choose a location close to your store or users. For this project, `nam5` is fine.
5. Start in production mode if Firebase asks for a security mode.
6. Finish database creation.

### Enable Google admin sign-in

1. In Firebase, open **Authentication**.
2. Click **Get started** if this is the first time opening Authentication.
3. Open **Sign-in method**.
4. Enable **Google** as a provider.
5. Choose a support email and save.
6. Open **Authentication > Settings > Authorized domains**.
7. Add only the domain names, not full URLs:

```text
chowdary101184.github.io
localhost
```

### Add admin emails

Add every admin email in `firebase-config.js`:

```js
window.STORE_HOURS_ADMIN_EMAILS = [
  "ciwa09@gmail.com",
  "manager@example.com"
];
```

Then add the same emails in `firestore.rules`:

```js
allow write: if request.auth != null
  && request.auth.token.email in [
    "ciwa09@gmail.com",
    "manager@example.com"
  ];
```

The email list must match in both files. `firebase-config.js` controls the admin UI, while `firestore.rules` protects the database.

### Publish Firestore rules

1. In Firebase, open **Firestore Database > Rules**.
2. Replace the existing rules with the contents of `firestore.rules`.
3. Click **Publish**.

### Publish the first schedule

1. Commit and push `index.html`, `firebase-config.js`, and `firestore.rules`.
2. Open the GitHub Pages site.
3. Sign in with one of the admin Google accounts.
4. Click **Publish shared schedule** once.
5. After that, any employee or shift edit is saved to Firestore and becomes visible to everyone.

Public visitors can read the latest schedule. Only the admin email in `firebase-config.js` and `firestore.rules` can write changes.

If Firebase is not configured or cannot load, the app shows remote-unavailable mode instead of saving schedule data locally.

## Google sign-in troubleshooting

If sign-in fails, check these first:

- Firebase **Authentication > Sign-in method > Google** is enabled.
- Firebase **Authentication > Settings > Authorized domains** contains the domain only, not the full URL. Use `chowdary101184.github.io` for GitHub Pages and `localhost` for local testing.
- Local testing uses a local server such as `http://localhost:8765`, not a direct `file://` browser open.
- Popups are allowed for the site.
