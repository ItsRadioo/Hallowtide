# Hallowtide: The Hollowing of Blackwood

GitHub Pages-ready campaign system using a completely flat repository structure.

## Entry points

- `index.html` — landing page
- `campaign.html?mode=dm` — DM console
- `campaign.html?mode=player` — player display
- `dm.html` — convenience DM redirect
- `player.html` — convenience player redirect

## App files

- `styles.css` — shared visual styling
- `app.js` — campaign data, navigation, state, maps and soundboard
- `campaign.html` — application shell

## GitHub Pages setup

1. Upload every file directly to the repository root.
2. Open **Settings → Pages**.
3. Choose **Deploy from a branch**.
4. Select **main** and **/(root)**.
5. Save.

GitHub Pages will serve `index.html` automatically.

## Recommended table setup

Open the DM console on your private screen:

`campaign.html?mode=dm`

Open the player display on the shared screen:

`campaign.html?mode=player`

The `.nojekyll` file is included so GitHub Pages serves the repository as static files without Jekyll processing.

## Detailed maps

The app references the root-level PNG files directly. Replace a map using the same filename and GitHub Pages will serve the new version without rebuilding `app.js`.

## Illustrated map set

The active map files have been replaced with the illustrated top-down Hallowtide map set. Player and DM filenames remain unchanged, so the campaign app requires no routing changes.

## Map selector

The Maps page now uses a dropdown to switch between maps instead of rendering the full set at once. The same selector automatically loads DM or player-safe versions depending on the active mode.

## Modular soundboard
Audio is stored in separate root-level files and mapped in `sounds.js`. See `SOUND_REPLACEMENT_GUIDE.md`.

## Projected-table Fog of War

The DM view always displays the fully revealed keyed DM map. The player view starts fully covered by opaque fog.

Open both from the same GitHub Pages site in two browser windows:
- `campaign.html?mode=dm`
- `campaign.html?mode=player`

The windows synchronize the selected map, fog reveals, fog hides, reveal-all/reset state, and blackout using `BroadcastChannel`, with `localStorage` as persistent fallback. Fog state is saved independently for every map.

DM controls:
- Reveal / Hide brush
- Adjustable brush size
- Undo
- Reveal All
- Reset Fog
- Blackout / Restore Players
- Optional translucent player-fog preview

The player window has only the player-safe map, opaque fog, and a fullscreen button for projection.

## Opaque Room Fog

Player fog is now completely opaque black. A new fog-state version resets old partially revealed states.

Indoor maps support:
- Reveal Room
- Hide Room
- Reveal Brush
- Hide Brush

Clicking inside a defined room reveals that entire room immediately on the player display. Brush tools remain available for corridors, outdoor spaces, cornfields, forests, and irregular reveals.

## Final map architecture

This build uses one shared labeled/legend map image per location:
- blackwood.png
- cemetery.png
- crowe-farm.png
- chapel-undercroft.png
- old-mill.png
- masquerade-hall.png
- hollow-blackwood.png
- hallow-square.png

The DM sees the complete image. The player projection uses the same file but crops the legend panel offscreen and applies 100% opaque fog of war.

## Custom ceremony cue
`cue-gift-for-the-wanderers.wav` is included and wired into the Gift for the Wandering scripted sequence.

## Audio upload organization

Audio assets are grouped in `AUDIO_FILES_UPLOAD/` only inside this download package.
Move the audio files themselves into the GitHub repository root when uploading.
The application does not reference the folder name.

Combat ambience and the heartbeat cue were removed. The soundboard now primes
browser audio on the first user interaction so scripted cues can continue without
repeated autoplay-block messages.
