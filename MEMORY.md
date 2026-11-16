# MEMORY

## Overview
Reta's Launcher: branded fork of Helios Launcher (Electron) for a friends' RP server.
Server: id "Main" (distro id `Main-1.21.11`), 143.20.155.28:25576, Minecraft 1.21.11, Fabric loader 0.20.1, Java 21 (helios-core default for 1.20.5+).
Run: `npm ci`, `npm start`. Build: `npm run dist` (or `dist:win`). Lint: `npm run lint`.

## Structure
- `app/assets/js/distromanager.js` — REMOTE_DISTRO_URL = https://cruxforged.github.io/retas-launcher/distribution.json
- `app/assets/js/configmanager.js` — data folder `.retaslauncher`
- `app/assets/js/ipcconstants.js` — AZURE_CLIENT_ID (still Helios's)
- `app/assets/lang/_custom.toml` — title, links, welcome text
- `electron-builder.yml` — appId/productName/artifact names
- `.github/workflows/build.yml` — builds win/mac/linux on push, uploads installers as artifacts
- `gh-pages` branch — Nebula root: `distribution.json`, `servers/Main-1.21.11/fabricmods/required/*.jar`, `repo/` (fabric libs)

## Distribution workflow
- Nebula cloned at `D:\Coding\Nebula`, `.env`: ROOT=`D:\Coding\retas-launcher-distro` (git worktree of gh-pages), BASE_URL=https://cruxforged.github.io/retas-launcher/
- Change mods: edit jars in `servers/Main-1.21.11/fabricmods/{required,optionalon,optionaloff}`, bump `servermeta.json` version, run `npm run faststart -- g distro` in Nebula, commit + push gh-pages.

## Screens / states
Upstream Helios screens unchanged: loading, welcome, login (Microsoft/Mojang), landing, settings, overlays (server select, errors, updates).

## Shared styles / components
- `app/assets/css/launcher.css`, `app/assets/lang/*.toml`, `app/assets/images/`

## Do not edit without asking
- `node_modules/`, `libraries/`, `package-lock.json`

## Decisions
- Based on upstream master (not v2.2.1): v2.2.1 cannot launch 1.20.5+ (Java 21, new version format).
- Artifact names `Retas-Launcher-setup-*` (no apostrophe/space) so release URLs and auto-update stay safe.
- Distro hosted on gh-pages branch of this repo (single repo; `.nojekyll`).
- Server id stays `Main-1.21.11` (Nebula convention: folder `<id>-<mcVersion>`).
- Create → Create Fly (unofficial Fabric port of Create 6).

## Done
- 2026-11-16: Fork, branding, distro URL, gh-pages distribution with 23 mods, build artifact upload.

## Next / known issues
- AZURE_CLIENT_ID is Helios's; register own Azure app + Minecraft API approval (docs/MicrosoftAuth.md).
- Not available for Fabric 1.21.11: ModernFix, Corpse (NeoForge only).
- Beta/alpha builds in pack: Emotecraft (beta).
- No server icon; no Discord RPC; no news RSS.
- index.js has 2 upstream lint errors (extra semicolons).
- Mod list is provisional; will change.
