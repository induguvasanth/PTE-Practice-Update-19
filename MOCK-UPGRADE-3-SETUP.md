# PTE Mock Test — Upgrade 3: cloud sessions + frozen questions

## Target workbook

Existing **PTE UPDATE 21** Google Spreadsheet:
`1mAFV5s3i0szE8sPthN8ui8T19AV5G8yxmm8uAaOpLrw`

The project keeps reading the **original PTE question tabs** from this workbook. It does not create a second bank of duplicate questions.

## New mock database tabs

The following tabs are already created in the workbook and are referenced by their exact names:

- `Mock Test Sessions`: student, slot, timer, progress and state
- `Mock Test Questions`: one frozen question snapshot per session/question
- `Mock Test Answers`: checkpointed text/selection/transcript and answer position
- `Mock Test Results`: completed practice result (objective score estimate)
- `Mock Test History`: completed attempts and practice-score change
- `Mock Test Config`: reserved for future editable timing/weights configuration; the current code still defines timing/counts in JavaScript / Code.gs

The previously existing `PTE Mock Test Database` tab is preserved and not used as a combined free-form table. The legacy `Mock Test Attempts` tab is also supported so students see prior results.

## Deployment steps

1. Keep a **backup** of the current GitHub Pages website and Apps Script project.
2. Upload the entire updated `PTE-Practice-Update-07-main` website folder contents to your GitHub Pages website root. Include `full-mock.html`, `mock-tests.html`, all JavaScript modules, the speech assets, and existing topic pages.
3. In the existing Google Apps Script project, replace `Code.gs` with `Google-Apps-Script/Code.gs` from this package. Keep/replace `Bridge.html` and `Teacher.html` according to this ZIP (do not omit either).
4. Select **Deploy → Manage deployments → Edit → New version → Deploy** to retain the same /exec URL. Ensure the deployment executes as the account allowed to edit the spreadsheet.
5. Confirm `sync-config.js` still has your current /exec deployment URL. `Bridge.html` accepts messages from `https://induguvasanth.github.io`; update its `allowed` origin if your site domain changes.
6. Sign in as a test student **before** starting a mock. Visit `mock-tests.html`, begin Speaking Mock 1, answer several questions, wait for checkpoint sync, reload and verify the same questions and saved answers return. Complete a short test manually, check the five data tabs, and open the Mock Test Center history page.
7. Confirm all four section mocks and four full mocks, media, timer expiry and mobile microphone permissions on the deployed site. The build environment cannot directly exercise your live website/backend.

## How cloud sessions work

- Questions are selected from your existing task sheets at first start, then copied as **snapshots** into `Mock Test Questions` so refreshing does not reshuffle the test.
- While signed in, progress and answers are checkpointed to the six-tab database, and a stored session may be recovered on another browser after the same student signs in.
- The student's browser stores an immediate local backup even when cloud sync fails. A cloud checkpoint is attempted a few seconds after changes and about every 15 seconds during active tests.
- The cloud timer also has a server-created expiry timestamp. A long browser outage or reload does not grant a brand-new test duration.
- Finished attempts go into `Mock Test Results` and `Mock Test History` and are merged with `Mock Test Attempts` for display.
- Choosing New Random Mock after finishing retains historical results. Selecting the reset button can mark a cloud session abandoned.

## Security/scoring disclosure

Objective question scoring is calculated by the existing **browser practice scorer**, and the backend validates basic ranges and question counts but does **not** independently regrade against every task answer key. Speaking and essay items remain ungraded. Percentages are *practice estimates*, not official Pearson PTE scores. For high-stakes exam scoring, add server-side rubric grading, role-based teacher controls, and a dedicated media/audio assessment pipeline.

## QA still required

- No live Apps Script execution or deployed-site browser QA is possible from this local package. Syntax checks alone do not guarantee production correctness.
- `Mock Test Config` is a reserved schema: changing its cells does not currently override hard-coded task timers/weights.
- Verify task-specific prep/response timers against official current Pearson specifications before calling the mock timings exam equivalent.
- Google Sheets has 50,000-character per-cell limits and Apps Script execution quotas. Extremely long text responses or high concurrency may need a proper database.
- Audio recordings themselves are **not** stored in Google Sheets; where available, only recognized transcripts and status are checkpointed.
