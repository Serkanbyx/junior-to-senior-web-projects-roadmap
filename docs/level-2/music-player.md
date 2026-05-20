# Music Player

> A modern music player with HTML5 Audio API, playlist management, shuffle/repeat modes, and Zustand state.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://music-playerrrrr.netlify.app/player) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/music-player)

---

## Purpose

This project teaches you to work with the HTML5 Audio API — controlling media playback
programmatically. You'll manage complex player state (current track, position, duration,
playing/paused, shuffle, repeat) and synchronize UI with audio events. It's the same
architecture used by Spotify's web player.

## Tech Stack

- **Framework:** React, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Zustand (player state: current track, playlist, shuffle, repeat)
- **Routing:** React Router
- **Validation:** Zod
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Set up the Audio API abstraction.** Create a custom hook or utility that wraps the HTML5 `Audio` object. Expose: play, pause, seek, setVolume, getCurrentTime, getDuration. Listen to audio events: `timeupdate`, `ended`, `loadedmetadata`.

2. **Build the player state in Zustand.** Track: `{ id, title, artist, album, duration, src }`. Player state: `{ currentTrack, playlist, isPlaying, currentTime, volume, shuffle, repeat }`. Actions: play, pause, next, previous, seek, toggleShuffle, toggleRepeat.

3. **Build the player UI.** Album art, track info (title, artist), progress bar (seekable), time display (current/total), play/pause button, next/previous, volume slider. All synced to Audio API state.

4. **Implement the progress bar.** Update current time from `timeupdate` events (fires ~4x/second). Render as a seekable bar. On click/drag, seek to that position. Show elapsed and remaining time.

5. **Build playlist management.** Display track list with current track highlighted. Click to play any track. Add/remove from playlist. Drag to reorder (optional).

6. **Implement shuffle and repeat.** Shuffle: on "next," pick a random unplayed track instead of sequential. Repeat modes: none (stop at end), repeat-all (loop playlist), repeat-one (loop current track).

7. **Add routing and deploy.** React Router for player page vs library/playlist views. Deploy on Netlify with `_redirects` for SPA routing.

## Tips

- The Audio API's `timeupdate` event fires approximately 4 times per second. Don't update React state on every fire — use a ref for current time and only setState for visual updates (throttled to ~15fps for smooth progress bar).
- Shuffle implementation: maintain a "shuffle queue" (randomized copy of playlist). Advance through the queue sequentially — this ensures every track plays once before repeating, unlike true random which can repeat.
- Extension: add equalizer visualization (Web Audio API + AnalyserNode), lyrics display, crossfade between tracks, or keyboard shortcuts.
