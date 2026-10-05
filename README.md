# SongForge: AI Music Studio (ISM4421Suno)

A single-page web app for generating music with the [Suno API](https://docs.sunoapi.org).
It's plain HTML, CSS and JS with no build step and no backend. It deploys to Netlify as a static site.

## Features
- **Simple mode**: describe a song and Suno writes the lyrics and music. Includes one-click idea prompts.
- **Custom mode**: title, your own lyrics, style tags, vocal gender, excluded styles, length (10–360s), style adherence, weirdness and variety.
- **AI lyric writer**: turn a short idea into lyrics, then pick one version to use.
- **Models**: V6 (default), V6 Wild and V6 Mini.
- **Live progress**: polls the task status and plays a streaming preview before the final file is ready.
- **Library**: stored in the browser. Includes a player, cover art, download, lyrics view, copy link, reuse settings and delete.
- **Extend**: continue any generated track from a timestamp you choose.
- **Credit balance** shown in the header.
- **Personalized**: asks for your name on first visit, then greets you and uses your name in status messages. Click "hi, <name> ✏️" to change it.
- **Pink & white polka-dot** design that works on desktop and mobile.

## Login (Supabase email auth)
The app is behind an email + password login powered by Supabase Auth
(project `songforge`, ref `tokuawtoxczyytmetsnk`). Sign-in, sign-up, forgot-password and sign-out are built in.
Each account gets its own library, API key and name in the browser, and the name typed at sign-up is saved to the account.
The Supabase URL and **publishable** key are in `index.html`. They're meant to be public, and access is enforced by Supabase Auth.

**One-time Supabase dashboard setup** (Authentication → URL Configuration):
- **Site URL**: your Netlify URL, e.g. `https://your-site.netlify.app`
- **Redirect URLs**: add `https://your-site.netlify.app/**`

Optional: Authentication → Sign In / Providers → Email → turn off **Confirm email** if you want people to sign in right after signing up.
Supabase's built-in email sender is limited to a few emails per hour, so add custom SMTP for real traffic.
You can see who signed up and when they last signed in under Authentication → Users.

## Profiles
Every account gets a profile row automatically when it signs up (a database trigger seeds it with the sign-up name).
New users see a "Set up your profile" screen. After that, click your avatar or "hi, <name> ✏️" to edit it.
- **Photo**: uploaded to the `avatars` Storage bucket under `<user id>/` (PNG/JPG/WebP/GIF, max 2 MB). The old photo is deleted when it's replaced.
- **Display name**: drives all the personalized greetings.
- **@username**: unique, 3–30 characters of lowercase letters, numbers and `_`. Taken names are rejected with a friendly message.
- **Bio**: up to 280 characters.
- **Favorite genres**: up to 10, shown first (★) in the style tags.
- **Default model**: preselected in the composer.

Database: `public.profiles`, with Row Level Security so each user can only read and update their own row.
Schema and policies are in [`supabase/migrations/`](supabase/migrations/).

## API key
Each user enters their own Suno API key (get one at https://sunoapi.org/api-key) with the 🔑 button.
The key is saved only in that browser's `localStorage` and is sent only to `api.sunoapi.org`.
No key is stored in this repo.

## Deploy to Netlify
1. In Netlify, choose **Add new site → Import an existing project** and pick this repo.
2. Branch: `main`. Leave the build command empty. Set the publish directory to `.` (`netlify.toml` already sets this).
3. Deploy, open the site, and paste your API key.

You can also drag this folder into https://app.netlify.com/drop.

## Run locally
Open `index.html` in a browser, or serve the folder (for example `npx serve .`).

Generated audio is hosted by Suno for about 14 days, so download anything you want to keep.
