# Stock Market Dashboard

> A real-time stock market dashboard with live quotes, interactive charts, and watchlist management.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://stock-market-dashboarddd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/stock-market-dashboard)

---

## Purpose

This project introduces real-time data, charting libraries, and Redux-style state management.
You'll learn to poll an API at intervals, format financial numbers correctly, and render
time-series data as interactive charts. The watchlist feature teaches normalized state (managing
a list of entities with their own update cycles) — the same pattern used in every dashboard app.

## Tech Stack

- **Frontend:** React 18, TypeScript, Tailwind CSS
- **Backend:** none (direct API calls or serverless proxy)
- **Database:** none (watchlist in Redux persist)
- **Key libraries / tools:** Redux Toolkit, Finnhub API, Recharts or similar charting library
- **Deployment:** Netlify

## Build Steps

1. **Set up Redux Toolkit.** Configure a store with slices for `stocks` (current quotes) and `watchlist` (user's tracked symbols). Use `createAsyncThunk` for API calls and `persist` middleware for the watchlist.
2. **Build the search/symbol lookup.** An input that searches stock symbols via the Finnhub symbol search endpoint. Display results as a dropdown with symbol, company name, and exchange. On select, add to the active view.
3. **Fetch and display quotes.** For each watchlist symbol, fetch the current quote (price, change, percent change, high, low). Format numbers with `Intl.NumberFormat` — always show 2 decimal places for prices and color-code positive (green) vs. negative (red) changes.
4. **Implement polling.** Set up a `setInterval` (every 15–60 seconds) that refreshes all watchlist quotes. Use a Redux thunk that dispatches updates. Clear the interval on unmount to prevent memory leaks.
5. **Render interactive charts.** Fetch historical candle data and render it as a line or candlestick chart. Add time range selectors (1D, 1W, 1M, 1Y). Make the chart responsive and add tooltips on hover showing exact price/date.
6. **Build the watchlist.** A sidebar or panel showing all tracked symbols with their latest price and daily change. Allow adding/removing symbols. Persist the list so it survives page refresh.
7. **Add responsive layout.** Dashboard grid: chart takes the main area, watchlist sits in a sidebar on desktop and collapses to a bottom sheet on mobile. Use Tailwind's responsive utilities.

## Deployment

Deploy on Netlify. If using Finnhub's free tier directly from the client, the API key is
exposed — wrap it in a Netlify Function for production. Set `FINNHUB_API_KEY` as an environment variable.

## Tips

- Financial data formatting is surprisingly tricky. Always use `Intl.NumberFormat` with explicit currency and decimal options — never format prices with string concatenation.
- Polling intervals should be configurable and respect API rate limits. The free Finnhub tier allows 60 calls/minute — plan your refresh strategy around this.
- Extension: add WebSocket support for truly real-time quotes (Finnhub offers a WebSocket endpoint), or add a portfolio tracker with buy/sell history and P&L calculation.

## README Guidance

The project repo's README should include a short description, a screenshot of the dashboard
with charts and watchlist, the live demo link, tech stack, API key setup, and local dev steps.
