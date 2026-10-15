# Test Plan

Run only with your own credentials and a small test count. Use a test Google Sheet.

| Test | Scenario | Expected behavior |
|---|---|---|
| Successful scrape | Actor run returns `SUCCEEDED` and has items | Dataset is retrieved and rows are mapped into the sheet |
| Failed run | Actor returns `FAILED` | Error status is formatted and visible to operator |
| Aborted run | Actor returns `ABORTED` | Error path is used |
| Timeout | Actor returns `TIMED-OUT` | Error path is used |
| Still running | Actor returns a non-terminal status | Workflow waits and checks again, within a configured retry limit |
| Empty dataset | Scraper returns zero items | Workflow reports no results without claiming jobs were saved |
| Missing company | A job item has no company name | Row is handled without mapping unrelated data into the field |
| Missing URL | A job item has no job link | Record is flagged or handled according to an explicit policy |
| Duplicate run | Same scrape is run twice | Duplicate behavior is measured; deduplication should prevent repeats if implemented |
| Google Sheets failure | Test credentials/target sheet are invalid | Failure is surfaced and not reported as success |
| Webhook body changes | Submit different count/URL values | Verify current fixed body ignores them; after dynamic mapping, verify values are validated and applied |

## Execution log

Record the test date, test ID, actor run status, number of dataset items, number of rows appended, failures, and follow-up changes. Use anonymized data and never store API tokens in the log.
