# Boblitz.exe

A responsive, personal anime catalogue with Supabase login + cloud database, AniList search, watch progress, reviews, character wall, calendar, collections and a local-file reference shelf.

## 1. Create the private database

1. Create a free project at https://supabase.com/.
2. In the Supabase dashboard, open **SQL Editor → New query**.
3. Paste all of `supabase-schema.sql` and run it.
4. Open **Project Settings → API** (or **API Keys**).
5. Copy the Project URL and the `anon` / publishable public key.
6. Paste both into `config.js`. Never use the `service_role` or secret key in browser code.
7. In **Authentication → URL Configuration**, add your eventual deployed website URL to the allowed Site URL / Redirect URLs. During local testing add `http://localhost:8000/**`.

## 2. Test on your computer

You need Python installed. Open a terminal in this folder and run:

```bash
python -m http.server 8000
```

Then visit http://localhost:8000. Create an account. If email confirmation is enabled, confirm the email before logging in.

## 3. Publish online with GitHub + Vercel

1. Create a GitHub account and a new **private** repository named `boblitz-exe`.
2. Upload the contents of this folder to that repository.
3. Create an account at https://vercel.com/ and import the repository.
4. Vercel can deploy this static site without a build command. Set the output directory to `.` if asked.
5. Add your deployed domain to Supabase Authentication URL Configuration.
6. Open the Vercel URL on your PC and phone. Log in with the same account on both.

The website files may be in a private GitHub repository, but the deployed site itself is reachable by URL. The Supabase login and row-level security policies protect your archive data. Keep the anon/public key in the client; database security comes from RLS, not hiding that key.

## 4. Install on your phone

Open the deployed HTTPS URL in your phone browser:
- Android / Chrome: browser menu → **Install app** or **Add to Home screen**.
- iPhone / Safari: Share → **Add to Home Screen**.

The service worker caches the app shell. Your database data still needs an internet connection to sync. The app is responsive and works on desktop and mobile.

## Important notes

- Anime catalogue search uses the public AniList GraphQL API. Its data and availability are controlled by AniList.
- Reviews, watch progress, collections, character entries, calendar events and file references are saved to your Supabase account.
- The quick note is stored only in the current browser on the current device (localStorage), not synced. Do not use it for sensitive information.
- The local video shelf stores metadata only. Browsers cannot preserve arbitrary local file paths across devices. Your video files stay on your own device; use a media player on the device that stores them. Do not upload copyrighted episodes to this website.
- This is a starter app. Before relying on it long-term, add backups/export, stronger error handling, and test account recovery.
