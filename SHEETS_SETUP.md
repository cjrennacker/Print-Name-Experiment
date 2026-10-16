# Google Sheets setup (about 5 minutes)

The task sends each trial to a Google Apps Script Web App, which appends it to a sheet.
Use a **new** sheet and script for this study. The gaze-cueing script writes different columns.

1. Create a new Google Sheet. Name it something like `Print Title Search Data`.
2. In the sheet, choose **Extensions > Apps Script**.
3. Delete the starter code, paste in everything from `apps-script/Code.gs`, and save.
4. Choose **Deploy > New deployment**. Click the gear and pick **Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Click **Deploy**, approve the permissions, and copy the **Web app URL** (it ends in `/exec`).
6. In `index.html`, paste that URL into `CONFIG.sheetWebAppUrl`. Commit and push.
7. Run a test session and confirm two tabs appear: **Trials** (one row per trial) and **Summary** (one row per participant).

If you change `Code.gs` later, choose **Deploy > Manage deployments > Edit > New version** or the old code keeps running.

You can also test without editing the file by adding `?sheet=YOUR_URL` to the page address.

## Columns in the Trials tab

| Column | Meaning |
|---|---|
| `session_id` | Participant ID (typed or auto-generated) |
| `consent`, `consent_version`, `consent_timestamp` | Consent given (`yes`), which wording was shown, and when. Participants who decline are never logged |
| `trial_num`, `phase`, `block_num` | Order; `phase` is `practice` or `experimental` |
| `similarity` | `low` or `high`: how much the other titles resemble the target |
| `signal` | `present` or `absent`: whether the target card was on the page |
| `target_title`, `target_family`, `target_len` | The title participants searched for |
| `target_source` | `catalog` (real Range & Focus title) or `invented` (sibling written for the high-similarity condition) |
| `n_invented_distractors` | How many distractors on the page were invented titles |
| `target_pos` | Card position 0 to 8 (left to right, top to bottom); `NA` when absent |
| `n_first_word_matches` | Distractors sharing the target's first word |
| `mean_len_diff` | Mean character-length gap between distractors and target |
| `distractor_titles`, `photo_ids` | Everything shown, so any trial can be rebuilt |
| `key_mapping` | `z_present` or `m_present` (randomized per participant) |
| `response` | `present`, `absent`, or `timeout` |
| `outcome` | `hit`, `miss`, `false_alarm`, `correct_rejection`, or `timeout` |
| `correct` | 1 or 0 |
| `response_time_ms` | From response screen onset; `NA` on timeouts |
| `display_ms_set`, `display_ms_actual` | Requested and measured page duration |
| `screen_w`, `screen_h`, `dpr`, `timestamp` | Device and time |

## Summary tab

One row per participant with hits, false alarms, hit rate, false-alarm rate, `d_prime` and `criterion_c` for `low`, `high`, and `all` trials.
Rates use the log-linear correction (add 0.5 to each count, 1 to each total). Timeouts are excluded.
