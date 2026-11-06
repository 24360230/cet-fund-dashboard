# 2026 Community Experts Fund dashboard

Static page (`index.html`, no build step). Host with GitHub Pages (Settings > Pages > deploy from `main`, root).

## Near-real-time option (recommended): Apps Script

1. In the sheet: Extensions > Apps Script. Replace the contents of `Code.gs` with `apps-script/Code.gs`. Save.
2. Deploy > New deployment > type **Web app**. Execute as: **Me**. Who has access: **Anyone**. Deploy and authorize.
3. Copy the web app URL (ends in `/exec`) into `API_URL` in `index.html`.
4. The page re-checks every 15 seconds (`POLL_SECONDS`) while the tab is open.

The script returns only totals and Approved awardees; scores, ranks, comments and other applicant names are never sent.
After editing the script later, use Deploy > Manage deployments > Edit > New version so the URL stays the same.
This replaces the CSV steps below; the `Public Summary` tab is not needed.

## Alternative: published CSV (about 5 min lag)

Never publish the `Decisions` tab: it holds applicant names, scores and ranks.

1. In the sheet, add a tab named `Public Summary`.
2. Open `public-summary.tsv`, copy everything, and paste into cell A1 of that tab.
   It holds the formulas, built for the current layout (data in `Decisions` rows 13-37,
   Focus areas = D, State = E, Request = F, Status = H, Award amount = I, Available = B4).
   If rows are added to `Decisions`, extend the `13:37` ranges.
3. File > Share > Publish to web > choose **Public Summary** only > CSV > Publish.
4. Paste the link into `SUMMARY_CSV_URL` in `index.html`.

Status values: `Approved`, `Decline`/`Declined` (matched with `Decline*`), `Under consideration`.
Applicant names appear on the public page only once their status is Approved.

## Tab layout

Columns `type, label, count, amount`. Types: `metric`, `state`, `focus`, `awardee`
(for `awardee` rows: label = organization, count column = state, amount = award).
Blank-type rows are ignored by the page.
