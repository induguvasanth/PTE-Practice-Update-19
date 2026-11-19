# PTE Mock Upgrade 2 — Google Sheets history and grading safeguards

1. Upload website files including `mock-tests.html` and `full-mock.html`, retaining all existing question pages and assets.
2. Replace existing Apps Script `Code.gs` with this updated copy; retain `Bridge.html`; redeploy as a NEW version (same existing web app URL when editing the deployment).
3. Ensure `sync-config.js` points at your deployed /exec URL and the site origin matches the `Bridge.html` allowed origin.
4. Teachers must register students and assign passwords. Students sign in through Student Login before starting mocks to enable cloud sync.
5. Submit a mock; open Mock Test Center to view synced history and offline-sync status. The Apps Script automatically creates a `Mock Test Attempts` sheet with one record per completed attempt (student ID + attempt ID prevents duplicates).
6. Validate with a test student in two browsers, and test losing/recovering connectivity. The original question sheets are untouched.

## Grading disclosure
This upgrade scores only supported objective tasks with actual answer keys. It no longer includes ungraded speaking/writing items in the objective grade denominator. These are local practice percentages, not PTE academic scores. No speaking/essay AI rubric scoring is claimed. Student-provided marks can be tampered with in the browser; the history sheet is useful for practice tracking, not high-stakes certification.

## Remaining QA limits
No live Apps Script deployment or browser microphone services are available in the build environment. Task interactions still require live cross-browser QA, including Highlight Incorrect Words, dictation, audio, timing, and the workbook's answer-key conventions. The app's existing practice timers remain approximations, not guaranteed Pearson timing fidelity. The cloud history stores compact question outcomes, not complete audio recordings. Existing section/full-mock selection logic and practice interfaces are retained.
