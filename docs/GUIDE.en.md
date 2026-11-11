# Trifl — user guide

Trifl lives in the macOS menu bar and automatically shrinks images, GIFs, videos, PDFs and audio. Everything runs on your Mac; files are never uploaded anywhere.

## Install and first run
1. Download `Trifl.dmg` from the [releases page](../../../releases/latest) and drag Trifl to Applications.
2. A short welcome lets you pick folders to watch (e.g. Desktop or Downloads).
3. Allow folder access and “Automation” (used by ⌃O in Finder) if macOS asks.
4. Updates arrive automatically (Trifl → “Check for updates…”).

Requires macOS 13 or later, Apple Silicon or Intel.

## How files get optimised
- **Clipboard.** Take a screenshot or copy an image — the clipboard already holds the optimised version.
- **Folders.** New files in watched folders are optimised automatically.
- **Drag & drop.** Drop files on the menu bar icon, the drop zone window or the app icon. Hold ⌘ on release for aggressive compression.
- **Finder.** Select files and press ⌃O, or use Services → “Optimize with Trifl”.
- **Command line and AI agents** — see below.

The original is always backed up (7 days by default) and can be restored from the result card.

## Result card
After optimising, a card appears at the bottom right: before → after, a thumbnail and buttons:
- **Aggressive**, **For messengers** (image ≤1280 px and ~1.5 MB, video 720p up to 16 MB);
- **Downscale** (75 / 50 / 25 %);
- **Convert:** WebP, JPEG XL, JPEG, PNG, HEIC, AVIF;
- **Fit to size** (500 KB … 5 MB);
- **Crop** to an aspect ratio (smart crop shifts the frame towards the main subject);
- video: remove audio, change speed, make a GIF;
- **Restore original**, **Copy**, **Show in Finder**, **Share**, AirDrop, open in an external editor (if set).

## Menu bar menu
- Optimise clipboard now · aggressive · downscale by half · revert last optimisation · bring back last result.
- **Ignore clipboard events from <app>** — toggles ignoring for the frontmost app. The quickest fix for CorelDRAW, Illustrator, Figma and similar.
- **Pause automatic optimisation.**
- Watch clipboard / folders, drop zone.
- Backups folder, working directory, clean working directory.
- Check for updates, report a problem, error log, settings.

## Hotkeys
| Keys | Action |
|---|---|
| ⌃⇧C | Optimise clipboard |
| ⌃⇧A | Aggressive clipboard optimisation |
| ⌃⇧− | Downscale clipboard image by half |
| ⌃⇧Z | Revert last optimisation |
| ⌃⇧= | Bring back last result |
| ⌃O | Optimise Finder selection |

## Settings
A sidebar window with search.

- **General** — quality, max image size, replace the file or save “name.min” next to it, result window, notifications, updates, launch at login.
- **Clipboard** — what to watch (image data, TIFF, image/video/audio/PDF files), clipboard pipeline, copy file path, ignored apps.
  - *TIFF data* is off by default: design apps (CorelDRAW etc.) put layers there.
  - Copies containing vectors or layers are detected and left alone.
- **Folders** — watched folders with per-folder mode, quality, max size, pipeline, screenshot sorting (into a “Screenshots” folder, by month or by day) and rename template.
- **Photo & video** — metadata (strip all / keep / keep without GPS) and video scenarios: universal (1080p), messengers (720p up to 16 MB), screen recording (HEVC), maximum quality, or custom.
- **Filters** — per type (images, video, audio, PDF): min/max size, min resolution, files per batch, extensions to skip. Filters only apply to automatic processing. PDF image dpi lives here too.
- **Advanced** — adaptive compression, smart crop, wide colour, video fps cap, AAC bitrate, Photos.app, clipboard file name template, external editors, hotkey list.
- **Storage** — backup retention, working directory, preserve file dates, pause.
- **Pipelines** — your own step chains (optimise, downscale, convert, crop, video scenario, GIF…) assignable to the clipboard, drops or folders.
- **Tools** — install the `trifl` command and MCP for AI agents.

## Command line
Install the command from the Tools tab, then:

```bash
trifl optimize photo.png
trifl optimize --convert webp --scale 50 photo.jpg
trifl optimize --video messenger recording.mov
trifl optimize --crop 16:9 --copy photo.jpg
```

Main options: `-a` aggressive, `--scale N`, `--convert webp|avif|jxl|jpeg|png|heic`, `--crop W:H`, `--max-size 2MB`, `--mute`, `--speed X`, `--gif`, `--metadata strip|keep|nogps`, `--video universal|messenger|screen|max`, `--video-limit MB`, `--quality low|medium|high`, `--max-dim N`, `--copy`, `--json`.
It also works in Shortcuts via “Run Shell Script”.

## AI agents (MCP)
`trifl mcp` is an MCP server (stdio). Add it to Claude Desktop, Claude Code or another client as the command `trifl mcp` and the agent can optimise files on your Mac.

## Troubleshooting
- **CorelDRAW layers get compressed.** Open Corel, then in the Trifl menu enable “Ignore clipboard events from CorelDRAW”.
- **File didn't shrink.** It is already optimal: Trifl never writes a result that isn't smaller.
- **Get the original back.** “Restore original” on the card, ⌃⇧Z, or the backups folder.
- **Error or crash.** Menu → “Report a problem…” opens a GitHub issue with version info and recent log lines. You can read and edit the log before sending.
