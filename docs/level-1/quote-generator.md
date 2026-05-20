# Quote Generator

> A random quote generator with API integration, real-time translation, text-to-speech, dynamic themes, and social sharing.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://quote-generatorrrrr.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/quote-generator)

---

## Purpose

This is your first encounter with consuming an external API from the browser. It teaches
`fetch`, async/await, error handling for network requests, and working with JSON responses.
Beyond the API, it introduces browser APIs you'll use constantly: the Web Speech API for
text-to-speech and the Web Share API for native sharing. The dynamic theme system shows how
CSS custom properties can be changed at runtime from JavaScript.

## Tech Stack

- **Frontend:** HTML5, CSS3, vanilla JavaScript
- **Backend:** none (API consumed directly from client)
- **Database:** none
- **Key libraries / tools:** ZenQuotes API, Web Speech API (TTS), Web Share API, MyMemory Translation API
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Fetch a quote.** Call the ZenQuotes API (or a similar quotes API) using `fetch` with async/await. Parse the JSON response and extract the quote text and author. Handle network errors gracefully — show a fallback message if the request fails.
2. **Display with animation.** Render the quote and author in the DOM. Add a fade-in or slide-up CSS transition on each new quote so the change feels smooth rather than abrupt.
3. **Add translation.** Call a translation API (e.g. MyMemory) to translate the English quote into Turkish (or another language). Show both the original and translated text. Handle the case where translation fails independently of the quote fetch.
4. **Implement text-to-speech.** Use the `SpeechSynthesis` API to read the quote aloud. Create a speak button that creates a `SpeechSynthesisUtterance`, sets the language, and calls `speechSynthesis.speak()`. Add a stop button to cancel mid-read.
5. **Build dynamic color themes.** On each new quote, randomly generate or select a color palette. Update CSS custom properties (`--primary`, `--bg`, `--text`) on the document root. This makes the page feel alive and unique with every click.
6. **Add social sharing.** Use the Web Share API (`navigator.share()`) where supported for native sharing on mobile. Fall back to Twitter/WhatsApp intent URLs on desktop. Format the shared text as `"quote" — author`.
7. **Handle loading states.** Show a spinner or skeleton while the API is being called. Disable the "new quote" button during the fetch to prevent duplicate requests.

## Deployment

Push to GitHub and deploy on Netlify. The ZenQuotes API has a CORS proxy requirement from
the browser — use the `api.allorigins.win` workaround or a similar CORS proxy if direct
requests are blocked. No environment variables needed for public APIs.

## Tips

- CORS is the most common blocker for client-side API calls. Understand what it is and how proxies solve it — this knowledge transfers to every future project.
- The Web Speech API voice list loads asynchronously. Wait for the `voiceschanged` event before populating voices, or your TTS may use the wrong language.
- Extension: add a "favorites" feature using `localStorage` so users can save and revisit quotes they liked.

## README Guidance

The project repo's README should include a short description, a screenshot showing a quote with
the dynamic theme, the live demo link, a features list (API, TTS, translation, themes, sharing),
and a one-step local run instruction.
