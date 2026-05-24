# Curaçao Group Travel Planner Dashboard

> A lightweight planning dashboard for coordinating an 8-person trip to Curaçao in August 2026.

## What It Does

This dashboard provides a shared planning template that helps your group compare villa costs vs flight estimates, draft a day-by-day itinerary, track dinner reservations, and manage transportation decisions for 8 travelers.

## Prerequisites

- Working Open Brain setup ([guide](../../docs/01-getting-started.md))
- Any static hosting option (Vercel, Netlify, GitHub Pages, or local file server)
- Modern web browser

## Credential Tracker

Copy this block into a text editor and fill it in as you go.

```text
CURAÇAO GROUP TRAVEL PLANNER -- CREDENTIAL TRACKER
--------------------------------------------------

FROM YOUR OPEN BRAIN SETUP
  Project URL:           ____________
  Anon key:              ____________

HOSTING
  Deploy URL:            ____________

--------------------------------------------------
```

## Steps

1. Clone this repository and open `dashboards/group-travel-planner/`.
2. Open `index.html` directly in your browser for local use, or deploy this folder to your static host.
3. Update budget inputs in the **Budget Tracker** section:
   - Villa nightly rate
   - Number of nights
   - One-time taxes/fees
   - Estimated flight cost per person
4. Use the itinerary table as your shared weekly template (including Cas Abou and Jan Thiel beach days).
5. Fill in dining reservation rows with real restaurants and change status from `Requested` to `Confirmed`.
6. Work through the transport checklist to choose either one large vehicle or two cars for comfortable 8-person movement.

## Expected Outcome

You will have a single, shareable dashboard page that your group can use to estimate costs quickly, coordinate key day plans, and keep logistics visible in one place.

## Troubleshooting

**Issue: Calculations are not updating when values change.**  
Solution: Confirm JavaScript is enabled in your browser and that numeric fields contain valid numbers.

**Issue: Team members see different versions of the plan.**  
Solution: Host one canonical copy on Vercel/Netlify and share only that URL with the group.

**Issue: Itinerary dates need to shift.**  
Solution: Update the date cells in the itinerary table to match your final flight dates before sharing.
