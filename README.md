# Pita Mediterranean Athens Store Hours

Static employee schedule manager for store working hours.

## Features

- Weekly employee schedule calendar
- Admin passcode mode for editing
- Add, edit, archive, and delete employees
- Add, edit, delete, and color-code shifts
- Employee-specific weekly schedule view
- Calendar filtering, daily totals, and employee weekly totals
- Shift checks for overlaps, inactive employees, and store-hour issues
- Optional Firebase shared database mode
- Print, export, and import support

## GitHub Pages

This repo is ready to deploy from the repository root. In GitHub, open **Settings > Pages**, set the source to the `main` branch and root folder, then save.

## Shared edits with Firebase

By default, the app stores data in each browser with `localStorage`. To make employee and shift edits visible to everyone, connect Firebase Firestore.

1. Create a Firebase project.
2. In Firebase, create a Web app and copy the Firebase config.
3. Enable **Firestore Database**.
4. Enable **Authentication > Sign-in method > Google**.
5. In **Authentication > Settings > Authorized domains**, add:

```text
chowdary101184.github.io
```

6. Edit `firebase-config.js`:
   - Replace the `YOUR_...` values with your Firebase web config.
   - Replace `your-admin-email@example.com` with the Google account that can edit schedules.
7. Edit `firestore.rules` and replace the same admin email.
8. In Firebase Firestore **Rules**, paste the contents of `firestore.rules` and publish.
9. Commit and push the updated `firebase-config.js`.
10. Open the GitHub Pages site, sign in with Google, then click **Publish shared schedule** once.

Public visitors can read the latest schedule. Only the admin email in `firebase-config.js` and `firestore.rules` can write changes.

If Firebase is not configured, the app automatically falls back to browser-only local storage.

Default demo admin passcode:

```text
1234
```

The demo passcode applies only to local fallback mode. Shared Firebase mode uses Google sign-in and Firestore security rules.
