# AppADay 045 — Water Reminder

**Category:** AI-Powered (A)
**Live URL:** <https://augustineiacopelli.github.io/appaday-045-water-reminder/>

## What it does

Water Reminder uses Claude’s vision capabilities to track how much you’re drinking by comparing photos of your glass over time, rather than asking you to log amounts manually.

**Setup:** Photograph your glass, mug, or bottle once. Claude estimates its capacity in ounces and you tell it whether the container is clear or opaque. This is editable anytime in Settings.

**Check-ins:** Whenever you take a sip, snap a new photo. For clear containers, one photo is enough — Claude estimates how many ounces are currently visible. For opaque containers, it asks for two photos: a side view for scale and shape, then a top-down view of the liquid surface, and estimates the fill level from both together.

**Tracking what you drank:** The app compares the new reading to your last one. If the level dropped, that difference is logged as consumed. If the level went *up*, that means a refill — the app asks one question: did you finish the glass before refilling? Yes counts the whole previous amount as consumed and resets the baseline; no (a top-off) logs zero for that gap since it can’t be measured precisely, and tracking restarts from the new level. Every check-in is logged with its photo, timestamp, and a note explaining what happened.

**Progress:** A filling glass-shaped vessel shows today’s total against a configurable daily goal (default 64 oz).

**Reminders:** An optional interval (in minutes) triggers an in-app banner prompting a check-in, with a best-effort browser notification if permission is granted. This won’t fire reliably in the background on iPhone, so the in-app banner is the primary mechanism.

## Setup

Open the Settings gear (⚙️) to enter your Claude API key, optional name, daily goal, reminder interval, and container details. The API key is stored only in your browser’s local storage and used only for direct calls to Anthropic’s API.

## Tech

Single-file vanilla HTML/CSS/JS. No frameworks, no build step. Uses the Anthropic API directly from the browser (`anthropic-dangerous-direct-browser-access: true`), model `claude-sonnet-4-20250514`. All data — API key, container profile, goal, and daily logs — lives in `localStorage`, wrapped in try/catch for sandbox compatibility.

## Part of AppADay

AppADay is a one-app-per-day build challenge. See the full portfolio at <https://augustineiacopelli.github.io/appaday/>.
