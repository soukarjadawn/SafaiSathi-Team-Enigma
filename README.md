# SafaiSathi demo

## Open it with GPS enabled

Browser GPS usually will not work when the page is opened as a `file://` file. Run it from localhost:

1. Open PowerShell in this `outputs` folder.
2. Run `py -m http.server 8000`.
3. Open `http://localhost:8000` in your browser.
4. Allow location access when prompted.

For a deployed site, use HTTPS. The report form checks OpenStreetMap data for mapped hospitals, clinics, and railway stations within 500 metres. Nearby-place data can be incomplete or temporarily unavailable.

Use the **Map / List** switch in Community reports, Admin dashboard, or Worker portal. Google Maps needs an internet connection and a configured API key. Report pins appear only for reports submitted with GPS coordinates. Admin maps also show worker locations that have been shared; worker maps show that worker's assigned geotagged jobs and current shared location. The nearby hospital/railway lookup still uses OpenStreetMap data.

## Configure Google Maps

1. In Google Cloud Console, rotate the key that was shared in chat.
2. Enable **Maps JavaScript API** for the project and configure billing.
3. Restrict the new key to **Websites** and allow `http://localhost:8000/*` (and `http://127.0.0.1:8000/*` if you use that address). Add your deployed HTTPS domain when you publish the site.
4. Under API restrictions, allow only **Maps JavaScript API**.
5. Paste the restricted key into `maps-config.js` in place of `PASTE_ROTATED_RESTRICTED_KEY_HERE`.

The Maps key is necessarily sent to the browser and can be viewed by site visitors. Website and API restrictions are therefore essential. `maps-config.js` is listed in `.gitignore` so it is not accidentally committed.

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
