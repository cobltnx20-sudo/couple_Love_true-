# HeartLens — Couple Connection Test

A mobile-friendly Malayalam + English couple reflection quiz. Both partners answer separately, and the comparison is revealed only after both submit.

## Important
This is a starter project. To make cross-device links and saved answers work, you must connect a Firebase project and publish this site. A quiz cannot reliably save answers across two phones with HTML/localStorage alone.

The quiz is **not** a scientific test and cannot determine whether a partner's love is true or fake. It compares multiple-choice answers and gives prompts for honest conversation.

## Part 1 — Create Firebase (free tier may be sufficient for a small personal project)

1. Open https://console.firebase.google.com/ in your phone browser and sign in.
2. Tap **Create a project** and give it a name, e.g. `heartlens-couple`.
3. In Project settings, add a **Web app** and copy its Firebase configuration.
4. From **Build → Realtime Database**, create a database. Choose a nearby region.
5. From **Build → Authentication → Sign-in method**, enable **Anonymous** sign-in.
6. Open `index.html` in a text editor and find `const firebaseConfig = {`.
7. Replace the placeholder values with the real `apiKey`, `authDomain`, `databaseURL`, `projectId`, and `appId` from your web app config. Keep the quotes.

## Part 2 — Database rules

For a simple prototype, these rules require anonymous sign-in but allow signed-in visitors to read/write room data. Because this is a public share-link quiz, anyone with the room link could potentially access or alter that room. Do not use it for sensitive information. For a production website, use server-enforced room membership and per-room access controls.

In Realtime Database → Rules, use:

```json
{
  "rules": {
    "rooms": {
      "$roomId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```

Press **Publish**. These prototype rules are intentionally simple, not production-grade privacy/security.

## Part 3 — Publish from your phone using GitHub Pages

1. Create/sign in to GitHub: https://github.com/
2. Create a new public repository, e.g. `heartlens-couple`.
3. Upload `index.html` to the repository root.
4. Go to **Settings → Pages**.
5. Under Build and deployment, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
6. Wait for the published URL to appear. Open that URL on your phone.
7. Create a couple room, then share the unique link with your partner. Each person chooses their own name and submits answers. The report unlocks when both have submitted.

## Troubleshooting
- If the page says “Setup needed”, the Firebase config is still placeholder text.
- If database access is denied, check that Anonymous Authentication is enabled and the rules were published.
- If the share URL is wrong, use the GitHub Pages URL, not the repository page.
- The link is a bearer link: anyone who gets it may be able to open the room. Don't enter secrets or highly sensitive details.
- This starter does not include an admin dashboard or a deletion button. Delete rooms manually from Firebase Realtime Database when no longer needed.

## Files
- `index.html` — responsive quiz app.
- `README.md` — setup and publishing instructions.
