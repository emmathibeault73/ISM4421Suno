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
