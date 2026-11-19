# PTE Mock Test Update

- Open `mock-tests.html` to access 4 tests for each of 4 sections and 4 full mocks (20 slots).
- Copy modified `Google-Apps-Script/Code.gs` into your existing Apps Script project and **redeploy** the web app. The old deployment will not support `mode=` selections until updated.
- Publish the whole website folder, including `full-mock.html` and `mock-tests.html`.
- The front end calls the existing Apps Script deployment URL defined in `full-mock.html`. If a newly deployed URL changes, update it.
- Student results are saved in browser localStorage per test slot. Prior attempt is overwritten on reattempt in the active slot, while a compact completion history is retained (up to 80). This is not synchronized across devices or stored in the Google Sheets Results tab.
- Student-facing exam hides live scoring and solutions, with review after submission. Spoken recording still requires microphone permission and manual start; browser permission rules prevent guaranteed auto recording.
- Task-level preparation/answer timers are approximate practice defaults, not validated official Pearson timings. Some listening tasks depend on recording length, which is not presently measured in this build.
- Chart percentages must not be construed as raw student marks or official scoring weights. The final reported percentage is objectively gradable practice score only; speaking and essay work remain ungraded unless an external qualified evaluator is integrated.
- Existing source spreadsheet remains unchanged; questions are fetched from the Apps Script question sheets.
- Smoke test: redeploy Apps Script; open each mode; answer one objective question; finish; verify the history and review.
