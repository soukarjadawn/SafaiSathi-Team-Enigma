# SafaiSathi demo

## Open it with GPS enabled

Browser GPS usually will not work when the page is opened as a `file://` file. Run it from localhost:

1. Open PowerShell in this `outputs` folder.
2. Run `py -m http.server 8000`.
3. Open `http://localhost:8000` in your browser.
4. Allow location access when prompted.

For a deployed site, use HTTPS. The report form checks OpenStreetMap data for mapped hospitals, clinics, and railway stations within 500 metres. Nearby-place data can be incomplete or temporarily unavailable.

## Demo accounts

- Admin: ID `admin`, password `safai123`
- Worker: `W-101` / `1234`, `W-102` / `2345`, or `W-103` / `3456`

## What the automation does

- Three reports from different names within 200 metres in 24 hours are flagged **Urgent** (when GPS is available; otherwise, exact matching location text is used).
- Three reports with the same name at that location in 24 hours are flagged for **manual review**. This is a spam signal, not proof of fraud.
- Reports near a mapped hospital, clinic, or railway station are flagged as sensitive and raised to high priority.
- Workers must press **Share live GPS** and grant location permission. Sharing stops when they press Stop sharing or sign out. The admin sees the most recently shared location and timestamp.

## Demo limitation

Reports, assignments, and worker locations use this browser's local storage. The tabs can share data in the same browser profile, but separate devices do not sync. Demo logins are visible in the frontend and are not secure accounts. Use Firebase Authentication, Firestore, and Storage with security rules before using this with real workers or residents.
