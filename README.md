# mpv-tube

mpv configured to behave like a dedicated YouTube client, meant to live at
`~/.config/mpv`.

## Why "mpv-tube"

- **SponsorBlock ad-skipping** — [YAS](https://github.com/edieguez/yas)
  (YouTube Ad Skipper) automatically skips sponsor segments and ads using
  the community SponsorBlock database.
- **Zero-wait playlist transitions** —
  [ytdl-prefetch](https://github.com/edieguez/ytdl-prefetch) resolves both
  neighboring playlist items' yt-dlp data in the background while the
  current one plays, so skipping to the next/previous YouTube video is
  near-instant instead of the usual multi-second yt-dlp resolution.
- **A persistent, perpetual queue** —
  [perpetual-playlist](https://github.com/edieguez/perpetual-playlist)
  saves the full playlist and exact resume position across restarts.
  `ctrl+v` inside mpv, or `mpv-add <url>` from a terminal (or a browser
  extension/shortcut), appends a URL to a running instance the same way
  you'd queue a video on youtube.com, without interrupting what's
  currently playing.
- **YouTube-style keyboard shortcuts** — `j`/`l` seek ±10s, arrow keys seek
  ±5s, number keys `0`–`9` jump to 0%–90% of the video, mirroring
  YouTube's own web player bindings.
- **In-player quality picker** — `F` opens a yt-dlp format/quality menu
  without leaving mpv.
- **One-key download** — the OSC's download button saves the current video
  straight to disk.
- **Watch history & SponsorBlock stats** — click or right-click the OSC
  title for stats or your watch history.

This file covers getting from a fresh clone to a working install.

## Setup

1. **Clone with submodules directly into place** — mpv reads `~/.config/mpv`,
   and several scripts under `scripts/` are symlinks into `plugins/*`, which
   are git submodules:

   ```sh
   git clone --recurse-submodules https://github.com/edieguez/mpv-tube.git ~/.config/mpv
   ```

2. **Per-machine `script-opts/*.conf`** — these files are gitignored on
   purpose: they hold personal customization (colors, key timings, the
   SponsorBlock `user_id`, etc.), which this repo expects to come from
   somewhere else (e.g. your own dotfiles). Every third-party script ships a
   reference `script-opts/<name>.conf.template` to copy from and adjust:

   | Template | Script it configures |
   |---|---|
   | `modernz.conf.template` | ModernZ OSC (colors, icon theme, buttons, ...) |
   | `pause_indicator_lite.conf.template` | Pause/play indicator overlay |
   | `perpetual_playlist.conf.template` | Perpetual playlist (persisted queue, resume position) |
   | `playlist_manager.conf.template` | Playlist manager (`ctrl+v` add, dedupe, ...) |
   | `thumbfast.conf.template` | Seekbar thumbnail previews |
   | `yas.conf.template` | YAS / SponsorBlock — set `user_id` here for stats to persist |

   None of these are required to exist — every script falls back to its own
   built-in defaults if its `script-opts/*.conf` is missing. mpv will just
   look and behave differently from the intended setup until they're
   populated.

That's it — no build step, no other dependencies beyond `yt-dlp` being on
`PATH` (for YouTube/etc. playback) and `mpv` itself.

## Credits

Third-party plugins this config builds on, pulled in as git submodules
under `plugins/`:

- [ModernZ](https://github.com/Samillion/ModernZ) by Samillion — the OSC
  (on-screen controller) replacing mpv's built-in one, including its
  `pause-indicator-lite` and `open-file` extras.
- [thumbfast](https://github.com/po5/thumbfast) by po5 — seekbar thumbnail
  previews.
- [mpv-selectformat](https://github.com/demurky/mpv-selectformat) by
  demurky — the `F` yt-dlp quality/format picker menu.

Plugins written for this config, also submodules under `plugins/`:

- [yas](https://github.com/edieguez/yas) — SponsorBlock ad-skipping.
- [perpetual-playlist](https://github.com/edieguez/perpetual-playlist) —
  persistent playlist and resume position across sessions.
- [playlist-manager](https://github.com/edieguez/playlist-manager) —
  `ctrl+v` paste-to-queue, dedup, interactive playlist.
- [ytdl-prefetch](https://github.com/edieguez/ytdl-prefetch) — background
  prefetching for near-instant playlist transitions.
- [picture-in-picture](https://github.com/edieguez/picture-in-picture) —
  the `i` PiP window toggle.
