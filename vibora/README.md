# VIBORA — Live music & lyrics

A responsive React + Vite music player with a live Audius catalogue integration and LRCLIB lyrics lookup.

## What works

- **Live music discovery:** loads trending tracks from the Audius public read API.
- **Live search:** searches Audius tracks and artists; selecting a result streams it through the Audius track-stream endpoint.
- **Lyrics:** looks up the current song in LRCLIB, preferring synced LRC lyrics and highlighting the current line while audio plays. Plain lyrics are shown when timed lyrics are unavailable.
- **Player:** play/pause, previous/next, seek, volume, shuffle, repeat and queue.
- **Library:** liked songs, recently played, playlists, and local audio-file uploads.
- **Personal recommendations:** on-device ranking based on liked songs, recent plays, artist and genre affinity.
- **Responsive luxury interface:** desktop, tablet and mobile layouts.

## Run locally

Requires Node.js 20.19+ or 22.12+.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite.

## Build for deployment

```bash
npm run build
npm run preview
```

The production site is generated in `dist/`.

## Deploy to GitHub Pages

1. Push this folder to a GitHub repository.
2. In **Settings → Pages**, select **GitHub Actions**.
3. Add this workflow as `.github/workflows/deploy.yml` (already included).
4. Push to the `main` branch. The workflow builds and publishes `dist/`.

Vite uses relative asset paths for GitHub Pages.

## Live provider integrations

### Audius

VIBORA uses the Audius public read API for trending discovery, track search and streaming. Most read-only endpoints are available without credentials; Audius recommends an API key for higher rate limits. If you later add a key, keep any secret server-side rather than embedding it in the browser bundle. Streaming availability depends on each creator's track settings and provider availability.

- API reference: https://docs.audius.co/api/
- Streaming guide: https://docs.audius.co/developers/api/stream-url/

### Lyrics (LRCLIB)

VIBORA calls `https://lrclib.net/api/get` for a track signature, then falls back to `/api/search` when a duration/signature match is unavailable. Synced LRC lines are highlighted against the audio playback clock. Lyrics may not exist for every song, and timed lyrics are not guaranteed.

- API documentation: https://lrclib.net/docs

## Storage and account limitations

This is a functioning browser app, but it is not yet a multi-user SaaS backend:

- Likes, playlists and listening history are saved in the current browser's local storage.
- Uploaded files use browser object URLs and are available only in the current session; they are not uploaded to a server or shared across devices.
- There is no user authentication, cloud database, admin upload portal, payment system or subscription enforcement in this build.
- The included recommendation engine is a local taste-based recommender, not a remote generative-AI service.

For a production multi-user launch, connect Supabase (Auth, Postgres and Storage), add server-side authorization and upload validation, and review provider licensing/terms for your intended territories and business model. Audius is an open creator catalogue; it is not a guarantee of access to every commercial recording. Do not upload or stream music unless you have the necessary rights.

## Attribution

- Music catalogue and streaming: Audius (track and artist attribution is displayed in VIBORA's track list).
- Lyrics metadata and text: LRCLIB. Availability varies by song.
