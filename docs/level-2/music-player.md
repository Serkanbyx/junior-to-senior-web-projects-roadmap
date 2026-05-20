# Music Player

> A music player with playlist management, shuffle/repeat modes, progress bar, and HTML5 Audio API integration.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://music-playerrrrr.netlify.app/player) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/music-player)

---

## Purpose

This project teaches you to work with the HTML5 Audio API — controlling playback, tracking
progress, and responding to media events. You'll build a stateful queue system (playlist with
current track, next/previous, shuffle, repeat) which is the same pattern used in media apps,
task queues, and carousel components. Zod validation introduces runtime type checking for data.

## Tech Stack

- **Frontend:** React, TypeScript, Tailwind CSS
- **Backend:** none
- **Database:** none (playlist state in Zustand)
- **Key libraries / tools:** Zustand, Zod (data validation), HTML5 Audio API
- **Deployment:** Netlify

## Build Steps

1. **Model the track data.** Define a track interface: `{ id, title, artist, album, duration, src, coverArt }`. Use Zod to validate track objects at runtime — this catches malformed data before it crashes the player.
2. **Set up the Audio element.** Create a React ref to an `<audio>` element. Build a custom hook (`useAudioPlayer`) that exposes: play, pause, seek, volume, currentTime, duration, and loading state. Listen to `timeupdate`, `ended`, `loadedmetadata` events.
3. **Build playback controls.** Play/pause toggle, next/previous track, volume slider, and a seek/progress bar. The progress bar shows elapsed time, total duration, and a draggable handle for seeking. Update the bar on every `timeupdate` event.
4. **Implement the playlist.** A scrollable list of tracks with the current track highlighted. Clicking a track starts playback immediately. Show track title, artist, duration, and album art thumbnail.
5. **Add shuffle and repeat.** Shuffle mode randomizes the next-track order without repeating until all tracks have played (Fisher-Yates on a queue copy). Repeat modes: off, repeat-all (loop playlist), repeat-one (loop current track). Persist mode preference.
6. **Build the "now playing" view.** A large album art display, animated progress ring or bar, track info, and controls. This is the main visual focus of the app — make it polished with smooth transitions between tracks.
7. **Handle edge cases.** Audio loading errors (show fallback message), empty playlist state, and browser autoplay restrictions (require user interaction before first play). Add keyboard shortcuts (space = play/pause, arrows = seek).

## Deployment

Deploy on Netlify. Include a few royalty-free audio files in the repo for demo purposes,
or link to external audio URLs. No environment variables needed.

## Tips

- The HTML5 Audio API fires events asynchronously. Always use event listeners (`timeupdate`, `ended`) rather than polling `currentTime` — it's more efficient and avoids race conditions.
- Browser autoplay policies block audio playback without user interaction. Always require a click before calling `.play()` for the first time.
- Extension: add an equalizer visualization using the Web Audio API's `AnalyserNode`, or implement queue management (add to queue, reorder, remove).

## README Guidance

The project repo's README should include a short description, a screenshot of the player UI
with album art, the live demo link, tech stack, features list (shuffle, repeat, progress bar),
and local dev instructions.
