<p align="center"><img width="96" src="frontend/public/256.png" alt="Soundkeep logo"></p>
<h1 align="center">Soundkeep</h1>

<p align="center"><b>Your music, kept.</b><br>A self-hosted music library: paste a Spotify, YouTube Music, Deezer or SoundCloud link and get a perfectly tagged audio file, then play it from any browser.</p>

<p align="center">
  <a href="#quick-start">Quick start</a> •
  <a href="#run-it-without-docker">Run without Docker</a> •
  <a href="#features">Features</a> •
  <a href="#credits-and-license">Credits</a>
</p>

---

## What it is

Soundkeep runs on your own computer or home server. You give it a link, it finds the song, downloads the audio, and writes the title, artists, album, cover art and lyrics into the file. Everything lands in a folder you choose, and the built-in web player lets you listen to your library straight away.

No Spotify account, Premium subscription or API key is needed.

```
Spotify / Deezer page  →  YouTube Music search  →  yt-dlp + ffmpeg + mutagen
     (metadata)               (audio match)            (download & tag)
```

## Quick start

You only need [Docker](https://docs.docker.com/get-docker/).

```bash
git clone https://github.com/khalilbrikTN/SoundKeep.git
cd SoundKeep
docker compose up -d --build
```

Open [http://localhost:8000](http://localhost:8000) and sign in:

| Username | Password   |
| -------- | ---------- |
| `admin`  | `downtify` |

Change that password straight away in **Settings → General**. Music is saved to `./docker/downloads`, and settings and accounts to `./docker/data`. Edit the `volumes:` in `docker-compose.yml` to use other folders.

Forgot the admin password? Run `python main.py auth-reset` (or `docker compose exec downtify python main.py auth-reset`) to put back `admin` / `downtify`.

## Run it without Docker

You need Python 3.10+, [uv](https://docs.astral.sh/uv/), Node.js and [ffmpeg](https://ffmpeg.org/) on your `PATH`.

```bash
uv sync
npm --prefix frontend ci
npm --prefix frontend run build
```

Then start the server, pointing it at your music folder:

```powershell
# Windows (PowerShell)
$env:DOWNLOAD_DIR = 'D:\spotify music'
$env:DATABASE_DIR = "$PWD\data"
$env:WEB_GUI_LOCATION = "$PWD\frontend\dist"
uv run python main.py web
```

```bash
# macOS / Linux
DOWNLOAD_DIR=~/Music/soundkeep DATABASE_DIR=./data \
WEB_GUI_LOCATION=./frontend/dist uv run python main.py web
```

> [!TIP]
> On Windows, if the project folder's path contains `&`, `npm run build` fails. Run `node node_modules/vite/bin/vite.js build` from inside `frontend/` instead.

## Features

| | |
| --- | --- |
| **Download** | Spotify tracks, albums, playlists and artists; YouTube Music, Deezer and SoundCloud links; free-text search; CSV imports from Soundiiz, TuneMyMusic and Exportify. MP3, FLAC, M4A, OGG or OPUS. |
| **Tags & lyrics** | Title, artists, album, year and cover art in every file, an explicit marker, and plain or time-synced lyrics from LRCLIB and NetEase. |
| **Library** | Albums, artists, playlists and tracks with search, sorting and multi-select. Create your own playlists, import folders you already have, and repair old files with **Upgrade library**. |
| **Player** | Full-screen player with synced lyrics, a karaoke view, an editable queue, a sleep timer, an equalizer and volume normalization. |
| **Playlist Monitor** | Watch playlists and artists; new songs and releases download on a schedule. |
| **Discover** | Charts, similar songs and artist suggestions based on what you listen to. |
| **Podcasts** | Subscribe by RSS feed or Spotify link; new episodes download by themselves. |
| **Users** | Accounts for everyone in the house, a shared library, per-user likes and playlists, and an activity log. |
| **Integrations** | Optional Soulseek downloads through slskd, Navidrome playlist mirroring, and M3U files for Jellyfin and Plex. |
| **Interface** | Light and dark themes, works from phone to widescreen, installable as an app (PWA), and available in 12 languages. |

## Troubleshooting

Most download problems come from YouTube wanting a signed-in session. Upload a `cookies.txt` in **Settings → YouTube cookies** and they usually go away. If YouTube still rate-limits you, raise *Delay between downloads* and lower *Parallel downloads*.

## Credits and license

Soundkeep is a fork of [**Downtify**](https://github.com/henriquesebastiao/downtify) by Henrique Sebastião and its contributors. The full feature reference, environment variables and API documentation live in the [Downtify documentation](https://downtify.henriquesebastiao.com/), which still applies to Soundkeep.

Licensed under the [GNU AGPL-3.0](LICENSE). If you run a modified version for other people over a network, you must offer them its source code.

> [!WARNING]
> You are responsible for what you download. Only download music you have the right to.
