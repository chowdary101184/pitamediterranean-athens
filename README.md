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
- Print, export, and import support

## GitHub Pages

This repo is ready to deploy from the repository root. In GitHub, open **Settings > Pages**, set the source to the `main` branch and root folder, then save.

Default demo admin passcode:

```text
1234
```

Data is stored in the browser with `localStorage`. The admin passcode is client-side only, so it is useful for a simple static workflow, not real security.
