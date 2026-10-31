# Project 46: System & Build Summary

## 1. How the System Works (Architecture)

The app is built as a simple two-tier dashboard: a Python backend that prepares the data and a Next.js web frontend that displays it.

* **Backend (`FastAPI`):**
  * Serves mock metrics for creator platforms (YouTube, TikTok, Instagram, and X), covering reach, clicks, watch hours, and sales conversions.
  * We removed heavy data science packages like `pandas` and rewrote the data logic using clean, native Python math. This keeps the backend lightweight, fast to boot, and free of installation errors on new machines.
  * Includes CORS setup out of the box so the frontend can request data without browser blocks.

* **Frontend (`Next.js` + `Tailwind CSS`):**
  * Uses a fixed two-column layout: the chart takes up the left 70% of the screen, and the control sidebar takes the right 30%.
  * **The Chart:** Uses Recharts with a logarithmic scale. A standard linear graph made small numbers like 1,000 conversions disappear next to 4,000,000 views; the log scale keeps every step of the funnel readable side-by-side with a revenue line graph.
  * **Interactive Sync:** Clicking any platform bar immediately updates the sidebar with that specific platform's drop-off percentage and earnings per click.
  * **Dark Terminal Theme:** Strictly styled with a dark background (`#030712`), deep navy cards (`#0B1117`), cyan highlights (`#38BDF8`), and indigo details (`#818CF8`).

---

## 2. How AI Was Used

AI was used as a development assistant throughout the build:

* **Initial Setup:** Generated the starting FastAPI server code and Next.js page structure based on the project requirements.
* **Bug Fixes & Debugging:** When standard library installs failed (like local Python build issues with `pandas`), AI helped replace them with simple, pure-Python logic.
* **Design & UX Reviews:** Audited screenshots of the running dashboard to catch readability issues—such as squished bars and missing revenue lines—and provided the exact code changes to fix them.
* **Testing Documentation:** Created the step-by-step test checklist covering dropdown filters, export downloads, and offline fallback behavior.

---

## 3. Practical Development Notes

* **Offline Fallback (The 2-Hour Rule):** If the Python backend is turned off, the frontend does not crash. It automatically detects the failed connection and switches to built-in fallback data so the dashboard stays interactive.
* **Why Logarithmic Scale Matters:** Because funnel drop-offs are steep (millions of views down to a few thousand purchases), a standard chart makes the smaller numbers look like zero. Switching to a log scale was necessary so users can still click and read the conversion bars.
* **One-Click JSON Export:** Users can click "Download Sample Data" to download a clean `.json` file containing whatever filters and numbers are currently on the screen.