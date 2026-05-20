# Weather App (Basic)

> A static weather app with city search, detailed weather display, and quick-access buttons — using demo JSON data instead of a live API.

**Level:** 1 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://weather-app-basicc.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/weather-app-basic)

---

## Purpose

This project teaches you to build a data-driven UI without the complexity of live API calls.
By using local JSON mock data, you focus purely on rendering conditional content (sunny vs.
rainy icons, temperature formatting, wind/humidity details) and handling search/filter logic.
It's the stepping stone to Level 2's real API weather app — same UI patterns, minus the
network layer. It also introduces icon libraries (Font Awesome) as a practical tool.

## Tech Stack

- **Frontend:** HTML5, CSS3, vanilla JavaScript (ES6+)
- **Backend:** none
- **Database:** none (uses local JSON demo data)
- **Key libraries / tools:** Font Awesome (weather icons)
- **Deployment:** Netlify (static hosting)

## Build Steps

1. **Create the mock data.** Build a JSON file (or a JavaScript object) containing weather data for several cities: temperature, condition (sunny, cloudy, rainy, etc.), humidity, wind speed, and a 5-day forecast. This simulates an API response without needing keys or network calls.
2. **Build the search UI.** An input field where the user types a city name. On submit (Enter or button click), look up the city in your data. Show an error message if the city isn't found. Add quick-access buttons for popular cities.
3. **Render current weather.** Display the city name, current temperature, weather condition with a matching icon (Font Awesome or custom SVG), "feels like" temperature, humidity percentage, and wind speed. Use conditional logic to pick the right icon and color scheme based on the condition.
4. **Display the forecast.** Show a 5-day forecast row below the current weather. Each day card shows the day name, high/low temperature, and a condition icon. Use `Date` methods or hardcoded day names from your mock data.
5. **Add responsive layout.** The current weather should stack vertically on mobile and sit beside detail cards on desktop. The forecast row scrolls horizontally on small screens. Use CSS Grid or Flexbox — no media query should be required if you use `auto-fill`.
6. **Handle UI states.** Three states: empty (no city searched yet — show a welcome message), loaded (city found — show weather), error (city not found — show a helpful message). Never leave the UI blank without explanation.
7. **Polish with transitions.** Fade in the weather card on load, animate temperature number changes, and add hover effects on forecast cards. These small details turn a basic project into a portfolio piece.

## Deployment

Push to GitHub and deploy on Netlify. Since this uses demo data (no API key), it works
anywhere without environment variables. No build step needed.

## Tips

- Using mock data isn't a shortcut — it's a professional practice. Frontend teams build against mock APIs all the time while the backend is still in development. Learning to structure realistic mock data is a skill.
- Keep the data shape identical to what a real weather API (like OpenWeatherMap) returns. This way, swapping in a real API later is a one-line change to the fetch URL.
- Extension: connect to the OpenWeatherMap API and add geolocation-based weather detection — this naturally leads into the Level 2 Weather App project.

## README Guidance

The project repo's README should include a short description, a screenshot showing weather for
a searched city, the live demo link, features list (city search, quick access buttons, responsive),
a note that it uses demo data (no API key required), and a one-step local run instruction.
