---
name: mapit-ride-summary
description: Build a ride summary or logbook for a period (a day, week, month or custom range) from the customer's Mapit routes, with total kilometres, riding time, number of rides, average and top speed, and a per-day breakdown. Use when the user asks things like "how many km did I ride this month?", "summarise my rides since June" or "compare this week with last week".
---

# Mapit ride summary

Use the My Mapit connector's `get_my_ride_stats` tool. It computes totals and per-day figures with the Mapit app's own statistics rules, so the numbers match what the customer sees in the app. Never add up `list_my_routes` results yourself.

Follow the `my-mapit` skill for choosing the vehicle, language and timezone. The customer must have allowed route history; if the tool is missing, explain how to grant it (see `my-mapit`).

## Steps

1. **Period.** Turn the request into local calendar days: "this month" is the 1st until today, "last week" is Monday to Sunday of the previous week. Pass `from` and `to` as `YYYY-MM-DD` (both inclusive, at most 90 days per call; split longer periods into chunks and present each one). Pass `timezone` only if the user gave one; otherwise the account timezone is used.
2. **Call** `get_my_ride_stats` once per vehicle and period. If several vehicles match, ask which one, or give one line per vehicle.
3. **Present:**
   - one line with the totals: rides, km, riding time (hours and minutes), average and top speed
   - a table per day (date, rides, km, time, top speed) for periods up to a month; per week for longer periods
   - the period and timezone used
   - speeds can be null; show "–". A top speed of 180 means "180 km/h or more", as in the app.
   - if the response has `truncated: true`, say the summary covers only the first 2,000 rides.
4. **Offer next steps:** the list of rides on a given day (`list_my_routes` with `day`), the details or map of one ride (`get_my_route`), or a comparison with another period.

Do not estimate fuel, emissions or costs, and do not invent rides the data does not show.
