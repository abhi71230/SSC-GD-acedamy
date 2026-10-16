# SSC GD Academy by Abhi Tiwari — Free hosting starter

This is a starter project for a bilingual SSC GD practice website using:
- GitHub Pages for static hosting
- Supabase Auth for student sign-up/login
- Supabase Postgres for saved results and leaderboard RPC

## Important limitations before launch
1. The included question pool is a demonstration pool expanded to 80 by repeating/rotating 15 sample questions. It is NOT a production-quality 80-unique-question paper. Replace the demo bank with 80 unique, checked questions and verified explanations before advertising it as an actual mock test.
2. Browser-based scoring can be manipulated by a determined user. For a competitive/official leaderboard, calculate/validate scores server-side (e.g. Supabase Edge Function) and don't trust client-submitted score values.
3. The leaderboard shows the highest recent stored attempts, not necessarily one best score per student. For a serious global ranking, add a server-side policy for best score per student/test.
4. This is not affiliated with SSC. Use only question papers and content you are permitted to publish.
5. Keep personal data minimal. Display names are public on the leaderboard; tell students this clearly and offer nicknames. Do not collect unnecessary sensitive information.

## A. Create the Supabase project
1. Visit https://supabase.com/ and create a free project.
2. Open **SQL Editor**.
3. Run all SQL in `supabase-schema.sql`.
4. Open **Project Settings / API** (or the project's Connect/API section).
5. Copy the Project URL and the publishable key (or legacy anon key). Never copy the `service_role` secret to frontend code.
6. Open `index.html` and replace:
   - `PASTE_YOUR_SUPABASE_PROJECT_URL`
   - `PASTE_YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY`
7. In Supabase **Authentication → URL Configuration**, set your deployed site as Site URL and add it to Redirect URLs if requested.
8. During testing, email confirmation may require you to click a link in your inbox. Configure email settings before broad launch.

## B. Publish with GitHub Pages
1. Visit https://github.com/ and create/sign into your account.
2. Create a new public repository named `ssc-gd-academy` (or another available name).
3. Upload `index.html` to the repository root. You may also upload this README and SQL file.
4. Open **Settings → Pages**.
5. Under Build and deployment choose **Deploy from a branch**, branch `main`, folder `/(root)`, then Save.
6. Wait for GitHub Pages to publish. The URL will look like `https://YOUR-USERNAME.github.io/ssc-gd-academy/`.
7. Add that exact URL to Supabase Authentication URL Configuration and test sign-up, email confirmation, login, result saving and leaderboard in a private/incognito window.

## C. Before sharing the link
- Test on Android Chrome and a desktop browser.
- Check email confirmation and password reset flow.
- Replace all repeated sample questions with a curated, unique question bank.
- Verify all answers and explanations.
- Add Privacy Policy and contact information.
- Don't collect Aadhaar, phone numbers, or other personal data unless truly needed.
- Do not promise official ranks or official SSC affiliation.
- Free plans have quotas and terms that may change; check current provider limits.

## Architecture
Student browser → GitHub Pages frontend → Supabase Auth + Postgres (RLS-protected)
Public leaderboard → restricted `get_leaderboard()` RPC returning display name and scores only.

## Files
- `index.html` — frontend
- `supabase-schema.sql` — database table, access policies and safe leaderboard RPC
