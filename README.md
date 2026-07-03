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

1. Create a Firebase project.
2. In Firebase, create a Web app and copy the Firebase config.
3. Enable **Firestore Database**.
4. Enable **Authentication > Sign-in method > Google**.
5. In **Authentication > Settings > Authorized domains**, add:

```text
chowdary101184.github.io
localhost
```

6. Confirm `firebase-config.js` has your Firebase web config and admin email.
7. Confirm `firestore.rules` has the same admin email.
8. In Firebase Firestore **Rules**, paste the contents of `firestore.rules` and publish.
9. Commit and push the Firebase files.
10. Open the GitHub Pages site, sign in with Google, then click **Publish shared schedule** once.

Public visitors can read the latest schedule. Only the admin email in `firebase-config.js` and `firestore.rules` can write changes.

If Firebase is not configured or cannot load, the app shows remote-unavailable mode instead of saving schedule data locally.

## Google sign-in troubleshooting

If sign-in fails, check these first:

- Firebase **Authentication > Sign-in method > Google** is enabled.
- Firebase **Authentication > Settings > Authorized domains** contains the domain only, not the full URL. Use `chowdary101184.github.io` for GitHub Pages and `localhost` for local testing.
- Local testing uses a local server such as `http://localhost:8765`, not a direct `file://` browser open.
- Popups are allowed for the site.
