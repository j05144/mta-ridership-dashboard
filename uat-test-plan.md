# Testing My Dashboard (UAT)

After building the dashboard, I wanted to check my own work the way a real
project team would, so I wrote a UAT (user acceptance testing) plan and ran
every test myself before calling the project done. Here's what I tested,
what I expected, and what actually happened.

## Test Cases

| # | What I'm testing | How | What should happen | What actually happened | Pass/Fail |
|---|-----------------|-----|--------------------|-----------------------|-----------|
| 1 | Fresh open | Open the .pbix with nothing selected | All visuals load, KPI card shows the full 2020-2026 total across all modes | Everything loaded fine, KPI card showed 10bn total, both charts and both slicers rendered | Pass |
| 2 | Year slicer | Pick just 2023 | Every visual updates to 2023 only | | |
| 3 | Multiple years | Pick 2021 + 2022 together | Charts show both years combined, and the line chart only spans those years | | |
| 4 | Mode slicer | Pick Subway only | Everything filters to Subway, other modes drop out of the legend | | |
| 5 | Both slicers at once | Pick 2024 AND LIRR | The filters stack, so I should only see LIRR's 2024 data | | |
| 6 | Clearing filters | Deselect everything after test 5 | Dashboard goes back to exactly how it looked in test 1 | | |
| 7 | Is my KPI actually right? | Filter to Subway 2022, then sum the same slice straight from the raw data in Excel | My DAX measure matches the number I calculated by hand | | |
| 8 | My Power Query cleaning worked | Look for congestion pricing entries anywhere in the visuals or slicers | They shouldn't exist since I filtered them out during data cleaning | | |
| 9 | Weekend dips | Zoom into one normal month with Subway selected | Ridership visibly drops every Sat/Sun (something I noticed while building, so if it's gone my dates are misaligned) | | |
| 10 | The COVID drop | Look at 2020 with no filters | The huge April 2020 collapse should be obvious in the line chart | The drop is right there at the left edge of the line chart, ridership falls off a cliff in spring 2020. I also hovered the earliest points and the tooltip confirmed dates back to March 1, 2020 | Pass |
| 11 | Bar chart math | Pick one mode and average its daily ridership from the raw data myself | The bar chart's average matches my hand calculation | | |
| 12 | README check | Go through my README like a stranger would | Screenshots load, the data source link works, and everything I claim matches what the dashboard shows | | |

## Issues I Found

| # | From test | What went wrong | How bad | How I fixed it | Re-tested? |
|---|-----------|----------------|---------|----------------|------------|
| 1 | Found while checking test 1 | The Year slicer only displayed 6 of the 7 years, so one year was always hidden (at first I thought 2020 was missing from my data entirely) | Medium, a user couldn't filter to the 2020 COVID period | Checked the Filters pane first: no filter was excluding 2020 and all 7 years existed in the field, so the data was fine. Turned out the slicer box was just too short to show the full list. Increased the slicer height so all years 2020-2026 display at once, then re-uploaded the .pbix and fresh screenshots | Yes, selected 2020 and the visuals correctly filtered to the March-Dec 2020 data |
## Results

- Passed: __ out of 12
- Issues found and fixed: __

Even though this was a personal project, testing it this way helped me identify issues that weren't obvious from the dashboard alone. It also gave me practical experience with the UAT process used on professional project teams.
