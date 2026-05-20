# Stock Market Dashboard

> A responsive stock market dashboard with real-time quotes, interactive Recharts, Redux Toolkit state, and Finnhub API integration.

**Level:** 2 &nbsp;·&nbsp; **Status:** ✅ Built
&nbsp;·&nbsp; [Live Demo](https://stock-market-dashboarddd.netlify.app/) &nbsp;·&nbsp; [Source Code](https://github.com/Serkanbyx/stock-market-dashboard)

---

## Purpose

This project introduces Redux Toolkit — the industry standard for complex state that
multiple components need to share. A stock dashboard has interconnected state: watchlist
affects which charts render, search updates the active symbol, and real-time data flows
through the entire app. Redux makes this manageable with slices, selectors, and async thunks.

## Tech Stack

- **Framework:** React 18, TypeScript, Vite
- **Styling:** Tailwind CSS
- **State:** Redux Toolkit (createSlice, createAsyncThunk)
- **Charts:** Recharts (line charts, area charts)
- **Forms:** React Hook Form + Zod
- **HTTP:** Axios
- **API:** Finnhub (stock quotes, company info)
- **Icons:** Lucide React
- **Deployment:** Netlify

## Build Steps

1. **Set up Redux Toolkit store.** Configure store with slices: `stocksSlice` (quotes, search results), `watchlistSlice` (saved symbols), `uiSlice` (loading, theme). Type the entire store with TypeScript for safety.

2. **Build async thunks for API calls.** `createAsyncThunk` handles the fetch lifecycle: pending → fulfilled → rejected. Fetch stock quotes, company profiles, and historical data from Finnhub. Handle errors in the rejected case.

3. **Build the stock search.** Search bar with debounce. Results dropdown showing matching symbols with company name. On select, dispatch action to set active stock and fetch its data.

4. **Build the chart view with Recharts.** Historical price data rendered as a line/area chart. Time range selector (1D, 1W, 1M, 3M, 1Y). Responsive container. Tooltip showing price on hover.

5. **Implement the watchlist.** Add/remove symbols. Show current price and daily change (green/red) for each. Click to navigate to that stock's detail. Persist watchlist in Redux with localStorage middleware.

6. **Add number formatting.** Stock prices need proper formatting: 2 decimal places, comma separators, +/- prefix for changes, color coding (green for up, red for down). Create utility formatters.

7. **Deploy on Netlify.** Set `VITE_FINNHUB_API_KEY` or use Netlify Functions for API key protection.

## Tips

- Redux Toolkit vs Zustand: use Redux when you have complex interconnected state with many async operations and need DevTools for debugging. Use Zustand for simpler, more isolated state.
- `createAsyncThunk` automatically dispatches pending/fulfilled/rejected actions. Handle all three in `extraReducers` to show loading spinners, display data, or show error messages.
- Extension: add real-time WebSocket quotes (Finnhub offers WebSocket), portfolio tracking, price alerts, or comparison mode (overlay multiple stocks).
